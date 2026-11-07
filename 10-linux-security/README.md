# 10 — Linux Security and Hardening

## 1. Security principles
Use least privilege, supported software, timely updates, minimal exposed services, secure authentication, logging, tested backups, and documented recovery.

## 2. Inventory
```bash
cat /etc/os-release
uname -r
systemctl --type=service --state=running
ss -tulpen
```

## 3. Updates
Ubuntu/Debian:
```bash
sudo apt update
apt list --upgradable
sudo apt upgrade
```
Review updates and maintenance windows before applying changes to production. Kernel updates may require reboot.

## 4. SSH hardening
Consider key-based authentication, restricted login accounts, no direct root login, updated packages, network restrictions, and monitoring. Do not blindly paste SSH configuration. Validate with `sshd -t` before reload; keep an existing session open while testing a second login.

## 5. Firewall
Inspect current policy first. Before enabling firewall enforcement remotely, allow the management connection. UFW, firewalld, and nftables syntax differs.

## 6. Permissions and secrets
Avoid world-writable configuration, protect private keys, use service accounts, and never commit credentials. Prefer a secrets manager or protected runtime injection.

## 7. Logs
```bash
journalctl -p warning --since today
last
```
Authentication log paths vary: Ubuntu commonly uses `/var/log/auth.log`; RHEL-family systems commonly use `/var/log/secure`.

## Lab: read-only security baseline
Record OS/kernel, running services, listening ports, firewall status, update status, and SSH configuration observations. Do not change remote access settings during this lab.

## Checklist
- Supported release.
- Updates reviewed.
- Unneeded services disabled.
- Firewall documented.
- SSH access tested.
- User and sudo access reviewed.
- Secrets kept outside source control.
- Logs retained.
- Backup restore tested.
