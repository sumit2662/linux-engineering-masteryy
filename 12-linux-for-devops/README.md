# 12 — Linux for DevOps

## 1. Linux in delivery systems
Linux hosts build agents, applications, databases, reverse proxies, containers, and monitoring tools. Reliable operation requires repeatable provisioning, version control, observability, and rollback.

## 2. Package and service workflow
```bash
sudo apt update
sudo apt install nginx
systemctl status nginx
curl -I http://127.0.0.1
ss -lntp
```
Use a disposable VM and record the package version and service state.

## 3. Git basics
```bash
git init
git status
git add README.md
git diff --staged
git commit -m "Document Linux service"
git log --oneline
```
Use `.gitignore`; inspect staged changes before committing. Never commit secrets.

## 4. Containers
A container packages an application and dependencies while sharing the host kernel. It is not a full VM. Namespaces isolate resource views; cgroups account for and limit resources.

If Docker is installed:
```bash
docker version
docker ps
docker images
docker logs CONTAINER
```
Docker daemon access is highly privileged. Do not expose its socket or mount sensitive host paths into untrusted containers.

## 5. Deployment checklist
1. Identify artifact version.
2. Verify provenance/checksum/signature where available.
3. Review configuration and secret injection.
4. Deploy to test.
5. Run health checks.
6. Monitor logs and metrics.
7. Roll back when defined health criteria fail.

## Lab
Install Nginx on a disposable Ubuntu VM, verify service state, check the listening socket, request localhost, and record the HTTP status.
