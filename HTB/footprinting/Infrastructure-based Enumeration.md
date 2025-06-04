## Infrastructure-based Enumeration

| **Command** | **Description** |
|-------------|------------------|
| `curl -s "https://crt.sh/?q=<target-domain>&output=json" | jq .` | Certificate transparency enumeration using crt.sh and jq. |
| `for i in $(cat ip-addresses.txt); do shodan host $i; done` | Scan each IP address in a list using Shodan. |

----

## Host-based Enumeration

### FTP

| **Command** | **Description** |
|-------------|------------------|
| `ftp <FQDN/IP>` | Interact with the FTP service on the target. |
| `nc -nv <FQDN/IP> 21` | Interact with the FTP service using netcat. |
| `telnet <FQDN/IP> 21` | Interact with the FTP service using telnet. |
| `openssl s_client -connect <FQDN/IP>:21 -starttls ftp` | Encrypted connection to the FTP service. |
| `wget -m --no-passive ftp://anonymous:anonymous@<target>` | Download all available files on the target FTP server. |

### SMB

| **Command** | **Description** |
|-------------|------------------|
| `smbclient -N -L //<FQDN/IP>` | Null session authentication on SMB. |
| `smbclient //<FQDN/IP>/<share>` | Connect to a specific SMB share. |
| `rpcclient -U "" <FQDN/IP>` | Interact with the target using RPC. |
| `samrdump.py <FQDN/IP>` | Username enumeration using Impacket scripts. |
| `smbmap -H <FQDN/IP>` | Enumerate SMB shares. |
| `crackmapexec smb <FQDN/IP> --shares -u '' -p ''` | Enumerate shares using null session. |
| `enum4linux-ng.py <FQDN/IP> -A` | SMB enumeration using enum4linux. |

### NFS

| **Command** | **Description** |
|-------------|------------------|
| `showmount -e <FQDN/IP>` | Show available NFS shares. |
| `mount -t nfs <FQDN/IP>:/<share> ./target-NFS/ -o nolock` | Mount the specific NFS share. |
| `umount ./target-NFS` | Unmount the specific NFS share. |

### DNS

| **Command** | **Description** |
|-------------|------------------|
| `dig ns <domain.tld> @<nameserver>` | NS request to the specified nameserver. |
| `dig any <domain.tld> @<nameserver>` | ANY request to the specified nameserver. |
| `dig axfr <domain.tld> @<nameserver>` | AXFR (zone transfer) request to the nameserver. |
| `dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o found_subdomains.txt -f ~/subdomains.list <domain.tld>` | Subdomain brute-forcing. |

### SMTP

| **Command** | **Description** |
|-------------|------------------|
| `telnet <FQDN/IP> 25` | Interact with the SMTP service. |

### IMAP/POP3

| **Command** | **Description** |
|-------------|------------------|
| `curl -k 'imaps://<FQDN/IP>' --user <user>:<password>` | Log in to IMAPS using curl. |
| `openssl s_client -connect <FQDN/IP>:imaps` | Connect to the IMAPS service. |
| `openssl s_client -connect <FQDN/IP>:pop3s` | Connect to the POP3s service. |

### SNMP

| **Command** | **Description** |
|-------------|------------------|
| `snmpwalk -v2c -c <community string> <FQDN/IP>` | Query OIDs using snmpwalk. |
| `onesixtyone -c community-strings.list <FQDN/IP>` | Bruteforce SNMP community strings. |
| `braa <community string>@<FQDN/IP>:.1.*` | Bruteforce SNMP OIDs. |

### MySQL

| **Command** | **Description** |
|-------------|------------------|
| `mysql -u <user> -p<password> -h <FQDN/IP>` | Log in to the MySQL server. |

### MSSQL

| **Command** | **Description** |
|-------------|------------------|
| `mssqlclient.py <user>@<FQDN/IP> -windows-auth` | Log in to the MSSQL server using Windows auth. |

### IPMI

| **Command** | **Description** |
|-------------|------------------|
| `msf6 auxiliary(scanner/ipmi/ipmi_version)` | Detect IPMI version. |
| `msf6 auxiliary(scanner/ipmi/ipmi_dumphashes)` | Dump IPMI hashes. |

### Linux Remote Management

| **Command** | **Description** |
|-------------|------------------|
| `ssh-audit.py <FQDN/IP>` | Security audit on SSH. |
| `ssh <user>@<FQDN/IP>` | Log in to SSH. |
| `ssh -i private.key <user>@<FQDN/IP>` | SSH login using a private key. |
| `ssh <user>@<FQDN/IP> -o PreferredAuthentications=password` | Force password authentication. |

### Windows Remote Management

| **Command** | **Description** |
|-------------|------------------|
| `rdp-sec-check.pl <FQDN/IP>` | Check RDP security settings. |
| `xfreerdp /u:<user> /p:"<password>" /v:<FQDN/IP>` | Connect to RDP from Linux. |
| `evil-winrm -i <FQDN/IP> -u <user> -p <password>` | Connect to WinRM. |
| `wmiexec.py <user>:"<password>"@<FQDN/IP> "<system command>"` | Execute WMI command. |

### Oracle TNS

| **Command** | **Description** |
|-------------|------------------|
| `./odat.py all -s <FQDN/IP>` | Run full ODAT scan on Oracle DB. |
| `sqlplus <user>/<pass>@<FQDN/IP>/<db>` | Log in to Oracle DB. |
| `./odat.py utlfile -s <FQDN/IP> -d <db> -U <user> -P <pass> --sysdba --putFile C:\\insert\\path file.txt ./file.txt` | Upload a file to Oracle RDBMS. |
