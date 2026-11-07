# 02 — Linux Architecture and Boot

## 1. Architecture overview
A Linux system can be viewed as hardware, kernel, system libraries/services, and user applications. Applications use system calls to request kernel services.

## 2. Kernel responsibilities
- Process scheduling: shares CPU time among runnable tasks.
- Memory management: manages virtual memory and physical pages.
- Device drivers: provide interfaces to hardware.
- Filesystem layer: provides a common interface to filesystem implementations.
- Networking: implements sockets, protocol stacks, and routing behavior.

Inspect:
```bash
uname -a
free -h
cat /proc/meminfo | head
lsmod | head
ls -l /dev | head
```

## 3. Boot process
A typical UEFI boot:
1. Firmware initializes hardware.
2. Firmware selects a boot entry.
3. Bootloader loads the Linux kernel and initramfs.
4. Kernel initializes core subsystems and devices.
5. Initramfs helps locate and mount the real root filesystem.
6. PID 1 starts services and system targets.
7. Login services provide console or remote access.

The exact process depends on firmware, bootloader, distribution, and configuration.

## 4. systemd and PID 1
On many modern distributions, systemd is PID 1 and manages services and system targets.
```bash
ps -p 1 -o pid,comm,args
systemctl get-default
systemctl list-units --type=target
systemctl --failed
```

## 5. Important directories
| Directory | Purpose |
|---|---|
| `/` | Root of the directory tree |
| `/etc` | System configuration |
| `/home` | Regular users' home directories |
| `/root` | Root user's home |
| `/var` | Logs, queues, caches, changing data |
| `/tmp` | Temporary files |
| `/usr` | Most user-space programs and shared data |
| `/dev` | Device nodes |
| `/proc` | Process and kernel information |
| `/sys` | Kernel/device interface |
| `/boot` | Kernel and boot-related files |

`/proc` and `/sys` are virtual filesystems exposing kernel information; they are not ordinary collections of files stored on disk.

## Lab: inspect boot and targets
```bash
systemd-analyze time
systemd-analyze blame | head
journalctl -b -p warning
systemctl get-default
```
`systemd-analyze blame` lists startup durations; it does not by itself prove the cause of a slow boot.

## Exercises
Explain firmware, bootloader, kernel, initramfs, and PID 1 in sequence. Identify three paths under `/proc` that provide system information.
