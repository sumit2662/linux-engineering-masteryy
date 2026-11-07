# 15 — Advanced Linux and Portfolio Projects

## 1. Kernel inspection
```bash
uname -r
cat /proc/meminfo | head
cat /proc/loadavg
dmesg --level=err,warn | tail
```
Kernel parameters exposed through `sysctl` can affect system behavior. Do not tune production systems without understanding the parameter, persistence, compatibility, and rollback.

## 2. Performance tools
```bash
top
vmstat 1 5
iostat -xz 1 5
pidstat 1 5
```
`iostat` and `pidstat` are commonly provided by the `sysstat` package. Correlate CPU, memory, I/O, network, and application metrics rather than relying on one number.

## 3. Namespaces and cgroups
Namespaces isolate views of process IDs, mounts, networks, and other resources. Cgroups account for and limit resource use. These mechanisms underpin container technologies.
```bash
lsns
cat /proc/self/cgroup
```

## 4. Capabilities
Linux capabilities divide some traditional root privileges into smaller permissions.
```bash
getcap -r /usr/bin 2>/dev/null | head
```
A capability can still be powerful; inspect why a binary has it before changing anything.

## Portfolio project A — Linux host inventory
Create a read-only script reporting OS, kernel, CPU, memory, storage, interfaces, routes, services, and listening sockets. Redact identifying details in sample output.

## Portfolio project B — Least-privilege shared workspace
Create two lab users, a shared group, a setgid directory, and scoped permissions. Include verification and cleanup.

## Portfolio project C — Service health checker
Accept a service name, report service state and disk usage, validate inputs, return meaningful exit codes, and never restart services automatically.

## Portfolio project D — Linux security baseline
Document updates, users, sudo access, services, ports, firewall, SSH, and log retention. Separate observations from recommendations.

## Portfolio project E — Incident triage runbook
Create a repeatable first-response checklist for service outage or suspicious login activity, including time normalization, evidence integrity, and escalation criteria.

## Project quality checklist
- Objective and architecture.
- Tested OS/version and prerequisites.
- Step-by-step implementation.
- Expected output and verification.
- Security considerations.
- Troubleshooting.
- Cleanup/rollback.
- Redacted evidence.
