
```shell
➜  HTB nuclei -u 10.129.232.101

                     __     _
   ____  __  _______/ /__  (_)
  / __ \/ / / / ___/ / _ \/ /
 / / / / /_/ / /__/ /  __/ /
/_/ /_/\__,_/\___/_/\___/_/   v2.9.15

		projectdiscovery.io

[INF] Current nuclei version: v2.9.15 (latest)
[INF] Current nuclei-templates version: v9.6.4 (latest)
[INF] New templates added in latest release: 121
[INF] Templates loaded for current scan: 6892
[INF] Targets loaded for current scan: 1
[INF] Running httpx on input host
[INF] Found 0 URL from httpx
[INF] Templates clustered: 1194 (Reduced 1133 Requests)
[openssh-detect] [tcp] [info] 10.129.232.101:22 [SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.3]
[pop3-detect] [tcp] [info] 10.129.232.101:110
[smtp-service-detect] [tcp] [info] 10.129.232.101:25
[INF] Using Interactsh Server: oast.live
➜  HTB sudo nmap 10.129.232.101 -sV -p110,143,993,995 -sC
[sudo] password for dz: 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-02 10:51 PDT
Nmap scan report for 10.129.232.101
Host is up (0.33s latency).

PORT    STATE SERVICE  VERSION
110/tcp open  pop3     Dovecot pop3d
|_pop3-capabilities: AUTH-RESP-CODE RESP-CODES PIPELINING SASL UIDL TOP STLS CAPA
| ssl-cert: Subject: commonName=dev.inlanefreight.htb/organizationName=InlaneFreight Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-11-08T23:10:05
|_Not valid after:  2295-08-23T23:10:05
|_ssl-date: TLS randomness does not represent time
143/tcp open  imap     Dovecot imapd
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=dev.inlanefreight.htb/organizationName=InlaneFreight Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-11-08T23:10:05
|_Not valid after:  2295-08-23T23:10:05
|_imap-capabilities: ID STARTTLS more LITERAL+ IMAP4rev1 capabilities IDLE listed Pre-login have LOGINDISABLEDA0001 OK post-login ENABLE SASL-IR LOGIN-REFERRALS
993/tcp open  ssl/imap Dovecot imapd
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=dev.inlanefreight.htb/organizationName=InlaneFreight Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-11-08T23:10:05
|_Not valid after:  2295-08-23T23:10:05
|_imap-capabilities: ID more LITERAL+ IMAP4rev1 capabilities IDLE listed Pre-login have post-login OK AUTH=PLAINA0001 ENABLE SASL-IR LOGIN-REFERRALS
995/tcp open  ssl/pop3 Dovecot pop3d
|_ssl-date: TLS randomness does not represent time
|_pop3-capabilities: AUTH-RESP-CODE RESP-CODES PIPELINING SASL(PLAIN) UIDL TOP CAPA USER
| ssl-cert: Subject: commonName=dev.inlanefreight.htb/organizationName=InlaneFreight Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-11-08T23:10:05
|_Not valid after:  2295-08-23T23:10:05

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 26.08 seconds

```




