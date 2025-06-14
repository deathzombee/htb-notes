
# Getting Started with OpenVAS

---

[OpenVAS](https://openvas.org/), by Greenbone Networks, is a publicly available vulnerability scanner. Greenbone Networks has an entire Vulnerability Manager, part of which is the OpenVAS scanner. Greenbone's Vulnerability Manager is also open to the public and free to use. OpenVAS has the capabilities to perform network scans, including authenticated and unauthenticated testing.

![image](https://academy.hackthebox.com/storage/modules/108/openvas/Greenbone_Security_Assistant.png)

We will get started with using OpenVAS by following the installation instruction below for Parrot Security. The tool is pre-installed on the host provided in a later section.

---

## Installing Package

First, we can start by installing the tool:

Getting Started with OpenVAS

```shell-session
cdeez@htb[/htb]$ sudo apt-get update && apt-get -y full-upgrade
cdeez@htb[/htb]$ sudo apt-get install gvm && openvas
```

Next, to begin the installation process, we can run the following command below:

Getting Started with OpenVAS

```shell-session
cdeez@htb[/htb]$ gvm-setup
```

This will begin the setup process and take up to 30 minutes.

![image](https://academy.hackthebox.com/storage/modules/108/openvas/gvmsetup.png)

---

## Starting OpenVas

Finally, we can start OpenVas:

Getting Started with OpenVAS

```shell-session
cdeez@htb[/htb]$ gvm-start
```

![image](https://academy.hackthebox.com/storage/modules/108/openvas/gvmstart.png)

**Note:** The VM provided in the `OpenVAS Skills Assessment` section has OpenVAS pre-installed and the targets running. You can go to that section and start the VM and use OpenVAS throughout the module, which can be accessed at `https://< IP >:8080`. The OpenVAS credentials are: `htb-student`:`HTB_@cademy_student!`. You may also use these credentials to SSH into the target VM to configure OpenVAS.
