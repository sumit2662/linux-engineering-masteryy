# 06 — Processes, Jobs, and systemd Services

## 1. Processes
A process is a running program instance with a PID. Parent processes can create child processes.
```bash
ps aux
ps -ef
top
pstree -p
pgrep -a ssh
```

## 2. Signals
```bash
kill -l
kill -TERM PID
kill -HUP PID
kill -KILL PID
```
SIGTERM requests graceful termination. SIGHUP behavior depends on the application. SIGKILL cannot be caught and should be a last resort.

## 3. Jobs
Run `sleep 200`, press Ctrl+Z, then use `jobs`, `bg`, and `fg`. `&` starts a command in the background. Use a service manager for long-running system services.

## 4. systemd
```bash
systemctl status ssh
systemctl is-active ssh
systemctl is-enabled ssh
sudo systemctl start ssh
sudo systemctl restart ssh
sudo systemctl enable ssh
```
Service names vary; Ubuntu often uses `ssh`, while other distributions may use `sshd`. `enable` configures startup behavior; it does not necessarily start the service immediately.

## 5. Logs
```bash
journalctl -b
journalctl -u ssh
journalctl -u ssh --since "1 hour ago"
journalctl -p warning
journalctl -f
```

## 6. Resource inspection
```bash
uptime
free -h
df -h
vmstat 1 5
ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head
```
Load average is not the same as CPU percentage; tasks waiting on I/O can contribute.

## Lab
Inspect a non-critical service with `systemctl status`, `systemctl is-active`, and `journalctl -u SERVICE`. Do not stop critical services on a machine you depend on.
