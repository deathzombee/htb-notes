
Nmap scan report for 10.129.202.20
Host is up (0.12s latency).
Not shown: 779 closed tcp ports (conn-refused), 216 filtered tcp ports (no-response)
PORT    STATE SERVICE
22/tcp  open  ssh
110/tcp open  pop3
143/tcp open  imap
993/tcp open  imaps
995/tcp open  pop3s


```
➜  ~ sudo nmap 10.129.202.20 -sV -p110,143,993,995 -sC
[sudo] password for dz: 
Starting Nmap 7.95 ( https://nmap.org ) at 2024-06-03 03:02 PDT
Stats: 0:00:16 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 43.75% done; ETC: 03:02 (0:00:00 remaining)
Nmap scan report for 10.129.202.20
Host is up (0.20s latency).

PORT    STATE SERVICE  VERSION
110/tcp open  pop3     Dovecot pop3d
|_pop3-capabilities: STLS CAPA UIDL AUTH-RESP-CODE RESP-CODES TOP PIPELINING USER SASL(PLAIN)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
143/tcp open  imap     Dovecot imapd (Ubuntu)
|_imap-capabilities: AUTH=PLAINA0001 STARTTLS IMAP4rev1 capabilities ENABLE more have post-login listed IDLE OK LOGIN-REFERRALS ID LITERAL+ Pre-login SASL-IR
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
993/tcp open  ssl/imap Dovecot imapd (Ubuntu)
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: AUTH=PLAINA0001 SASL-IR IMAP4rev1 capabilities ENABLE more post-login listed have LOGIN-REFERRALS OK ID LITERAL+ Pre-login IDLE
995/tcp open  ssl/pop3 Dovecot pop3d
|_pop3-capabilities: TOP CAPA SASL(PLAIN) USER UIDL AUTH-RESP-CODE RESP-CODES PIPELINING
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_ssl-date: TLS randomness does not represent time
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.33 seconds
```

```
➜  ~ sudo nmap -sU 10.129.202.20
[sudo] password for dz: 
Starting Nmap 7.95 ( https://nmap.org ) at 2024-06-03 03:40 PDT
Stats: 0:00:02 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 1.73% done; ETC: 03:42 (0:01:53 remaining)
Stats: 0:01:36 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 9.58% done; ETC: 03:57 (0:15:06 remaining)
Stats: 0:01:38 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 9.88% done; ETC: 03:57 (0:14:54 remaining)
Stats: 0:14:56 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 85.48% done; ETC: 03:58 (0:02:32 remaining)
Nmap scan report for 10.129.202.20
Host is up (0.19s latency).
Not shown: 998 closed udp ports (port-unreach)
PORT    STATE         SERVICE
68/udp  open|filtered dhcpc
161/udp open          snmp

```


```
➜  foot-h sudo nmap -sU -p 161 -sV -sC 10.129.90.41 
Starting Nmap 7.95 ( https://nmap.org ) at 2024-06-03 04:12 PDT
Nmap scan report for 10.129.90.41
Host is up (0.20s latency).

PORT    STATE SERVICE VERSION
161/udp open  snmp    net-snmp; net-snmp SNMPv3 server
| snmp-info: 
|   enterprise: net-snmp
|   engineIDFormat: unknown
|   engineIDData: 5b99e75a10288b6100000000
|   snmpEngineBoots: 11
|_  snmpEngineTime: 1m25s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.86 seconds
```


# oids
>oids obtained using community string list and onesixtyone
>followed by snmpwalk from backup

