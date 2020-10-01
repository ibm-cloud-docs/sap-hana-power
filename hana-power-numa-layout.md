---

copyright:
  years: 2020
lastupdated: "2020-09-16"

keywords: SAP HANA, disk, saptune, apply, solution

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

# NUMA layout
{: #numa_layout}

Check that the balance of CPU and memory placement is optimized for SAP HANA by running the `chk_numa_lpm.py` script.
{: shortdesc}

The `chk_numa_lpm.py` script does the following actions:

* Checks the non-uniform memory access (NUMA) layout according to SAP HANA rules. The script verifies that there are no cores without memory and that the memory distribution among the cores does not exceed a 50% margin. In the first case, the script generates an error; in the latter case, the script generates a warning.
* Checks whether a Live Partition Mobility (LPM) operation occurred. After LPM, the NUMA layout might differ from the configuration at boot time. The script scans the system log for the last LPM. A warning is generated if an LPM operation occurred since the last system boot.

Download the `chk_numa_lpm.py` script from the following SAP Note: [SAP Note 2923962 - Check SAP HANA NUMA Layout on IBM Power Systems Virtual Servers](https://launchpad.support.sap.com/#/notes/2923962){: external} 

Then, run the `chk_numa_lpm.py` script on your newly provisioned {{site.data.keyword.cloud}} {{site.data.keyword.powerSys_notm}}.

Run the script as follows:

```
ibmdmhan01:/backup/software/numa # ./chk_numa_lpm.py
WARNING: LPM may have occurred

ibmdmhan01:/backup/software/numa # ls
chk_numa_lpm.log  chk_numa_lpm.py
ibmdmhan01:/backup/software/numa # cat chk_numa_lpm.log

###  Check run on  : 2020-09-10 09:37:21  #####

Hostname           : ibmdmhan01
Partition UUID     : 2e2fb3e5-ef18-48c6-819a-bd85bfefa953

WARNING: A possible Live Partition Migration (LPM) might have happened after boot!

Date of lastest started LPM : 2020-07-16 06:08:38
Date of lastest boot        : 2020-07-02 10:01:00

Numa Node :  0   Number of virt. CPUs :  32   Amount of memory :   255667 MB
Numa Node :  1   Number of virt. CPUs :  32   Amount of memory :   255738 MB
```

In this example, a warning was generated. There are two NUMA nodes with an equal amount of CPU and memory. For more information, see [SAP Note 2923962](https://launchpad.support.sap.com/#/notes/2923962){: external}.

