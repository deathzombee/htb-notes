Nmap scan report for 139.59.191.22
Host is up (0.077s latency).
Not shown: 35413 closed tcp ports (conn-refused), 30098 filtered tcp ports (no-response)
PORT      STATE SERVICE    VERSION
30092/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-robots.txt: 1 disallowed entry 
|_/admin-login-page.php
|_http-title: HTB Academy
30134/tcp open  http       Node.js (Express middleware)
|_http-title: Diogenes' Rage
30174/tcp open  http       Node.js Express framework
|_http-title: Weather App
30233/tcp open  http       nginx
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
30308/tcp open  http       Node.js Express framework
|_http-title: inside starship enterprise
30413/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
| http-auth: 
| HTTP/1.1 401 Authorization Required\x0D
|_  Basic realm=Access denied
30569/tcp open  http       nginx 1.19.2
|_http-server-header: nginx/1.19.2
|_http-title: Site doesn't have a title (text/html).
30579/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-title: Search Ports
|_Requested resource was search.php
30701/tcp open  unknown
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, GetRequest, HTTPOptions, RTSPRequest: 
|     Welcome to Qubit Enterprises. Would you like your own time capsule? (Y/n) I'm sorry I don't understand
|     Welcome to Qubit Enterprises. Would you like your own time capsule? (Y/n)
|   NULL, RPCCheck: 
|_    Welcome to Qubit Enterprises. Would you like your own time capsule? (Y/n)
31064/tcp open  unknown
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, JavaRMI, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, NCP, NULL, NotesRPC, RPCCheck, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, TerminalServerCookie, WMSRequest, X11Probe, ms-sql-s, oracle-tns: 
|     You know who are 0xDiablos:
|   FourOhFourRequest: 
|     You know who are 0xDiablos: 
|     /nice%20ports%2C/Tri%6Eity.txt%2ebak HTTP/1.0
|   GetRequest: 
|     You know who are 0xDiablos: 
|     HTTP/1.0
|   HTTPOptions: 
|     You know who are 0xDiablos: 
|     OPTIONS / HTTP/1.0
|   Help: 
|     You know who are 0xDiablos: 
|     HELP
|   LPDString: 
|     You know who are 0xDiablos: 
|     default
|   RTSPRequest: 
|     You know who are 0xDiablos: 
|     OPTIONS / RTSP/1.0
|   SIPOptions: 
|     You know who are 0xDiablos: 
|_    OPTIONS sip:nm SIP/2.0
31190/tcp open  http       Apache httpd 2.4.38 ((Debian))
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
|_http-server-header: Apache/2.4.38 (Debian)
31322/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Blank Page
|_http-server-header: Apache/2.4.41 (Ubuntu)
31362/tcp open  http       Apache httpd 2.4.46 ((Unix))
|_http-title: Broken Authentication Login - Final question
|_http-server-header: Apache/2.4.46 (Unix)
31471/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Inlanefreight
31714/tcp open  http       nginx
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: ImageTok
31764/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-generator: WordPress 5.6.1
|_http-title: Getting Started &#8211; Just another WordPress site
|_http-server-header: Apache/2.4.41 (Ubuntu)
32154/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Recommended Modules
32167/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Blank Page
|_http-server-header: Apache/2.4.41 (Ubuntu)
32177/tcp open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Getting Started &#8211; Just another WordPress site
|_http-generator: WordPress 5.6.1
32342/tcp open  http       nginx 1.19.2
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: nginx/1.19.2
32477/tcp open  http       Apache httpd 2.4.46 ((Unix))
|_http-title: Broken Authentication Login - Reset token questions
|_http-server-header: Apache/2.4.46 (Unix)
32571/tcp open  http       Apache httpd 2.4.46 ((Unix))
|_http-server-header: Apache/2.4.46 (Unix)
|_http-title: Broken Authentication Login - Bruteforce cookies questions
32650/tcp open  http       Node.js Express framework
|_http-title: Weather App
43897/tcp open  tcpwrapped
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port30701-TCP:V=7.93%I=7%D=5/1%Time=644F0A33%P=x86_64-pc-linux-gnu%r(NU
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
SF-Port31064-TCP:V=7.93%I=7%D=5/1%Time=644F0A34%P=x86_64-pc-linux-gnu%r(NU
SF:LL,1D,"You\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(GenericLines,1
SF:F,"You\x20know\x20who\x20are\x200xDiablos:\x20\n\r\n")%r(GetRequest,2D,
SF:"You\x20know\x20who\x20are\x200xDiablos:\x20\nGET\x20/\x20HTTP/1\.0\r\n
SF:")%r(HTTPOptions,31,"You\x20know\x20who\x20are\x200xDiablos:\x20\nOPTIO
SF:NS\x20/\x20HTTP/1\.0\r\n")%r(RTSPRequest,31,"You\x20know\x20who\x20are\
SF:x200xDiablos:\x20\nOPTIONS\x20/\x20RTSP/1\.0\r\n")%r(RPCCheck,1D,"You\x
SF:20know\x20who\x20are\x200xDiablos:\x20\n")%r(DNSVersionBindReqTCP,1D,"Y
SF:ou\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(DNSStatusRequestTCP,1D
SF:,"You\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(Help,23,"You\x20kno
SF:w\x20who\x20are\x200xDiablos:\x20\nHELP\r\n")%r(SSLSessionReq,20,"You\x
SF:20know\x20who\x20are\x200xDiablos:\x20\n\x16\x03\n")%r(TerminalServerCo
SF:okie,1F,"You\x20know\x20who\x20are\x200xDiablos:\x20\n\x03\n")%r(TLSSes
SF:sionReq,20,"You\x20know\x20who\x20are\x200xDiablos:\x20\n\x16\x03\n")%r
SF:(Kerberos,1E,"You\x20know\x20who\x20are\x200xDiablos:\x20\n\n")%r(SMBPr
SF:ogNeg,1D,"You\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(X11Probe,1D
SF:,"You\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(FourOhFourRequest,5
SF:0,"You\x20know\x20who\x20are\x200xDiablos:\x20\nGET\x20/nice%20ports%2C
SF:/Tri%6Eity\.txt%2ebak\x20HTTP/1\.0\r\n")%r(LPDString,26,"You\x20know\x2
SF:0who\x20are\x200xDiablos:\x20\n\x01default\n")%r(LDAPSearchReq,20,"You\
SF:x20know\x20who\x20are\x200xDiablos:\x20\n0\x84\n")%r(LDAPBindReq,1D,"Yo
SF:u\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(SIPOptions,35,"You\x20k
SF:now\x20who\x20are\x200xDiablos:\x20\nOPTIONS\x20sip:nm\x20SIP/2\.0\r\n"
SF:)%r(LANDesk-RC,1D,"You\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(Te
SF:rminalServer,1D,"You\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(NCP,
SF:1D,"You\x20know\x20who\x20are\x200xDiablos:\x20\n")%r(NotesRPC,1D,"You\
SF:x20know\x20who\x20are\x200xDiablos:\x20\n")%r(JavaRMI,1D,"You\x20know\x
SF:20who\x20are\x200xDiablos:\x20\n")%r(WMSRequest,1D,"You\x20know\x20who\
SF:x20are\x200xDiablos:\x20\n")%r(oracle-tns,1D,"You\x20know\x20who\x20are
SF:\x200xDiablos:\x20\n")%r(ms-sql-s,1D,"You\x20know\x20who\x20are\x200xDi
SF:ablos:\x20\n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 252.14 seconds
