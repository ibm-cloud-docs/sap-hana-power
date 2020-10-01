---

copyright:
  years: 2020
lastupdated: "2020-09-14"

keywords: SAP HANA, disk, provisioning

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:tip: .tip}

# Disk provisioning and layout
{: #disk_provisioning_and_layout}

When you provision a new Linux&reg; server, the default size of the boot logical volume is 100 GB. To prepare your {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}} instance, see the following resources.
{: shortdesc}

| Link                                                                          | Description                               |
|-------------------------------------------------------------------------------|-------------------------------------------|
| [SAP Note 2055470 - HANA on POWER Planning and Installation Specifics - Central Note](https://launchpad.support.sap.com/#/notes/2055470)               | Server and storage setup and configuration        |
| [SAP Note 1943937 - Hardware Configuration Check Tool - Central Note](https://launchpad.support.sap.com/#/notes/1943937/E)                                   | Required checks to run with the HWCCT (Hardware Configuration Check Tool)                         |
| [Best Practices TDI Certified for IBM Storage](http://www-03.ibm.com/support/techdocs/atsmastr.nsf/WebIndex/WP102347)     |  How to configure SAP HANA TDI certified IBM storage                    |
{: caption="Table 1. Information resources" caption-side="top"}

For test systems, follow these guidelines for storage allocation:

* 52 GB of free disk space for the partition `/usr/sap`. 
* Space for three partitions for SAP HANA file storage locations as shown in Table 2: 

| Directory    | Purpose                                    |
|--------------|--------------------------------------------|
| /usr/sap     | 52 GB required in the test system          |
| /hana/data   | Same size as RAM                           |
| /hana/log    | Same size as RAM up to a maximum of 512 GB |
| /hana/shared | Same size as RAM up to a maximum of 1 TB   |
| /export      | Local storage for exported images **       |
| /backup      | A preliminary backup on disk **           |
{: caption="Table 2. SAP HANA file storage locations" caption-side="top"}

** Optional directory for the Linux server

If all disks that you want to use to construct the storage layer for SAP HANA are equal in size, it can be complicated to determine which disks to include in which volume groups.

Create an Excel spreadsheet with an overview of the naming convention that you want to use, the size of the disks, and LVM information.
{: tip}

For example, multiple disks aren't needed for the SAPVG using the `/usr/sap` directory. The amount of I/O workload is negligible and not intensive compared to `/hana/data` and `/hana/log` (`/hana/log` depends on your log archive mode).

## Example
{: #disk_provisioning_example}
Consider a system that requires 400 GB storage. For `/usr/sap` and `hdb_usrsap_vg`, you create one 52 GB disk.

For `/hana/data` and `hdb_data_vg`, the data is accessed randomly, depending on the disk action or request at the time. For performance purposes, you create eight physical volumes. When you provision your new virtual server instance, specify the following settings on the storage provisioning page:

**Add storage volumes:** New Storage Volume

**Provide the name of the new storage volume(s):** datavolumes1-8

**Size of volumes to be created**: 60G

**Shareable:** Off

**Quantity**: 8

Disk type is automatically set to **Tier 1**.

**Create and Attach**

480 GB of space is allocated for the `datavg`.

For the `/hana/log` and the `hdb_log_vg`, logs are created every 5 minutes, so the I/O activity is intense. Eight physical volumes are created for performance purposes.

## Another example
{: #disk_provisioning_example2}

If `log_mode=normal` and you are using a backup method such as Spectrum Protect that backs up log files and removes them after saving them, provision more storage space. If the process is interrupted, the space in `/hana/log` will be reduced quickly, which can result in a database crash and possible loss of data. See the following example of provisioning storage for `/hana/log` when more space is added.

**Add Storage Volumes** New Storage Volume

**Provide the name of the new storage volume(s)** logvolumes1-8

**Size of Volumes to be created** 70G

**Shareable** Off

**Quantity** 8

Disk type is automatically set to **Tier 1**

560 GB of space is allocated for the `hdb_log_vg`.

For `/hana/shared`, provision one physical volume by using the following formula:

Size = installation(single - node) = MIN(1x RAM ; 1 TB)

For example, a test HANA server is a scale up sized at 400 GB, thus provisioning a single PD of 400 GB.

Currently, scale out is not supported on {{site.data.keyword.powerSys_notm}}s.

When custom sizes are assigned to each of the physical volumes, you can use a simple script to create each of the required file systems. For more information, see [Disk discovery and storage setup](/docs/sap-hana-power?topic=sap-hana-power-disk_discovery_and_storage_setup).
