---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: SAP HANA, {{site.data.keyword.cloud_notm}}, configure system, SAP HANA workload

subcollection: sap-hana-power

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Configuring the system for the SAP HANA workload
{: #configure_system}

After you deploy {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}}, the following needs to be done within the operating system.
{: shortdesc}

1. Configure root user access. You can log in to the system as a root user by using a configured SSH key. Logging in as a root user with a password through SSH is deactivated. You can log in as a root user by using the default password `root` in a virtual console window. After you log in, change the default password for the root user.
1. Start and enable the multipath deamon, for example, by running `systemctl start multipathd` and `systemctl enable multipathd`.
1. Set jumbo frames for network adapters. _Jumbo frames_ is another way of saying network maximum transmission units (MTU) of 9000-byte payload frames. All the network components in {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}}s support jumbo frames. In cases where certain network components don't support jumbo frames (for example, in communication to the external world), setting MTU=9000 can cause network issues. Therefore, set MTU=9000 only on adapters that are used internally.

  You must set jumbo frames on private networks that are used for communication between multiple instances in SAP three-tier systems as follows:

  ```
  # cd /etc/sysconfig/network
  # vi ifcfg-ethX <--- name of ethernet device used for communication between SAP instances
  BROADCAST=''
  ETHTOOL_OPTIONS=''
  BOOTPROTO='static'
  IPADDR='xx.xx.xx.xx/xx'
  NAME='Virtual Ethernet card 0' NETWORK=''
  REMOTE_IPADDR=''
  STARTMODE='auto'
  USERCONTROL='no'
  MTU='9000'
  ```
  {: pre}
  
  To activate the changes, restart your network (`ifdown ethX; ifup ethX`), or set the MTU for the current configuration (with `ip link set dev <ethX> mtu 9000`).
1. Verify hostname resolution. Check that the DNS server is correctly entered in `/etc/resolv.conf` and that instance hostname resolution is possible (in the simplest case, through an entry in `/etc/hosts`).
1. Synchronize time. Ensure that the {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}}s that belong to the same SAP system have their time synchronized. For example, connect you partition to the time server with `ntpdate -u <ntpserver>`.
1. Tune SUSE Linux&reg; Enterprise Server for the SAP HANA workload. On {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}}s, the same SUSE Linux&reg; Enterprise Server image is used for SAP NetWeaver and SAP HANA. Run the following command to tune the operating system for the SAP HANA workload: `saptune solution apply HANA`. Enable the tuning daemon by running `systemctl enable tuned`.
1. Prepare file systems on additional storage volumes. If you attached additional storage volumes to your {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}}, you must create file systems by using Linux Logical Volume Manager. For an example, see [Create file systems on SLES12 SP4 by using the command-line interface](/docs/sap-hana-power?topic=sap-hana-power-create_file_systems).
1. Register your SAP virtual server by SUSE. Register your {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}}s by SUSE (for example, via SUSE RMT server as described in the [SUSE documentation](https://documentation.suse.com/sles/15-SP1/html/SLES-all/cha-rmt-client.html){: external}).

## SAP HCMT system validation

After you configure your {{site.data.keyword.IBM_notm}} {{site.data.keyword.powerSys_notm}}s for SAP HANA, verify your system with [SAP HANA hardware and cloud measurement tools](https://help.sap.com/viewer/02bb1e64c2ae4de7a11369f4e70a6394/2.0/en-US){: external}.

For information about downloading, installing, and configuring the HCMT tool, see [SAP Note 2493172](https://launchpad.support.sap.com/#/notes/2493172){: external}. The document also provides an upload link for loading the file that is generated by HCMT so you can get a pictorial view of the health and readiness of your system.

## Next Steps
{: #configure-system-next-steps}

[Configuring system access for SAP HANA installation](/docs/sap-hana-power?topic=sap-hana-power-configure_access)

[Ordering storage](/docs/sap-hana-power?topic=sap-hana-power-manage_order_storage)

[Downloading and installing SAP software and applications](/docs/sap-hana-power?topic=sap-hana-power-download_and_install)

[Creating an SAP license key](/docs/sap-hana-power?topic=sap-hana-power-create_key)

[Monitoring the system with SAP tools](/docs/sap-hana-power?topic=sap-hana-power-monitoring)