```

➜  HTB curl -k 'imaps://10.129.232.101' -v --user robin:robin
* processing: imaps://10.129.232.101
*   Trying 10.129.232.101:993...
* Connected to 10.129.232.101 (10.129.232.101) port 993
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* Server certificate:
*  subject: C=UK; ST=London; L=London; O=InlaneFreight Ltd; OU=DevOps Dep�artment; CN=dev.inlanefreight.htb; emailAddress=cto.dev@dev.inlanefreight.htb
*  start date: Nov  8 23:10:05 2021 GMT
*  expire date: Aug 23 23:10:05 2295 GMT
*  issuer: C=UK; ST=London; L=London; O=InlaneFreight Ltd; OU=DevOps Dep�artment; CN=dev.inlanefreight.htb; emailAddress=cto.dev@dev.inlanefreight.htb
*  SSL certificate verify result: self-signed certificate (18), continuing anyway.
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* old SSL session ID is stale, removing
< * OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN] HTB{roncfbw7iszerd7shni7jr2343zhrj}
> A001 CAPABILITY
< * CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN
< A001 OK Pre-login capabilities listed, post-login capabilities have more.
> A002 AUTHENTICATE PLAIN AHJvYmluAHJvYmlu
< * CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY PREVIEW=FUZZY LITERAL+ NOTIFY SPECIAL-USE
< A002 OK Logged in
> A003 LIST "" *
< * LIST (\Noselect \HasChildren) "." DEV
* LIST (\Noselect \HasChildren) "." DEV
< * LIST (\Noselect \HasChildren) "." DEV.DEPARTMENT
* LIST (\Noselect \HasChildren) "." DEV.DEPARTMENT
< * LIST (\HasNoChildren) "." DEV.DEPARTMENT.INT
* LIST (\HasNoChildren) "." DEV.DEPARTMENT.INT
< * LIST (\HasNoChildren) "." INBOX
* LIST (\HasNoChildren) "." INBOX
< A003 OK List completed (0.001 + 0.000 secs).
* Connection #0 to host 10.129.232.101 left intact
➜  HTB openssl s_client -connect 10.129.232.101:imaps
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
verify error:num=18:self-signed certificate
verify return:1
depth=0 C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
verify return:1
---
Certificate chain
 0 s:C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
   i:C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Nov  8 23:10:05 2021 GMT; NotAfter: Aug 23 23:10:05 2295 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIEUzCCAzugAwIBAgIUDf35PqFuv6Uv0EECM8dFmNSZoY8wDQYJKoZIhvcNAQEL
BQAwgbcxCzAJBgNVBAYTAlVLMQ8wDQYDVQQIDAZMb25kb24xDzANBgNVBAcMBkxv
bmRvbjEaMBgGA1UECgwRSW5sYW5lRnJlaWdodCBMdGQxHDAaBgNVBAsME0Rldk9w
cyBEZXDDg2FydG1lbnQxHjAcBgNVBAMMFWRldi5pbmxhbmVmcmVpZ2h0Lmh0YjEs
MCoGCSqGSIb3DQEJARYdY3RvLmRldkBkZXYuaW5sYW5lZnJlaWdodC5odGIwIBcN
MjExMTA4MjMxMDA1WhgPMjI5NTA4MjMyMzEwMDVaMIG3MQswCQYDVQQGEwJVSzEP
MA0GA1UECAwGTG9uZG9uMQ8wDQYDVQQHDAZMb25kb24xGjAYBgNVBAoMEUlubGFu
ZUZyZWlnaHQgTHRkMRwwGgYDVQQLDBNEZXZPcHMgRGVww4NhcnRtZW50MR4wHAYD
VQQDDBVkZXYuaW5sYW5lZnJlaWdodC5odGIxLDAqBgkqhkiG9w0BCQEWHWN0by5k
ZXZAZGV2LmlubGFuZWZyZWlnaHQuaHRiMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
MIIBCgKCAQEAxvMwFE6m+iBUSujb5d6DUy1xDYR5awzQRwddyvq6iBrMxbnptSrn
+j0UOKWHCOpD5LREwP26ghUg0lVJzfo+v5pQJGnxEXKg0OFlzWEd8xgx/JWW/z1/
rDsWlNa2yYZkCy68YWJlC7UZxvcDFrI0V0pDJIkrjForw26laoYDkrh1A5F8uUXD
1TwRLLYo+NGmtNHT3BADJpv6aFUZ4CGrqBQNi7XpsTZ948WLhUwQvWmebiK06Dai
TvMNKBctjWAiNI4xvq34W9hIUaPxT1JJzuujRslep6nHGHW00QEWTWgyOMYThc3b
HtKIHMfDLTUMz7s8RhVVwlWE6+ly1DMRgQIDAQABo1MwUTAdBgNVHQ4EFgQUGDTC
9B5KCKPWT7vXbnMunL/mEE4wHwYDVR0jBBgwFoAUGDTC9B5KCKPWT7vXbnMunL/m
EE4wDwYDVR0TAQH/BAUwAwEB/zANBgkqhkiG9w0BAQsFAAOCAQEADh0v5XWCf3KO
atrWcoiIOC67Z0ZIO7yEF+fQo8z+Wx1dWzmCFVu7u4+l7slcdJICCGBbOX8eItWS
chwzgnWJToyX8PWY8lSaB8ifMDQcr457Y7O6NmvgU35sRcLnYYqXzu2oh0lxsFLR
vL1wpyDLPhhoI++j1fELhiJ3GWiUQrb0vfJPcbSkHTgzf0hm7mLJTaqt3WfS/Gr2
8Oh7vSfzvqvHLE7HHAO0G5Q81zo+wWsrQF0s40HEF/raEMfOy2Htm79YjyjAlLWf
ueS+u8rX2smOYdRIpL3UPx7+yZPGu47vYoetde1Z5cfTCgmeS05BQ2qMOp6Tw6+G
xUuqg8nK1Q==
-----END CERTIFICATE-----
subject=C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
issuer=C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1667 bytes and written 373 bytes
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
    Session-ID: 61AAA178A9637B83D5853A836CB8EDE1F452B17380DAC6D41EF83611AE7372FE
    Session-ID-ctx: 
    Resumption PSK: EA7B9F63C2FCA825EA78936BA80FBDE2E4C8117F7739A760346F8BB98CF4BFADEE28532E6463F31735B81DE958942B0C
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - ba c1 c2 17 ac 66 25 81-92 1e a8 fc 10 d8 c0 c8   .....f%.........
    0010 - 0b 4a fe fe b5 ad 88 ba-44 50 0f 8d 87 af 7e a2   .J......DP....~.
    0020 - 01 ae 6e d7 74 f2 f1 21-90 04 ed 93 fb 60 1c 19   ..n.t..!.....`..
    0030 - 13 60 78 5e 77 d1 35 32-08 25 cf 2b 88 3c 64 36   .`x^w.52.%.+.<d6
    0040 - 6e bf 44 fd 0d ac c0 fc-cb 98 39 87 5e d6 d2 be   n.D.......9.^...
    0050 - 0b db 90 8c 64 b3 b5 20-72 bd 7d f7 da 67 e7 52   ....d.. r.}..g.R
    0060 - 21 08 2e 1e 58 39 35 55-02 20 d2 01 f5 7e f2 e8   !...X95U. ...~..
    0070 - 4c 77 36 76 92 ac 95 c3-cc 9c ca a1 ca c9 2b bf   Lw6v..........+.
    0080 - e9 53 b1 d9 58 ba 3c 39-11 d5 65 a4 8b 27 43 23   .S..X.<9..e..'C#
    0090 - 0d 97 d6 70 2f 1c 21 7d-a1 40 ed eb 68 58 32 ca   ...p/.!}.@..hX2.
    00a0 - 6b 19 63 b1 89 88 5f ef-8b b4 80 fb 2d 26 55 74   k.c..._.....-&Ut
    00b0 - f9 ca 7c 9d 2a 4d 74 03-e3 50 e4 cd b4 8a 26 25   ..|.*Mt..P....&%

    Start Time: 1696274618
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
    Session-ID: 8EAAFA3A33D871599BB6EB02C25F2626492145DD4173AE8581C4CDEE465852D3
    Session-ID-ctx: 
    Resumption PSK: 63A2887866EA217ABED912A3EA81BC8590204BEE629F1CBCDAB702036C70221FFCAA8FB9B34163352F6896D764F621F9
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - ba c1 c2 17 ac 66 25 81-92 1e a8 fc 10 d8 c0 c8   .....f%.........
    0010 - cb b1 b4 24 79 a2 be a5-39 19 d6 96 d8 a3 a6 08   ...$y...9.......
    0020 - d3 8e bb f0 cb 30 3a b2-ae fb c3 19 e4 0f f2 f3   .....0:.........
    0030 - 04 73 37 28 4a 70 88 7e-b0 34 b2 56 16 8e 63 88   .s7(Jp.~.4.V..c.
    0040 - 1e c6 5f b8 4a 5e e5 2a-c1 d9 32 6d e1 1b d1 9d   .._.J^.*..2m....
    0050 - 60 71 dd 31 db 82 1c b0-b9 81 ab 85 e5 d0 38 4d   `q.1..........8M
    0060 - b0 12 08 b0 62 83 a9 96-d5 a2 06 56 53 74 ea e5   ....b......VSt..
    0070 - 1b 10 7d e2 83 e5 04 c1-ed 62 5d 2b b3 30 c4 3f   ..}......b]+.0.?
    0080 - 1b 7b b1 6e c4 50 43 66-fe f9 1a ae 84 6e 30 f2   .{.n.PCf.....n0.
    0090 - 09 3d 83 4d a5 c5 e7 2a-e9 0e be ab 91 05 ed a6   .=.M...*........
    00a0 - 2a f7 e4 6c b0 a9 0c 70-b1 3c ae 9e 30 0e bb 5f   *..l...p.<..0.._
    00b0 - d1 bb 7e 02 36 25 5a f4-71 8e 63 c0 6d 06 3b 6a   ..~.6%Z.q.c.m.;j

    Start Time: 1696274618
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
* OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN] HTB{roncfbw7iszerd7shni7jr2343zhrj}
tag login robin robin
tag OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY PREVIEW=FUZZY LITERAL+ NOTIFY SPECIAL-USE] Logged in
tag LIST "" "*"
* LIST (\Noselect \HasChildren) "." DEV
* LIST (\Noselect \HasChildren) "." DEV.DEPARTMENT
* LIST (\HasNoChildren) "." DEV.DEPARTMENT.INT
* LIST (\HasNoChildren) "." INBOX
tag OK List completed (0.001 + 0.000 secs).
tag SELECT INBOX
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 0 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1636414280] UIDs valid
* OK [UIDNEXT 1] Predicted next UID
tag OK [READ-WRITE] Select completed (0.004 + 0.000 + 0.003 secs).
tag STATUS INBOX (MESSAGES)
* STATUS INBOX (MESSAGES 0)
tag OK [CLIENTBUG] Status on selected mailbox completed (0.001 + 0.000 secs).
tag LIST "" "*"
* LIST (\Noselect \HasChildren) "." DEV
* LIST (\Noselect \HasChildren) "." DEV.DEPARTMENT
* LIST (\HasNoChildren) "." DEV.DEPARTMENT.INT
* LIST (\HasNoChildren) "." INBOX
tag OK List completed (0.001 + 0.000 secs).
tag STATUS INBOX (MESSAGES)
* STATUS INBOX (MESSAGES 0)
tag OK [CLIENTBUG] Status on selected mailbox completed (0.001 + 0.000 secs).
tag STATUS DEV.DEPARTMENT.INT (MESSAGES) 
* STATUS DEV.DEPARTMENT.INT (MESSAGES 1)
tag OK Status completed (0.003 + 0.000 + 0.002 secs).
tag FETCH 1:1 (BODY[HEADER])
tag BAD Error in IMAP command FETCH: Invalid messageset (0.001 + 0.000 secs).
tag SELECT DEV.DEPARTMENT.INT
* OK [CLOSED] Previous mailbox closed.
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 1 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1636414279] UIDs valid
* OK [UIDNEXT 2] Predicted next UID
tag OK [READ-WRITE] Select completed (0.001 + 0.000 secs).
tag FETCH 1:1 (BODY[HEADER])
* 1 FETCH (BODY[HEADER] {133}
Subject: Flag
To: Robin <robin@inlanefreight.htb>
From: CTO <devadmin@inlanefreight.htb>
Date: Wed, 03 Nov 2021 16:13:27 +0200

)
tag OK Fetch completed (0.003 + 0.000 + 0.002 secs).
tag FETCH 1:1 (BODY)        
* 1 FETCH (BODY ("text" "plain" ("charset" "us-ascii") NIL NIL "7bit" 34 1))
tag OK Fetch completed (0.001 + 0.000 secs).
tag FETCH 1 (BODY[n])
tag BAD Error in IMAP command FETCH: Invalid BODY[..] section (0.001 + 0.000 secs).
tag FETCH 1 (BODY[0])
* 1 FETCH (BODY[0] {0}
)
tag OK Fetch completed (0.001 + 0.000 secs).
tag FETCH 1 (BODY[1])
* 1 FETCH (BODY[1] {34}
HTB{983uzn8jmfgpd8jmof8c34n7zio}
)
tag OK Fetch completed (0.001 + 0.000 secs).


