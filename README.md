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

## My laptop (host machine) Details
- Processor: Intel Core i5-6200U @ 2.30 GHz
- RAM (Random Access Memory): 8 GB (7.88 GB usable)
- Operating system: Windows 11 Pro
- Storage: C: drive 237 GB, D: drive 476 GB (virtual machines are stored on D:)

## Lab Environment Details
| Item | Setting |
|---|---|
| Virtualization software | VirtualBox 7.2.10 |
| Attacking machine | Kali Linux (VM named KALI 1) |
| Network | NatNetwork, 10.0.0.0/24, DHCP (Dynamic Host Configuration Protocol) enabled |
| Kali IP (Internet Protocol) address | 10.0.0.2/24 |
| Gateway | 10.0.0.1 |
| DNS (Domain Name System) server | 8.8.8.8 |
| Clipboard and drag/drop | Bidirectional |
| Shared folder | Windows Downloads folder, mounted in Kali at /media/sf_Downloads |
| Snapshot | "WK1 - Kali 10.0.0.2 configured" |


## What I did
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

## Verification
- `ip a` shows `10.0.0.2/24` on eth0.
- `ping -c 4 google.com` returned 4 of 4 replies with 0% packet loss, so internet and DNS work.
- `ls /media/sf_Downloads` lists my Windows Downloads files.

## Problems I faced and how I fixed them
1. **Wrong network range.** My NatNetwork was set to 10.0.2.0/24, so Kali got 10.0.2.15 automatically. I changed the IPv4 prefix to 10.0.0.0/24 and set the static address.
2. **CPU (Central Processing Unit) warning.** VirtualBox warned that the VM had more virtual CPUs (3) than my laptop's physical CPUs (2). I lowered it to 2.
3. **Missing settings.** The clipboard options were not under "Advanced" in this VirtualBox version; they are in General > Features. The shared folder option was called "Make Global", not "Make Permanent".
4. **Drag and drop was unreliable.** It worked once, then showed "Can't drop data to guest". I used the shared Downloads folder and shared clipboard instead.

## Screenshots
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