```
➜  foot-h onesixtyone -c commun.txt 10.129.90.41
Scanning 1 hosts, 1 communities
Cant open hosts file, scanning single host: 10.129.90.41
10.129.90.41 [backup] Linux NIXHARD 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64
➜  foot-h rm snmp-community.txt 
➜  foot-h nano snmp-community.txt
➜  foot-h onesixtyone -c snmp-community.txt 10.129.90.41
Scanning 1 hosts, 3217 communities
Cant open hosts file, scanning single host: 10.129.90.41
10.129.90.41 [backup] Linux NIXHARD 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64
➜  foot-h snmpwalk -v 2c -c backup 10.129.90.41   
SNMPv2-MIB::sysDescr.0 = STRING: Linux NIXHARD 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64
SNMPv2-MIB::sysObjectID.0 = OID: NET-SNMP-MIB::netSnmpAgentOIDs.10
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (82049) 0:13:40.49
SNMPv2-MIB::sysContact.0 = STRING: Admin <tech@inlanefreight.htb>
SNMPv2-MIB::sysName.0 = STRING: NIXHARD
SNMPv2-MIB::sysLocation.0 = STRING: Inlanefreight
SNMPv2-MIB::sysServices.0 = INTEGER: 72
SNMPv2-MIB::sysORLastChange.0 = Timeticks: (35) 0:00:00.35
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
SNMPv2-MIB::sysORDescr.1 = STRING: The SNMP Management Architecture MIB.
SNMPv2-MIB::sysORDescr.2 = STRING: The MIB for Message Processing and Dispatching.
SNMPv2-MIB::sysORDescr.3 = STRING: The management information definitions for the SNMP User-based Security Model.
SNMPv2-MIB::sysORDescr.4 = STRING: The MIB module for SNMPv2 entities
SNMPv2-MIB::sysORDescr.5 = STRING: View-based Access Control Model for SNMP.
SNMPv2-MIB::sysORDescr.6 = STRING: The MIB module for managing TCP implementations
SNMPv2-MIB::sysORDescr.7 = STRING: The MIB module for managing IP and ICMP implementations
SNMPv2-MIB::sysORDescr.8 = STRING: The MIB module for managing UDP implementations
SNMPv2-MIB::sysORDescr.9 = STRING: The MIB modules for managing SNMP Notification, plus filtering.
SNMPv2-MIB::sysORDescr.10 = STRING: The MIB module for logging SNMP Notifications.
SNMPv2-MIB::sysORUpTime.1 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.2 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.3 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.4 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.5 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.6 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.7 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.8 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.9 = Timeticks: (35) 0:00:00.35
SNMPv2-MIB::sysORUpTime.10 = Timeticks: (35) 0:00:00.35
HOST-RESOURCES-MIB::hrSystemUptime.0 = Timeticks: (83352) 0:13:53.52
HOST-RESOURCES-MIB::hrSystemDate.0 = STRING: 2024-6-3,11:25:4.0,+0:0
HOST-RESOURCES-MIB::hrSystemInitialLoadDevice.0 = INTEGER: 393216
HOST-RESOURCES-MIB::hrSystemInitialLoadParameters.0 = STRING: "BOOT_IMAGE=/vmlinuz-5.4.0-90-generic root=/dev/mapper/ubuntu--vg-ubuntu--lv ro ipv6.disable=1 maybe-ubiquity
"
HOST-RESOURCES-MIB::hrSystemNumUsers.0 = Gauge32: 0
HOST-RESOURCES-MIB::hrSystemProcesses.0 = Gauge32: 140
HOST-RESOURCES-MIB::hrSystemMaxProcesses.0 = INTEGER: 0
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.1.0 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.2.6.66.65.67.75.85.80 = Wrong Type (should be INTEGER): STRING: "/opt/tom-recovery.sh"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.3.6.66.65.67.75.85.80 = Wrong Type (should be INTEGER): STRING: "tom NMds732Js2761"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.4.6.66.65.67.75.85.80 = Wrong Type (should be INTEGER): ""
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.5.6.66.65.67.75.85.80 = INTEGER: 5
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.6.6.66.65.67.75.85.80 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.7.6.66.65.67.75.85.80 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.20.6.66.65.67.75.85.80 = INTEGER: 4
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.21.6.66.65.67.75.85.80 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.3.1.1.6.66.65.67.75.85.80 = Wrong Type (should be INTEGER): STRING: "chpasswd: (user tom) pam_chauthtok() failed, error:"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.3.1.2.6.66.65.67.75.85.80 = Wrong Type (should be INTEGER): STRING: "chpasswd: (user tom) pam_chauthtok() failed, error:
Authentication token manipulation error
chpasswd: (line 1, user tom) password not changed
Changing password for tom."
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.3.1.3.6.66.65.67.75.85.80 = INTEGER: 4
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.3.1.4.6.66.65.67.75.85.80 = INTEGER: 1
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.4.1.2.6.66.65.67.75.85.80.1 = Wrong Type (should be INTEGER): STRING: "chpasswd: (user tom) pam_chauthtok() failed, error:"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.4.1.2.6.66.65.67.75.85.80.2 = Wrong Type (should be INTEGER): STRING: "Authentication token manipulation error"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.4.1.2.6.66.65.67.75.85.80.3 = Wrong Type (should be INTEGER): STRING: "chpasswd: (line 1, user tom) password not changed"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.4.1.2.6.66.65.67.75.85.80.4 = Wrong Type (should be INTEGER): STRING: "Changing password for tom."
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.4.1.2.6.66.65.67.75.85.80.4 = No more variables left in this MIB View (It is past the end of the MIB tree)
➜  foot-h 
```

# login with imaps

