# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**

## 📌 Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration-testing laboratory** using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled, isolated environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly. The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

## 🎯 Objectives

* Install and configure Oracle VM VirtualBox.

* Import and set up Kali Linux as the primary attacker virtual machine.

* Create a private **NAT Network** for the cybersecurity lab to ensure isolation.

* Configure manual network connectivity and a static IP for Kali Linux.

* Verify active network connectivity and DNS resolution.

* Document the setup process and capture baseline snapshots.

* Prepare the environment for future cybersecurity project modules.

## ⚙️ Lab Configuration

| 🧩 Component | ⚙️ Configuration | 
| ----- | ----- | 
| 🖥️ Host OS | Windows 11 | 
| 🧠 Host RAM | 8 GB (Minimum) | 
| ⚡ Processor | Intel Core i7 (or equivalent) | 
| 🧰 Hypervisor | VirtualBox 7.2 | 
| 🐉 Security OS | Kali Linux 2026.2 | 
| 🧠 Kali RAM | 2048 MB | 
| 🌐 Virtual Network | NAT Network | 
| 📡 Network Address | `10.0.0.0/24` | 
| 🐧 Kali IP Address | `10.0.0.2/24` | 
| 🚪 Default Gateway | `10.0.0.1` | 
| 🌍 DNS Server | `10.0.0.1` | 

## 📸 Lab Environment & Screenshots

Below is the visual documentation of the configured environment.

### 1. VirtualBox Manager Setup

The hypervisor is configured with the Kali Linux VM and the custom NAT Network.

![VirtualBox snapshot manager](<Screenshot 2026-10-28 022828.png>)

### 2. Kali Linux Virtual Machine

The primary attacker machine successfully imported and running.

![Kali Linux virtual machine](<Screenshot 2026-10-28 022633.png>)

### 3. Wired Connection & Static IP Configuration

Manual IPv4 settings configured to `10.0.0.2/24` with the gateway pointing to `10.0.0.1`.

![Kali Linux static IPv4 configuration](<Screenshot 2026-10-28 022713.png>)

### 4. Internet Connectivity Verification

Successful internet connection and DNS resolution verified via Mozilla Firefox.

![Internet connectivity verification in Firefox](<Screenshot 2026-10-28 022749.png>)

## 🪜 Lab Setup Procedure

### Step 1: Install VirtualBox & Required Tools

* Downloaded and installed 7-Zip to extract the Kali Linux `.7z` archive.

* Installed Oracle VM VirtualBox as the primary hypervisor.

### Step 2: Create the NAT Network

A dedicated NAT Network was created in VirtualBox to allow VMs to communicate with each other while maintaining outbound internet access.

* **Network Name:** NatNetwork

* **IPv4 Prefix:** `10.0.0.0/24`

* **DHCP:** Enabled

### Step 3: Import and Configure Kali Linux

* Imported the official Kali Linux VirtualBox image.

* Configured the Network Adapter to attach to the `NAT Network` (`NatNetwork`).

* Allocated 2048 MB of Base Memory (RAM).

* Configured shared folders for seamless host-to-guest file transfers.

### Step 4: Configure the Kali Linux Network

Set up a consistent static IP address through the Network Manager to ensure the machine can be easily referenced in future exercises.

* **Address:** `10.0.0.2`

* **Netmask:** `24` (`255.255.255.0`)

* **Gateway:** `10.0.0.1`

* **DNS:** `8.8.8.8`

### Step 5: Create a Clean VM Snapshot

After verifying all configurations and connectivity, a clean baseline snapshot was taken (e.g., `Clean Kali - Network Setup`). This allows for safe recovery if future testing disrupts the system.

## 🐞 Problems Encountered & Solutions

### Internet Connectivity After Static IP Configuration

**Issue:** After manually configuring the static IPv4 settings (`10.0.0.2`), the Kali VM experienced connectivity issues and could not access the internet.

**Solution:** Thanks to the detailed troubleshooting video provided by my instructor, I learned this is a known duplicate address detection/timeout behavior in newer versions of Kali and VirtualBox. I resolved it by running the following commands in the terminal to modify and restart the connection:

```
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"

```

After executing these commands, full internet access was successfully restored.

## 💡 What I Learned

Through this Week 1 project, I gained hands-on experience in:

1. **NAT vs. NAT Network:** Understanding how a NAT Network facilitates inter-VM communication (essential for a multi-machine lab) while still allowing external access.

2. **Virtual Machine Networking:** Managing virtual adapters, static routing, and manual IPv4 configurations within a Linux environment.

3. **Troubleshooting Network Interfaces:** Using `nmcli` (NetworkManager command-line tool) to diagnose and fix interface connectivity bugs.

4. **Snapshot Management:** Understanding the critical importance of establishing a "known-good" baseline before conducting experimental security tests.

## 🔐 Security & Ethical Use

**⚠️ Important:** This laboratory is intended strictly for educational purposes. The tools and techniques practiced within this environment must only be used on systems that you own or have explicit, documented permission to test.

## 👤 Author

**Mst Umme Sabiha**

Cybersecurity Intern | Network Walks

LinkedIn: https://www.linkedin.com/in/umme-sabiha/

## 📌 Project Information

**Program Name:** Cybersecurity Internship at Network Walks

**Week:** 01

**Project:** Cybersecurity & Pentesting Lab Setup