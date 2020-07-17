---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: file systems, example, Linux Logical Volume Manager

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:table: .aria-labeledby="caption"}
{:important: .important}
{:note: .note}


# Create file systems on SLES12 SP4 by using the command-line interface
{: #create_file_systems}

You can use this example to create volumes for file systems that are required by SAP HANA (HANA data, HANA log, and HANA shared). 
{:shortdesc}

The following example shows how you can use Linux Logical Volume Manager to create a file system called `/hana/data` based on eight storage volumes, each with a size of 110 GB. The name of the volume group is `hana_data_vg`, and the name of the logical volume is `hana_data_lv`. The volume size should be unique so it can be used as an identifier to find a required storage volume.

The root volume 100 GB in size. Use different sizes for additional volumes.
{: note}

```
export pv_size=110G
export lv_name=hana_data_lv
export vg_name=hana_data_vg
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