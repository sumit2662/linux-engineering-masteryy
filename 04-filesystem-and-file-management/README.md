# 04 — Filesystem and File Management

## 1. Create and manage files
```bash
mkdir -p ~/linux-lab/{input,output,archive}
touch ~/linux-lab/input/notes.txt
cp ~/linux-lab/input/notes.txt ~/linux-lab/output/
mv ~/linux-lab/output/notes.txt ~/linux-lab/archive/notes-old.txt
```
`mkdir -p` creates missing parent directories. `cp` copies; `mv` moves or renames.

## 2. Read files
```bash
cat /etc/os-release
less /var/log/syslog
head -n 10 /etc/passwd
tail -n 20 /var/log/syslog
```
Some distributions use different log paths. `less` is useful for large files.

## 3. Search
```bash
find ~/linux-lab -type f
find /etc -name "*.conf" 2>/dev/null
grep -in "error" sample.log
grep -Rni "Listen" /etc 2>/dev/null | head
```
`find` searches filesystem entries; `grep` searches file contents.

## 4. File types and metadata
```bash
file /etc/passwd
stat /etc/passwd
ls -l
```
The first character in `ls -l` indicates file type: `-` regular file, `d` directory, `l` symbolic link.

## 5. Hard links and symbolic links
```bash
echo "training" > original.txt
ln original.txt hard-link.txt
ln -s original.txt symbolic-link.txt
ls -li
```
A hard link references the same inode. A symbolic link stores a path and may become dangling if its target disappears.

## 6. Archive and compression
```bash
tar -czf lab-backup.tar.gz ~/linux-lab
tar -tzf lab-backup.tar.gz
mkdir -p /tmp/lab-restore
tar -xzf lab-backup.tar.gz -C /tmp/lab-restore
```
Check archive contents before extracting. Avoid extracting untrusted archives as root.

## Exercises
Create a symlink, identify it with `ls -l`, inspect a file with `stat`, and archive a test directory.
