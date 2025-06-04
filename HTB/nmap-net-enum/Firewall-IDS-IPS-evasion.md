## nmap evasion options
1. Fragmentation of packets
2. use of decoys 
3. dns proxy
---
> fragmentation of packets

instead of using the default tcp connect scan with nmap or SYN scan, one method of bypassing firewall restrictions is to use a TCP ACK scan -sA

the ACK flag (being the flag in the middle of a connection) are often passed by firewalls beause it cant determine if the beginning of the connection originated from external network or internally. 

---
> Decoys

sometimes specific subnets from certain regins are blocked across the board by sysmins like china lol. Also another reason to use a decoy, is preemptively avoiding IPS blocks, -D , nmap will generate RND: num of ips (rnd means the ips are random), they are seperated by colons and our real ip is randomly placed between them. 

these decoys must be alive or the service we are trying to scan might be unreachable due to SYN-flooding security mechanisms

these spoofed packets are often also filtered out by ISPs and routers, even when they come from the same network range, so we can also specify the source ip of a vps we control to scan the target. 

one way of testing if certain services are blocked to certain subnets is using the source ip option -S to test if we have better results.

- Decoys can be used for SYN, ACK, ICMP, and OS detect scans.
- -e specifies the interface to use
- -Pn disables ICMP echo requests
- -n disables DNS resolution
- -O performs os detect scan
---
> DNS Proxying

By default Nmap performs reverse DNS resolution unless told not to

previously they occured over UDP port 53, but due to new ipv6 and DNSSEC expansions many DNS requests get sent to TCP 53, where it used to only be used for so-called "Zone Transfers" between DNS servers or data transfers larger than 512 bytes. 

Nmap still lets us specify DNS servers ourselves 
--dns-server \<ns\>, \<ns\> 
- this can be fundemental if we are in the DMZ, the companies DNS servers are usually more trusted than those from the internet.

For example we can use them to resolve hosts on an internal network, and we can use tcp 53 as the source port. 
- if this is only managed by the firewall, and IDS/IPS are not set to filter properly our TCP packets will be trusted and passed through

- -sS performs SYN scan
- -sA performs ACK scan
- --packet-trace shows all packets sent and recv
- --source-port performs scans from the specified port

> if we find the firewall accepts port 53 TCP we can try to netcat to the port we are scanning that showed as filtered before as its very likely that IDS/IPS filters are weaker than others by a big factor


---