```





>https://tewarid.github.io/2011/05/10/access-imap-server-from-the-command-line-using-openssl.html



```
➜  HTB openssl s_client -connect 10.129.232.101:pop3s
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
verify error:num=18:self-signed certificate
verify return:1
depth=0 C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
verify return:1
---
Certificate chain
 0 s:C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
   i:C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Nov  8 23:10:05 2021 GMT; NotAfter: Aug 23 23:10:05 2295 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIEUzCCAzugAwIBAgIUDf35PqFuv6Uv0EECM8dFmNSZoY8wDQYJKoZIhvcNAQEL
BQAwgbcxCzAJBgNVBAYTAlVLMQ8wDQYDVQQIDAZMb25kb24xDzANBgNVBAcMBkxv
bmRvbjEaMBgGA1UECgwRSW5sYW5lRnJlaWdodCBMdGQxHDAaBgNVBAsME0Rldk9w
cyBEZXDDg2FydG1lbnQxHjAcBgNVBAMMFWRldi5pbmxhbmVmcmVpZ2h0Lmh0YjEs
MCoGCSqGSIb3DQEJARYdY3RvLmRldkBkZXYuaW5sYW5lZnJlaWdodC5odGIwIBcN
MjExMTA4MjMxMDA1WhgPMjI5NTA4MjMyMzEwMDVaMIG3MQswCQYDVQQGEwJVSzEP
MA0GA1UECAwGTG9uZG9uMQ8wDQYDVQQHDAZMb25kb24xGjAYBgNVBAoMEUlubGFu
ZUZyZWlnaHQgTHRkMRwwGgYDVQQLDBNEZXZPcHMgRGVww4NhcnRtZW50MR4wHAYD
VQQDDBVkZXYuaW5sYW5lZnJlaWdodC5odGIxLDAqBgkqhkiG9w0BCQEWHWN0by5k
ZXZAZGV2LmlubGFuZWZyZWlnaHQuaHRiMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
MIIBCgKCAQEAxvMwFE6m+iBUSujb5d6DUy1xDYR5awzQRwddyvq6iBrMxbnptSrn
+j0UOKWHCOpD5LREwP26ghUg0lVJzfo+v5pQJGnxEXKg0OFlzWEd8xgx/JWW/z1/
rDsWlNa2yYZkCy68YWJlC7UZxvcDFrI0V0pDJIkrjForw26laoYDkrh1A5F8uUXD
1TwRLLYo+NGmtNHT3BADJpv6aFUZ4CGrqBQNi7XpsTZ948WLhUwQvWmebiK06Dai
TvMNKBctjWAiNI4xvq34W9hIUaPxT1JJzuujRslep6nHGHW00QEWTWgyOMYThc3b
HtKIHMfDLTUMz7s8RhVVwlWE6+ly1DMRgQIDAQABo1MwUTAdBgNVHQ4EFgQUGDTC
9B5KCKPWT7vXbnMunL/mEE4wHwYDVR0jBBgwFoAUGDTC9B5KCKPWT7vXbnMunL/m
EE4wDwYDVR0TAQH/BAUwAwEB/zANBgkqhkiG9w0BAQsFAAOCAQEADh0v5XWCf3KO
atrWcoiIOC67Z0ZIO7yEF+fQo8z+Wx1dWzmCFVu7u4+l7slcdJICCGBbOX8eItWS
chwzgnWJToyX8PWY8lSaB8ifMDQcr457Y7O6NmvgU35sRcLnYYqXzu2oh0lxsFLR
vL1wpyDLPhhoI++j1fELhiJ3GWiUQrb0vfJPcbSkHTgzf0hm7mLJTaqt3WfS/Gr2
8Oh7vSfzvqvHLE7HHAO0G5Q81zo+wWsrQF0s40HEF/raEMfOy2Htm79YjyjAlLWf
ueS+u8rX2smOYdRIpL3UPx7+yZPGu47vYoetde1Z5cfTCgmeS05BQ2qMOp6Tw6+G
xUuqg8nK1Q==
-----END CERTIFICATE-----
subject=C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
issuer=C = UK, ST = London, L = London, O = InlaneFreight Ltd, OU = DevOps Dep\C3\83artment, CN = dev.inlanefreight.htb, emailAddress = cto.dev@dev.inlanefreight.htb
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1667 bytes and written 373 bytes
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
    Session-ID: 70915DFFA9DE699EE67593F0B5BFC7E0C04EFC584E56FA90B98035B224D02DE9
    Session-ID-ctx: 
    Resumption PSK: 101E7B892E2B823E517A8D003060B793E63B9C331B130E39A23D7E0D5C96B0B69879A42802AFF0F46E7B3DBCE6BA67FC
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 2f 13 48 c0 72 22 35 81-00 ba 1d 19 d4 08 ed 27   /.H.r"5........'
    0010 - 21 f2 95 08 4b a9 86 ee-81 ed a4 bf 9e a2 f4 8f   !...K...........
    0020 - b3 13 fa 5c b7 1d ab e5-a0 5a 44 4c c8 cd 88 06   ...\.....ZDL....
    0030 - 9d 09 f2 28 d7 3f c6 a4-06 57 0a df d1 ad 28 92   ...(.?...W....(.
    0040 - c2 07 1f 72 99 55 35 d9-f0 80 a9 14 26 ce 9e 4f   ...r.U5.....&..O
    0050 - ef 8f 7c 83 b0 e2 04 12-62 65 49 df ba 94 c5 e2   ..|.....beI.....
    0060 - da 52 3e 95 a7 73 9d e8-05 d8 41 e1 13 64 4c a2   .R>..s....A..dL.
    0070 - 72 b8 25 63 0d 39 c5 a4-6f 6e 35 01 85 d0 5c 3a   r.%c.9..on5...\:
    0080 - 6f 7e 74 e8 4e 36 72 a5-04 d0 b3 42 5b e6 38 92   o~t.N6r....B[.8.
    0090 - 9a d3 24 43 6e 3b 13 e3-6a 6e ed 6a c7 2b 21 7d   ..$Cn;..jn.j.+!}
    00a0 - 22 ab 1c e9 db 1d df d9-cc 00 ce 97 bd 09 63 ee   ".............c.
    00b0 - b6 af e2 7b 42 a6 bf 36-37 dd a9 20 ba 06 94 81   ...{B..67.. ....

    Start Time: 1696275698
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
    Session-ID: 5392CB6A3D074742A3BA00A282BF20DEFFE3908E61726534EE84BF08CFE80A96
    Session-ID-ctx: 
    Resumption PSK: EC2BA1C114708F537CC38C67E86B2586B6FA83F5ACDB9211A2DDFF7FF167D96C342B1394D4A3F16E3E9130D937A1607E
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 2f 13 48 c0 72 22 35 81-00 ba 1d 19 d4 08 ed 27   /.H.r"5........'
    0010 - 45 fc c7 2b 4a bc 64 2b-5d c7 01 4e d5 78 b1 04   E..+J.d+]..N.x..
    0020 - ed 38 56 6a d3 55 a2 4d-33 05 3e 33 c8 de e2 24   .8Vj.U.M3.>3...$
    0030 - 1f 9d 14 3c 22 50 5b 6d-7f d0 f9 a9 b9 91 5c 2f   ...<"P[m......\/
    0040 - 58 1a 6c 79 ac f1 80 9d-07 fe 70 1a c7 25 24 2e   X.ly......p..%$.
    0050 - 96 1c 81 82 ee 8c 0d 63-b3 5b 2c 10 88 3a 55 58   .......c.[,..:UX
    0060 - 1e d2 dc d4 8c 89 ba 14-2b 88 e5 49 f2 69 78 05   ........+..I.ix.
    0070 - 0c 39 17 5c d3 7f 28 96-3f 37 0f 0b f6 f8 f8 6c   .9.\..(.?7.....l
    0080 - 33 58 b6 f6 46 da 16 b7-59 f5 d3 39 c5 8d a8 67   3X..F...Y..9...g
    0090 - b3 22 b5 07 8a 0f df 64-17 a3 04 70 c8 0a 49 ae   .".....d...p..I.
    00a0 - b6 3c 29 ff 83 b3 08 8c-03 d5 d3 5b a3 9b 5e 52   .<)........[..^R
    00b0 - f8 10 bd b6 c8 cc 7b 4c-0b 7b 74 8d 4b 16 2d e7   ......{L.{t.K.-.

    Start Time: 1696275698
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
+OK InFreight POP3 v9.188
tag LOGIN robin:robin
-ERR Unknown command.
USER robin
+OK
PASS robin
+OK Logged in.
LIST
+OK 0 messages:
.
CAPA
+OK
CAPA
TOP
UIDL
RESP-CODES
PIPELINING
AUTH-RESP-CODE
.
STAT
+OK 0 0


```

