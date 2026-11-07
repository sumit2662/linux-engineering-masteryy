# 11 — Linux for Cybersecurity

## 1. Authorization and scope
Only inspect systems you own or are explicitly authorized to assess. Define scope, time window, allowed methods, and evidence handling before beginning.

## 2. Basic host triage
```bash
date -Is
hostname
uname -a
who
w
last -n 10
ps auxf
ss -tulpen
ip addr
ip route
```
Document the environment and time zone. Even read-only commands can affect shell history or access metadata depending on configuration.

## 3. Logs
Common sources include systemd journal, `/var/log/auth.log` on many Debian/Ubuntu systems, `/var/log/secure` on many RHEL-family systems, and application logs.
```bash
journalctl -u ssh --since today
journalctl -p warning --since today
```
Correlate timestamps and time zones; logs can be incomplete or rotated.

## 4. Hashes
```bash
sha256sum sample.bin
sha256sum sample.bin > sample.sha256
sha256sum -c sample.sha256
```
A hash helps detect whether bytes changed between measurements. It does not prove who created a file or that it is safe.

## 5. Evidence handling
Obtain authorization, document collector/time/location/method, preserve originals, use write-blocking where appropriate, work from verified copies, record tool versions and commands, and secure evidence with access controls.

## 6. Tools
Examples include `auditd`, `ausearch`, `journalctl`, `ss`, `lsof`, `tcpdump`, AIDE, Lynis, and rkhunter. Tool output requires validation and may contain false positives.

## Lab: hash a sample
```bash
mkdir -p ~/evidence-lab
cd ~/evidence-lab
printf 'training evidence\n' > evidence.txt
sha256sum evidence.txt | tee evidence.sha256
sha256sum -c evidence.sha256
```
Expected: `evidence.txt: OK`. Modify the file and repeat to observe a mismatch. This is a training exercise, not forensic acquisition.