```
 foot-h openssl s_client -connect 10.129.90.41:imaps
Connecting to 10.129.90.41
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN=NIXHARD
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=NIXHARD
verify return:1
---
Certificate chain
 0 s:CN=NIXHARD
   i:CN=NIXHARD
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Nov 10 01:30:25 2021 GMT; NotAfter: Nov  8 01:30:25 2031 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIC0zCCAbugAwIBAgIUC6tYfrtqQqCrhjYv11bUtaKet3EwDQYJKoZIhvcNAQEL
BQAwEjEQMA4GA1UEAwwHTklYSEFSRDAeFw0yMTExMTAwMTMwMjVaFw0zMTExMDgw
MTMwMjVaMBIxEDAOBgNVBAMMB05JWEhBUkQwggEiMA0GCSqGSIb3DQEBAQUAA4IB
DwAwggEKAoIBAQDEBpDfkH4Ro5ZXW44NvnF3N9lKz27V1hgRppyUk5y/SEPKt2zj
EU+r2tEHUeHoJHQZBbW0ybxh+X2H3ZPNEG9nV1GtFQfTBVcrUEpN5VV15aIbdh+q
j53pp/wcL/d8+Zg2ZAaVYWvQHVqtsAudQmynrV1MHA39A44fG3/SutKlurY8AKR0
MW5zMPtflMc/N3+lH8UUMBf2Q+zNSyZLiBEihxK3kfMW92HqWeh016egSIFuxUsH
kk4xpGmyG9NDYna47dQzoHCg+42KgqFvWrGw2nIccaEIX5XA8rU9u53C7EQzDzmQ
vAtHpKWBwNmiivxAz/QC7MPExWIWtZtOqxmfAgMBAAGjITAfMAkGA1UdEwQCMAAw
EgYDVR0RBAswCYIHTklYSEFSRDANBgkqhkiG9w0BAQsFAAOCAQEAG+Dm9pLJgNGC
X1YmznmtBUekhXMrU67tQl745fFasJQzIrDgVtK27fjAtQRwvIbDruSwTj47E7+O
XdS7qyjFNBerklWNq4fEAVI7BmkxnTS9542okA/+UmeG70LdKjzFS+LjjOnyWzTh
YwU8uUjLfnRca74kY0DkVHOIkwZQha0J+BrKSADq/zDjkG0g4v0vzHINOmHx9eiE
67NoJKJPY5S3RYWxl/4x8Kphx7PNJBPC75gYjlxxDhxdYu9a3daqJUa58/qOm6P8
w1P9nA6lkg7NopyqepulLAzIcqnTjb/nMD2Pd9b6vgWc3IqSfFreqjzshZ+FjNZo
zR+tR6z4TQ==
-----END CERTIFICATE-----
subject=CN=NIXHARD
issuer=CN=NIXHARD
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1283 bytes and written 379 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
This TLS version forbids renegotiation.
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 9D9F38335A449F229869688E47144E888B5158FEFEB8FFD9AF2EE1883A30F7D4
    Session-ID-ctx: 
    Resumption PSK: 9C352D52CA1D3A02E9AC2E103C48214D3E26515B747F6E9FA7BEEE6396FDC6BAB2FF9D6133176EDC4557779768B5AEB2
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - e4 5e e4 a5 8b 85 ac 16-8e d2 f4 26 3e f0 15 e6   .^.........&>...
    0010 - 43 74 0d c1 ef cd 59 1d-52 a0 6d e1 83 7f 4f 27   Ct....Y.R.m...O'
    0020 - 61 44 40 78 d0 29 d8 4c-b0 d6 28 91 61 ea 34 75   aD@x.).L..(.a.4u
    0030 - 3b 55 8e 48 d1 0a c8 83-20 5f 52 3f 0e 11 1e 8a   ;U.H.... _R?....
    0040 - 7e e5 de b8 c3 8f 47 98-b1 57 6c 0f 24 1b 47 b3   ~.....G..Wl.$.G.
    0050 - 85 8d 57 13 4f 5e d9 19-3b ac b9 cc 12 af f3 08   ..W.O^..;.......
    0060 - dd 13 95 44 8c 58 a2 01-48 00 72 05 b7 00 08 7a   ...D.X..H.r....z
    0070 - 89 eb d2 7b 75 13 f0 5a-d9 e6 fa 5e 7d 54 6d 8f   ...{u..Z...^}Tm.
    0080 - 84 bc b3 c4 35 45 ba 89-3a f6 6b 06 06 bb dd 28   ....5E..:.k....(
    0090 - 0c af 32 e2 43 c9 59 c9-51 df b9 75 69 03 0b a5   ..2.C.Y.Q..ui...
    00a0 - e3 1a 6a 29 f3 1b 32 00-41 b2 7e 39 be ab 9b 16   ..j)..2.A.~9....
    00b0 - 63 61 6b 2d b7 9c a7 e7-bf 57 da 78 ce 82 ba f2   cak-.....W.x....

    Start Time: 1717414360
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: C0E14E924DD5543FF957CCD1B766B436B0CF5C25F9A318D2600C6A3A72C8F27C
    Session-ID-ctx: 
    Resumption PSK: F13F7E038870021646F9065C9D7139D56D855B608100DD2B1CE0C44208872CB25D7CF52B692A594B7D41C9A61FCFE5F0
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - e4 5e e4 a5 8b 85 ac 16-8e d2 f4 26 3e f0 15 e6   .^.........&>...
    0010 - a1 f3 7e 6f 38 95 49 51-89 6f 95 f1 78 95 02 f5   ..~o8.IQ.o..x...
    0020 - 4c 2d e2 89 0c 2b f5 73-33 92 5f 88 dd 4e a8 b5   L-...+.s3._..N..
    0030 - 3a 0b 89 14 ad 41 d5 a2-74 95 a2 e4 18 13 95 45   :....A..t......E
    0040 - 94 ae 3d 1c 9e 9f 1f 20-72 4f 21 bd f7 48 fe 34   ..=.... rO!..H.4
    0050 - 04 14 1a 67 aa bf 01 30-4f 1d 36 5a 6a a1 62 64   ...g...0O.6Zj.bd
    0060 - 00 78 9c 2c 09 5d e0 d7-07 97 4c 76 6a 4b a9 f4   .x.,.]....LvjK..
    0070 - e2 ef c3 63 e7 63 50 d7-55 b3 4a 64 cb 2a bf 83   ...c.cP.U.Jd.*..
    0080 - 2b ee 3e bd 7f e1 b5 e6-b6 b9 ee 59 e4 3e a5 94   +.>........Y.>..
    0090 - 99 0c a8 77 ef 49 58 a8-d8 f3 a1 a7 60 1b cb e3   ...w.IX.....`...
    00a0 - 94 34 bc 3e 74 80 95 97-ac ed 69 d4 d9 58 46 63   .4.>t.....i..XFc
    00b0 - 04 c0 5f 35 e0 7c d0 1f-e3 ec 74 17 37 6c 0a 6d   .._5.|....t.7l.m

    Start Time: 1717414360
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
* OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN] Dovecot (Ubuntu) ready.
1 LOGIN tom
1 BAD Error in IMAP command received by server.
1 LOGIN tom NMds732Js2761        
1 OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY PREVIEW=FUZZY LITERAL+ NOTIFY SPECIAL-USE] Logged in

