# Linux Command Cheatsheet

| Task | Command |
|---|---|
| Current directory | `pwd` |
| List hidden files | `ls -lah` |
| Identify OS | `cat /etc/os-release` |
| Kernel version | `uname -r` |
| Current identity | `id` |
| Search filename | `find /path -name '*.conf'` |
| Search text | `grep -Rni 'pattern' /path` |
| Disk capacity | `df -hT` |
| Directory size | `du -sh /path` |
| Block devices | `lsblk -f` |
| IP addresses | `ip -br addr` |
| Routes | `ip route` |
| Listening sockets | `ss -tulpen` |
| Processes | `ps aux` |
| Memory | `free -h` |
| Service status | `systemctl status SERVICE` |
| Service logs | `journalctl -u SERVICE` |
| Hash file | `sha256sum FILE` |
| Create archive | `tar -czf archive.tgz directory/` |

Always consult `man COMMAND` and verify options on your distribution.
