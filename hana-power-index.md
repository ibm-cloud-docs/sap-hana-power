---

copyright:
  years: 2020
lastupdated: "2020-07-21"

keywords: SAP HANA, {{site.data.keyword.cloud_notm}}, SAP-certified {{site.data.keyword.powerSys_notm}}, {{site.data.keyword.powerSysShort}}, {{site.data.keyword.powerSys_notm}}

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Getting started with SAP HANA on IBM Power Systems Virtual Servers
{: #getting-started}

{{site.data.keyword.IBM}} and SAP continue a collaboration since the early 1970s in multiple areas, including hardware, software, cloud, services, and finance. They are now collaborating to run SAP HANA-based applications on {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}}s.
{: shortdesc}

{{site.data.keyword.powerSys_notm}} is a Power Systems enterprise infrastructure as a service (IaaS) offering. {{site.data.keyword.powerSys_notm}}s are physically located with low-latency connectivity to the IBM Cloud&trade; Infrastructure. This infrastructure design enables {{site.data.keyword.powerSys_notm}}s to maintain key enterprise software certification and support as its architecture is identical to certified on-premises infrastructure.

This content provides you with recommendations for the provisioning and installation of the infrastructure to support SAP HANA-based products and subscription on {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}}s. It does not replace any SAP HANA implementation-related documentation. Its purpose is to help you with infrastructure planning and provisioning so you can begin your SAP installation. The SAP HANA installation does not vary from installations for on-premises environments. Recommendations and guidelines are provided to help you operate your SAP system in the {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}} environment.

## Before you begin
{: #before-you-begin-getting-started}

Table 1 contains information that will help you with your implementation.

| Task | Details |
| ----- | ----- |
| Read IBM Cloud and SAP content that is related to your implementation | * [What is IBM Cloud](https://www.ibm.com/cloud) |
| | * [Get started with IBM Cloud](https://www.ibm.com/cloud/get-started) |
| | * [SAP workloads on IBM Cloud](https://www.ibm.com/cloud/sap/certified-infrastructure)|
| You might also find the following SAP documentation useful:  | * [How to create an SAP S-user ID](https://www.youtube.com/watch?v=4wICiRTP8u0/) Only super administrators or S-users with the required authorization are allowed to create S-user IDs. |
| | * [SAP HANA Help](https://help.sap.com/viewer/product/SAP_HANA_PLATFORM/2.0.04/en-US) |
| | * [SAP Notes through SAP Support](https://support.sap.com/en/index.html) |
| Sign up for IBM Cloud | [Signing up for IBM Cloud](/docs/account/adminpublic.html#signing-up-for-ibm-cloud) |
| Create a public and private SSH key | Use the SSH keys to securely connect to your Power Systems Virtual Server. To create a public and private SSH key, see [Adding an SSH key](/docs/ssh-keys?topic=ssh-keys-adding-an-ssh-key). |
| Access the IBM Cloud console | [IBM Cloud console](https://cloud.ibm.com) is your graphical gateway to all your infrastructure components-compute, networking, and storage. You need an [IBMid and password](/docs/account?topic=account-signup#signing-up-for-ibm-cloud) to access the console. |
| Invite users to your account and manage their access | IBM Identity and Access Management (IAM) service is used to set up your users and grant them access to based on their roles. See [Getting started with IAM tutorial](/docs/iam?topic=iam-getstarted) and [Best practices for organizing resources and assigning access](/docs/account?topic=account-account_setup) set up your users and grant them system access. |
| Create resource groups | A **resource** is anything that you can create from the catalog that is managed by and contained within a **resource** group. For more information, see [Creating and managing resource groups](/docs/resources?topic=resources-rgs).
{: caption="Table 1. Before you begin steps" caption-side="top"}

## Terminology
{: #terminology}

Before you create a virtual server, you must understand the terminology that is associated with a {{site.data.keyword.powerSys_notm}}.

### {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}}s versus {{site.data.keyword.cloud}} classic infrastructure
{: #cloud-vs-classic}

{{site.data.keyword.powerSys_notm}}s are located in the same IBM data centers as the x86-based IBM Cloud servers, which are referred to as [IBM Cloud classic infrastructure](/docs/cloud-infrastructure?topic=cloud-infrastructure-compare-infrastructure). In the data centers, the {{site.data.keyword.powerSys_notm}}s are separated from the rest of the IBM Cloud servers with separate networks and direct-attached storage. The internal networks are fenced but offer connectivity options to IBM Cloud infrastructure or on-premises environments.

### Resource versus resource group
{: resource-versus-group}

A **resource** in the context of {{site.data.keyword.powerSys_notm}}s is not a user, it's anything that you can create from the catalog, for example, a {{site.data.keyword.powerSys_notm}}. A **resource group** contains multiple resources, for example, a set of servers used strictly for development activities. For more information, see [What is a resource?](/docs/resources?topic=resources-resource).

### Service versus instance
{: #service-versus-instance}

There is difference between a {{site.data.keyword.powerSys_notm}} **service** and a {{site.data.keyword.powerSys_notm}} **instance**. Think of the {{site.data.keyword.powerSys_notm}} **service** as a container for all {{site.data.keyword.powerSys_notm}} **instances** at a specific geographic location. The {{site.data.keyword.powerSys_notm}} **service** is available from the **Resource list** in the {{site.data.keyword.cloud}} UI. The service can contain multiple {{site.data.keyword.powerSys_notm}} **instances**.

For example, you can have two {{site.data.keyword.powerSys_notm}} **services**, one in Dallas and another in Washington DC. Each service can contain multiple {{site.data.keyword.powerSys_notm}} **instances**. For more information, see [Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-getting-started).

All instances of an SAP system must run in the same service. Multiple systems can be distributed through different services, in which case IT operations must ensure that latency is acceptable for their scenarios.
{: note}

### Preconfigured instance profiles for SAP HANA
{: #preconfigured_profiles}

An instance profile is a preconfigured combination of a number of CPUs and memory size. The number of supported combinations is restricted. There are instance profiles that are already certified for SAP HANA and are fully supported. Other profiles are currently being certified.

## Implementing SAP HANA on {{site.data.keyword.powerSys_notm}}

Table 2 contains steps to help you get your {{site.data.keyword.powerSys_notm}} infrastructure quickly built.

| Task | Details |
| ----- | ----- |
| Plan your landscape | Use the information in [Planning your system landscape](/docs/sap-hana-power?topic=sap-hana-power-planning-your-system-landscape) to architect, size, and provision your {{site.data.keyword.IBM}} {{site.data.keyword.powerSys_notm}} environment to support your SAP HANA workload. |
| Provision your system | Use the steps and information in [Provisioning your SAP HANA environment](/docs/sap-hana-power?topic=sap-hana-power-provision_environment) to set up your {{site.data.keyword.IBM}} {{site.data.keyword.powerSys_notm}} infrastructure. |
| Manage your environment | Use the information in [Managing your SAP HANA environment](/docs/sap-hana-power?topic=sap-hana-power-manage_environment) to perform an initial configuration after provisioning, or to change your {{site.data.keyword.IBM}} {{site.data.keyword.powerSys_notm}}s. |
| Install SAP software | You prepare the OS and install SAP software on your {{site.data.keyword.IBM}} {{site.data.keyword.powerSys_notm}} infrastructure as if the servers were on-premises. For more information about installing SAP software, see [Downloading and installing SAP software and applications](/docs/sap-hana-power?topic=sap-hana-power-download_and_install) for more information. |
{: caption="Table 2. Steps to get up and running quickly" caption-side="top"}
