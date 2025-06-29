# MSSQL

---

[Microsoft SQL](https://www.microsoft.com/en-us/sql-server/sql-server-2019) (`MSSQL`) is Microsoft's SQL-based relational database management system. Unlike MySQL, which we discussed in the last section, MSSQL is closed source and was initially written to run on Windows operating systems. It is popular among database administrators and developers when building applications that run on Microsoft's .NET framework due to its strong native support for .NET. There are versions of MSSQL that will run on Linux and MacOS, but we will more likely come across MSSQL instances on targets running Windows.

#### MSSQL Clients

[SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15) (`SSMS`) comes as a feature that can be installed with the MSSQL install package or can be downloaded & installed separately. It is commonly installed on the server for initial configuration and long-term management of databases by admins. Keep in mind that since SSMS is a client-side application, it can be installed and used on any system an admin or developer is planning to manage the database from. It doesn't only exist on the server hosting the database. This means we could come across a vulnerable system with SSMS with saved credentials that allow us to connect to the database. The image below shows SSMS in action.

![SSMS](https://academy.hackthebox.com/storage/modules/112/ssms.png)

Many other clients can be used to access a database running on MSSQL. Including but not limited to:

| **mssql-cli** | **SQL Server PowerShell** | **HeidiSQL** | **SQLPro** | **Impacket's mssqlclient.py** |
|---------------|---------------------------|--------------|------------|-------------------------------|
| [mssql-cli](https://docs.microsoft.com/en-us/sql/tools/mssql-cli?view=sql-server-ver15) | [SQL Server PowerShell](https://docs.microsoft.com/en-us/sql/powershell/sql-server-powershell?view=sql-server-ver15) | [HeidiSQL](https://www.heidisql.com) | [SQLPro](https://www.macsqlclient.com) | [mssqlclient.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/mssqlclient.py) |



Of the MSSQL clients listed above, pentesters may find Impacket's mssqlclient.py to be the most useful due to SecureAuthCorp's Impacket project being present on many pentesting distributions at install. To find if and where the client is located on our host, we can use the following command:

MSSQL Clients

```shell-session
cdeez@htb[/htb]$ locate mssqlclient

/usr/bin/impacket-mssqlclient
/usr/share/doc/python3-impacket/examples/mssqlclient.py
```

#### MSSQL Databases

MSSQL has default system databases that can help us understand the structure of all the databases that may be hosted on a target server. Here are the default databases and a brief description of each:

|Default System Database|Description|
|---|---|
|`master`|Tracks all system information for an SQL server instance|
|`model`|Template database that acts as a structure for every new database created. Any setting changed in the model database will be reflected in any new database created after changes to the model database|
|`msdb`|The SQL Server Agent uses this database to schedule jobs & alerts|
|`tempdb`|Stores temporary objects|
|`resource`|Read-only database containing system objects included with SQL server|

Table source: [System Databases Microsoft Doc](https://docs.microsoft.com/en-us/sql/relational-databases/databases/system-databases?view=sql-server-ver15)

---

## Default Configuration

When an admin initially installs and configures MSSQL to be network accessible, the SQL service will likely run as `NT SERVICE\MSSQLSERVER`. Connecting from the client-side is possible through Windows Authentication, and by default, encryption is not enforced when attempting to connect.

![SSMS](https://academy.hackthebox.com/storage/modules/112/auth.png)

Authentication being set to `Windows Authentication` means that the underlying Windows OS will process the login request and use either the local SAM database or the domain controller (hosting Active Directory) before allowing connectivity to the database management system. Using Active Directory can be ideal for auditing activity and controlling access in a Windows environment, but if an account is compromised, it could lead to privilege escalation and lateral movement across a Windows domain environment. Like with any OS, service, server role, or application, it can be beneficial to set it up in a VM from installation to configuration to understand all the default configurations and potential mistakes that the administrator could make.

---

## Dangerous Settings

It can be beneficial to place ourselves in the perspective of an IT administrator when we are on an engagement. This mindset can help us remember to look for various settings that may have been misconfigured or configured in a dangerous manner by an admin. A workday in IT can be rather busy, with lots of different projects happening simultaneously and the pressure to perform with speed & accuracy being a reality in many organizations, mistakes can be easily made. It only takes one tiny misconfiguration that could compromise a critical server or service on the network. This applies to just about every network service and server role that can be configured, including MSSQL.

This is not an extensive list because there are countless ways MSSQL databases can be configured by admins based on the needs of their respective organizations. We may benefit from looking into the following:

- MSSQL clients not using encryption to connect to the MSSQL server
    
- The use of self-signed certificates when encryption is being used. It is possible to spoof self-signed certificates
    
- The use of [named pipes](https://docs.microsoft.com/en-us/sql/tools/configuration-manager/named-pipes-properties?view=sql-server-ver15)
    
- Weak & default `sa` credentials. Admins may forget to disable this account
    

---

## Footprinting the Service

There are many ways we can approach footprinting the MSSQL service, the more specific we can get with our scans, the more useful information we will be able to gather. NMAP has default mssql scripts that can be used to target the default tcp port `1433` that MSSQL listens on.

The scripted NMAP scan below provides us with helpful information. We can see the `hostname`, `database instance name`, `software version of MSSQL` and `named pipes are enabled`. We will benefit from adding these discoveries to our notes.

```
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248
[sudo] password for dz: 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-02 17:37 PDT
Nmap scan report for 10.129.201.248
Host is up (0.12s latency).

PORT     STATE SERVICE  VERSION
1433/tcp open  ms-sql-s Microsoft SQL Server 2019
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
|_ms-sql-hasdbaccess: ERROR: Script execution failed (use -d to debug)
|_ms-sql-config: ERROR: Script execution failed (use -d to debug)
|_ms-sql-xp-cmdshell: ERROR: Script execution failed (use -d to debug)
|_ms-sql-dac: ERROR: Script execution failed (use -d to debug)
|_ms-sql-tables: ERROR: Script execution failed (use -d to debug)
|_ms-sql-empty-password: ERROR: Script execution failed (use -d to debug)
|_ms-sql-dump-hashes: ERROR: Script execution failed (use -d to debug)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.24 seconds

```

```
msf6 > use auxiliary/scanner/mssql/mssql_ping
msf6 auxiliary(scanner/mssql/mssql_ping) > set rhosts 10.129.201.248
rhosts => 10.129.201.248
msf6 auxiliary(scanner/mssql/mssql_ping) > run

[*] 10.129.201.248:       - SQL Server information for 10.129.201.248:
[+] 10.129.201.248:       -    ServerName      = ILF-SQL-01
[+] 10.129.201.248:       -    InstanceName    = MSSQLSERVER
[+] 10.129.201.248:       -    IsClustered     = No
[+] 10.129.201.248:       -    Version         = 15.0.2000.5
[+] 10.129.201.248:       -    tcp             = 1433
[+] 10.129.201.248:       -    np              = \\ILF-SQL-01\pipe\sql\query
[*] 10.129.201.248:       - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

```


```
~  pipx install impacket --force
Installing to existing venv 'impacket'
  installed package impacket 0.11.0, installed using Python 3.11.5
  These apps are now globally available
    - DumpNTLMInfo.py
    - Get-GPPPassword.py
    - GetADUsers.py
    - GetNPUsers.py
    - GetUserSPNs.py
    - addcomputer.py
    - atexec.py
    - changepasswd.py
    - dcomexec.py
    - dpapi.py
    - esentutl.py
    - exchanger.py
    - findDelegation.py
    - getArch.py
    - getPac.py
    - getST.py
    - getTGT.py
    - goldenPac.py
    - karmaSMB.py
    - keylistattack.py
    - kintercept.py
    - lookupsid.py
    - machine_role.py
    - mimikatz.py
    - mqtt_check.py
    - mssqlclient.py
    - mssqlinstance.py
    - net.py
    - netview.py
    - nmapAnswerMachine.py
    - ntfs-read.py
    - ntlmrelayx.py
    - ping.py
    - ping6.py
    - psexec.py
    - raiseChild.py
    - rbcd.py
    - rdp_check.py
    - reg.py
    - registry-read.py
    - rpcdump.py
    - rpcmap.py
    - sambaPipe.py
    - samrdump.py
    - secretsdump.py
    - services.py
    - smbclient.py
    - smbexec.py
    - smbpasswd.py
    - smbrelayx.py
    - smbserver.py
    - sniff.py
    - sniffer.py
    - split.py
    - ticketConverter.py
    - ticketer.py
    - tstool.py
    - wmiexec.py
    - wmipersist.py
    - wmiquery.py
done! ✨ 🌟 ✨
➜  ~  mssqlclient.py -debug backdoor@10.129.201.248 -windows-auth 
Impacket v0.11.0 - Copyright 2023 Fortra

[+] Impacket Library Installation Path: /home/dz/.local/pipx/venvs/impacket/lib/python3.11/site-packages/impacket
Password:
[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(ILF-SQL-01): Line 1: Changed database context to 'master'.
[*] INFO(ILF-SQL-01): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (150 7208) 
[!] Press help for extra shell commands
SQL (ILF-SQL-01\backdoor  dbo@master)> show databases
[-] ERROR(ILF-SQL-01): Line 1: Could not find stored procedure 'show'.
SQL (ILF-SQL-01\backdoor  dbo@master)> SELECT name FROM sys.databases;
name        
---------   
master      

tempdb      

model       

msdb        

Employees   

SQL (ILF-SQL-01\backdoor  dbo@master)> 
```


