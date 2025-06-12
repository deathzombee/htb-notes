

## Advantages

- standardize methods and routes during recon: when doing a repetitive task during recon, we can often overlook something. having an automated flow can keep things from going over the wayside.

- scale: automation is simply faster at scale, when you have a lot of targets to look into recursive automation makes more sense at least on the front end

- standard output: again with scale having a standard output allows your tool to feed into other tools. 


## frameworks

- FinalRecon: python based recon tool with modules for different tasks like SSL cert checking, Whois info gathering, header anal, and crawling.

- Recon-ng: python based framework with modular structure with modules for different recon tasks. DNS enum, subdomain disco, port scanning, web crawling, and exploiting known vulns. 

- SpiderFoot: An opensource intel automation tool that integrates with various data sources. ip addresses, domain names, email addresses, and social media profiles. It can also perform DNS lookups, web crawling, and port scanning. 

- theHarvester: Designed for gathering email addresses, subdomains, hosts, employee names, open ports, and banners from different public sources like search engines, pgp key servers, and shodan. its a cli tool, written in python

- OSINT framework: A bunch of tools and resources for osinting. basically everything you can imagine. 

- Project Discovery: Like the OSINT Framework, but more focused on automation. Tools like nuclei, and tight integration between tools httpx -> nuclei -> notify


### FinalRecon
- `Header Information`: Reveals server details, technologies used, and potential security misconfigurations.
- `Whois Lookup`: Uncovers domain registration details, including registrant information and contact details.
- `SSL Certificate Information`: Examines the SSL/TLS certificate for validity, issuer, and other relevant details.
- `Crawler`:
    - HTML, CSS, JavaScript: Extracts links, resources, and potential vulnerabilities from these files.
    - Internal/External Links: Maps out the website's structure and identifies connections to other domains.
    - Images, robots.txt, sitemap.xml: Gathers information about allowed/disallowed crawling paths and website structure.
    - Links in JavaScript, Wayback Machine: Uncovers hidden links and historical website data.
- `DNS Enumeration`: Queries over 40 DNS record types, including DMARC records for email security assessment.
- `Subdomain Enumeration`: Leverages multiple data sources (crt.sh, AnubisDB, ThreatMiner, CertSpotter, Facebook API, VirusTotal API, Shodan API, BeVigil API) to discover subdomains.
- `Directory Enumeration`: Supports custom wordlists and file extensions to uncover hidden directories and files.
- `Wayback Machine`: Retrieves URLs from the last five years to analyse website changes and potential vulnerabilities.

#### FinalRecon install

`git clone https://github.com/thewhiteh4t/FinalRecon.git`
`cd FinalRecon`
`nake a virtualenv or set your pyenv, in my case I pyenv shell soup312`
`python -m pip install -r requirements.txt`

|Option|Argument|Description|
|---|---|---|
|`-h`, `--help`||Show the help message and exit.|
|`--url`|URL|Specify the target URL.|
|`--headers`||Retrieve header information for the target URL.|
|`--sslinfo`||Get SSL certificate information for the target URL.|
|`--whois`||Perform a Whois lookup for the target domain.|
|`--crawl`||Crawl the target website.|
|`--dns`||Perform DNS enumeration on the target domain.|
|`--sub`||Enumerate subdomains for the target domain.|
|`--dir`||Search for directories on the target website.|
|`--wayback`||Retrieve Wayback URLs for the target.|
|`--ps`||Perform a fast port scan on the target.|
|`--full`||Perform a full reconnaissance scan on the target.|


>example

```shell
cdeez@htb[/htb]$ ./finalrecon.py --headers --whois --url http://inlanefreight.com

 ______  __   __   __   ______   __
/\  ___\/\ \ /\ "-.\ \ /\  __ \ /\ \
\ \  __\\ \ \\ \ \-.  \\ \  __ \\ \ \____
 \ \_\   \ \_\\ \_\\"\_\\ \_\ \_\\ \_____\
  \/_/    \/_/ \/_/ \/_/ \/_/\/_/ \/_____/
 ______   ______   ______   ______   __   __
/\  == \ /\  ___\ /\  ___\ /\  __ \ /\ "-.\ \
\ \  __< \ \  __\ \ \ \____\ \ \/\ \\ \ \-.  \
 \ \_\ \_\\ \_____\\ \_____\\ \_____\\ \_\\"\_\
  \/_/ /_/ \/_____/ \/_____/ \/_____/ \/_/ \/_/

[>] Created By   : thewhiteh4t
 |---> Twitter   : https://twitter.com/thewhiteh4t
 |---> Community : https://twc1rcle.com/
[>] Version      : 1.1.6

[+] Target : http://inlanefreight.com

[+] IP Address : 134.209.24.248

[!] Headers :

Date : Tue, 11 Jun 2024 10:08:00 GMT
Server : Apache/2.4.41 (Ubuntu)
Link : <https://www.inlanefreight.com/index.php/wp-json/>; rel="https://api.w.org/", <https://www.inlanefreight.com/index.php/wp-json/wp/v2/pages/7>; rel="alternate"; type="application/json", <https://www.inlanefreight.com/>; rel=shortlink
Vary : Accept-Encoding
Content-Encoding : gzip
Content-Length : 5483
Keep-Alive : timeout=5, max=100
Connection : Keep-Alive
Content-Type : text/html; charset=UTF-8

[!] Whois Lookup : 

   Domain Name: INLANEFREIGHT.COM
   Registry Domain ID: 2420436757_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.registrar.amazon.com
   Registrar URL: http://registrar.amazon.com
   Updated Date: 2023-07-03T01:11:15Z
   Creation Date: 2019-08-05T22:43:09Z
   Registry Expiry Date: 2024-08-05T22:43:09Z
   Registrar: Amazon Registrar, Inc.
   Registrar IANA ID: 468
   Registrar Abuse Contact Email: abuse@amazonaws.com
   Registrar Abuse Contact Phone: +1.2024422253
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Name Server: NS-1303.AWSDNS-34.ORG
   Name Server: NS-1580.AWSDNS-05.CO.UK
   Name Server: NS-161.AWSDNS-20.COM
   Name Server: NS-671.AWSDNS-19.NET
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/


[+] Completed in 0:00:00.257780

[+] Exported : /home/htb-ac-643601/.local/share/finalrecon/dumps/fr_inlanefreight.com_11-06-2024_11:07:59

```
