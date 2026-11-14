# Network Reconnaissance and OSINT Assessment

## Project Overview

This project documents a series of cybersecurity reconnaissance activities completed as part of the NetworkWalks Internship. The activities involved gathering publicly available information about an assigned domain, identifying externally visible technologies and DNS records, discovering hosts within a controlled virtual network, and using OSINT techniques to identify publicly associated email addresses.

The exercises provided practical exposure to reconnaissance tools, network discovery, information gathering, technical analysis, and security reporting.

## Objectives

- Gather publicly available information about an assigned domain.
- Identify domain infrastructure, DNS records, and web technologies.
- Detect the presence of web application firewall technology.
- Discover active hosts within a controlled virtual network.
- Use Maltego to identify publicly associated email addresses.
- Interpret findings and document relevant security observations.

## Scope

The project consisted of three separate activities:

1. **External Domain Reconnaissance:** Examining `networkwalks.com` using six reconnaissance tools in Kali Linux.
2. **Internal Network Discovery:** Identifying active hosts within my own VirtualBox NAT Network using Zenmap on a Windows virtual machine.
3. **OSINT Investigation:** Using Maltego to discover publicly associated email addresses linked to the assigned domain.

The activities were limited to information gathering and host discovery. No exploitation, intrusive vulnerability testing, or penetration testing was performed.

## Project Approach

The activities were completed individually using a structured internship guide. I independently installed and configured the required tools, followed the prescribed procedures, executed the relevant commands and transforms, examined the results, and documented my observations.

---

# 1. External Domain Reconnaissance

## Objective

To examine the publicly exposed information and infrastructure associated with `networkwalks.com` using passive and non-intrusive reconnaissance techniques.

## Tools Used

- WHOIS
- WhatWeb
- nslookup
- DNSrecon
- WAFW00F
- cURL

## Methodology and Technical Findings

### 1.1 Domain Registration Analysis — WHOIS

Used WHOIS to investigate the domain's registration details, registrar, registration dates, nameservers, domain status codes, and DNSSEC status.

**Key observations:**
- The domain is registered through GoDaddy.com, LLC.
- Registrant information is protected by a domain privacy service.
- Multiple nameservers associated with HostGator and DomainControl were listed.
- The domain was marked as DNSSEC unsigned.
- Several client-side domain locks were enabled, restricting certain unauthorized domain modifications.

**Security relevance:**

This exercise demonstrated the ability to extract and interpret domain registration intelligence. The domain locks represent useful protective controls, while the absence of DNSSEC presents an area worth reviewing as part of DNS security hardening.

### 1.2 Web Technology Fingerprinting — WhatWeb

Used WhatWeb to identify technologies and services exposed by the target website.

**Key observations:**
- Web server identified as Apache.
- Content management system identified as WordPress.
- WordPress Download Manager was detected.
- jQuery and other frontend technologies were fingerprinted.
- The website returned HTTP 200 over HTTPS.
- The HTTP endpoint redirected to HTTPS.
- A publicly displayed email address was identified: `info@networkwalks.com`.

**Security relevance:**

Technology fingerprinting helps establish an understanding of a website's externally visible technology stack. Disclosed software versions can inform subsequent security research, although version identification alone does not establish that a component is vulnerable.

### 1.3 DNS Resolution — nslookup

Used nslookup with Google's public DNS resolver (`8.8.8.8`) to determine the IPv4 address associated with the domain.

**Key observation:**
- `networkwalks.com` resolved to `192.232.216.135`.

**Security relevance:**

This exercise demonstrated the ability to query DNS infrastructure and identify the public IP address associated with a domain, providing a starting point for understanding its external network presence.

### 1.4 DNS Enumeration — DNSrecon

Used DNSrecon to enumerate publicly available DNS records and identify additional infrastructure information.

**Key observations:**
- Identified A, NS, SOA, MX, TXT, and SRV records.
- Identified the mail host associated with the domain.
- Retrieved SPF information from the domain's TXT records.
- Observed DNSSEC query failure, consistent with the unsigned status reported by WHOIS.
- Identified BIND version information exposed through DNS enumeration.

