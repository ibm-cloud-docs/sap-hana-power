---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: SAP HANA, SAP landscape, SAP Business Suite, SAP Business Warehouse, SAP BW

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:faq: .faq}
{:note: .note}

# Planning your system landscape
{: #planning-your-system-landscape}

An SAP *landscape* is a group of two or more SAP *systems* that usually include development, quality and test, and production. One SAP system consists of one or more SAP instances and a database (in this case SAP HANA), which are a group of processes that are started and stopped at the same time. For more information about SAP landscapes, see the following documentation:
 * [SAP NetWeaver on IBM Power Systems Virtual Servers](/docs/sap-netweaver-power?topic=sap-netweaver-power-getting-started)
 * [SAP on Power Systems Best Practices Guide](https://www-03.ibm.com/support/techdocs/atsmastr.nsf/WebIndex/WP102618){: external} (click the link in the middle of the page)
 * [IBM Power Systems Virtualization Operation Management for SAP Applications](http://www.redbooks.ibm.com/abstracts/redp5579.html?Open){: external}
 * [SAP HANA on IBM Power Systems and IBM System Storage - Guides](http://www-03.ibm.com/support/techdocs/atsmastr.nsf/WebIndex/WP102502){: external}
 * [SAP Note 2903141 - Best practice configuration checks for SAP HANA](https://launchpad.support.sap.com/#/notes/2903141){: external}
{: shortdesc}

There are several possible landscape configurations for many SAP solutions in the market. These solutions include SAP S/4HANA, SAP Business Suite powered by SAP HANA, SAP NetWeaver-based products with SAP HANA, and all specific SAP solutions, which the {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}}s support. More solutions to keep in mind are any non-SAP NetWeaver-based SAP solutions and any third-party software that might integrate with SAP. Contact [SAP Support](https://support.sap.com/en/index.html){: external} if you’re planning to deploy non-SAP NetWeaver-based or third-party software in your {{site.data.keyword.cloud}} IaaS landscape.

You want to be as detailed as possible when you determine the size of your server based on the applications you plan to run, potential growth, and performance. Additionally, keep in mind your storage and memory requirements for your applications. SAP systems in a landscape have specific requirements for connectivity, either among each other or to external systems.

Table 1 contains the steps within the planning process. Use it to help build your target SAP landscape.

| Step | Details |
| --- | --- |
| 1 | [Items to consider when you plan your SAP landscape](/docs/sap-hana-power?topic=sap-hana-power-considerations) |
| 2 | [Get SAP and {{site.data.keyword.cloud_notm}} credentials and create accounts](/docs/sap-hana-power?topic=sap-hana-power-get_sap_ibm_credentials#get_sap_ibm_credentials) |
| 3 | [Review any relevant SAP and {{site.data.keyword.cloud_notm}} documentation](/docs/sap-hana-power?topic=sap-hana-power-review_doc) |
| 4 | [Determine your SAP applications](/docs/sap-hana-power?topic=sap-hana-power-determine-apps) |
| 5 | [Bring your OS product license](/docs/sap-hana-power?topic=sap-hana-power-bring-your-own-os-product-license)
| 6 | [Bring your SAP product license](/docs/sap-hana-power?topic=sap-hana-power-bring-your-own-sap-product-license)
| 7 | [Size the server](/docs/sap-hana-power?topic=sap-hana-power-size_the_server) |
| 8 | [Configure high availability](/docs/sap-hana-power?topic=sap-hana-power-ha_config) |
| 9 | [Determine your configuration](/docs/sap-hana-power?topic=sap-hana-power-determine_configuration#determine_configuration) |
{: caption="Table 1. Planning process overview" caption-side="top"}

## Next Steps
{: #planning-landscape-next-steps}

Select the appropriate step in Table 1 to begin planning your SAP landscape.
