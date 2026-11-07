# Android 9 x86 Virtual Machine Lab Setup

## 1. Project Overview

This project documents the installation and configuration of Android 9 (Android x86) in an Oracle VM VirtualBox environment.

The objective was to create a virtualized Android environment capable of running on standard x86-64 architecture without requiring a physical Android device.

The lab covers virtual machine creation, hardware resource allocation, OS installation, disk partitioning, bootloader configuration, network setup, static IP assignment, and connectivity verification between virtual machines.

## 2. Tools and Technologies

| Tool | Purpose |
|---|---|
| Oracle VM VirtualBox | Virtualization platform |
| Android 9 x86 ISO | Operating system installation image |
| Virtual Hard Disk | Storage for the Android installation |
| NAT Network | Virtual network connectivity |
| Android Terminal Emulator | Network testing and command execution |
| Kali Linux | Inter-VM connectivity testing |
| ICMP / Ping | Network connectivity verification |

## 3. Virtual Machine Creation and Configuration

### Step 1: Downloading the Android x86 ISO

The Android x86 disk image (ISO) was downloaded from SourceForge. This image served as the bootable installation media for the virtual machine.

### Step 2: Creating a New Virtual Machine

1. Opened Oracle VM VirtualBox.
2. Navigated to the **Machine** tab and selected **New**.
3. Configured the virtual machine with the following settings:

| Configuration | Selected Value |
|---|---|
| VM Name | `Android9_Lab` |
| Operating System Type | Linux |
| Version | Other Linux (64-bit) |
| Architecture | x86-64 |

### Step 3: Attaching the Installation Image

The downloaded Android x86 ISO file was selected and attached to the virtual machine's virtual optical drive.

This allowed VirtualBox to boot from the ISO and launch the Android x86 installation environment.

### Step 4: Creating the Virtual Hard Disk

A new virtual hard disk was created to provide storage for the Android operating system.

| Storage Configuration | Value |
|---|---|
| Virtual Disk Capacity | 10 GB |
| Disk Type | Virtual Hard Disk |

The 10 GB virtual disk provides storage space for the Android x86 installation and its associated system files.

### Step 5: Allocating Hardware Resources

The virtual machine's hardware resources were configured to provide sufficient memory and graphics capabilities for the Android environment.

| Hardware Component | Configuration |
|---|---|
| Base Memory (RAM) | 2048 MB (2 GB) |
| Video Memory | 128 MB |
| Graphics Controller | VBoxSVGA |

**Configuration Notes:**

- **RAM (2048 MB):** Allocated 2 GB of system memory to support the Android operating system.
- **Video Memory (128 MB):** Allocated 128 MB of video memory for graphical output.
- **Graphics Controller (VBoxSVGA):** Selected VirtualBox's VBoxSVGA graphics controller for the virtual display environment.

## 4. Android x86 Installation

### Step 6: Booting the Virtual Machine

After completing the initial VM configuration, the virtual machine was started.

The Android x86 installation ISO booted successfully, displaying the available boot options.

The **Installation – Install Android-x86 to harddisk** option was selected to install the operating system onto the virtual hard disk rather than running it temporarily as a Live CD.

### Step 7: Disk Partitioning

The installation process prompted for a target disk partition.

The `cfdisk` partitioning utility was used to create a new partition on the previously allocated 10 GB virtual hard disk.

The following operations were performed:

1. Selected the available virtual disk.
2. Created a new partition using the available disk capacity.
3. Allocated the available 10 GB of storage to the partition.
4. Marked the partition as **Bootable**.
5. Selected the **Write** option to save the partition table changes to the virtual disk.
6. Confirmed the changes and exited the partitioning utility.

This prepared the virtual hard disk for filesystem formatting and operating system installation.

### Step 8: Formatting the Partition

After creating the partition, the installer prompted for a filesystem type.

The newly created partition was formatted using **ext4 (Fourth Extended Filesystem)**.

Ext4 was selected as the filesystem for storing Android x86's system files and other installation data.

### Step 9: Installing the GRUB Bootloader

The installer prompted for bootloader installation.

**GRUB (Grand Unified Bootloader)** was installed to enable the virtual machine to locate and load the Android x86 operating system during startup.

The bootloader allows the VM to boot from the installed operating system on the virtual hard disk without relying on the installation ISO.

### Step 10: Rebooting and Removing the Installation Media

After completing the installation, the virtual machine was rebooted.

The Android installation ISO was ejected from the virtual optical drive to prevent the VM from booting back into the installation environment.

The operating system was then restarted from the newly created virtual hard disk.

## 5. Network Configuration

### Step 11: Connecting the VM to a NAT Network

After successfully installing Android x86, the virtual machine was powered off to allow network adapter configuration.

In VirtualBox, the VM's network settings were opened and its network adapter was connected to an existing NAT Network named **My NAT Network**.

This allowed the Android virtual machine to communicate with external networks through VirtualBox's NAT Network infrastructure.

### Step 12: Enabling Developer Options

After reconnecting the virtual machine to the NAT Network, Android was started.

The next objective was to configure a static IPv4 address rather than relying on automatic DHCP assignment.

However, the network configuration interface initially restricted access to the required IP configuration options.

To resolve this, Developer Options were enabled through the Android **About Phone** menu.

Once Developer Options had been enabled, the necessary network configuration options became accessible.

### Step 13: Configuring a Static IPv4 Address

The Android network configuration was changed from **DHCP** to **Static**.

The following network parameters were manually assigned:

