# 09 — Bash Scripting and Automation

## 1. First script
Create `hello.sh`:
```bash
#!/usr/bin/env bash
set -euo pipefail
name="${1:-Linux learner}"
printf 'Hello, %s!\n' "$name"
```
Run `chmod +x hello.sh`, then `./hello.sh` and `./hello.sh Sumit`.

`set -euo pipefail` helps catch many errors but does not replace validation and error handling.

## 2. Variables and quoting
```bash
service="nginx"
printf 'Service: %s\n' "$service"
```
Quote variable expansions to prevent word splitting and wildcard expansion.

## 3. Conditions
```bash
if [[ -f /etc/os-release ]]; then
  echo "OS metadata found"
else
  echo "OS metadata missing"
fi
```
Common tests: `-f` regular file, `-d` directory, `-r` readable, `-x` executable, `-n` non-empty string.

## 4. Loops
```bash
for file in /var/log/*.log; do
  [[ -e "$file" ]] || continue
  printf '%s\n' "$file"
done
```

## 5. Functions and exit codes
```bash
is_root() {
  [[ "$EUID" -eq 0 ]]
}
if is_root; then echo "root"; else echo "regular user"; fi
```
Exit code 0 conventionally means success; non-zero means failure.

## 6. Scheduling
Edit a user's cron table with `crontab -e`. Example daily schedule:
```cron
30 2 * * * /home/USER/bin/report.sh >> /home/USER/report.log 2>&1
```
Use absolute paths; cron has a limited environment. systemd timers are another scheduling option.

## Lab: disk usage alert (read-only)
```bash
#!/usr/bin/env bash
set -euo pipefail
threshold="${1:-80}"
usage="$(df -P / | awk 'NR==2 {gsub(/%/, "", $5); print $5}')"
if [[ ! "$threshold" =~ ^[0-9]+$ ]] || (( threshold < 1 || threshold > 100 )); then
  echo "Usage: $0 [threshold 1-100]" >&2
  exit 2
fi
printf 'Root filesystem usage: %s%%\n' "$usage"
if (( usage >= threshold )); then
  echo "WARNING: threshold reached"
else
  echo "OK"
fi
```
This reports usage; it does not delete files.

## Exercises
Add a timestamp, accept a mount point, and return a non-zero exit code when the threshold is exceeded.
