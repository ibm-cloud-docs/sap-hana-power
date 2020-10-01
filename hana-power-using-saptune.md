---

copyright:
  years: 2020
lastupdated: "2020-09-17"

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

# Using saptune
{: #using_saptune}

Use the `saptune` tool to apply the HANA solution to your server. The HANA solution applies recommended operating system settings for SAP HANA on SUSE Linux&reg; Enterprise Server. 
{: shortdesc}

The following sample workflow shows how you can use the `saptune` tool to apply the HANA solution to your server. For more information about `saptune`, see [SAP Note 1275776 - Linux: Preparing SLES for SAP environments](https://launchpad.support.sap.com/#/notes/1275776){: external}.


1. Verify that the package status is current.
    ```
    zypper info saptune
    ```
1. Verify that the saptune version is at least 2.
    ```
    saptune version
    ```
1. List all available solutions. Numbered entries represent integrated SAP Notes for each of the solutions.
    ```
    saptune solution list
    ```
1. Get an overview of `saptune` options.
    ```
    saptune --help
    ```
1. List SUSE OS defaults for instance network tunables and THP. Most of the defaults aren't set correctly for SAP HANA.
    ```
    sysctl -a| grep -E 
    ``` 
1. Optional: Simulate the changes that will be applied.
    ```
    saptune solution simulate HANA 
    ```
    `saptune` autotunes parameters based on fixed or calculated values. `saptune` indicates which parameters can't be changed automatically, and provides links to related SAP or IBM documentation to assist with manual steps.
    {: note}
1. Apply the HANA saptune solution.
    ```
    saptune solution apply HANA 
    ```
1. If you want to automatically activate the solution's tuning options after a reboot, run the following command:
    ```
    saptune daemon start 
    ```

To diagnose startup issues, see [SAP Note 401162 - Linux: Avoiding TCP/IP port conflicts and start problems](https://launchpad.support.sap.com/#/notes/401162){: external}.
{: tip}

