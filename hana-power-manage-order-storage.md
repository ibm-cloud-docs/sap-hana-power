---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: SAP HANA, {{site.data.keyword.cloud_notm}}, configure system, SAP HANA workload

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

# Ordering storage
{: #manage_order_storage}

Use the following steps to add a storage volume.
{: shortdesc}

1. Click **New volume**.
2. Enter the **Name**, **Type**, and **Size** of the storage volume. You can also select whether to make it **Shareable** and set an **Affinity policy**.

  Specify a unique name for the volume so you can identify it in the list of all volumes.
  {: tip} 

1. Select **Affinity Policy** and identify the boot disk as an **Affinity Volume**. Specifying an Affinity Policy ensures that the new storage will be available in the list to attach to your virtual server instance. By identifying the boot disk as an Affinity Volume, your volumes are on the same backbone storage.

   Mixing storage tiers is not supported. If you have a virtual server instance using Tier 1, you cannot define Tier 3 disks.
   {: important}

2. Agree to the **Service Agreement** and **Terms and Conditions**, then click **Create Storage Volume**.
3. Go to the Storage Volume overview to see your new volume listed.
4. Attach the new volume to your virtual server instance by selecting your instance in the list of Attached Volumes, then click **Manage Existing**. Select the volume that you created and click **Finish**. If you attached new volumes to your Linux&reg; OS, you must run a SCSI scan or restart the operating system (OS) to see the disks (for example: `/usr/bin/rescan-scsi-bus.sh -a -c -v`).
1. Extend your existing file systems or create a new one with OS Logic Volume Manager (LVM).

If you'd like to attach or detach a volume, click **Manage existing volumes** and select the volume. You can also change the boot status of a volume by clicking the **Bootable** toggle.

## Next Steps
{: #manage_order_storage_next_steps}

[Downloading and installing SAP software and applications](/docs/sap-hana-power?topic=sap-hana-power-download_and_install)

[Creating an SAP license key](/docs/sap-hana-power?topic=sap-hana-power-create_key)

[Monitoring the system with SAP tools](/docs/sap-hana-power?topic=sap-hana-power-monitoring)