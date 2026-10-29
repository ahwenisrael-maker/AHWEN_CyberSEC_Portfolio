# Kali Linux Home Lab Setup — VirtualBox

## Overview
I set up a Kali Linux virtual machine using Oracle VirtualBox as part of my cybersecurity home lab.

## Setup Process
1. Installed Oracle VirtualBox.
2. Created a virtual NAT network.
3. Configured the network using `10.0.0.0/24` as the IPv4 prefix.
4. Imported the Kali Linux virtual machine into VirtualBox.
5. Started the virtual machine and verified that it booted successfully.
6. Configured Kali Linux with the IP address `10.0.0.4`.
7. Configured two DNS servers to use `10.0.0.1` as primary and `8.8.8.8` as the secondary.
8. Tested internet connectivity with Google.com
9. Created a virtual machine snapshot to preserve the configured state.

## Skills Demonstrated
- Virtualisation and virtual machine management.
- IPv4 network configuration and DNS setup.
- Virtual network setup and snapshot management.

## Purpose
Establishing a dedicated environment for practising penetration testing and developing practical cybersecurity skills in a controlled laboratory.
## Screenshots
### NAT Network Configuration in VirtualBox
![VirtualBox NAT network settings](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/d8489bb0a472d632db8ac563c03b1af9e1d97b41/Virtualisation/kali/images/Screenshot%20(315).png)

### Kali Linux Virtual Machine
![Kali Linux running in VirtualBox](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/c612faf704de2c686007003587680d3b34869a00/Virtualisation/kali/images/Screenshot%20(309).png)

### IP Address Configuration
![Kali Linux IP configuration](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/07324e08ea082d166118eb323ac239316d41e4ee/Virtualisation/kali/images/Screenshot%20(322).png)

![Kali Linux IP configuration](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/0fb54a1a42e9f120dfa46b5e03e258aa810dbb5f/Virtualisation/kali/images/Screenshot%20(318).png)


### Internet connectivity Test on the VM
![Kali Linux network Test](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/0fb54a1a42e9f120dfa46b5e03e258aa810dbb5f/Virtualisation/kali/images/Screenshot%20(320).png)

### Virtual Machine Snapshot
![Kali Linux virtual machine snapshot](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/d8489bb0a472d632db8ac563c03b1af9e1d97b41/Virtualisation/kali/images/Screenshot%20(316).png)
