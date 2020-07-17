---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: SAP HANA, {{site.data.keyword.cloud_notm}}, RDBMS, SAP Application Performance Standards, SAPS, SAP Certified, database

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:table: .aria-labeledby="caption"}


# Determining your configuration
{: #determine_configuration}

It's important to design your SAP stack configuration, deployment, and SAP HANA database. For example, with an S4/HANA system, you have two deployment options:
  * Central system, which is a single-host installation (two-tier)
  * Distributed system, which is a multi-host installation (three-tier)

The options influence your server choice. You might want to distribute your workload to different servers or keep the workload on one server for simplicity. For more information, see [Setting up your Power Systems Virtual Server instances](/docs/sap-hana-power?topic=sap-hana-power-provision_environment).
{:shortdesc}

## Network configuration
{: #network-config}

Ensure that you have a working network Direct Link connection between the {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}} colocation and {{site.data.keyword.cloud}} or your on-premises networks. This connection is required for management and for access to your SAP applications. For more information, see [Ordering Direct Link Connect on classic](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## Storage configuration
{: #storage_config}

When you provision storage for an instance that will host SAP HANA, mandatory TDI storage requirements must be adhered to. For more information, see [SAP TDI (SAP HANA Tailored Data Center Integration) & IBM POWER](http://www-03.ibm.com/support/techdocs/atsmastr.nsf/WebIndex/WP102347).

When you create requests for storage volumes, keep the following points in mind:

* Only Tier 1 storage is supported.
* After you provision the storage with Affinity, you cannot change it. Carefully plan your storage layer and ensure that your configuration is correct. Affinity prevents issues with new volume discovery on existing virtual server instances.
* When you finish provisioning new volumes, you can toggle bootable and sharing switches.
* Volumes that belong to different OS file systems should have unique sizes. Otherwise, it is difficult to identify the storage volumes within the operating system.
* When you install your server and provision your storage, remember that the TDI guidelines must be followed for Linux servers that are installed with SAP HANA. With multiple volumes assigned to the DATA and LOG LVMs, the striping and multipath enhancements increase I/O performance. For more information, see the following documents:
  
  [SAP TDI Advisory](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)

  [SAP HANA Tailored Data Center Integration FAQ (Updated May 2020)](https://www.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)

The following table shows an example of a storage layout for an SAP HANA system. Filesystems for HANA Data and HANA Log directories must be striped over eight storage volumes. Striping for other file systems (SAP executables, HANA Shared, HANA Backup, HANA Export) is not required. See the SAP TDI documents for general storage requirements.

| HANA Filesystem | Total Space Required | Size of Volumes | Number of Volumes |
|-----------------|----------------------|-----------------|-------------------|
| /hana/data      | 560                  | 70              | 8                 |
| /hana/log       | 640                  | 80              | 8                 |
| /hana/shared    | 200                  | 200             | 1                 |
| /usr/sap        | 130                  | 130             | 1                 |
| /backup         | 560                  | 560             | 1                 |
| /export         | 560                  | 560             | 1                 |
{: caption="Table 2. Example of a storage layout for an SAP HANA system" caption-side="top"}

## Next Steps
{: #determine-configuration-next-steps}

You are now ready to begin provisioning your {{site.data.keyword.powerSys_notm}}. See [Setting up your Power Systems Virtual Server instances](/docs/sap-hana-power?topic=sap-hana-power-provision_environment) for your next steps.
