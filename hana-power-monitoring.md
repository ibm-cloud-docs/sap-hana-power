---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: SAP HANA, {{site.data.keyword.cloud_notm}}, download, install

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Monitoring system with SAP tools
{: #monitoring}

SAP system monitoring for {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}}s is available through the [SAP Host Agent](https://help.sap.com/viewer/3ce0859db2164fe19541dda577d29020/7.5.9/en-US/48c6f9627a004da5e10000000a421937.html){: external}, which provides monitoring functions that are similar to on-premises installations.
{: shortdesc}

For Infrastructure as a Service (IaaS) environments such as {{site.data.keyword.powerSys_notm}}s, the operating system metrics that the SAP Host agent provides were enhanced. Make sure you have the prerequisite SAP Host Agent patch level installed. For a description of the new metrics and required patch level, see [SAP Note 2932766](https://launchpad.support.sap.com/#/notes/2932766){: external}.