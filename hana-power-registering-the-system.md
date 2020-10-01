---

copyright:
  years: 2020
lastupdated: "2020-09-29"

keywords: SAP HANA, disk, registering, suse

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

# Registering the system
{: #register_system}

You can register your {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}}s with SUSE for operating system updates in one of two ways.
{: shortdesc}

* Register your system by using a public SUSE repository server. This method isn't recommended for SAP HANA systems because connectivity to the internet is required through a public network adapter.

    To register by using a public SUSE repository server, run the following command:
    ```
    SUSEConnect -r <REGISTRATION_KEY> -e <EMAIL_ADDRESS>
    ```
* Mirror operating system repositories with the SUSE Repository Mirroring Tool (RMT), and register your systems by using the SUSE RMT server. Because the mirror is running in the private network, connectivity to the internet through the public network isn't required. For more information, see [Configuring Clients to Use SUSE RMT (versions 12 and 15)](https://documentation.suse.com/sles/15-SP1/html/SLES-all/cha-rmt-client.html){: external}.

   To register by using the SUSE RMT server, run the following commands:
    ```
    curl http://<RMT_SERVER_IP>/tools/rmt-client-setup --output rmt-client-setup
    chmod +x rmt-client-setup
    ./rmt-client-setup https://<RMT_SERVER_IP>
    ```








