# Metasploitable 2 — Security Assessment

## Overview

Metasploitable 2 is a deliberately vulnerable Linux system designed for cybersecurity training and security testing.

It was assessed as part of the TS Academy Cybersecurity Capstone Project, where the objective was to identify security weaknesses, evaluate their potential impact, and recommend appropriate remediation measures.

> **Disclaimer:** This assessment was conducted in a controlled laboratory environment for educational purposes. No real organisation or third-party infrastructure was targeted.

---

## Assessment Objectives

The objectives of the Metasploitable 2 assessment were to:

* Identify vulnerabilities affecting the system.
* Identify insecure and unnecessarily exposed services.
* Assess the potential impact of identified vulnerabilities.
* Evaluate risks to confidentiality, integrity, and availability.
* Identify potential attacker objectives.
* Recommend appropriate security controls and remediation measures.
* Translate technical findings into practical security recommendations.

---

## System Assessed

| System             | Metasploitable 2                                      |
| ------------------ | ----------------------------------------------------- |
| Environment        | Controlled cybersecurity laboratory                   |
| Assessment Type    | Vulnerability Assessment / Penetration Testing        |
| Primary Focus      | Legacy services, authentication, and exposed services |
| Key Services       | Telnet, FTP, rlogin, Samba, MySQL, Apache             |
| Critical Finding   | Unauthenticated root shell on port 1524               |
| Assessment Context | TS Academy Cybersecurity Capstone Project             |

---

# Vulnerabilities Identified

## 1. Insecure Remote Login Protocols

### Affected Services

**Telnet, FTP, and rlogin**

### Description

Several legacy remote-access services were identified as transmitting usernames and passwords in plaintext.

Because the credentials are not adequately protected during transmission, an attacker positioned to intercept network traffic could potentially obtain valid credentials.

### Potential Attacker Goal

An attacker could potentially:

* Intercept user credentials.
* Obtain unauthorised access to accounts.
* Use compromised credentials to access systems or services.
* Perform additional malicious activities within the network.

### Risk

**High**

The use of plaintext authentication creates a significant risk of credential interception and subsequent unauthorised access.

---

## 2. Outdated Software and Services

### Affected Services

* FTP
* Samba
* MySQL
* Apache

### Description

Multiple services on the system were identified as running outdated versions containing publicly known vulnerabilities.

Running unsupported or outdated software increases the attack surface and gives attackers opportunities to exploit known weaknesses.

### Potential Attacker Goal

An attacker could attempt to:

* Exploit known vulnerabilities.
* Gain unauthorised access.
* Compromise individual services.
* Use compromised services as a pathway to further compromise the system.

### Risk

**High**

The presence of multiple outdated services significantly weakens the overall security posture of the system.

---

## 3. Unauthenticated Root Shell — Port 1524

### Affected Service

**Root Shell — TCP Port 1524**

### Description

A root shell was exposed on port 1524 and provided direct root-level access without requiring authentication.

This represents a critical security weakness because successful access would provide unrestricted administrative control over the system.

### Potential Attacker Goal

An attacker could potentially:

* Obtain immediate root privileges.
* Take complete control of the server.
* Access or modify sensitive information.
* Alter system configurations.
* Disrupt services.
* Use the compromised system for further attacks.

### Risk

**High**

Unauthenticated root-level access represents a severe compromise of system confidentiality, integrity, and availability.

---

# Risk Summary

| Vulnerability                   | Likelihood | Impact | Overall Risk |
| ------------------------------- | ---------- | ------ | ------------ |
| Insecure Remote Login Protocols | High       | High   | **High**     |
| Outdated Software & Services    | High       | High   | **High**     |
| Root Shell Backdoor — Port 1524 | High       | High   | **High**     |

---

# Security Impact

The findings demonstrate the risks created by legacy services, weak authentication practices, outdated software, and unnecessary exposure of privileged services.

In the simulated healthcare environment, successful exploitation could potentially result in:

* Unauthorised system access.
* Credential compromise.
* Privilege escalation or administrative compromise.
* Unauthorised access to sensitive information.
* Modification or destruction of data.
* Service disruption.
* Compromise of other systems within the environment.

The combination of multiple exposed and outdated services significantly increases the potential attack surface.

---

# Recommended Remediation

## 1. Replace Insecure Remote Login Protocols

Telnet, FTP, and rlogin should be removed or disabled where they are not required.

Secure alternatives should be used for remote administration and file transfer, such as encrypted protocols that protect credentials and data during transmission.

## 2. Patch and Update Software

All outdated services should be upgraded to supported versions.

A formal patch management process should be implemented to ensure security updates are identified, tested, prioritised, and deployed consistently.

## 3. Remove the Root Shell Backdoor

The unauthenticated root shell on port 1524 should be immediately removed.

The associated service should be disabled and the system should be investigated for any unauthorised changes resulting from exposure of the privileged shell.

## 4. Restrict Network Exposure

Firewall rules should be implemented to prevent unnecessary access to sensitive services.

Only required services should be accessible, and access should be restricted to authorised networks and users.

## 5. Reduce the Attack Surface

Unnecessary services should be disabled or removed.

Regular service reviews should be conducted to ensure systems are only exposing functionality that is required for business operations.

## 6. Implement Regular Vulnerability Assessments

Regular vulnerability scanning and security assessments should be conducted to identify outdated software, insecure configurations, exposed services, and newly discovered vulnerabilities.

---

# Security Controls

The assessment highlighted the need for:

* Secure remote-access protocols.
* Strong authentication and access controls.
* Regular patch management.
* Vulnerability scanning.
* Firewall rules and network segmentation.
* Service hardening.
* Removal of unnecessary services.
* Centralised security monitoring and logging.
* Regular security assessments.

---

# Skills Demonstrated

Through this assessment, I developed practical experience in:

* Vulnerability assessment
* Penetration testing concepts
* Network security
* Service enumeration concepts
* Risk assessment
* Vulnerability prioritisation
* Security impact analysis
* Security control recommendations
* System hardening
* Technical security documentation
* Security reporting
* GRC and remediation planning

---

# Key Takeaway

The Metasploitable 2 assessment demonstrated how insecure legacy protocols, outdated services, and exposed privileged access can create significant security risks.

The exercise reinforced the importance of:

1. Keeping software and services patched.
2. Removing unnecessary and insecure services.
3. Protecting authentication credentials during transmission.
4. Restricting network exposure.
5. Preventing unauthorised privileged access.
6. Continuously assessing systems for known vulnerabilities.

The findings from this assessment were incorporated into the wider security recommendations and GRC controls developed for the simulated Apex Healthcare environment.
