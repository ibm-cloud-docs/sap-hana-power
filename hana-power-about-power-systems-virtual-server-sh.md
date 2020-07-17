---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: power systems, infrastructure as a service, multiple virtual servers, hybrid cloud environment, Linux

subcollection: sap-hana-power

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# What is a Power Systems Virtual Server?
{: #about-virtual-server}

{{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}}s are colocated and connected with {{site.data.keyword.cloud}}. {{site.data.keyword.powerSys_notm}}s, also known as logical partitions (LPAR), run on IBM Power Systems hardware with the PowerVM hypervisor.
{:shortdesc}

{{site.data.keyword.powerSysShort}}s are a form of infrastructure as a service (IaaS). With the {{site.data.keyword.powerSys_notm}} service, you can quickly create and deploy one or more virtual servers that are running Linux&reg; operating systems. After you provision the virtual server, it is your responsibility to make sure that your operating system is secure.

Current Linux clients can use the {{site.data.keyword.powerSys_notm}} service for a number of workload scenarios, including disaster recovery, development environments, and partial IT infrastructure moves. {{site.data.keyword.powerSys_notm}} clients can stay competitive with the scaling of their infrastructure and remain flexible with their workload management and capacity both on- and off-premise. And since the infrastructure layer is identical, system administrators who run on-premises Linux systems today can use their same tools, workflows, and enhancements in the cloud.

## Key features
{: #key-features}

The following are some of the key features for the {{site.data.keyword.powerSys_notm}} service.

### Straightforward billing
{: #straightforward-billing}

{{site.data.keyword.IBM_notm}} PowerLinux clients can use their own licenses for the operating systems images that are provided by {{site.data.keyword.IBM_notm}} (BYOL – Bring your own license). In this way, clients can reuse their licenses in {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}} environment without any additional costs.

### Hybrid cloud environment
{: #hybrid-cloud}

You can use the {{site.data.keyword.powerSys_notm}} service to run any Linux workloads off-premise from your existing Power Systems hardware infrastructure. By running your workloads in {{site.data.keyword.powerSys_notm}}s, you can enjoy all of the advantages the cloud has to offer such as self-service, fast delivery, elasticity, and connectivity to other {{site.data.keyword.cloud}} services. Although your Linux workloads are running in {{site.data.keyword.powerSys_notm}}s, you still keep the same scalable, resilient, production-ready features that Power Systems hardware is known to provide.

### Infrastructure customization
{: #infra-customization}

You can configure and customize the following options when you create a {{site.data.keyword.powerSys_notm}}:

* Number of virtual server instances
* Number of cores
* Amount of memory
* Data volume size and type
* Network interfaces

## Hardware specifications
{: #hardware-specifications}

SAP HANA on {{site.data.keyword.powerSys_notm}} is hosted on IBM Power System E980 (9080-M9S). For more information about these systems and how they're used inside the {{site.data.keyword.powerSys_notm}} service, see their data sheets and the hardware overview table. 

If you'd like to compare your current environment's performance to what's available through the {{site.data.keyword.powerSys_notm}} service, see the [IBM Power Systems performance report](https://www.ibm.com/downloads/cas/K90RQOW8){: new_window}{: external}. For a more condensed comparison, see [IBM Power Systems CPW performance data comparison](https://www.itechsol.com/wp-content/uploads/2018/07/IBM-Power-Systems-CPW-Performance-Data-Comparison-P7-vs-P8-vs-P9-rev3-July-2018.pdf){: new_window}{: external}.
{: tip}

**Data sheet:** [IBM Power System E980 (9080-M9S)](https://www.ibm.com/downloads/cas/VX0AM0EP){: external}

| Compute  | Storage   | Network   |
|--------- | --------- | --------- |
|<ul><li>Power e980 (9080-M9S)</li></ul>| <ul><li>Storwize V7000F(2076-AF6) dual controller</li><li>Storwize V7000 (2076-624) dual controller </li><li>IBM SAN64B-6 (Brocade)</li></ul> | <ul><li>Cisco Nexus9000 93180YC-EX (10G)</li><li>Cisco Nexus9000 C9348GC-FXP (1G)</li><li>Avocent ACS8048</li></ul> |
{: class="simple-tab-table"}
{: tab-group="hardware"}
{: caption="Table 1. Hardware overview" caption-side="top"}
{: #hw-spec-1}
{: tab-title="Washington, D.C. (WDC04), Dallas (DAL13), Frankfurt and London (FRA04/FRA05/LON06)"}
