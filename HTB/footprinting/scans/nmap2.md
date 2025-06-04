tarting Nmap 7.93 ( https://nmap.org ) at 2023-05-01 03:34 BST
Stats: 0:00:30 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 33.33% done; ETC: 03:35 (0:00:22 remaining)
Nmap scan report for 161.35.40.57
Host is up (0.082s latency).
Not shown: 12281 closed tcp ports (conn-refused), 79 filtered tcp ports (no-response)
PORT      STATE SERVICE    VERSION
30086/tcp open  http       nginx 1.19.2
|_http-server-header: nginx/1.19.2
|_http-title: Site doesn't have a title (text/html).
30119/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Blank Page
30155/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Tiny File Manager
30158/tcp open  http       Werkzeug httpd 1.0.1 (Python 3.9.0)
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
30276/tcp open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 f406256677eb7bb858f3ec2eef711ceb (ECDSA)
|_  256 98aff5e46a147e2d5c3d71be811c7497 (ED25519)
30308/tcp open  http       Node.js Express framework
|_http-title: inside starship enterprise
30408/tcp open  http       nginx 1.19.2
|_http-server-header: nginx/1.19.2
|_http-title: Site doesn't have a title (text/html).
30431/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
30501/tcp open  http       nginx 1.19.2
|_http-server-header: nginx/1.19.2
|_http-title: Site doesn't have a title (text/html).
30521/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Blank Page
30581/tcp open  http       Node.js Express framework
|_http-title: AbuseHumanDB
30701/tcp open  unknown
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, GetRequest, HTTPOptions, RTSPRequest: 
|     Welcome to Qubit Enterprises. Would you like your own time capsule? (Y/n) I'm sorry I don't understand
|     Welcome to Qubit Enterprises. Would you like your own time capsule? (Y/n)
|   NULL, RPCCheck: 
|_    Welcome to Qubit Enterprises. Would you like your own time capsule? (Y/n)
31014/tcp open  http       Werkzeug httpd 2.0.1 (Python 3.9.5)
|_http-title: petpet brcee
31073/tcp open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
31077/tcp open  unknown
| fingerprint-strings: 
|   DNSStatusRequestTCP, GenericLines: 
|     Inside the dark cave. 
|     Scream.
|     outside.
|     Scream.
|     outside.
|   DNSVersionBindReqTCP: 
|     Inside the dark cave. 
|     Scream.
|     outside.
|     Scream.
|     outside.
|     have enough energy for that, you fainted!
|   GetRequest: 
|     Inside the dark cave. 
|     Scream.
|     outside.
|     HTTP/1.0
|     Scream.
|     outside.
|   HTTPOptions: 
|     Inside the dark cave. 
|     Scream.
|     outside.
|     OPTIONS / HTTP/1.0
|     Scream.
|     outside.
|     Scream.
|     outside.
|   Help: 
|     Inside the dark cave. 
|     Scream.
|     outside.
|     HELP
|     Scream.
|     outside.
|   NULL: 
|     Inside the dark cave. 
|     Scream.
|     outside.
|   RPCCheck: 
|     Inside the dark cave. 
|     Scream.
|     outside.
|     Scream.
|     outside.
|     Scream.
|     outside.
|     Scream.
|     outside.
|   RTSPRequest: 
|     Inside the dark cave. 
|     Scream.
|     outside.
|     OPTIONS / RTSP/1.0
|     Scream.
|     outside.
|     Scream.
|_    outside.
31214/tcp open  http       nginx 1.19.2
|_http-server-header: nginx/1.19.2
|_http-title: Site doesn't have a title (text/html).
31495/tcp open  http       Node.js Express framework
|_http-title: Weather App
31868/tcp open  http       Werkzeug httpd 1.0.1 (Python 3.9.0)
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
32215/tcp open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 ea54a54616cf30f2670bc802f3eab905 (RSA)
|   256 f406256677eb7bb858f3ec2eef711ceb (ECDSA)
|_  256 98aff5e46a147e2d5c3d71be811c7497 (ED25519)
32363/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Employee Login
32706/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Blank Page
32738/tcp open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 ea54a54616cf30f2670bc802f3eab905 (RSA)
|   256 f406256677eb7bb858f3ec2eef711ceb (ECDSA)
|_  256 98aff5e46a147e2d5c3d71be811c7497 (ED25519)
32759/tcp open  http       nginx 1.18.0
|_http-title: InlaneFreight
|_http-server-header: nginx/1.18.0
|_http-trane-info: Problem with XML parsing of /evox/about
42383/tcp open  tcpwrapped
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port30701-TCP:V=7.93%I=7%D=5/1%Time=644F2563%P=x86_64-pc-linux-gnu%r(NU
SF:LL,4A,"Welcome\x20to\x20Qubit\x20Enterprises\.\x20Would\x20you\x20like\
SF:x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20")%r(GenericLines,B1,
SF:"Welcome\x20to\x20Qubit\x20Enterprises\.\x20Would\x20you\x20like\x20you
SF:r\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20I'm\x20sorry\x20I\x20don't\
SF:x20understand\nWelcome\x20to\x20Qubit\x20Enterprises\.\x20Would\x20you\
SF:x20like\x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20")%r(GetReque
SF:st,B1,"Welcome\x20to\x20Qubit\x20Enterprises\.\x20Would\x20you\x20like\
SF:x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20I'm\x20sorry\x20I\x20
SF:don't\x20understand\nWelcome\x20to\x20Qubit\x20Enterprises\.\x20Would\x
SF:20you\x20like\x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20")%r(HT
SF:TPOptions,B1,"Welcome\x20to\x20Qubit\x20Enterprises\.\x20Would\x20you\x
SF:20like\x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20I'm\x20sorry\x
SF:20I\x20don't\x20understand\nWelcome\x20to\x20Qubit\x20Enterprises\.\x20
SF:Would\x20you\x20like\x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20
SF:")%r(RTSPRequest,B1,"Welcome\x20to\x20Qubit\x20Enterprises\.\x20Would\x
SF:20you\x20like\x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20I'm\x20
SF:sorry\x20I\x20don't\x20understand\nWelcome\x20to\x20Qubit\x20Enterprise
SF:s\.\x20Would\x20you\x20like\x20your\x20own\x20time\x20capsule\?\x20\(Y/
SF:n\)\x20")%r(RPCCheck,4A,"Welcome\x20to\x20Qubit\x20Enterprises\.\x20Wou
SF:ld\x20you\x20like\x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20")%
SF:r(DNSVersionBindReqTCP,B1,"Welcome\x20to\x20Qubit\x20Enterprises\.\x20W
SF:ould\x20you\x20like\x20your\x20own\x20time\x20capsule\?\x20\(Y/n\)\x20I
SF:'m\x20sorry\x20I\x20don't\x20understand\nWelcome\x20to\x20Qubit\x20Ente
SF:rprises\.\x20Would\x20you\x20like\x20your\x20own\x20time\x20capsule\?\x
SF:20\(Y/n\)\x20")%r(DNSStatusRequestTCP,B1,"Welcome\x20to\x20Qubit\x20Ent
SF:erprises\.\x20Would\x20you\x20like\x20your\x20own\x20time\x20capsule\?\
SF:x20\(Y/n\)\x20I'm\x20sorry\x20I\x20don't\x20understand\nWelcome\x20to\x
SF:20Qubit\x20Enterprises\.\x20Would\x20you\x20like\x20your\x20own\x20time
SF:\x20capsule\?\x20\(Y/n\)\x20");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port31077-TCP:V=7.93%I=7%D=5/1%Time=644F2563%P=x86_64-pc-linux-gnu%r(NU
SF:LL,3E,"\n\xf0\x9f\xa6\x87\x20Inside\x20the\x20dark\x20cave\.\x20\xf0\x9
SF:f\xa6\x87\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20")%r(GenericL
SF:ines,60,"\n\xf0\x9f\xa6\x87\x20Inside\x20the\x20dark\x20cave\.\x20\xf0\
SF:x9f\xa6\x87\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20\r\n\r\n\n1
SF:\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20")%r(GetRequest,6E,"\n\xf
SF:0\x9f\xa6\x87\x20Inside\x20the\x20dark\x20cave\.\x20\xf0\x9f\xa6\x87\n1
SF:\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20GET\x20/\x20HTTP/1\.0\r\n
SF:\r\n\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20")%r(HTTPOptions,9
SF:0,"\n\xf0\x9f\xa6\x87\x20Inside\x20the\x20dark\x20cave\.\x20\xf0\x9f\xa
SF:6\x87\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20OPTIONS\x20/\x20H
SF:TTP/1\.0\r\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20\n\r\n\n1\.\
SF:x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20")%r(RTSPRequest,90,"\n\xf0\
SF:x9f\xa6\x87\x20Inside\x20the\x20dark\x20cave\.\x20\xf0\x9f\xa6\x87\n1\.
SF:\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20OPTIONS\x20/\x20RTSP/1\.0\r
SF:\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20\n\r\n\n1\.\x20Scream\
SF:.\n2\.\x20Run\x20outside\.\n>\x20")%r(RPCCheck,9A,"\n\xf0\x9f\xa6\x87\x
SF:20Inside\x20the\x20dark\x20cave\.\x20\xf0\x9f\xa6\x87\n1\.\x20Scream\.\
SF:n2\.\x20Run\x20outside\.\n>\x20\x80\n1\.\x20Scream\.\n2\.\x20Run\x20out
SF:side\.\n>\x20\xa0\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20\n1\.
SF:\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20")%r(DNSVersionBindReqTCP,9
SF:2,"\n\xf0\x9f\xa6\x87\x20Inside\x20the\x20dark\x20cave\.\x20\xf0\x9f\xa
SF:6\x87\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20\n1\.\x20Scream\.
SF:\n2\.\x20Run\x20outside\.\n>\x20\nYou\x20do\x20not\x20have\x20enough\x2
SF:0energy\x20for\x20that,\x20you\x20fainted!\n")%r(DNSStatusRequestTCP,5C
SF:,"\n\xf0\x9f\xa6\x87\x20Inside\x20the\x20dark\x20cave\.\x20\xf0\x9f\xa6
SF:\x87\n1\.\x20Scream\.\n2\.\x20Run\x20outside\.\n>\x20\n1\.\x20Scream\.\
SF:n2\.\x20Run\x20outside\.\n>\x20")%r(Help,62,"\n\xf0\x9f\xa6\x87\x20Insi
SF:de\x20the\x20dark\x20cave\.\x20\xf0\x9f\xa6\x87\n1\.\x20Scream\.\n2\.\x
SF:20Run\x20outside\.\n>\x20HELP\r\n\n1\.\x20Scream\.\n2\.\x20Run\x20outsi
SF:de\.\n>\x20");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 190.95 seconds