**Security relevance:**

DNS enumeration provided a broader picture of the domain's infrastructure and email configuration. The SPF record used a softfail policy (`~all`), which warrants review alongside DKIM and DMARC configuration. The disclosed DNS server version also represents information that could assist infrastructure fingerprinting.

### 1.5 Web Application Firewall Detection — WAFW00F

Used WAFW00F to identify whether a web application firewall was present.

**Key observation:**
- The tool identified ModSecurity (SpiderLabs) as the web application firewall protecting the website.

**Security relevance:**

Identifying an existing WAF provided insight into the website's defensive infrastructure. However, detection alone does not establish the effectiveness of its rules or configuration.

### 1.6 HTTP Response Header Inspection — cURL

Used `curl -I` to retrieve the HTTP response headers returned by the HTTPS endpoint.

**Key observations:**
- The server returned HTTP/2 200.
- The response included `Permissions-Policy` and `Referrer-Policy` headers.
- The `__wpdm_client` cookie was marked `Secure` and `HttpOnly`.
- WordPress REST API endpoints were advertised through the response's `Link` header.
- HSTS and Content Security Policy headers were not observed in the captured response.

**Security relevance:**

HTTP header inspection provided insight into the website's transport-related behaviour, browser security controls, cookie handling, and publicly advertised application endpoints. The absence of certain headers from this particular response warrants further verification rather than an immediate conclusion that they are missing site-wide.

### 1.7 Screenshots and Evidence

The following screenshots provide evidence of the external reconnaissance procedures and their corresponding results.

**WHOIS**
![WHOIS Results](screenshots/external-recon/whois.png)

**WhatWeb**
![WhatWeb Results](screenshots/external-recon/whatweb.png)

**nslookup**
![nslookup Results](screenshots/external-recon/nslookup.png)

**DNSrecon**
![DNSrecon Results](screenshots/external-recon/dnsrecon.png)

**WAFW00F**
![WAFW00F Results](screenshots/external-recon/wafw00f.png)

**cURL**
![cURL Results](screenshots/external-recon/curl.png)

### Skills Demonstrated

- Domain registration intelligence gathering.
- DNS lookup and record enumeration.
- Web technology fingerprinting.
- WAF identification.
- HTTP response and security-header analysis.
- Interpretation of publicly exposed infrastructure information.
- Identification of potential security-hardening opportunities.

---

# 2. Internal Network Discovery

## Objective

To identify active hosts within a controlled VirtualBox NAT Network and understand the devices participating in the virtual lab environment.

## Tools Used

- Zenmap (Nmap GUI)
- Windows Command Prompt
- Oracle VirtualBox

## Methodology and Findings

Zenmap was downloaded and executed on a Windows virtual machine hosted in VirtualBox. The following host-discovery scan was performed against my own NAT Network:

```bash
nmap -sn 10.0.0.0/24
```

The `-sn` option performs host discovery without conducting a port scan.

**Four active hosts were identified:**

| IP Address | Identified Device |
|---|---|
| 10.0.0.1 | VirtualBox NAT gateway |
| 10.0.0.2 | Kali Linux VM |
| 10.0.0.10 | Windows VM (scanning machine) |
| 10.0.0.254 | VirtualBox DHCP server |

Windows Command Prompt was also used to inspect local network interface information and retrieve the Windows VM's MAC address:

```cmd
ipconfig /all
```

## Security Relevance

The exercise demonstrated practical understanding of subnet notation, host discovery, virtual network architecture, and device identification.

By comparing scan results with the known VirtualBox configuration, I was able to distinguish the gateway, DHCP server, and virtual machines participating in the network.

It also reinforced the importance of understanding scan scope: this activity was restricted to my own controlled lab environment and did not involve the internship's target infrastructure.

## 2.1 Screenshots and Evidence

The following screenshots document the internal network discovery process, including the host-discovery results and Windows network configuration inspection.

**Zenmap Host Discovery**
![Zenmap Host Discovery](screenshots/internal-recon/zenmap.png)

