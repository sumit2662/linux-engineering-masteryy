# 00 — Linux from Zero

## 1. What is an operating system?
An operating system manages hardware and provides services to applications. It coordinates CPU time, memory, storage, devices, users, and networking. Examples include Windows, macOS, and Linux distributions.

## 2. What is Linux?
Linux is technically the **kernel**. The kernel is the core software that manages hardware and provides services to programs. A Linux distribution combines the kernel with utilities, libraries, package management, an init system, and applications.

Examples of distributions:
- Ubuntu and Debian: widely used on servers and desktops.
- Fedora: fast-moving community distribution.
- Rocky Linux and AlmaLinux: enterprise-oriented RHEL-compatible systems.
- Arch Linux: user-controlled rolling-release distribution.

## 3. Kernel vs shell vs terminal
- **Kernel:** manages CPU, memory, devices, processes, filesystems, and networking.
- **Shell:** interprets commands; Bash and Zsh are examples.
- **Terminal emulator:** application that displays a text session and accepts keyboard input.
- **Distribution:** complete operating system assembled around the Linux kernel.

## 4. Why engineers use Linux
Linux is common in cloud servers, containers, web hosting, networking, embedded systems, and security appliances. It offers automation, remote administration, visibility into system behavior, and a large ecosystem of tools.

## 5. Open source basics
Open source software makes source code available under a license that grants defined rights to use, study, modify, and redistribute it. Open source does not mean that every project is automatically secure or maintained. Check project activity, release history, maintainers, and security advisories.

## 6. First commands
```bash
whoami       # current username
pwd          # current working directory
uname -r     # running kernel release
uname -m     # machine architecture
date         # system date and time
uptime       # time since boot and load averages
```

## 7. Identify the distribution
```bash
cat /etc/os-release
hostnamectl
```
`/etc/os-release` provides standard distribution identification fields. `hostnamectl` is available on many systemd-based systems.

## Lab: your first Linux session
1. Open a Linux terminal.
2. Run `whoami`, `pwd`, `uname -r`, and `cat /etc/os-release`.
3. Write down your distribution, version, kernel, architecture, and username.
4. Explain the difference between the terminal, shell, and kernel.

## Exercises
1. Is Ubuntu a kernel or a distribution?
2. What does the kernel manage?
3. Name two Linux distributions used on servers.
4. Why is open source not automatically the same as secure?

## Answers
1. Ubuntu is a Linux distribution.
2. Hardware resources and core operating-system services.
3. Examples: Ubuntu Server, Debian, Rocky Linux.
4. Security also depends on code quality, maintenance, configuration, and timely updates.
