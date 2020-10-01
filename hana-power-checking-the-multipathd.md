---

copyright:
  years: 2020
lastupdated: "2020-09-30"

keywords: SAP HANA, disk, Linux, multipathd, multipath daemon, LMV

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


# Checking the multipathd
{: #checking_the_multipathd}

Check the status of the multipath daemon after the LVM actions finish.
{: shortdesc} 

To enable the multipathd at boot time, run the following command as a root user:

```
systemctl enable multipathd
```

To check the status of the multipathd, run the following command:

```
systemctl status multipathd
```

To stop the service, run the following command. This isn't advisable because it can cause the partition to no longer boot.

```
systemctl stop multipathd
```

Whenever you enable or disable the multipathd, you must rebuild the `initrd`. After enabling the multipath services, run the following command to force a rebuild of the `initrd`:

```
dracut --force --add multipath
```

When you disable the multipath services, run the following command to force a rebuild of the `initrd`:

```
dracut --force -o multipath
```