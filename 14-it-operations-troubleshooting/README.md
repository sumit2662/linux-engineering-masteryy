# 14 — IT Operations and Troubleshooting

## 1. Operational method
Confirm impact, scope, start time, and recent changes. Gather evidence before changing configuration. Change one layer at a time and document actions.

## 2. First-response commands
```bash
uptime
free -h
df -hT
df -ih
systemctl --failed
journalctl -p err --since "30 minutes ago"
ss -s
```
`df -ih` checks inode usage; a filesystem can run out of inodes while byte capacity remains.

## 3. Service unavailable runbook
```bash
systemctl status SERVICE
journalctl -u SERVICE --since "15 minutes ago"
ss -lntp
curl -v --max-time 10 http://127.0.0.1:PORT/
df -h
free -h
```
- Inactive service: inspect logs and configuration.
- No listener: inspect application bind address and startup.
- Local request fails: inspect application and dependencies.
- Local works but remote fails: inspect firewall, routing, proxy, and DNS.

## 4. Incident notes
Record symptom, business impact, affected host/service, first observed time and timezone, recent changes, commands and results, actions, owner, and next update.

## 5. Escalation
Escalate with exact error messages, timestamps, scope, logs (redacted), recent changes, and tests already performed. Avoid speculative root-cause claims.
