# 05 — Users, Groups, Ownership, and Permissions

## 1. Identity
Linux uses numeric UIDs and GIDs. Names map to these identifiers.
```bash
whoami
id
groups
getent passwd
getent group
```
Important files: `/etc/passwd` (account metadata), `/etc/shadow` (protected password data), and `/etc/group` (groups). Never publish shadow-file contents.

## 2. Create users and groups
Ubuntu/Debian examples:
```bash
sudo adduser trainee
sudo groupadd projectteam
sudo usermod -aG projectteam trainee
id trainee
```
`-aG` appends supplementary groups. Omitting `-a` can replace a user's supplementary group list.

## 3. Read permissions
Example: `-rwxr-x---`
- Owner: read, write, execute.
- Group: read and execute.
- Others: no permissions.

For files, read means read contents; write means modify contents; execute means run as a program. For directories, execute means traverse/search; read means list names; write allows creating/removing entries (with execute).

## 4. Numeric chmod
`r=4`, `w=2`, `x=1`.
- `7` = rwx
- `6` = rw-
- `5` = r-x
- `4` = r--
- `0` = ---

```bash
chmod 640 report.txt
chmod 750 script.sh
chmod u+x script.sh
```
Never use `chmod -R 777` as a generic permission fix.

## 5. Ownership
```bash
sudo chown trainee:projectteam report.txt
sudo chgrp projectteam report.txt
```
Recursive ownership changes can affect many files; inspect paths before using `-R`.

## 6. sudo and ACL
Use `sudo` for specific administrative commands. Edit sudo rules with `sudo visudo`.
ACL example:
```bash
getfacl report.txt
setfacl -m u:trainee:r-- report.txt
getfacl report.txt
setfacl -x u:trainee report.txt
```

## Lab: shared directory
```bash
sudo groupadd projectteam
sudo mkdir -p /srv/project-share
sudo chown root:projectteam /srv/project-share
sudo chmod 2770 /srv/project-share
ls -ld /srv/project-share
```
The setgid bit on a directory helps new entries inherit its group. Test with two non-root lab users. Do this only in a VM.

## Exercises
Create a file with mode 640. Explain why the setgid bit is useful on shared directories. Compare a UID with a username.
