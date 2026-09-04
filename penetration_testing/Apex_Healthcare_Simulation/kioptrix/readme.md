# Kioptrix — Security Assessment

## Overview

Kioptrix is a deliberately vulnerable legacy system assessed as part of the TS Academy Cybersecurity Capstone Project.

The assessment focused on identifying security weaknesses within the system, evaluating their potential impact, and recommending appropriate remediation measures.

> **Disclaimer:** This assessment was conducted in a controlled laboratory environment for educational purposes. Kioptrix was not a production system and no real organisation or third-party infrastructure was targeted.

---

## Assessment Objectives

The objectives of the Kioptrix assessment were to:

* Identify vulnerabilities affecting the system.
* Determine the potential impact of identified weaknesses.
* Assess how vulnerabilities could affect confidentiality, integrity, and availability.
* Identify potential attacker objectives.
* Recommend appropriate security controls and remediation measures.
* Demonstrate how technical vulnerabilities can translate into organisational security risks.

---

## System Assessed

| System             | Kioptrix                                       |
| ------------------ | ---------------------------------------------- |
| Environment        | Controlled cybersecurity laboratory            |
| Assessment Type    | Vulnerability Assessment / Penetration Testing |
| Primary Focus      | Legacy services and system configuration       |
| Key Services       | Samba, Apache HTTP Server, Operating System    |
| Assessment Context | TS Academy Cybersecurity Capstone Project      |

---

# Vulnerabilities Identified

## 1. Username Mapping Script Vulnerability

### Affected Service

**Samba (SMB File Sharing)**

### Description

The Samba service was identified as running an outdated version affected by a known username-mapping vulnerability.

The vulnerability results from improper handling of username mapping requests and could allow an unauthorised user to execute arbitrary commands on the system.

### Potential Attacker Goal

An attacker could potentially:

* Gain unauthorised remote access.
* Execute malicious commands.
* Compromise the server.
* Use the compromised system as a starting point for further attacks.

### Risk

**High**

The vulnerability presents significant risk because successful exploitation could result in unauthorised remote access and command execution.

---

## 2. Weak System Configuration and Unpatched Operating System

### Affected Component

**Operating System**

### Description

The operating system was identified as lacking current security updates and containing legacy vulnerabilities that remained publicly documented.

Systems that are no longer regularly patched have an increased attack surface because known vulnerabilities remain available for attackers to target.

### Potential Attacker Goal

An attacker could attempt to:

* Exploit known vulnerabilities.
* Obtain elevated privileges.
* Establish persistence.
* Fully compromise the server.

### Risk

**High**

The combination of an outdated operating system and known vulnerabilities increases the likelihood of successful compromise.

---

## 3. Outdated Apache Web Server

### Affected Service

**Apache HTTP Server**

### Description

The Apache web server was running an outdated version containing publicly known security flaws.

An attacker could potentially exploit weaknesses in the outdated service to compromise the web server or the underlying system.

### Potential Attacker Goal

An attacker could attempt to:

* Compromise the web server.
* Access sensitive files.
* Exploit the underlying system.
* Disrupt web services.

### Risk

**High**

An outdated, publicly exposed web service increases the attack surface and can provide attackers with an avenue into the system.

---

# Risk Summary

| Vulnerability                     | Likelihood | Impact | Overall Risk |
| --------------------------------- | ---------- | ------ | ------------ |
| Username Mapping / Outdated Samba | High       | High   | **High**     |
| Unpatched Operating System        | High       | High   | **High**     |
| Outdated Apache Server            | High       | High   | **High**     |

---

# Security Impact

The vulnerabilities identified demonstrate the risks associated with maintaining legacy systems without regular security updates.

Outdated software and weak system configurations increase the attack surface and can allow attackers to exploit publicly documented vulnerabilities.

In the simulated healthcare environment, successful compromise could potentially result in:

* Unauthorised access to sensitive information.
* Compromise of internal systems.
* Exposure of patient-related information.
* Service disruption.
* Loss of confidentiality, integrity, and availability.

---

# Recommended Remediation

## 1. Patch and Update Samba

Upgrade the Samba service to a supported and secure version.

Where the service is not required, it should be disabled or removed.

Network access to SMB services should also be restricted using appropriate firewall rules.

## 2. Maintain Regular Operating System Patching

Implement a formal patch management process to ensure operating systems receive security updates within defined timeframes.

Critical vulnerabilities should receive priority remediation.

## 3. Harden the Operating System

Review system configuration and disable unnecessary services and functionality.

Apply secure configuration standards and regularly review the system for weaknesses.

## 4. Update Apache

Upgrade Apache to a supported version and ensure security updates are applied regularly.

Unnecessary modules and services should be disabled to reduce the attack surface.

## 5. Implement Network Segmentation

Restrict access to vulnerable or sensitive services through firewall rules and network segmentation.

Critical systems should not be unnecessarily exposed to untrusted networks.

## 6. Conduct Regular Vulnerability Assessments

Regular vulnerability scanning and security assessments should be performed to identify newly introduced or previously overlooked weaknesses.

---

# Security Controls

The assessment highlighted the need for several foundational security controls:

* Regular vulnerability scanning.
* Patch and update management.
* Network segmentation.
* Firewall access controls.
* Secure system configuration.
* Service hardening.
* Continuous security monitoring.
* Regular security assessments.

---

# Skills Demonstrated

Through this assessment, I developed practical experience in:

* Vulnerability assessment
* Penetration testing concepts
* Network security
* Vulnerability identification
* Risk assessment
* Security impact analysis
* Security control recommendations
* System hardening concepts
* Technical documentation
* Security reporting
* GRC and remediation planning

---

# Key Takeaway

The Kioptrix assessment demonstrated how outdated services and unsupported system configurations can create significant security risks.

The exercise reinforced an important principle of cybersecurity: **a vulnerability is not only a technical problem—it can become a business risk when it affects critical systems, sensitive information, or service availability.**

The findings from this assessment were subsequently used to develop broader security controls and governance recommendations for the simulated Apex Healthcare environment.
