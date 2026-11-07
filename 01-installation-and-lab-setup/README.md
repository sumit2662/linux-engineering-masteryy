# 01 — Installation and Lab Setup

## 1. Choose a safe lab
For learning system administration, use a virtual machine rather than your primary operating system. A VM gives you a separate virtual disk and lets you take snapshots before risky experiments.

Suggested baseline:
- Ubuntu Server 24.04 LTS or 22.04 LTS.
- 2 virtual CPU cores.
- 4 GB RAM.
- 25 GB dynamically allocated virtual disk.
- NAT networking for basic internet access.

## 2. Installation concepts
During installation you may choose language, keyboard, hostname, user account, disk layout, network settings, and optional server packages. For a beginner VM, guided use of the VM's empty virtual disk is suitable. Never select a physical disk containing personal data.

## 3. First boot checklist
```bash
whoami
hostnamectl
ip -br addr
df -h
free -h
sudo apt update
```
The update command refreshes package metadata. It does not itself install all available upgrades.

## 4. Install common learning utilities
```bash
sudo apt install -y curl wget git vim nano tree dnsutils net-tools
```
Package names can differ between distributions. `net-tools` provides older utilities such as `ifconfig`; prefer the modern `ip` command for new work.

## 5. Snapshots
Create a VM snapshot before:
- Editing SSH configuration.
- Enabling firewall enforcement.
- Changing partitions or filesystems.
- Changing bootloader or kernel settings.
- Testing account lockout or authentication policies.

## Lab: build your learning environment
1. Install an Ubuntu VM.
2. Create a non-root account with administrative access.
3. Update package metadata.
4. Install `curl`, `git`, and a text editor.
5. Record OS version, kernel, IP address, and disk capacity.

## Troubleshooting
- No internet: check VM network mode, interface state, route, and DNS.
- Cannot use sudo: confirm the account was added to the appropriate admin group and start a new login session.
- Low disk space: inspect `df -h` before deleting anything.
