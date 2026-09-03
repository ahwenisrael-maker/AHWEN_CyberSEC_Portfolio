# Apex Healthcare — Legacy Systems Security Assessment

## Project Overview

A simulated penetration testing and security assessment conducted as part of the TS Academy Cybersecurity Capstone Project.

The assessment simulated a security engagement for **Apex Healthcare Solutions**, an organisation providing digital patient record services to healthcare facilities. The objective was to assess two legacy systems, **Kioptrix** and **Metasploitable 2**, identify security weaknesses, evaluate their potential impact, and recommend appropriate security controls and remediation measures.

> **Disclaimer:** Apex Healthcare Solutions is a simulated organisation used for educational purposes. All security testing was performed in controlled laboratory environments.

---

## Objectives

* Identify vulnerabilities within two legacy systems.
* Assess the likelihood and potential impact of identified vulnerabilities.
* Demonstrate how vulnerabilities could affect confidentiality, integrity, and availability.
* Recommend appropriate technical security controls.
* Develop governance, risk, and compliance (GRC) recommendations.
* Provide a prioritised roadmap for improving the simulated organisation's security posture.

---

## Systems Assessed

| System               | Assessment Focus                                               |
| -------------------- | -------------------------------------------------------------- |
| **Kioptrix**         | Legacy services, Samba, Apache, system configuration           |
| **Metasploitable 2** | Legacy services, authentication, exposed services, root access |

---

## Vulnerabilities Identified

### Kioptrix

1. **Username Mapping Script Vulnerability / Outdated Samba**

   * Potential for unauthorised remote command execution.
   * Rated High likelihood / High impact.

2. **Weak System Configuration & Unpatched Operating System**

   * Legacy vulnerabilities and missing security updates.
   * Rated High likelihood / High impact.

3. **Outdated Apache Web Server**

   * Publicly known vulnerabilities potentially exposing the web server and sensitive information.
   * Rated High likelihood / High impact.

### Metasploitable 2

1. **Insecure Remote Login Services**

   * Telnet, FTP, and rlogin transmit credentials insecurely.
   * Rated High likelihood / High impact.

2. **Outdated Software & Services**

   * Multiple outdated services with publicly known vulnerabilities.
   * Rated High likelihood / High impact.

3. **Root Shell Backdoor — Port 1524**

   * Provides unauthenticated root-level access.
   * Rated High likelihood / High impact.

---

## Security Recommendations

Key recommendations included:

* Regular operating-system and application patching.
* Firewall rules and network segmentation.
* Replacement of insecure remote-access protocols with secure alternatives.
* Removal of unnecessary services and the root shell backdoor.
* Strong authentication and access-control mechanisms.
* Vulnerability scanning and regular security assessments.
* Centralised security monitoring and logging.

---

## GRC Recommendations

The assessment also produced four proposed organisational security policies:

* **Software Update & Patch Management Policy**
* **Access Control & Authentication Policy**
* **Network Segmentation Policy**
* **Vulnerability Management & Security Assessment Policy**

These recommendations were designed to address the technical weaknesses identified during the assessment and establish longer-term security processes.

---

## Tools & Technologies

* Kali Linux
* Nmap
* Nessus
* Wazuh
* VirtualBox
* [Add other tools used]

---

## Skills Demonstrated

* Vulnerability Assessment
* Penetration Testing
* Network Security
* Security Risk Assessment
* Vulnerability Prioritisation
* Security Controls
* Incident Response Concepts
* SIEM / Security Monitoring
* Technical Documentation
* GRC & Security Policy Development

---

## Project Deliverables

* Vulnerability findings and analysis
* Risk assessments
* Security control recommendations
* GRC policy recommendations
* 12-month security implementation roadmap

---

## Key Takeaways

This project demonstrated how technical vulnerabilities in legacy systems can translate into broader organisational risks. It also provided practical experience connecting vulnerability assessment and penetration testing findings with remediation, security controls, governance, and organisational risk management.
