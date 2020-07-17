---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: SAP HANA, {{site.data.keyword.cloud_notm}}, support, help

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

# Getting help and support
{: #support}

If you have an issue that requires support, open a support ticket.
{: shortdesc}

1. If the issue is related to {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}} infrastructure, open a case through the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com){: external} > Support. All performance-related issues must be checked by [{{site.data.keyword.cloud_notm}} Customer Support](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support) first to rule out any infrastructure-related issues before a case of the software stack above is opened.

    You can check whether the infrastructure is set up correctly by running Python script on Linux&reg;: `python chk_numa_lpm.py`
    For more information, see [Checking system readiness for SAP HANA](/docs/sap-hana-power?topic=sap-hana-power-check_system).
    {: tip}

2. If the issue is operating system (OS) related, go the support portal of the Linux distribution to open a case.
3. If the issue is related to SAP, open a case by going to [support.sap.com](https://support.sap.com/en/index.html){: external} and click **Report an Incident**. Run the following commands and attach the output to the case:

  * `sapsysinfo` [SAP Note 618104](https://launchpad.support.sap.com/#/notes/618104){: external}
  * `supportconfig` [SAP Note 1642802](https://launchpad.support.sap.com/#/notes/1642802){: external}
  * `full-system-info-dump` [SAP Note 1732157](https://launchpad.support.sap.com/#/notes/1732157){: external}

