---

copyright:
  years: 2020
lastupdated: "2020-09-14"

keywords: SAP HANA, disk, provisioning

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

# Checking SAP settings
{: #check_sap_settings}

The prebuilt, default SUSE 12 SP4 image does not include all SAP network optimizations. Check your current settings, compare them to SAP-recommended network and operating system settings, and update your settings if necessary.  
{: shortdesc}

To check your current settings, run the following command:

```
sysctl -a| grep -E 
"net.core.somaxconn|net.ipv4.tcp_max_syn_backlog|net.ipv4.ip_local_port_range|net.ipv4.ip_local_reserved_ports|net.ipv4.tcp_tw_reuse|net.ipv4.tcp_tw_recycle|net.ipv4.tcp_timestamps|net.ipv4.tcp_syn_retries|net.ipv4.tcp_wmem|net.ipv4.tcp_rmem|net.core.wmem_max|net.core.rmem_max|net.ipv4.tcp_window_scaling|net.ipv4.tcp_slow_start_after_idle"
```

Compare the output with the SAP-recommended network and operating system configuration settings. For more information, see [SAP Note 2382421 - Optimizing the Network Configuration on HANA- and OS-Level](https://launchpad.support.sap.com/#/notes/2382421).

Record your current settings before you make changes. If you have issues with the network after you make changes, you can restore the original values. 
{: tip}

For a persistent change, edit `/etc/sysctl.conf`. If a required parameter is not listed in the file, you can append it.

For a temporary change to take effect immediately until the next reboot, you can submit the corresponding `sysctl` commands:

```
sysctl -w <parameter_name>=<parameter_value>
```

Example:

```
ibmdmhan01:/etc/sysconfig/network # sysctl -w net.core.somaxconn=4096
net.core.somaxconn = 4096
```

To diagnose start-up issues, see [SAP Note 401162 - Linux: Avoiding TCP/IP port conflicts and start problems](https://launchpad.support.sap.com/#/notes/401162){: external}.
