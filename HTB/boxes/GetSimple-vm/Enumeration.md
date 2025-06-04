
	- nmap -sV --open -oA unknown_initial_scan \<ip address \>
	-  nmap -p- --open -oA unkown_full_tcp_scan \<ip address\>
	- nc -nv \<ip address\> \<port\>
	- nmap -sV --script=http-enum -oA unkown_nmap_http_enum \<ip address\> 

> all we determine here is that port 80 and port 22 are open
> the banners are ssh and http