**Windows Network Configuration**
![Windows Network Configuration](screenshots/internal-recon/ipconfig.png)

## Skills Demonstrated

- Network discovery using Nmap/Zenmap.
- CIDR notation and subnet awareness.
- Virtual network configuration and topology identification.
- Windows network diagnostics.
- Interpretation of host-discovery results.
- Responsible definition of scanning scope.

---

# 3. Open-Source Intelligence (OSINT) Investigation

## Objective

To use Maltego to identify publicly discoverable email addresses associated with the assigned domain, `networkwalks.com`.

## Tool Used

- Maltego

## Methodology and Findings

Installed and activated Maltego using my Maltego ID, then initiated an investigation by adding `networkwalks.com` as a Domain entity to the graph.

From the Transform menu, I searched for and executed the **Utilities to email@domain** transform to retrieve email intelligence associated with the domain.

**Key observations:**
- The investigation returned one email address: `info@networkwalks.com`.
- The same address had also been identified during the earlier WhatWeb reconnaissance.

## Security Relevance

This exercise demonstrated the use of entity-based OSINT to investigate relationships between publicly available domain information and associated email addresses.

The discovery of the same email address through two different tools provided consistency between the observations. However, this does not independently verify that the mailbox is active or establish the identity of its owner.

Publicly discoverable email addresses can provide useful intelligence for understanding an organization's external exposure and assessing potential social-engineering risks.

## 3.1 Screenshots and Evidence

The following screenshots document the Maltego investigation, including the domain entity, selected transform, and resulting email intelligence.

**Domain Entity**
![Maltego Domain Entity](screenshots/osint/maltego-domain.png)

**Transform Selection**
![Maltego Transform](screenshots/osint/maltego-transform.png)

**Email Discovery Result**
![Maltego Email Discovery](screenshots/osint/maltego-result.png)

## Skills Demonstrated

- OSINT tool installation and configuration.
- Domain-based intelligence gathering.
- Entity and transform selection in Maltego.
- Graph-based investigation.
- Identification and interpretation of publicly associated email intelligence.
- Correlation of findings across reconnaissance tools.

---

# 4. Consolidated Findings and Security Observations

The reconnaissance activities produced several observations about the target domain's publicly visible infrastructure and the configuration of my controlled virtual network.

## 4.1 Positive Security Observations

- **Domain Protection:** WHOIS revealed multiple client-side domain locks, providing protection against certain unauthorized domain changes.
- **HTTPS Enforcement:** HTTP requests were redirected to HTTPS, encouraging encrypted communication.
- **Web Application Firewall:** WAFW00F detected ModSecurity, indicating the presence of a web application firewall.
- **Cookie Protection:** The observed `__wpdm_client` cookie included the `Secure` and `HttpOnly` attributes.
- **Network Awareness:** Internal host discovery successfully identified all four expected devices within the controlled virtual network.

## 4.2 Areas Requiring Further Security Review

| Observation | Security Implication |
|---|---|
| DNSSEC unsigned | DNS integrity protection could be strengthened through DNSSEC deployment. |
| SPF softfail (`~all`) | Email authentication policy should be reviewed alongside DKIM and DMARC. |
| Server version disclosure | Exposed version information may assist infrastructure fingerprinting. |
| HTTP security headers | HSTS and Content Security Policy were not observed in the captured response and warrant further verification. |
| Nameserver listing discrepancy | WHOIS and DNSrecon returned different nameserver lists; authoritative DNS records should be verified. |
| Publicly advertised WordPress REST API | Endpoint permissions and publicly accessible information should be reviewed. |

## 4.3 Overall Assessment

The reconnaissance exercise identified existing defensive controls as well as several configuration and information-disclosure areas that could benefit from further review.

The findings are preliminary observations based on publicly available information and limited host discovery. They do not establish the presence of exploitable vulnerabilities or evidence of compromise.

Further investigation would be necessary to validate the identified observations, determine their actual security impact, and establish appropriate remediation priorities.

## 4.4 Recommended Follow-up Actions

