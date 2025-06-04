
```
~ dig @10.129.124.225 inlanefreight.htb NS   


; <<>> DiG 9.18.27 <<>> @10.129.124.225 inlanefreight.htb NS
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16220
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: 59e87d502a29a3c001000000665e1dd875f032c9034baef1 (good)
;; QUESTION SECTION:
;inlanefreight.htb.		IN	NS

;; ANSWER SECTION:
inlanefreight.htb.	604800	IN	NS	ns.inlanefreight.htb.

;; ADDITIONAL SECTION:
ns.inlanefreight.htb.	604800	IN	A	127.0.0.1

;; Query time: 343 msec
;; SERVER: 10.129.124.225#53(10.129.124.225) (UDP)
;; WHEN: Mon Jun 03 12:47:36 PDT 2024
;; MSG SIZE  rcvd: 107

➜  ~ dig @10.129.124.225 inlanefreight.htb axfr


; <<>> DiG 9.18.27 <<>> @10.129.124.225 inlanefreight.htb axfr
; (1 server found)
;; global options: +cmd
inlanefreight.htb.	604800	IN	SOA	inlanefreight.htb. root.inlanefreight.htb. 2 604800 86400 2419200 604800
inlanefreight.htb.	604800	IN	NS	ns.inlanefreight.htb.
admin.inlanefreight.htb. 604800	IN	A	10.10.34.2
ftp.admin.inlanefreight.htb. 604800 IN	A	10.10.34.2
careers.inlanefreight.htb. 604800 IN	A	10.10.34.50
dc1.inlanefreight.htb.	604800	IN	A	10.10.34.16
dc2.inlanefreight.htb.	604800	IN	A	10.10.34.11
internal.inlanefreight.htb. 604800 IN	A	127.0.0.1
admin.internal.inlanefreight.htb. 604800 IN A	10.10.1.11
wsus.internal.inlanefreight.htb. 604800	IN A	10.10.1.240
ir.inlanefreight.htb.	604800	IN	A	10.10.45.5
dev.ir.inlanefreight.htb. 604800 IN	A	10.10.45.6
ns.inlanefreight.htb.	604800	IN	A	127.0.0.1
resources.inlanefreight.htb. 604800 IN	A	10.10.34.100
securemessaging.inlanefreight.htb. 604800 IN A	10.10.34.52
test1.inlanefreight.htb. 604800	IN	A	10.10.34.101
us.inlanefreight.htb.	604800	IN	A	10.10.200.5
cluster14.us.inlanefreight.htb.	604800 IN A	10.10.200.14
messagecenter.us.inlanefreight.htb. 604800 IN A	10.10.200.10
ww02.inlanefreight.htb.	604800	IN	A	10.10.34.112
www1.inlanefreight.htb.	604800	IN	A	10.10.34.111
inlanefreight.htb.	604800	IN	SOA	inlanefreight.htb. root.inlanefreight.htb. 2 604800 86400 2419200 604800
;; Query time: 306 msec
;; SERVER: 10.129.124.225#53(10.129.124.225) (TCP)
;; WHEN: Mon Jun 03 12:47:42 PDT 2024
;; XFR size: 22 records (messages 1, bytes 594)
```