```

> list , remember to put a unique identifier before the command in imaps

```
read R BLOCK
* OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN] Dovecot (Ubuntu) ready.
1 LOGIN tom
1 BAD Error in IMAP command received by server.
1 LOGIN tom NMds732Js2761        
1 OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY PREVIEW=FUZZY LITERAL+ NOTIFY SPECIAL-USE] Logged in
1 LIST "" *
* LIST (\HasNoChildren) "." Notes
* LIST (\HasNoChildren) "." Meetings
* LIST (\HasNoChildren \UnMarked) "." Important
* LIST (\HasNoChildren) "." INBOX
1 OK List completed (0.007 + 0.000 + 0.007 secs).

```


>select inbox and print the entire email

```
1 SELECT INBOX
* OK [CLOSED] Previous mailbox closed.
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 1 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1636509064] UIDs valid
* OK [UIDNEXT 2] Predicted next UID
1 OK [READ-WRITE] Select completed (0.006 + 0.000 + 0.005 secs).
1 FETCH 1 (BODY[])
* 1 FETCH (BODY[] {3661}
HELO dev.inlanefreight.htb
MAIL FROM:<tech@dev.inlanefreight.htb>
RCPT TO:<bob@inlanefreight.htb>
DATA
From: [Admin] <tech@inlanefreight.htb>
To: <tom@inlanefreight.htb>
Date: Wed, 10 Nov 2010 14:21:26 +0200
Subject: KEY

-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
)
1 OK Fetch completed (0.004 + 0.000 + 0.003 secs).

```

> now we have an ssh private key
> make that file and ssh in, remember to set correct permissions for private key file


```
➜  foot-h nano foot-h-key
➜  foot-h ssh tom@10.129.90.41 -i foot-h-key 
The authenticity of host '10.129.90.41 (10.129.90.41)' can't be established.
ED25519 key fingerprint is SHA256:AtNYHXCA7dVpi58LB+uuPe9xvc2lJwA6y7q82kZoBNM.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:28: 10.129.42.195
    ~/.ssh/known_hosts:49: 10.129.202.20
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.129.90.41' (ED25519) to the list of known hosts.
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for 'foot-h-key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "foot-h-key": bad permissions
tom@10.129.90.41: Permission denied (publickey).
➜  foot-h chmod 600 foot-h-key 
➜  foot-h ssh tom@10.129.90.41 -i foot-h-key
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-90-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon 03 Jun 2024 11:48:07 AM UTC

  System load:  0.16              Processes:               166
  Usage of /:   68.6% of 5.40GB   Users logged in:         0
  Memory usage: 29%               IPv4 address for ens192: 10.129.90.41
  Swap usage:   0%

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

0 updates can be applied immediately.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Wed Nov 10 02:51:52 2021 from 10.10.14.20
tom@NIXHARD:~$ 

