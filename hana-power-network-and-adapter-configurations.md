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

# Verifying network and adapter configurations
{: #network_and_adapter_configurations}

Review the following considerations when you set the MTU for the adapter that is used for your private network.
{: shortdesc}

Local connections in the same data center (for example, within SAP HANA scale-out nodes or with a local system replication scenario) can often take advantage of jumbo frames (MTU = 9000).

Remote connections to other data centers (for example, with smart data access or system replication) have an increased risk that network components can't efficiently handle jumbo frames. You might need to set MTU = 1500.

If you want to check whether a connection uses jumbo frames, run the following ping command:

```
ping -M do -c 4 -s 8972 <remote_host_or_ip>
```

The ping command sends 9 KB requests to the remote host. If one component can't handle jumbo frames, the package is broken into smaller pieces. This fragmentation is not allowed due to the `-M do` option. A `100% packet loss` error is generated if all components aren't able to handle jumbo frames.

To change the network adapter for the private network, follow the steps in [Configuring the system for the SAP HANA workload](/docs/sap-hana-power?topic=sap-hana-power-configure_system).
