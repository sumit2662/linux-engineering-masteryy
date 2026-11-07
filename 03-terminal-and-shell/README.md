# 03 — Terminal and Shell Fundamentals

## 1. Command structure
A common command structure is:
```text
command [options] [arguments]
```
Example: `ls -lah /var/log`. `ls` is the command, `-l/-a/-h` are options, and `/var/log` is the argument.

## 2. Navigation
```bash
pwd
ls
ls -lah
cd /etc
cd ..
cd ~
cd -
```
An absolute path starts at `/`. A relative path starts from the current directory. `.` means current directory; `..` means parent directory.

## 3. Help
```bash
man ls
ls --help
type cd
command -v python3
apropos network
```
Press `q` to exit a man page. `type` identifies shell builtins, aliases, functions, and executables.

## 4. Variables and environment
```bash
name="Linux learner"
echo "$name"
printenv PATH
export LAB_NAME="linux-basics"
```
Use quotes around variable expansions to avoid unwanted word splitting and wildcard expansion.

## 5. Pipes and redirection
```bash
echo "first line" > notes.txt
echo "second line" >> notes.txt
cat notes.txt
ls /etc | head
command > output.txt 2> errors.txt
```
`>` overwrites, `>>` appends, `2>` redirects standard error, and `|` sends one command's output to another command.

## 6. Quoting
- Single quotes preserve literal characters: `echo '$HOME'`.
- Double quotes allow variable expansion: `echo "$HOME"`.
- Backslash can escape a special character: `echo \$HOME`.

## Lab
Create a folder, a file, append a second line, count lines with `wc -l`, and pipe a directory listing to `head`.

## Exercises
What is the difference between an absolute and relative path? What is standard error? Why should variables usually be quoted?
