---

copyright:
  years: 2020
lastupdated: "2020-09-14"

keywords: SAP HANA, disk, hostname, verification

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

# Hostname verification
{: #hostname_verification}

Make sure that your {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}} hostname resolves correctly.
{: shortdesc}

Check that the DNS server is entered correctly in `/etc/resolv.conf` and that instance hostname resolution is possible (in the simplest case, through an entry in `/etc/hosts`).

If you are using virtual hostnames for the SAP HANA database server, make sure that the IP addresses, short name, and fully qualified domain names are includes in the hosts file on the SAP HANA server and on any application servers that are connected to the database instance. Issues with hostname or virtual hostname resolution cause problems when you connect the application server to the database backend and configure the hdbuserstore. 


