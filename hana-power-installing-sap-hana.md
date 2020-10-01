---

copyright:
  years: 2020
lastupdated: "2020-09-21"

keywords: SAP HANA, linux, jump, server

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

# Installing SAP HANA 
{: #installing_sap_hana}

Instead of a Windows jump server, you can provision a Linux&reg; jump server and a server with a public and private network. You can use this server as a software repository.
{: shortdesc}

When you provision the jump server, remember to request more disk space so you can create the LVM setup and directory structure. Because the jump server has public access, it can access SAP Market Place and download the software on to the locations you specify. Then, you can enable the file system to be shared with NFS across your new cloud landscape.

There are several benefits to this approach:

* Your software is centrally located; there's no need to provision more storage on your {{site.data.keyword.IBM}} {{site.data.keyword.powerSysShort}} instances. Mount the jump server on each new server and install the software.
* The jump server has a public IP interface. You can create a shadow of the SUSE software repositories.
* It's easier for SAP Basis Administrators to manage one location instead of several.

When you use this setup, you can mount remotely through NFS. Remember to activate `rpcbind` on your {{site.data.keyword.powerSys_notm}}:

1. Run the following command:

    ```
    systemctl start rpcbind
    ```
1. Check that the service is active:

    ```
    systemctl status rpcbind
    ```
1. Start the NFS client service:

    ```
    systemctl start nfs
    ```