```


>find other users

```
agentx  backups  cache  crash  lib  local  lock  log  mail  opt  run  snap  spool  tmp
tom@NIXHARD:/var$ lsof -i
tom@NIXHARD:/var$ cd /
tom@NIXHARD:/$ cd e 
tom@NIXHARD:~$ cd /etc/
tom@NIXHARD:/etc$ ls
adduser.conf                   group-           mime.types               security
alternatives                   grub.d           mke2fs.conf              selinux
apparmor                       gshadow          modprobe.d               sensors3.conf
apparmor.d                     gshadow-         modules                  sensors.d
apport                         gss              modules-load.d           services
apt                            hdparm.conf      mtab                     shadow
at.deny                        host.conf        multipath.conf           shadow-
bash.bashrc                    hostname         mysql                    shells
bash_completion                hosts            nanorc                   skel
bash_completion.d              hosts.allow      network                  snmp
bindresvport.blacklist         hosts.deny       networkd-dispatcher      snmp-mibs-downloader
binfmt.d                       init             networks                 sos
byobu                          init.d           newt                     sos.conf
ca-certificates                initramfs-tools  nsswitch.conf            ssh
ca-certificates.conf           inputrc          opt                      ssl
ca-certificates.conf.dpkg-old  iproute2         os-release               subgid
calendar                       iscsi            overlayroot.conf         subgid-
cloud                          issue            PackageKit               subuid
console-setup                  issue.net        pam.conf                 subuid-
cron.d                         kernel           pam.d                    sudoers
cron.daily                     landscape        passwd                   sudoers.d
cron.hourly                    ldap             passwd-                  sysctl.conf
cron.monthly                   ld.so.cache      perl                     sysctl.d
crontab                        ld.so.conf       pki                      systemd
cron.weekly                    ld.so.conf.d     pm                       terminfo
cryptsetup-initramfs           legal            polkit-1                 thermald
crypttab                       libaudit.conf    pollinate                timezone
dbus-1                         libblockdev      popularity-contest.conf  tmpfiles.d
dconf                          libnl-3          profile                  ubuntu-advantage
debconf.conf                   locale.alias     profile.d                ucf.conf
debian_version                 locale.gen       protocols                udev
default                        localtime        python3                  udisks2
deluser.conf                   logcheck         python3.8                ufw
depmod.d                       login.defs       rc0.d                    update-manager
dhcp                           logrotate.conf   rc1.d                    update-motd.d
dovecot                        logrotate.d      rc2.d                    update-notifier
dpkg                           lsb-release      rc3.d                    UPower
e2scrub.conf                   ltrace.conf      rc4.d                    vim
environment                    lvm              rc5.d                    vmware-tools
ethertypes                     machine-id       rc6.d                    vtrgb
fonts                          magic            rcS.d                    wgetrc
fstab                          magic.mime       resolv.conf              X11
fuse.conf                      mailcap          rmt                      xattr.conf
fwupd                          mailcap.order    rpc                      xdg
gai.conf                       manpath.config   rsyslog.conf             zsh_command_not_found
groff                          mdadm            rsyslog.d
group                          mecabrc          screenrc
tom@NIXHARD:/etc$ cat passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:106::/nonexistent:/usr/sbin/nologin
syslog:x:104:110::/home/syslog:/usr/sbin/nologin
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false
uuidd:x:107:112::/run/uuidd:/usr/sbin/nologin
tcpdump:x:108:113::/nonexistent:/usr/sbin/nologin
landscape:x:109:115::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:110:1::/var/cache/pollinate:/bin/false
sshd:x:111:65534::/run/sshd:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
ubuntu:x:1000:1000:ubuntu:/home/ubuntu:/bin/bash
lxd:x:998:100::/var/snap/lxd/common/lxd:/bin/false
cry0l1t3:x:1001:1001:,,,:/home/cry0l1t3:/bin/bash
usbmux:x:112:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
mysql:x:114:119:MySQL Server,,,:/nonexistent:/bin/false
tom:x:1002:1002:,,,:/home/tom:/bin/bash
dovecot:x:113:120:Dovecot mail server,,,:/usr/lib/dovecot:/usr/sbin/nologin
dovenull:x:115:121:Dovecot login user,,,:/nonexistent:/usr/sbin/nologin
Debian-snmp:x:116:122::/var/lib/snmp:/bin/false
```

```

