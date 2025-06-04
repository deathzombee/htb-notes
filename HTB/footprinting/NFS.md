

# NFS

---

`Network File System` (`NFS`) is a network file system developed by Sun Microsystems and has the same purpose as SMB. Its purpose is to access file systems over a network as if they were local. However, it uses an entirely different protocol. [NFS](https://en.wikipedia.org/wiki/Network_File_System) is used between Linux and Unix systems. This means that NFS clients cannot communicate directly with SMB servers. NFS is an Internet standard that governs the procedures in a distributed file system. While NFS protocol version 3.0 (`NFSv3`), which has been in use for many years, authenticates the client computer, this changes with `NFSv4`. Here, as with the Windows SMB protocol, the user must authenticate.

|**Version**|**Features**|
|---|---|
|`NFSv2`|It is older but is supported by many systems and was initially operated entirely over UDP.|
|`NFSv3`|It has more features, including variable file size and better error reporting, but is not fully compatible with NFSv2 clients.|
|`NFSv4`|It includes Kerberos, works through firewalls and on the Internet, no longer requires portmappers, supports ACLs, applies state-based operations, and provides performance improvements and high security. It is also the first version to have a stateful protocol.|

NFS version 4.1 ([RFC 8881](https://datatracker.ietf.org/doc/html/rfc8881)) aims to provide protocol support to leverage cluster server deployments, including the ability to provide scalable parallel access to files distributed across multiple servers (pNFS extension). In addition, NFSv4.1 includes a session trunking mechanism, also known as NFS multipathing. A significant advantage of NFSv4 over its predecessors is that only one UDP or TCP port `2049` is used to run the service, which simplifies the use of the protocol across firewalls.

NFS is based on the [Open Network Computing Remote Procedure Call](https://en.wikipedia.org/wiki/Sun_RPC) (`ONC-RPC`/`SUN-RPC`) protocol exposed on `TCP` and `UDP` ports `111`, which uses [External Data Representation](https://en.wikipedia.org/wiki/External_Data_Representation) (`XDR`) for the system-independent exchange of data. The NFS protocol has `no` mechanism for `authentication` or `authorization`. Instead, authentication is completely shifted to the RPC protocol's options. The authorization is taken from the available information of the file system where the server is responsible for translating the user information supplied by the client to that of the file system and converting the corresponding authorization information as correctly as possible into the syntax required by UNIX.

The most common authentication is via UNIX `UID`/`GID` and `group memberships`, which is why this syntax is most likely to be applied to the NFS protocol. One problem is that the client and server do not necessarily have to have the same mappings of UID/GID to users and groups, and the server does not need to do anything further. No further checks can be made on the part of the server. This is why NFS should only be used with this authentication method in trusted networks.

---

## Default Configuration

NFS is not difficult to configure because there are not as many options as FTP or SMB have. The `/etc/exports` file contains a table of physical filesystems on an NFS server accessible by the clients. The [NFS Exports Table](http://manpages.ubuntu.com/manpages/trusty/man5/exports.5.html) shows which options it accepts and thus indicates which options are available to us.

#### Exports File

```cat /etc/exports
# /etc/exports - exports(5) - directories exported to NFS clients
#
# Example for NFSv3:
#  /srv/home        hostname1(rw,sync) hostname2(ro,sync)
# Example for NFSv4:
#  /srv/nfs4	    hostname1(rw,sync,fsid=0)
#  /srv/nfs4/home   hostname1(rw,sync,nohide)
# Using Kerberos and integrity checking:
#  /srv/nfs4        *(rw,sync,sec=krb5i,fsid=0)
#  /srv/nfs4/home   *(rw,sync,sec=krb5i,nohide)
#
# Use `exportfs -arv` to reload.
/srv/nfs/fed	192.168.1.0/24

```

```
➜  HTB sudo su
[sudo] password for dz: 
[root@archlinux HTB]#  echo '/mnt/nfs 10.129.98.0/24(sync,no_subtree_check)'>>/etc/exports
[root@archlinux HTB]# su dz

```

```
➜  HTB sudo systemctl start nfs-server
➜  HTB sudo exportfs
/srv/nfs/fed  	192.168.1.0/24
/mnt/nfs      	10.129.98.0/24

```





```sudo nmap 10.129.98.116  -p111,2049 -sV -sC
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-28 17:20 PDT
Nmap scan report for 10.129.98.116
Host is up (0.091s latency).

PORT     STATE SERVICE VERSION
111/tcp  open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100003  3           2049/udp   nfs
|   100003  3,4         2049/tcp   nfs
|   100005  1,2,3      50639/tcp   mountd
|   100005  1,2,3      51047/udp   mountd
|   100021  1,3,4      39501/tcp   nlockmgr
|   100021  1,3,4      53957/udp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|_  100227  3           2049/udp   nfs_acl
2049/tcp open  nfs     3-4 (RPC #100003)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.64 seconds

```


```
➜  HTB sudo nmap --script nfs-ls 10.129.98.116 -sV -p111,2049
[sudo] password for dz: 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-28 17:44 PDT
Nmap scan report for 10.129.98.116
Host is up (0.22s latency).

PORT     STATE SERVICE VERSION
111/tcp  open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100003  3           2049/udp   nfs
|   100003  3,4         2049/tcp   nfs
|   100005  1,2,3      50639/tcp   mountd
|   100005  1,2,3      51047/udp   mountd
|   100021  1,3,4      39501/tcp   nlockmgr
|   100021  1,3,4      53957/udp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|_  100227  3           2049/udp   nfs_acl
| nfs-ls: Volume /var/nfs
|   access: Read Lookup Modify Extend Delete NoExecute
| PERMISSION  UID    GID    SIZE  TIME                 FILENAME
| rwxr-xr-x   65534  65534  4096  2021-11-08T15:08:27  .
| ??????????  ?      ?      ?     ?                    ..
| rw-r--r--   65534  65534  39    2021-11-08T15:08:27  flag.txt
| 
| 
| Volume /mnt/nfsshare
|   access: Read Lookup Modify Extend Delete NoExecute
| PERMISSION  UID    GID    SIZE  TIME                 FILENAME
| rwxr-xr-x   65534  65534  4096  2021-11-08T14:06:40  .
| ??????????  ?      ?      ?     ?                    ..
| rw-r--r--   65534  65534  59    2021-11-08T14:06:40  flag.txt
|_
2049/tcp open  nfs     3-4 (RPC #100003)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.62 seconds

```

> note in zsh you need to quote the replacement for scripts

```
➜  HTB sudo nmap --script "nfs-*" 10.129.98.116 -sV -p111,2049
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-28 17:47 PDT
Nmap scan report for 10.129.98.116
Host is up (0.090s latency).

PORT     STATE SERVICE VERSION
111/tcp  open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100003  3           2049/udp   nfs
|   100003  3,4         2049/tcp   nfs
|   100005  1,2,3      50639/tcp   mountd
|   100005  1,2,3      51047/udp   mountd
|   100021  1,3,4      39501/tcp   nlockmgr
|   100021  1,3,4      53957/udp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|_  100227  3           2049/udp   nfs_acl
| nfs-showmount: 
|   /var/nfs 10.0.0.0/8
|_  /mnt/nfsshare 10.0.0.0/8
2049/tcp open  nfs     3-4 (RPC #100003)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.66 seconds

```

```
➜  HTB showmount -e 10.129.98.116
Export list for 10.129.98.116:
/var/nfs      10.0.0.0/8
/mnt/nfsshare 10.0.0.0/8

```

```
➜  HTB showmount -e 10.129.98.116
Export list for 10.129.98.116:
/var/nfs      10.0.0.0/8
/mnt/nfsshare 10.0.0.0/8
➜  HTB mkdir target-NFS
➜  HTB sudo mount -t nfs 10.129.98.116:/ ./target-NFS/ -o nolock
➜  HTB cd target-NFS
➜  target-NFS ls -R
.:
mnt  var

./mnt:
nfsshare

./mnt/nfsshare:
flag.txt

./var:
nfs

./var/nfs:
flag.txt

```


```
➜  target-NFS ls -l mnt/nfsshare/             
total 4
-rw-r--r-- 1 nobody nobody 59 Nov  8  2021 flag.txt
➜  target-NFS ls -n  mnt/nfsshare/
total 4
-rw-r--r-- 1 65534 65534 59 Nov  8  2021 flag.txt

```


