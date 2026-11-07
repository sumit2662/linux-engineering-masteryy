# 08 — Storage, Filesystems, and Backup

## 1. Inspect before modifying
```bash
lsblk -f
blkid
findmnt
df -hT
du -sh /var/log
```
`lsblk` lists block devices, `findmnt` shows mounts, `df` reports filesystem capacity, and `du` estimates directory usage.

## 2. Disk concepts
A disk is a block device. A partition table describes partitions. A filesystem organizes data. A mount point attaches a filesystem to the directory tree. Formatting a device destroys existing filesystem structures; never do it without verifying the target and having a backup.

## 3. Common filesystems
ext4, XFS, and Btrfs are common Linux filesystems. Choose based on workload, distribution support, snapshot requirements, and operational policy.

## 4. LVM
- PV: physical volume.
- VG: volume group storage pool.
- LV: logical volume created from a VG.
Inspect with `sudo pvs`, `sudo vgs`, and `sudo lvs`. Do not initialize or format a device unless it is a dedicated disposable lab disk.

## 5. fstab
`/etc/fstab` describes persistent mounts. UUIDs are generally more stable than device names.
```bash
cat /etc/fstab
findmnt --verify
```
A bad fstab entry can affect boot. Take a VM snapshot and keep recovery access before editing it.

## 6. Backup principles
Define scope, frequency, retention, isolation, encryption, and restore testing. A second copy on the same disk is not a resilient backup.

```bash
tar -czf "$HOME/lab-backup.tgz" "$HOME/linux-lab"
tar -tzf "$HOME/lab-backup.tgz" | head
```
Test extraction to a different directory. A backup is not proven until a restore has been tested.
