---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: SAP HANA, {{site.data.keyword.cloud_notm}}, system readiness

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}

# Checking system readiness for SAP HANA
{: #check_system}

After you provision your new {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}} for SAP HANA, ensure that the memory NUMA (non-uniform memory access) configuration is correct and supported for the SAP HANA workload. 
{: shortdesc}

Memory NUMA configuration is not supported by SAP HANA when {{site.data.keyword.IBM}} {{site.data.keyword.powerSys_notm}} is deployed on a physical server where most of the CPUs and memory are already allocated.

You can run a Python script on Linux&reg; to see whether the infrastructure is set up correctly. Download the script from [SAP Note 2923962](https://launchpad.support.sap.com/#/notes/2923962){: external} and run the script on the command line (without any parameters). First, add the execution permissions to the script file. For example, download the script to the `/root` location and run as follows:

```
chmod +x /root/chk_numa_lpm.py 

/root/chk_numa_lpm.py
```

The tool checks the NUMA layout and whether a Live Partition Mobility (LPM) operation has taken place. Both can impact performance.

The LPM check finds the date of the last LPM in the log file from the DLPAR operations, and compares it to the date of the last boot. If it detects that a possible LPM occurred after the last boot, a warning is generated.

The NUMA check is based on SAP rules. The script checks that there are no cores without memory; if found, the script issues an error. The script also checks that the memory distribution among the cores does not exceed a 50% margin; if so, the script generates a warning.

The tool writes a log file (`chk_numa_lpm.log`) in the current directory with its findings. If an error or warning is generated, open a case through the {{site.data.keyword.cloud}} console.


## Next Steps
{: #check_system_next_steps}

[Configuring the system for the SAP HANA workload](/docs/sap-hana-power?topic=sap-hana-power-configure_system)

[Configuring system access for SAP HANA installation](/docs/sap-hana-power?topic=sap-hana-power-configure_access)

[Ordering storage](/docs/sap-hana-power?topic=sap-hana-power-manage_order_storage)

[Downloading and installing SAP software and applications](/docs/sap-hana-power?topic=sap-hana-power-download_and_install)

[Creating an SAP license key](/docs/sap-hana-power?topic=sap-hana-power-create_key)

[Monitoring the system with SAP tools](/docs/sap-hana-power?topic=sap-hana-power-monitoring)