tom@NIXHARD:/etc$ cat gro
groff/  group   group-  
tom@NIXHARD:/etc$ cat gro
groff/  group   group-  
tom@NIXHARD:/etc$ cat group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,ubuntu
tty:x:5:syslog
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:ubuntu
floppy:x:25:
tape:x:26:
sudo:x:27:ubuntu,cry0l1t3
audio:x:29:
dip:x:30:ubuntu
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
gnats:x:41:
shadow:x:42:
utmp:x:43:
video:x:44:
sasl:x:45:
plugdev:x:46:ubuntu
staff:x:50:
games:x:60:
users:x:100:
nogroup:x:65534:
systemd-journal:x:101:
systemd-network:x:102:
systemd-resolve:x:103:
systemd-timesync:x:104:
crontab:x:105:
messagebus:x:106:
input:x:107:
kvm:x:108:
render:x:109:
syslog:x:110:
tss:x:111:
uuidd:x:112:
tcpdump:x:113:
ssh:x:114:
landscape:x:115:
lxd:x:116:ubuntu
systemd-coredump:x:999:
ubuntu:x:1000:
netdev:x:117:
cry0l1t3:x:1001:
mysql:x:119:tom
tom:x:1002:
ssl-cert:x:118:
dovecot:x:120:
dovenull:x:121:
Debian-snmp:x:122:
```

>what groups are tom in?

```
tom@NIXHARD:/etc$ grep tom group
mysql:x:119:tom
tom:x:1002:
tom@NIXHARD:/etc$ 
```

> from earlier 

```
Type (should be INTEGER): STRING: "/opt/tom-recovery.sh"
HOST-RESOURCES-MIB::hrSystemMaxProcesses.1.2.1.3.6.66.65.67.75.85.80 = Wrong Type (should be INTEGER): STRING: "tom NMds732Js2761"
```

> mysql -utom -pNMds732Js2761


```
tom@NIXHARD:~/Maildir/cur$ mysql -utom -pNMds732Js2761
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.27-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

No entry for terminal type "xterm-kitty";
using dumb terminal settings.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```


> list the databases

```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| users              |
+--------------------+
5 rows in set (0.01 sec)

mysql> 
```

> all bases are belong to me 

```
mysql> USE users;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW tables
    -> ;
+-----------------+
| Tables_in_users |
+-----------------+
| users           |
+-----------------+
1 row in set (0.00 sec)

