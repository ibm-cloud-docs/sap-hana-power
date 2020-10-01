---

copyright:
  years: 2020
lastupdated: "2020-09-30"

keywords: SAP HANA, disk, provisioning, storage, discovery

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}

# Disk discovery and storage setup
{: #disk_discovery_and_storage_setup}

On the Linux operating system, scan for the new storage that was provisioned.
{: shortdesc}

Run the following command for storage and disk discovery:

```
/usr/bin/rescan-scsi-bus.sh -a -c -v
```

Newly discovered disks are listed at the end of the report.

It's easier to check the system when the physical disks have different sizes. If the volumes are the same size, you can use the worldwide name (WWN) of the volume that is shown in the {{site.data.keyword.cloud}} UI. The WWN corresponds to the ID in the output of the `multipath -ll` command.

For example, a storage volume with the name sapdata_vol has a worldwide name 3600507681081814CE80000000000054D. In the operating system output of the `multipath -ll` command, the corresponding device name for this WWN is dm-4. The device name is required to create the logical volume and the volume group.

```
ibmdmhan01:~ # multipath -ll
3600507681081814ce80000000000054d dm-4 IBM,2145
size=100G features='0' hwhandler='1 alua' wp=rwv
```

The WWN in the {{site.data.keyword.cloud}} UI contains uppercase letters. In the operating system, the same ID contains lowercase letters.
{: note}

The following example shows how to identify disks by using disk sizes. The eight data volumes are 60 GB each, the eight log volumes are 70 GB each, the single volume for `sapdata` is 52 GB, and the single volume for the `/hana/shared` directory is 400 GB.

Run the following command to check how many volumes were created based on size:

```
ibmdmhan01:/usr/sap/DM2/SYS # /sbin/multipath -ll | grep -i 70G

size=70G features='0' hwhandler='1 alua' wp=rw
size=70G features='0' hwhandler='1 alua' wp=rw
size=70G features='0' hwhandler='1 alua' wp=rw
size=70G features='0' hwhandler='1 alua' wp=rw
size=70G features='0' hwhandler='1 alua' wp=rw
size=70G features='0' hwhandler='1 alua' wp=rw
size=70G features='0' hwhandler='1 alua' wp=rw
size=70G features='0' hwhandler='1 alua' wp=rw
```

Eight 70 GB volumes were created for the log volumes.

Run the following command to see the physical volumes that were created for the data volumes:

```
ibmdmhan01:/usr/sap/DM2/SYS # /sbin/multipath -ll | grep -i 60G

size=60G features='0' hwhandler='1 alua' wp=rw
size=60G features='0' hwhandler='1 alua' wp=rw
size=60G features='0' hwhandler='1 alua' wp=rw
size=60G features='0' hwhandler='1 alua' wp=rw
size=60G features='0' hwhandler='1 alua' wp=rw
size=60G features='0' hwhandler='1 alua' wp=rw
size=60G features='0' hwhandler='1 alua' wp=rw
size=60G features='0' hwhandler='1 alua' wp=rw
```

To create the volume groups, logical volumes, striping, and the file systems, you can use a simple script as follows. Alternatively, you can use your own standard of LVM configuration.

```
# Sample script for mkfs.sh
export pv_size=60G
export lv_name=hdb_data_lv
export vg_name=hdb_data_vg
export mount=/hana/data
devices=$(multipath -ll | grep -B 1 $pv_size | grep dm- | awk '{print "/dev/"$2}' | tr '\n' ' ')
stripes=$(multipath -ll | grep -B 1 $pv_size | grep dm- | awk '{print "/dev/"$2}' | wc | awk '{print $1}')
pvcreate $devices
vgcreate ${vg_name} ${devices}
lvcreate -i${stripes} -I64 -l100%VG -n ${lv_name} ${vg_name}
mkfs.xfs /dev/mapper/${vg_name}-${lv_name}
mkdir -p ${mount}
mount /dev/mapper/$vg_name-$lv_name ${mount}
echo "/dev/mapper/$vg_name-$lv_name ${mount} xfs defaults 1 2 " >> /etc/fstab
```

The script creates the `/hana/data` mount point and puts it in `/etc/fstab`.

If HANA scale-out or HA node failover is used, do not add the DATA and LOG file system to `/etc/fstab`. Mounting is done by SAP HANA. Always add the `/hana/shared` file system to `fstab`.
{: important}

Repeat the same process and update the `pv_size` variable to the next LVM entry that you want to create, update the `lv_name`, and so on. 

When you create entries for `/usr/sap` and `/hana/shared`, you might get a system message that says striping can be done on multiple volumes and not a single volume. Striping isn't necessary if you use one volume only.  