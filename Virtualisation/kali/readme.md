# Kali Linux Home Lab Setup — VirtualBox

## Overview
I set up a Kali Linux virtual machine using Oracle VirtualBox as part of my cybersecurity home lab.

## Setup Process
1. Installed Oracle VirtualBox.
2. Created a virtual NAT network.
3. Configured the network using `10.0.0.0/24` as the IPv4 prefix.
4. Imported the Kali Linux virtual machine into VirtualBox.
5. Started the virtual machine and verified that it booted successfully.
6. Configured Kali Linux with the IP address `10.0.0.2`.
7. Configured the DNS server to use `8.8.8.8` as the primary.
8. Confirmed IP address settings & internet connectivity in the vm terminal with `nmcli connection show "My NAT Network" | grep -E 'ipv4.method|ipv4.addresses|ipv4.gateway'` `firefox www.google.com`
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

### Kali Linux VM Imported to VirtualBox
![Kali Linux Imported to VirtualBox](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/de264367edce1a5b03fdbc2304b60f324da449a1/Virtualisation/kali/images/Screenshot%20(311).png)

### Kali Linux Virtual Machine Running in VirtualBox
![Kali Linux running in VirtualBox](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/c612faf704de2c686007003587680d3b34869a00/Virtualisation/kali/images/Screenshot%20(309).png)

### IP Address Configuration in Kali
![Kali Linux IP configuration]()

![Kali Linux IP configuration]()


### IP address confirmation & Internet connectivity Test on the VM
![Kali Linux network Test](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/0fb54a1a42e9f120dfa46b5e03e258aa810dbb5f/Virtualisation/kali/images/Screenshot%20(320).png)

### Taking the Virtual Machine Snapshot
![Kali Linux virtual machine snapshot](https://github.com/ahwenisrael-maker/AHWEN_CyberSEC_Portfolio/blob/d8489bb0a472d632db8ac563c03b1af9e1d97b41/Virtualisation/kali/images/Screenshot%20(316).png)
### Problems Encountered
- IP Address 10.0.0.2 was not registering on the VM
### Investigative steps taken
- Confirmed I used the right subnet in the VirtualBox Network settings.
- Once sure I was correct, I arpinged the IP with `sudo arping -I eth0 -c 3 10.0.0.2` and discovered it was in use because it returned responses from a mac address `08:00:27:6e:5e:b4`
- Checked the mac address of my network adapter and confirmed it wasn't from it, and then I found that it had a similar prefix to mine and on further investigation, I learnt that the prefix is common to virtualbox network adapters.
- I checked my list of dhcp servers using `& "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" list dhcpservers` in my Windows(my host) Powershell
- Discovered that my network was using `10.0.0.2` as DHCP server.
### Solution to the problem
- Changing the DHCPd IP to 10.0.0.254 using `& "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" dhcpserver modify --network="My NAT Network" --server-ip=10.0.0.254 --lower-ip=10.0.0.3 --upper-ip=10.0.0.253 --netmask=255.255.255.0 --enable` in Windows Powershell.
- Reassigning the IP to Kali.