mysql> select * from users;
+------+-------------------+------------------------------+
| id   | username          | password                     |
+------+-------------------+------------------------------+
|    1 | ppavlata0         | 6znAfvTbB2                   |
|    2 | ktofanini1        | TP2NxFD62e                   |
|    3 | rallwell2         | t1t7WaqvEfv                  |
|    4 | efernier3         | ZRYOBO9PI                    |
|    5 | fpoon4            | 5Spyx2Jb                     |
|    6 | jgurnell5         | LMCnWKD                      |
|    7 | aminter6          | ngCyGg3                      |
|    8 | dwattinham7       | H2bpGC5                      |
|    9 | ddumphreys8       | eGek5Q8                      |
|   10 | etookey9          | kXBd88ZX                     |
|   11 | mlindbacka        | H9uTnIvli92                  |
|   12 | awebbeb           | RALeM2IfuwA                  |
|   13 | tswannellc        | oHdZWwO9                     |
|   14 | slydiattd         | r3wRgn                       |
|   15 | cparslowe         | nVdJAHr                      |
|   16 | sheartfieldf      | ofTf0hE7OL                   |
|   17 | aalvesg           | diTzuE                       |
|   18 | eshilstoneh       | NVSRa5L8Lx                   |
|   19 | eludovicoi        | w2uUtLGYkDi                  |
|   20 | rcoppenhallj      | 8T1AO16C4pm                  |
|   21 | rfuxmank          | oOVWyPyo                     |
|   22 | tmoraledal        | CDNj7KH                      |
|   23 | vdurdanm          | KBM4BTldF                    |
|   24 | mlandisn          | oCOZcC                       |
|   25 | gfancutto         | RNHlBaFKLLt                  |
|   26 | dfigliovannip     | Cf7T9osx                     |
|   27 | ngoedeq           | eDfTnH                       |
|   28 | abalhamr          | Qc2Tia0zM                    |
|   29 | tmartys           | VC65xd6o                     |
|   30 | sallewellt        | Y5VSv1rm                     |
|   31 | mjoveyu           | ej3amn                       |
|   32 | mgoodlifev        | lCbzNIw7B90                  |
|   33 | gmargeramw        | hbVF2G                       |
|   34 | leberlex          | Nj6UCAQ                      |
|   35 | mtrimbyy          | jfNkfg5ZW                    |
|   36 | mkimmz            | pZZepTCVlkN                  |
|   37 | mflaunier10       | 9TZ8mfLA                     |
|   38 | vgomes11          | qM6nHjMtD                    |
|   39 | sbrimham12        | FoXudHc4Ocr                  |
|   40 | cbendle13         | zFUIGVBx                     |
|   41 | ralgeo14          | YTB8IXOk                     |
|   42 | rsandyfirth15     | vARbkPRQv                    |
|   43 | bcarlesi16        | m4H6q6pH                     |
|   44 | cfrude17          | Za8UHiSe25N                  |
|   45 | rjullian18        | 6QyxSjg                      |
|   46 | bgissing19        | fjes6w8Ovw0                  |
|   47 | limore1a          | gVzkv8syQ                    |
|   48 | scarlisle1b       | sR9rPBL5                     |
|   49 | hamoss1c          | tbmK9XBhn57j                 |
|   50 | cradmore1d        | TQkfKxEl7                    |
|   51 | apetican1e        | ABibihOvMOu                  |
|   52 | eweber1f          | sEDynNORm7b                  |
|   53 | nbockmaster1g     | M1tVaH                       |
|   54 | cianne1h          | Vc8agpinq                    |
|   55 | khatchette1i      | xXOnQFOsF0I                  |
|   56 | tkroger1j         | uisR7g1eVEU                  |
|   57 | sgladtbach1k      | iIVQ4l                       |
|   58 | bmockford1l       | BBsZPmwk0r                   |
|   59 | balabone1m        | aTUbGm0                      |
|   60 | jmantripp1n       | DTVAdvbadbA2                 |
|   61 | tchown1o          | dCulXiBc                     |
|   62 | vconradsen1p      | v5E0sgqzo                    |
|   63 | hfudge1q          | cSODbEMtCm                   |
|   64 | syaneev1r         | ilXo6tKGHY7                  |
|   65 | btheyer1s         | LxNk1t                       |
|   66 | fcahn1t           | oSBmcLx                      |
|   67 | edurrington1u     | LMomwfQkq3                   |
|   68 | kcounter1v        | 1zUE6RHS                     |
|   69 | bqueripel1w       | 0A2OfeQPnhd                  |
|   70 | mnacci1x          | lNyUiY8U4t                   |
|   71 | dcabell1y         | W6Q7R3zsxB                   |
|   72 | ctaleworth1z      | d3JWwTj                      |
|   73 | mmcgrah20         | yPxlvhS                      |
|   74 | jgannaway21       | oGfIrDxkSIo                  |
|   75 | eiacovone22       | 8jKlhgvC                     |
|   76 | rnaughton23       | Gyf6awYCm4                   |
|   77 | adobbins24        | ashZ0G                       |
|   78 | pwarbeys25        | nSmfKSYW9GL                  |
|   79 | bbrabbins26       | YZWuH6D8Q                    |
|   80 | adandy27          | dF1VPsn                      |
|   81 | mfarrens28        | ucPclA8K9c                   |
|   82 | dhaysar29         | MeGzIGeyKXyw                 |
|   83 | efoot2a           | Q2ks5eg                      |
|   84 | tpelosi2b         | 8yjhdx                       |
|   85 | binman2c          | 3uO3PeL8e                    |
|   86 | krait2d           | EFD5FpEtu2                   |
|   87 | jcrook2e          | VFsdmvhDz4O                  |
|   88 | falonso2f         | 4ifO54                       |
|   89 | jmacak2g          | KUDAxTXU                     |
|   90 | nnorville2h       | WCYa9C1G                     |
|   91 | tlevington2i      | If46bHoGr                    |
|   92 | abartak2j         | erFX4u0e0                    |
|   93 | jgoad2k           | gunnsPy1pMCd                 |
|   94 | dwadham2l         | 89IiRFy0frst                 |
|   95 | hvenditti2m       | NS0U18XON                    |
|   96 | gpitchers2n       | j7RVE2                       |
|   97 | aiskowitz2o       | 8iVpSQUEXn2K                 |
|   98 | gcars2p           | 8i3nsQU9wp                   |
|   99 | bjacke2q          | 2PtrA0C                      |
|  100 | fstorton2r        | XmjbfR1vK1                   |
|  101 | pbrinded2s        | Jf9uWJ                       |
|  102 | penriques2t       | o3kmQ5zHF5Qb                 |
|  103 | awinckworth2u     | LEwOydD3nncQ                 |
|  104 | lkinsell2v        | kvoIZupHNt                   |
|  105 | wdavisson2w       | nk5HVS                       |
|  106 | rrenzini2x        | LiCJccRxumYU                 |
|  107 | kdavys2y          | ZXpRVEn                      |
|  108 | ravann2z          | YLkKN4JzzM                   |
|  109 | hrallings30       | 6wS4x0IeLW                   |
|  110 | sbrackpool31      | lBa8AVaPQg                   |
|  111 | epulham32         | yIV88FM9DM                   |
|  112 | mspeachley33      | JSa9aUv1h                    |
|  113 | vforkan34         | 26Q6gTgsOE8T                 |
|  114 | jprichard35       | sggVPPMfRA3T                 |
|  115 | abisatt36         | GcSlKIuky                    |
|  116 | todocherty37      | BwSfFV3qj                    |
|  117 | njayne38          | D8yr44NNQ                    |
|  118 | gwhyman39         | h0WJ4p2F2x8                  |
|  119 | lkristoffersson3a | mARndSF                      |
|  120 | lmcallan3b        | gmpkAKF                      |
|  121 | kdouble3c         | qYtstjmdR                    |
|  122 | sgooding3d        | venooIUMMHE                  |
|  123 | lgaffney3e        | 1fCwgoaCtz                   |
|  124 | emuriel3f         | Wz582Y22                     |
|  125 | mlamasna3g        | MhqsPNMRYwJE                 |
|  126 | omander3h         | CuB3JbXJ                     |
|  127 | fropkes3i         | jVBeawjIPXS                  |
|  128 | mhawk3j           | g0sPpI8                      |
|  129 | wseres3k          | zgsXeR7blA                   |
|  130 | bflaws3l          | 0dTvgBkaFYqi                 |
|  131 | ccyson3m          | EtCscA                       |
|  132 | afowell3n         | cRG0x5                       |
|  133 | jmolian3o         | fCwa9ry                      |
|  134 | gterzo3p          | Srv77g                       |
|  135 | ravrahamy3q       | dFjfFMEJ                     |
|  136 | amaden3r          | n1WAtKT                      |
|  137 | gdeverall3s       | 1Vj3bbr                      |
|  138 | ejansema3t        | 4MyiArdEVq                   |
|  139 | snormanville3u    | l1s9Ao9omd                   |
|  140 | nfinder3v         | Rd1POwc3                     |
|  141 | lrodway3w         | UNW82GQfd0q                  |
|  142 | lstening3x        | JaSkROwU83UB                 |
|  143 | hemer3y           | GlPpKB                       |
|  144 | eblamphin3z       | 7Zjz7RvcC9x                  |
|  145 | lwederell40       | eyWsJl                       |
|  146 | nverick41         | Mr1r2H                       |
|  147 | mlawlie42         | XrHEZJbuUd                   |
|  148 | swahlberg43       | 46gOiZ                       |
|  149 | crubinivitz44     | FLlYii1mQz84                 |
|  150 | HTB               | cr3n4o7rzse7rzhnckhssncif7ds |
|  151 | wdoswell46        | FYXMuelBVcS                  |
|  152 | ccollingwood47    | LM6SU2N3w7KQ                 |
|  153 | nfoux48           | N40DfFww                     |
|  154 | gboyat49          | W1LDy7                       |
|  155 | csuddick4a        | UIGXl3lL                     |
|  156 | tmatieu4b         | c5PYl7yfJi                   |
|  157 | ielsy4c           | 3hLC705Oj                    |
|  158 | ebotwood4d        | aQmW5c7                      |
|  159 | gcirlos4e         | SPsU9obCa                    |
|  160 | smucklestone4f    | Ho96mUx                      |
|  161 | hdain4g           | BGMRtb                       |
|  162 | dmcquillin4h      | 37kwHEdFhAlL                 |
|  163 | gfolan4i          | 1d9kcofM                     |
|  164 | gtamlett4j        | 4HlL18RM37l3                 |
|  165 | cchapelle4k       | xezsRgOt8OW8                 |
|  166 | channy4l          | 68lHKp                       |
|  167 | ffennick4m        | jNLpCeyoYY                   |
|  168 | mmcgarrell4n      | Ttvat7WvkI                   |
|  169 | mmcdowell4o       | jfOR6B                       |
|  170 | sconquer4p        | ase5Qid5vWD                  |
|  171 | hskune4q          | UUoqC30g5w                   |
|  172 | mblasli4r         | dcjNDHzrA                    |
|  173 | sefford4s         | ui0r4FKwD38                  |
|  174 | gscotter4t        | f2vUKUzHLmEW                 |
|  175 | nmenhenitt4u      | gXHceINuKdF                  |
|  176 | laldridge4v       | 7o4agC3m                     |
|  177 | rlingner4w        | 8mYREIR7                     |
|  178 | mmcfall4x         | sd3N0GDK                     |
|  179 | smoscon4y         | BCPAyKFkKKL                  |
|  180 | ggillespey4z      | LHyQ7f4Br                    |
|  181 | onewberry50       | aKdinUPQ9r                   |
|  182 | dinsley51         | hy8agAF9c4VS                 |
|  183 | mcommon52         | Buh2VR                       |
|  184 | bmosdill53        | IgNAGOBrzlu                  |
|  185 | rrobart54         | SkBqsiQGSK                   |
|  186 | hdurrance55       | 1cljoZoy7Fc                  |
|  187 | hwinterflood56    | F9PH0X0                      |
|  188 | jbier57           | Ug88Nd37N96v                 |
|  189 | hmaccumeskey58    | 3rb3rz2kq2                   |
|  190 | orangell59        | IWz01iHsv                    |
|  191 | velsie5a          | mWcslVm2                     |
|  192 | igeorgelin5b      | 6WHS6OS                      |
|  193 | rrushsorth5c      | hXiQn9bW6W                   |
|  194 | mbrucker5d        | cT5Z6K                       |
|  195 | darnull5e         | EzagIo6Sd                    |
|  196 | jparkhouse5f      | HCEchNzf                     |
|  197 | smcgunley5g       | 9ivT96O                      |
|  198 | ssoal5h           | qi6WX7TGIA                   |
|  199 | npeak5i           | 3gR7Iuc0                     |
|  200 | mleidl5j          | qwfjY9RGk6                   |
+------+-------------------+------------------------------+
200 rows in set (0.00 sec)
```

>|  150 | HTB               | cr3n4o7rzse7rzhnckhssncif7ds |