# 🔐 Kali Linux Lab Setup and Network Configuration (WK1-PM1)

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-red)
![VirtualBox](https://img.shields.io/badge/VirtualBox-v7.2-blue)
![Kali Linux](https://img.shields.io/badge/OS-Kali_Linux-black)
![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-teal)
![Skill](https://img.shields.io/badge/Skill-Virtualization-red)
![Focus](https://img.shields.io/badge/Focus-Ethical_Hacking-orange)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)

A home cybersecurity testing lab built with VirtualBox and Kali Linux, connected on a private NAT (Network Address Translation) network.

## 📌 Project Overview
This project documents how I set up a cybersecurity practice lab on my own laptop using VirtualBox and Kali Linux, on a private NAT (Network Address Translation) network, and the problems I solved along the way.

The purpose of the lab is to create a safe and controlled environment for cybersecurity tools, hands-on repeated practices such as  network scanning, reconnaissance, vulnerability assessment, and other security-testing activities.

As earlier stated, the lab is configured on a private virtual network, so that additional machines can be added and used later as targets for authorized security testing.

## Objectives
Install and configure VirtualBox
Import  and configure Kali Linux virtual machine (VM).
Create a NAT network on the range 10.0.0.0/24.
Give Kali a fixed IP (Internet Protocol) address: 10.0.0.2/24.
Verify network connectivity for Kali Linux
Turn on the shared clipboard, drag and drop, and a shared Downloads folder.
Confirm that Kali has full internet access.
Take a snapshot so the lab can be restored.

## Purpose of the Lab
A safe, separate environment is needed to practise ethical hacking. This lab lets me test tools on virtual machines without touching my real files or network, and the snapshot lets me undo mistakes quickly.

## ⚙️Lab Environment Configuration
| Component | Details |
|---|---|
| 💻 Host machine | HP Laptop (My Laptop) |
| 🖥️ Host OS (Operating System) | Windows 11 Pro |
| 🧠 Host RAM (Random Access Memory) | 8GB |
| ⚡ Host processor | Intel Core i5 |
| 🧰 Virtualization software | VirtualBox 7.2.10 |
| 🐉 Attacking machine | Kali Linux (VM named KALI 1) |
| 🧠 Kali Linux RAM | 4200 MB |
| ⚡ Kali Linux CPUs (Central Processing Units) | 2 |
| 💿 VM disk | 75.51GB |
| 🌐 Virtual network | NatNetwork, 10.0.0.0/24, DHCP (Dynamic Host Configuration Protocol) enabled |
| 📡 Network address | 10.0.0.0/24 |
| 🐧 Kali Linux IP Address | 10.0.0.2/24 |
| 🚪 Default gateway | 10.0.0.1 |
| 🌍 DNS (Domain Name System) server | 8.8.8.8 |
| 🔌 Network interface | eth0 |
| 🌐 Subnet mask | 255.255.255.0 (/24) |
| 📁 Shared folder | Windows Downloads, mounted in Kali at /media/sf_Downloads |
| 📸 Snapshot | "WK1 - Kali 10.0.0.2 configured" |


## 🪜Lab Setup Procedure (What I did)
1. Installed VirtualBox 7.2.10 on Windows.
2. Imported Kali Linux as a virtual machine.
3. Created the NAT network `NatNetwork` with the range 10.0.0.0/24.
4. Attached the Kali network adapter to NatNetwork and set Promiscuous Mode to Allow All.
5. Turned on Shared Clipboard and Drag'n'Drop (Bidirectional).
6. Shared my Windows Downloads folder with Kali.
7. Set a fixed IP address in Kali with the Network Manager command line tool (nmcli):

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.method manual ipv4.addresses 10.0.0.2/24 ipv4.gateway 10.0.0.1 ipv4.dns 8.8.8.8
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

8. Tested the lab and took a snapshot.


## Commands Used

Check the IP address:

```bash
ip a
```

Set a fixed IP address, gateway and DNS server:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.method manual ipv4.addresses 10.0.0.2/24 ipv4.gateway 10.0.0.1 ipv4.dns 8.8.8.8
```

Turn off the DAD (Duplicate Address Detection) delay:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

Restart the connection so the changes apply:

```bash
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

Test internet access and DNS:

```bash
ping -c 4 google.com
```

Check the shared folder:

```bash
ls /media/sf_Downloads
```

## Verification Results
| Test | Result |
|---|---|
| Kali IP address is 10.0.0.2/24 (ip a) | Successful |
| Internet and DNS (ping -c 4 google.com: 4 of 4 replies, 0% packet loss) | Successful |
| Shared Downloads folder visible in Kali | Successful |
| Shared clipboard between Windows and Kali | Successful |
| Drag and drop | Worked once, then unreliable |
| Snapshot taken | Successful |


## Problems I faced and how I fixed them
1. **Wrong network range.** My NatNetwork was set to 10.0.2.0/24, so Kali got 10.0.2.15 automatically. I changed the IPv4 prefix to 10.0.0.0/24 and set the static address.
2. **CPU (Central Processing Unit) warning.** VirtualBox warned that the VM had more virtual CPUs (3) than my laptop's physical CPUs (2). I lowered it to 2.
3. **Missing settings.** The clipboard options were not under "Advanced" in this VirtualBox version; they are in General > Features. The shared folder option was called "Make Global", not "Make Permanent".
4. **Drag and drop was unreliable.** It worked once, then showed "Can't drop data to guest". I used the shared Downloads folder and shared clipboard instead.

## Lab Evidence Screenshots 
### 1. NAT network set to 10.0.0.0/24
![NAT network](WK.1%20SCREENSHOTS/1-nat-network-10.0.0.0-24.png)

### 2. Kali IP address 10.0.0.2/24
![Kali IP address](WK.1%20SCREENSHOTS/2-kali-ip-10.0.0.2.png)

### 3. Internet check (ping google.com)
![Ping google.com](WK.1%20SCREENSHOTS/3-ping-google.png)

### 4. Shared Downloads folder
![Shared folder](WK.1%20SCREENSHOTS/4-shared-folder-downloads.png)

### 5. Snapshot
![Snapshot](WK.1%20SCREENSHOTS/5-snapshot.png)

### Problem 1: NAT network on the wrong range (10.0.2.0/24)
![Wrong NAT range](WK.1%20SCREENSHOTS/6-problem-wrong-nat-range.png)

### Problem 1: Kali received an automatic address (10.0.2.15)
![Automatic IP address](WK.1%20SCREENSHOTS/7-problem-dynamic-ip-10.0.2.15.png) 

## Author
Clementina Oluchi A.
