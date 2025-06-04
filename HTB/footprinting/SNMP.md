

`Simple Network Management Protocol` ([SNMP](https://datatracker.ietf.org/doc/html/rfc1157)) was created to monitor network devices. In addition, this protocol can also be used to handle configuration tasks and change settings remotely. SNMP-enabled hardware includes routers, switches, servers, IoT devices, and many other devices that can also be queried and controlled using this standard protocol. Thus, it is a protocol for monitoring and managing network devices. In addition, configuration tasks can be handled, and settings can be made remotely using this standard. The current version is `SNMPv3`, which increases the security of SNMP in particular, but also the complexity of using this protocol.

In addition to the pure exchange of information, SNMP also transmits control commands using agents over UDP port `161`. The client can set specific values in the device and change options and settings with these commands. While in classical communication, it is always the client who actively requests information from the server, SNMP also enables the use of so-called `traps` over UDP port `162`. These are data packets sent from the SNMP server to the client without being explicitly requested. If a device is configured accordingly, an SNMP trap is sent to the client once a specific event occurs on the server-side.

For the SNMP client and server to exchange the respective values, the available SNMP objects must have unique addresses known on both sides. This addressing mechanism is an absolute prerequisite for successfully transmitting data and network monitoring using SNMP.

#### MIB

To ensure that SNMP access works across manufacturers and with different client-server combinations, the `Management Information Base` (`MIB`) was created. MIB is an independent format for storing device information. A MIB is a text file in which all queryable SNMP objects of a device are listed in a standardized tree hierarchy. It contains at least one `Object Identifier` (`OID`), which, in addition to the necessary unique address and a name, also provides information about the type, access rights, and a description of the respective object. MIB files are written in the `Abstract Syntax Notation One` (`ASN.1`) based ASCII text format. The MIBs do not contain data, but they explain where to find which information and what it looks like, which returns values for the specific OID, or which data type is used.

#### OID

An OID represents a node in a hierarchical namespace. A sequence of numbers uniquely identifies each node, allowing the node's position in the tree to be determined. The longer the chain, the more specific the information. Many nodes in the OID tree contain nothing except references to those below them. The OIDs consist of integers and are usually concatenated by dot notation. We can look up many MIBs for the associated OIDs in the [Object Identifier Registry](https://www.alvestrand.no/objectid/).

#### SNMPv1

SNMP version 1 (`SNMPv1`) is used for network management and monitoring. SNMPv1 is the first version of the protocol and is still in use in many small networks. It supports the retrieval of information from network devices, allows for the configuration of devices, and provides traps, which are notifications of events. However, SNMPv1 has `no built-in authentication` mechanism, meaning anyone accessing the network can read and modify network data. Another main flaw of SNMPv1 is that it `does not support encryption`, meaning that all data is sent in plain text and can be easily intercepted.

#### SNMPv2

SNMPv2 existed in different versions. The version still exists today is `v2c`, and the extension `c` means community-based SNMP. Regarding security, SNMPv2 is on par with SNMPv1 and has been extended with additional functions from the party-based SNMP no longer in use. However, a significant problem with the initial execution of the SNMP protocol is that the `community string` that provides security is only transmitted in plain text, meaning it has no built-in encryption.

#### SNMPv3

The security has been increased enormously for `SNMPv3` by security features such as `authentication` using username and password and transmission `encryption` (via `pre-shared key`) of the data. However, the complexity also increases to the same extent, with significantly more configuration options than `v2c`.

#### Community Strings

Community strings can be seen as passwords that are used to determine whether the requested information can be viewed or not. It is important to note that many organizations are still using `SNMPv2`, as the transition to `SNMPv3` can be very complex, but the services still need to remain active. This causes many administrators a great deal of concern and creates some problems they are keen to avoid. The lack of knowledge about how the information can be obtained and how we as attackers use it makes the administrators' approach seem inexplicable. At the same time, the lack of encryption of the data sent is also a problem. Because every time the community strings are sent over the network, they can be intercepted and read.


```
HOST-RESOURCES-MIB::hrSWRunParameters.892 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.959 = STRING: "-F"
HOST-RESOURCES-MIB::hrSWRunParameters.961 = STRING: "-f -u bind"
HOST-RESOURCES-MIB::hrSWRunParameters.966 = STRING: "-f"
HOST-RESOURCES-MIB::hrSWRunParameters.979 = STRING: "/usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal"
HOST-RESOURCES-MIB::hrSWRunParameters.980 = STRING: "-f"
HOST-RESOURCES-MIB::hrSWRunParameters.981 = STRING: "-LOw -u Debian-snmp -g Debian-snmp -I -smux mteTrigger mteTriggerConf -f -p /run/snmpd.pid"
HOST-RESOURCES-MIB::hrSWRunParameters.1023 = STRING: "-o -p -- \\u --noclear tty1 linux"
HOST-RESOURCES-MIB::hrSWRunParameters.1038 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.1044 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.1045 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.1046 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.1081 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.2036 = STRING: "-w"
HOST-RESOURCES-MIB::hrSWRunParameters.2038 = STRING: "-l -t unix -u"
HOST-RESOURCES-MIB::hrSWRunParameters.2344 = STRING: "-l -t unix -u -c"
HOST-RESOURCES-MIB::hrSWRunParameters.2355 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.2419 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.2548 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.2995 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.3057 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.3877 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.3878 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.5856 = STRING: "-l -t unix -u -c"
HOST-RESOURCES-MIB::hrSWRunParameters.6875 = ""
HOST-RESOURCES-MIB::hrSWRunParameters.7425 = ""
HOST-RESOURCES-MIB::hrSWRunPath.663 = STRING: "/lib/systemd/systemd-timesyncd"
HOST-RESOURCES-MIB::hrSWRunPath.665 = ""
HOST-RESOURCES-MIB::hrSWRunPath.675 = STRING: "/usr/bin/VGAuthService"
HOST-RESOURCES-MIB::hrSWRunPath.676 = STRING: "/usr/bin/vmtoolsd"
HOST-RESOURCES-MIB::hrSWRunPath.712 = STRING: "/sbin/dhclient"
HOST-RESOURCES-MIB::hrSWRunPath.740 = STRING: "/usr/lib/accountsservice/accounts-daemon"
HOST-RESOURCES-MIB::hrSWRunPath.741 = STRING: "/usr/bin/dbus-daemon"
HOST-RESOURCES-MIB::hrSWRunPath.746 = STRING: "/usr/sbin/irqbalance"
HOST-RESOURCES-MIB::hrSWRunPath.748 = STRING: "/usr/bin/python3"
HOST-RESOURCES-MIB::hrSWRunPath.752 = STRING: "/usr/sbin/rsyslogd"
HOST-RESOURCES-MIB::hrSWRunPath.755 = STRING: "/usr/lib/snapd/snapd"
HOST-RESOURCES-MIB::hrSWRunPath.756 = STRING: "/lib/systemd/systemd-logind"
HOST-RESOURCES-MIB::hrSWRunPath.757 = STRING: "/usr/lib/udisks2/udisksd"
HOST-RESOURCES-MIB::hrSWRunPath.833 = STRING: "/usr/lib/policykit-1/polkitd"
HOST-RESOURCES-MIB::hrSWRunPath.892 = STRING: "/lib/systemd/systemd-resolved"
HOST-RESOURCES-MIB::hrSWRunPath.959 = STRING: "/usr/sbin/dovecot"
HOST-RESOURCES-MIB::hrSWRunPath.961 = STRING: "/usr/sbin/named"
HOST-RESOURCES-MIB::hrSWRunPath.966 = STRING: "/usr/sbin/cron"
HOST-RESOURCES-MIB::hrSWRunPath.979 = STRING: "/usr/bin/python3"
HOST-RESOURCES-MIB::hrSWRunPath.980 = STRING: "/usr/sbin/atd"
HOST-RESOURCES-MIB::hrSWRunPath.981 = STRING: "/usr/sbin/snmpd"
HOST-RESOURCES-MIB::hrSWRunPath.1023 = STRING: "/sbin/agetty"
HOST-RESOURCES-MIB::hrSWRunPath.1038 = STRING: "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
HOST-RESOURCES-MIB::hrSWRunPath.1044 = STRING: "dovecot/anvil"
HOST-RESOURCES-MIB::hrSWRunPath.1045 = STRING: "dovecot/log"
HOST-RESOURCES-MIB::hrSWRunPath.1046 = STRING: "dovecot/config"
HOST-RESOURCES-MIB::hrSWRunPath.1081 = STRING: "/usr/sbin/mysqld"
HOST-RESOURCES-MIB::hrSWRunPath.2036 = STRING: "/usr/lib/postfix/sbin/master"
HOST-RESOURCES-MIB::hrSWRunPath.2038 = STRING: "qmgr"
HOST-RESOURCES-MIB::hrSWRunPath.2344 = STRING: "tlsmgr"
HOST-RESOURCES-MIB::hrSWRunPath.2355 = STRING: "dovecot/stats"

```


```
sudo  nmap -sU -p 161 --script=snmp-netstat 10.129.232.101
[sudo] password for dz: 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-02 13:45 PDT
Nmap scan report for 10.129.232.101
Host is up (0.35s latency).

PORT    STATE SERVICE
161/udp open  snmp
| snmp-netstat: 
|   TCP  0.0.0.0:22           0.0.0.0:0
|   TCP  0.0.0.0:25           0.0.0.0:0
|   TCP  0.0.0.0:110          0.0.0.0:0
|   TCP  0.0.0.0:143          0.0.0.0:0
|   TCP  0.0.0.0:993          0.0.0.0:0
|   TCP  0.0.0.0:995          0.0.0.0:0
|   TCP  0.0.0.0:3306         0.0.0.0:0
|   TCP  0.0.0.0:33060        0.0.0.0:0
|   TCP  10.129.232.101:53    0.0.0.0:0
|   TCP  10.129.232.101:58842 8.8.8.8:53
|   TCP  127.0.0.1:53         0.0.0.0:0
|   TCP  127.0.0.1:953        0.0.0.0:0
|   TCP  127.0.0.53:53        0.0.0.0:0
|   UDP  0.0.0.0:68           *:*
|   UDP  0.0.0.0:161          *:*
|   UDP  10.129.232.101:53    *:*
|   UDP  127.0.0.1:53         *:*
|_  UDP  127.0.0.53:53        *:*

Nmap done: 1 IP address (1 host up) scanned in 7.43 seconds
```


>https://medium.com/@minimalist.ascent/enumerating-snmp-servers-with-nmap-89aaf33bce28


```
➜  HTB snmpwalk -v2c -c public 10.129.232.101 -Lf output.txt

SNMPv2-MIB::sysDescr.0 = STRING: Linux NIX02 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64
SNMPv2-MIB::sysObjectID.0 = OID: NET-SNMP-MIB::netSnmpAgentOIDs.10
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (1316435) 3:39:24.35
SNMPv2-MIB::sysContact.0 = STRING: devadmin <devadmin@inlanefreight.htb>
SNMPv2-MIB::sysName.0 = STRING: NIX02
SNMPv2-MIB::sysLocation.0 = STRING: InFreight SNMP v0.91
SNMPv2-MIB::sysServices.0 = INTEGER: 72
SNMPv2-MIB::sysORLastChange.0 = Timeticks: (48) 0:00:00.48
SNMPv2-MIB::sysORID.1 = OID: SNMP-FRAMEWORK-MIB::snmpFrameworkMIBCompliance
SNMPv2-MIB::sysORID.2 = OID: SNMP-MPD-MIB::snmpMPDCompliance
SNMPv2-MIB::sysORID.3 = OID: SNMP-USER-BASED-SM-MIB::usmMIBCompliance
SNMPv2-MIB::sysORID.4 = OID: SNMPv2-MIB::snmpMIB
SNMPv2-MIB::sysORID.5 = OID: SNMP-VIEW-BASED-ACM-MIB::vacmBasicGroup
SNMPv2-MIB::sysORID.6 = OID: TCP-MIB::tcpMIB
SNMPv2-MIB::sysORID.7 = OID: IP-MIB::ip
SNMPv2-MIB::sysORID.8 = OID: UDP-MIB::udpMIB
SNMPv2-MIB::sysORID.9 = OID: SNMP-NOTIFICATION-MIB::snmpNotifyFullCompliance
SNMPv2-MIB::sysORID.10 = OID: NOTIFICATION-LOG-MIB::notificationLogMIB

```


```
HOST-RESOURCES-MIB::hrSystemInitialLoadDevice.0 = INTEGER: 393216
HOST-RESOURCES-MIB::hrSystemInitialLoadParameters.0 = STRING: "BOOT_IMAGE=/vmlinuz-5.4.0-90-generic root=/dev/mapper/ubuntu--vg-ubuntu--lv ro ipv6.disable=1 maybe-ubiquity
"
HOST-RESOURCES-MIB::hrSystemNumUsers.0 = Gauge32: 0
HOST-RESOURCES-MIB::hrSystemProcesses.0 = Gauge32: 163
HOST-RESOURCES-MIB::hrSystemMaxProcesses.0 = INTEGER: 0
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.1.0 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.2.4.70.76.65.71 = Wrong Type (should be INTEGER): STRING: "/usr/share/flag.sh"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.3.4.70.76.65.71 = Wrong Type (should be INTEGER): ""
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.4.4.70.76.65.71 = Wrong Type (should be INTEGER): ""
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.5.4.70.76.65.71 = INTEGER: 5
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.6.4.70.76.65.71 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.7.4.70.76.65.71 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.20.4.70.76.65.71 = INTEGER: 4
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.21.4.70.76.65.71 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.3.1.1.4.70.76.65.71 = Wrong Type (should be INTEGER): STRING: "HTB{5nMp_fl4g_uidhfljnsldiuhbfsdij44738b2u763g}"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.3.1.2.4.70.76.65.71 = Wrong Type (should be INTEGER): STRING: "HTB{5nMp_fl4g_uidhfljnsldiuhbfsdij44738b2u763g}"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.3.1.3.4.70.76.65.71 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.3.1.4.4.70.76.65.71 = INTEGER: 0
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.4.1.2.4.70.76.65.71.1 = Wrong Type (should be INTEGER): STRING: "HTB{5nMp_fl4g_uidhfljnsldiuhbfsdij44738b2u763g}"

```