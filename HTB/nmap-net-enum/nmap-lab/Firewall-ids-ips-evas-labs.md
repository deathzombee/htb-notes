- bypass firewall, ids, and ips
- be quiet otherwise we will be blocked by ips

---
## Lab 1 Easy

> A company hired us to test their IT security defenses, Including their IDS and IPS systems. The client wishes to increase their IT sec, and will make specific Improvements to their IDS/IPS systems based on our tests. We do not know however, what guidlines these changes will be based on.

>Goal: find out specific information from the target in each scenario

- we are only ever provided with machine protected by IDS/IPS
- to understand how these systems behave we have access to a status page at http://target/status.php

>this page shows us the number of alerts , We are given that if a threshold number of alerts are triggered we will be banned. So we need to stay as quiet as possible

## flag condition

>OS of clients system

from the beginning we found ports 22,80,10001 open

10001 is an ftp server
80 has the ids alert page
22 is ssh

- tried
```
nmap -sS -O --osscan-guess --traceroute --source-port 53 -oA easy-target-osscan 10.129.2.80
```

we knew a nix system was running from Syst request to port 10001 via netcat
its worth noting the hostname is also leaked here as nix-nmap-easy for comments to be sent to the host

osscan guessed versions of linux kernel but no deffinite on distro

404 apache error page gave the OS away as Ubuntu

---
## Lab 2 Medium

> After first test conducted and results submitted to client the admins made changes and improvements to the IDS/IPS as well as the firewall

- they did not seem satisfied with their previous configs during the meeting, and want to filter network traffic more strictly

## flag condition

> find the DNS server version of the target

we retrieved the DNS server version through dig

```
dig @10.129.2.48 version.bind chaos txt
```

>version.bind is a reserved query name for version queries, chaos is a special class used for retrieving  server-related information. The txt query type is used to retrieve the response in human readable format

the answer section contained the flag

---
## Lab 3 Hard

> After our help identifying lax security of clients IDS/IPS and firewall when dns gives its version when asked through standard dns query, they sent one of their admins to a training course on IDS/IPS systems.

- its a one week training course
- believe they have taken all precautions now
- client wants another test as specific services must be changed, so the software comms had to be modified. 
- basically a fresh untested system now


## flag condition

> find the version of the running service

- alert cap lowered from 100 to 75 before IPS bans client IP

