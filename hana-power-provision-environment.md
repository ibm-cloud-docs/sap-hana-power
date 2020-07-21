---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: SAP HANA, SAP deployment

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}


# Setting up your Power Systems Virtual Server instances
{: #provision_environment}

The guidance for setting up your SAP HANA-certified {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}}, including data volume and operating system (OS), is in the following sections.
{:shortdesc}

## Before you begin
{: #before-you-begin-provisioning}

Be sure to do the following steps before you order your {{site.data.keyword.IBM}} {{site.data.keyword.powerSys_notm}}:

 * Set up your [resource groups](/docs/resources?topic=resources-rgs) if you're setting up multiple servers for various purposes.
 * [Invite users](/docs/iam?topic=iam-getstarted) and determine what resources and resource groups they can access.
 * Select a version of the {{site.data.keyword.IBM_notm}} provided SUSE Enterprise Linux&reg; Server (SLES) stock images. The operating system version levels of the stock images are subject to change. For more information, see [SAP Note 2855850](https://launchpad.support.sap.com/#/notes/2855850){: external}. You must use your own SLES license.

## Create your {{site.data.keyword.powerSys_notm}} service
{: order-server}

The {{site.data.keyword.cloud}} console requires a unique log-in ID, which is an {{site.data.keyword.IBM_notm}}id. Do the following steps to order your {{site.data.keyword.powerSys_notm}} service. Additional information can be found under [Creating a {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).

1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com){: external} with your unique credentials.
1. Click **Create resource** > **Compute** > **Infrastructure** > **{{site.data.keyword.powerSys_notm}}**.
1. Select your **region** and **pricing plan**.
1. Enter a **Service name** and select your **Resource group**. You can also enter a **Tag** for your service.
1. Click **Create**. You are redirected to the Resource list for your account where you can see when your service was provisioned.

### Configure your {{site.data.keyword.powerSys_notm}} service
{: #configure-dedicated-server}

Do the following steps to configure your {{site.data.keyword.powerSys_notm}} service.

1. Add an SSH key to securely connect to your {{site.data.keyword.powerSys_notm}}. For more information, see [Adding an SSH key](/docs/ssh-keys?topic=ssh-keys-adding-an-ssh-key).
1.	Configure the private network subnets that will be used for the SAP workload. For more information, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
1. Open a support ticket to connect your private networks to {{site.data.keyword.dl_full}} on classic connection. Provide information about the private network (network name, CIDR) in the ticket.
1.	If required, create more management systems (for example, OS update server, time server, jump server).
1.	If required, configure {{site.data.keyword.dl_full}} to {{site.data.keyword.cloud}} classic or to on-premises networks. 

## Create a new {{site.data.keyword.powerSys_notm}} instance
{: create-instance}

Do the following steps to create a new {{site.data.keyword.powerSys_notm}} instance.

1. Highlight your provisioned {{site.data.keyword.powerSys_notm}} service from the Resources list and click **New Instance**.
1. Enter a **Name**, which is a permanent or temporary name for your servers and enter the **Number of instances** to be provisioned. Be aware that more options will appear if you enter more than one instance. See [Creating a {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) for option details.
1. Specify a VM-pinning rule. You can choose to soft pin or hard pin a VM to the host where it is running. When you soft pin a VM for high availability, PowerVC that runs in the background automatically migrates the VM back to the original host when the host is back to its operating state. If the VM has a licensing restriction with the host, the hard pin option restricts the movement of the VM during maintenance. The default pinning policy is none. Choose soft pin for {{site.data.keyword.powerSys_notm}}s hosting SAP HANA.
1. Select your **SSH key**.
4. Select **SLES for SAP (HANA) – Client supplied subscription** for the operating system, and select the version of one of the {{site.data.keyword.IBM_notm}}-provided Linux stock images.
6. Select a profile with the number of CPU cores and memory (RAM) that fits the size of your SAP HANA database. You can choose one of the popular profile configurations, or select a profile from a list of all profiles that best suits your needs. To view all available profiles, click **View all profiles** on the provisioning page.
7. You can either create a new storage volume or attach existing storage volumes that are already defined in your {{site.data.keyword.cloud}} account. For SAP HANA data and log volumes, filesystems must be striped over eight volumes. If you create storage volumes for SAP HANA data or log file systems, specify `8` for the Quantity. Choose a unique name for the volume so you can identify it in the list of all volumes.
8. Select **Private networks** for communication between SAP instances. For more information, see [Configuring a private network](/docs/power-iaas?topic=power-iaas-configuring-subnet). Optionally, you can configure an additional public network, for example, to get OS updates over the internet.
9.  Click **I have read and agree to the agreements listed below** and click **Create**. The new instance becomes visible in the list of virtual server instances with a status of Creating for a few minutes. When the status changes to Active, you can log in to the server (for example, by using SSH).

## Next Steps
{: #provisioning-next-steps}

You are now ready to begin managing your {{site.data.keyword.powerSys_notm}}. See [Managing your SAP HANA environment](/docs/sap-hana-power?topic=sap-hana-power-manage_environment) for your next steps.