- Evaluate the feasibility of enabling DNSSEC.
- Review SPF configuration and verify DKIM and DMARC implementation.
- Minimize unnecessary infrastructure version disclosure.
- Review HTTP security-header configuration, including HSTS and Content Security Policy.
- Verify authoritative nameserver delegation.
- Review publicly accessible WordPress REST API resources and permissions.
- Maintain and regularly review WAF rules and software updates.

---

# 5. Skills Acquired and Professional Competencies

The practical exercises provided hands-on experience in several areas of cybersecurity reconnaissance and information gathering.

## Technical Competencies

- **Domain Intelligence:** Extracting and interpreting domain registration information using WHOIS.
- **Web Technology Fingerprinting:** Identifying publicly exposed web technologies and application components using WhatWeb.
- **DNS Analysis:** Performing DNS lookups and enumerating records using nslookup and DNSrecon.
- **WAF Identification:** Detecting web application firewall technology using WAFW00F.
- **HTTP Analysis:** Inspecting HTTP response headers, cookies, and application metadata using cURL.
- **Network Discovery:** Identifying active hosts and interpreting scan results using Nmap and Zenmap.
- **Windows Network Diagnostics:** Examining network interface configuration and MAC address information using Windows Command Prompt.
- **OSINT Investigation:** Conducting domain-based intelligence gathering and identifying associated email information using Maltego.
- **Virtualization:** Working with VirtualBox-hosted virtual machines and a controlled NAT Network.

## Analytical and Professional Competencies

Beyond operating the tools, the exercises strengthened my ability to:

- Interpret technical output and extract relevant security information.
- Correlate observations obtained from different reconnaissance tools.
- Distinguish security controls from potential configuration weaknesses.
- Identify areas requiring further investigation without making unsupported vulnerability claims.
- Understand and maintain defined assessment scope.
- Document technical procedures and communicate findings in a structured manner.
- Recognize the limitations of automated reconnaissance tools.

These competencies provide a foundation for further development in security assessment, vulnerability management, and penetration testing.

---

# 6. Project Limitations

This exercise was limited to reconnaissance, OSINT, and host discovery.

- No exploitation or penetration testing was performed.
- No intrusive vulnerability scanning was conducted.
- No open-port or service enumeration was performed during the internal network scan.
- Publicly identified software versions and configuration observations were not independently validated for exploitability.
- The Maltego result identified one publicly discoverable email address; it did not establish that the mailbox was active.
- Findings represent observations made during the exercise and may change as the target infrastructure changes.

These limitations are important when interpreting the results and prevent preliminary observations from being presented as confirmed security vulnerabilities.

---

# 7. Tools and Technologies

| Category | Tools |
|---|---|
| Operating Systems | Kali Linux, Windows |
| Virtualization | Oracle VirtualBox |
| Domain Intelligence | WHOIS |
| Web Fingerprinting | WhatWeb |
| DNS Analysis | nslookup, DNSrecon |
| WAF Detection | WAFW00F |
| HTTP Inspection | cURL |
| Network Discovery | Nmap, Zenmap |
| OSINT | Maltego |
| Windows Diagnostics | Command Prompt |

---

# 8. Conclusion

This project provided practical experience in external domain reconnaissance, internal network discovery, and open-source intelligence gathering.

Through the use of Kali Linux reconnaissance tools, Zenmap, Windows Command Prompt, Maltego, and VirtualBox, I gained experience identifying publicly exposed infrastructure information, examining DNS and HTTP configurations, discovering hosts within a controlled network, and correlating intelligence from multiple sources.

More importantly, the exercise strengthened my ability to interpret technical findings, recognize potential security concerns, understand the importance of assessment scope, and document observations responsibly.

The experience has reinforced my interest in offensive security and provided a practical foundation for progressing into more advanced network security assessments and penetration testing.

---

# 9. Project Evidence

Screenshots documenting the installation, execution, and results of the reconnaissance activities are included within their respective sections of this README.

They provide supporting evidence of the procedures performed and the observations documented throughout the project.
# Author
Ahwen Israel Lutor | Networkwalks Batch B084E