| Network Parameter | Assigned Value |
|---|---|
| IP Address | `10.0.0.9` |
| CIDR Prefix | `/24` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.0.0.1` |
| Preferred DNS Server | `8.8.8.8` |
| IP Assignment | Static |

**Configuration Notes:**

- **IP Address (10.0.0.9):** Assigned a fixed IPv4 address to the Android virtual machine.
- **CIDR Prefix (/24):** Defined the network prefix, equivalent to the subnet mask `255.255.255.0`.
- **Default Gateway (10.0.0.1):** Specified the gateway through which the VM communicates with external networks.
- **DNS Server (8.8.8.8):** Configured Google's public DNS resolver for domain name resolution.
- **Static Assignment:** Ensured the VM retained its manually assigned network configuration instead of requesting an address through DHCP.

## 6. Internet Connectivity Testing

### Step 14: Verifying Internet Connectivity

After configuring the static IP address, network connectivity was tested using Android's built-in Terminal Emulator.

The following command was executed:

```bash
ping 8.8.8.8
```

The command sends ICMP Echo Request packets to Google's public DNS server at `8.8.8.8`.

The terminal returned four successful responses, confirming that the Android virtual machine could reach the external IP address.

**Test Result:** Successful — Four responses received.

The successful ping responses demonstrated that the VM had external IP connectivity through the configured NAT Network.

## 7. Inter-VM Network Connectivity Testing

### Step 15: Testing Communication Between Android x86 and Kali Linux

After verifying external internet connectivity, an additional connectivity test was performed to establish communication between the Android x86 virtual machine and an existing Kali Linux virtual machine.

Both virtual machines were connected to the same VirtualBox NAT Network (**My NAT Network**) and configured with static IPv4 addresses within the same subnet.

| Virtual Machine | IPv4 Address | Subnet |
|---|---|---|
| Android9_Lab | `10.0.0.9` | `10.0.0.0/24` |
| Kali Linux | `10.0.0.2` | `10.0.0.0/24` |

**Test 1: Pinging Kali Linux from Android x86**

The Android Terminal Emulator was used to send ICMP Echo Requests to the Kali Linux machine.

Command executed:

```bash
ping -c 4 10.0.0.2
```

The Kali Linux machine returned four successful ICMP Echo Replies.

**Result:** Successful — 4 responses received with 0% packet loss.

**Test 2: Pinging Android x86 from Kali Linux**

To verify communication in the opposite direction, the Kali Linux terminal was used to ping the Android x86 virtual machine.

Command executed:

```bash
ping -c 4 10.0.0.9
```

The Android x86 machine successfully returned ICMP Echo Replies to Kali Linux.

**Result:** Successful — Responses received from Android x86.

### Network Testing Summary

| Connectivity Test | Result |
|---|---|
| Android x86 → Google DNS (`8.8.8.8`) | Successful |
| Android x86 → Kali Linux (`10.0.0.2`) | Successful |
| Kali Linux → Android x86 (`10.0.0.9`) | Successful |
| Bidirectional Inter-VM Communication | Verified |

### Observations

The successful tests established that:

- Both virtual machines were reachable over the shared NAT Network.
- Both machines could communicate using their assigned static IPv4 addresses.
- ICMP traffic was successfully exchanged in both directions.
- The Android x86 virtual machine had external IP connectivity.

These results confirmed successful network communication between the two virtual machines and verified the basic network configuration of the lab.

## 8. Conclusion

Successfully installed and configured Android 9 x86 in Oracle VM VirtualBox.

The lab involved creating a virtual machine, allocating hardware resources, partitioning and formatting a virtual disk, installing the GRUB bootloader, and configuring static network parameters.

Network connectivity was subsequently verified through external ICMP testing and bidirectional communication with a Kali Linux virtual machine.

This exercise provided practical experience with operating system virtualization, disk partitioning, bootloader configuration, IPv4 addressing, static network configuration, and inter-VM network troubleshooting.

## 9. Screenshots and Lab Evidence

This section contains screenshots documenting the various stages of the Android 9 x86 virtual machine setup, installation, network configuration, and connectivity testing.

### 9.1 Virtual Machine Configuration

Displays the initial VirtualBox configuration, including memory allocation, video memory, graphics controller, and virtual disk creation.

![Android VM Configuration](screenshots/android-vm-configuration.png)

### 9.2 Android x86 Installation

Screenshots showing the Android x86 installation process, including the boot menu, disk partitioning, ext4 filesystem formatting, and GRUB bootloader installation.

![Android x86 Installation](screenshots/android-installation.png)

### 9.3 Successful Android Boot

Evidence of Android 9 x86 successfully booting from the installed virtual hard disk.

![Android 9 Desktop](screenshots/android-desktop.png)

### 9.4 Static IP Configuration

Displays the Android network configuration after switching from DHCP to Static IP assignment.

The VM was configured with the following parameters:

- IP Address: `10.0.0.9`
- Subnet Prefix: `/24`
- Gateway: `10.0.0.1`
- DNS Server: `8.8.8.8`

![Android Static IP Configuration](screenshots/android-static-ip.png)

### 9.5 Internet Connectivity Verification

Evidence of successful ICMP connectivity testing from Android x86 to Google's public DNS server (`8.8.8.8`).

![Android Internet Connectivity Test](screenshots/android-internet-ping.png)

### 9.6 Inter-VM Connectivity Testing

Screenshots demonstrating successful bidirectional communication between Android x86 and Kali Linux over the shared VirtualBox NAT Network.

**Android x86 to Kali Linux:**

![Android to Kali Ping](screenshots/android-to-kali-ping.png)

**Kali Linux to Android x86:**

![Kali to Android Ping](screenshots/kali-to-android-ping.png)
## Author
Ahwen Israel Lutor | NetworkWalks Batch B084E
