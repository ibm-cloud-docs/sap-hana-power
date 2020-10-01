---

copyright:
  years: 2020
lastupdated: "2020-09-24"

keywords: SAP HANA, {{site.data.keyword.cloud_notm}}, network connectivity, NTP, time server

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configuring the NTP client      
{: #ntp_time_server}

A newly provisioned {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}} might not show the correct time when you run the `date` command. The initial time setting on the server often differs by 10 - 15 minutes from the correct time. This time difference can cause problems when you install and run your SAP system on the server, or when you connect the SAP system to your on-premises landscape.
{: shortdesc}

Ensure that time is synchronized for all {{site.data.keyword.powerSys_notm}}s in your SAP system by using the same time server. For information about setting up NTP on Linux&reg;, see [Time Synchronization with NTP](https://documentation.suse.com/sles/12-SP5/html/SLES-all/cha-netz-xntp.html){: external}.
  
