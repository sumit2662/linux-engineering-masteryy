# 13 — Linux for DevSecOps

## 1. DevSecOps
DevSecOps integrates security checks into software delivery. Checks should be repeatable, actionable, and risk-based. A scanner finding is an input for analysis, not automatic proof of exploitability.

## 2. Secret hygiene
Never commit private SSH keys, cloud access keys, API tokens, passwords, or credential-bearing connection strings. Use the CI platform's protected secret store or an approved secrets manager. Rotate any credential accidentally exposed; deleting it in a later commit does not remove it from Git history.

## 3. Least-privilege CI runners
Use dedicated runner identities, patched runner images, restricted network access, isolated jobs, and narrowly scoped cloud roles. Do not expose production secrets to untrusted pull-request code.

## 4. Scanning
Tools include Trivy, Grype, Syft, and dependency scanners. Pin tool versions according to policy. Example when Trivy is installed:
```bash
trivy fs --scanners vuln,secret,misconfig .
```
Review package, severity, fix version, reachability, runtime exposure, and false-positive context.

## 5. Repository hygiene
```bash
git status
git diff --staged
git grep -n -I -E 'password=|api_key=|secret='
```
This simple search is not a full secret scanner and can miss many patterns. Never add a real secret to test a scanner.

## 6. Pipeline stages
Formatting/linting → tests → dependency scan → secret scan → IaC scan → image scan → artifact publication/provenance → controlled deployment.

Define severity thresholds, exception owners, rationale, and expiry dates.
