# Linux Cheatsheet

## File Operations

```bash
# List files
ls
ls -l  # Long format
ls -la  # Include hidden files
ls -lh  # Human readable sizes
ls -lt  # Sort by time

# Change directory
cd <directory>
cd ~  # Home directory
cd -  # Previous directory
cd ..  # Parent directory

# Print working directory
pwd

# Create directory
mkdir <directory>
mkdir -p path/to/directory  # Create parent directories

# Remove directory
rmdir <directory>
rm -r <directory>  # Recursive
rm -rf <directory>  # Force recursive

# Copy file/directory
cp <source> <destination>
cp -r <source> <destination>  # Recursive
cp -p <source> <destination>  # Preserve attributes

# Move/rename
mv <source> <destination>

# Remove file
rm <file>
rm -f <file>  # Force
rm -i <file>  # Interactive

# Create file
touch <file>

# View file
cat <file>
less <file>
more <file>
head <file>  # First 10 lines
head -n 20 <file>  # First 20 lines
tail <file>  # Last 10 lines
tail -f <file>  # Follow file
tail -n 20 <file>  # Last 20 lines
```

## File Permissions

```bash
# Change permissions
chmod 755 <file>
chmod +x <file>  # Add execute
chmod -x <file>  # Remove execute
chmod u+x <file>  # User execute
chmod g+w <file>  # Group write
chmod o+r <file>  # Others read

# Change ownership
chown user:group <file>
chown -R user:group <directory>  # Recursive

# Change group
chgrp <group> <file>
```

## Text Processing

```bash
# Search in file
grep <pattern> <file>
grep -r <pattern> <directory>  # Recursive
grep -i <pattern> <file>  # Case insensitive
grep -n <pattern> <file>  # Show line numbers
grep -v <pattern> <file>  # Invert match

# Find files
find <directory> -name "<pattern>"
find . -type f -name "*.txt"
find . -type d -name "dir*"
find . -size +100M
find . -mtime -7  # Modified in last 7 days

# Sort
sort <file>
sort -r <file>  # Reverse
sort -n <file>  # Numeric
sort -u <file>  # Unique

# Count lines/words/characters
wc <file>
wc -l <file>  # Lines only
wc -w <file>  # Words only
wc -c <file>  # Characters only

# Unique lines
uniq <file>
sort <file> | uniq

# Cut columns
cut -d',' -f1,3 <file>  # Comma delimiter, fields 1 and 3
cut -f1-3 <file>  # Tab delimiter, fields 1-3

# Replace text
sed 's/old/new/g' <file>
sed -i 's/old/new/g' <file>  # In-place edit

# Stream editor
awk '{print $1}' <file>  # Print first column
awk -F',' '{print $1}' <file>  # Comma delimiter
```

## Process Management

```bash
# List processes
ps
ps aux  # All processes
ps -ef  # Full format
ps aux | grep <process>

# Process tree
pstree

# Top processes
top
htop  # If installed

# Kill process
kill <pid>
kill -9 <pid>  # Force kill
killall <process-name>

# Background process
<command> &
nohup <command> &  # No hangup

# Jobs
jobs
fg %1  # Bring to foreground
bg %1  # Send to background

# Find process by name
pgrep <process-name>
pidof <process-name>
```

## System Information

```bash
# System info
uname -a
hostname
uptime

# Disk usage
df -h
du -h <directory>
du -sh <directory>  # Summary

# Memory usage
free -h
cat /proc/meminfo

# CPU info
lscpu
cat /proc/cpuinfo

# Network
ifconfig
ip addr
netstat -tulpn
ss -tulpn
```

## Network Commands

```bash
# Ping
ping <host>
ping -c 4 <host>  # 4 packets

# DNS lookup
nslookup <domain>
dig <domain>
host <domain>

# Download file
wget <url>
curl <url>
curl -O <url>  # Save as file
curl -L <url>  # Follow redirects

# SSH
ssh user@host
ssh -p <port> user@host
ssh -i <key-file> user@host

# SCP
scp <file> user@host:/path
scp -r <directory> user@host:/path
scp user@host:/path/file ./

# Port forwarding
ssh -L <local-port>:<remote-host>:<remote-port> user@host
```

## Archive and Compression

```bash
# Tar
tar -cf archive.tar <files>  # Create
tar -xf archive.tar  # Extract
tar -czf archive.tar.gz <files>  # Compress with gzip
tar -xzf archive.tar.gz  # Extract gzip
tar -cjf archive.tar.bz2 <files>  # Compress with bzip2
tar -xjf archive.tar.bz2  # Extract bzip2

# Zip
zip archive.zip <files>
unzip archive.zip

# Gzip
gzip <file>
gunzip <file>.gz

# Bzip2
bzip2 <file>
bunzip2 <file>.bz2
```

## Environment Variables

```bash
# Set variable
export VAR=value

# View variable
echo $VAR
env | grep VAR

# List all variables
env
printenv

# Add to PATH
export PATH=$PATH:/new/path

# Persistent (add to ~/.bashrc or ~/.zshrc)
export VAR=value
```

## Package Management

```bash
# Debian/Ubuntu (apt)
apt update
apt upgrade
apt install <package>
apt remove <package>
apt search <package>
apt list --installed

# RedHat/CentOS (yum)
yum update
yum install <package>
yum remove <package>
yum search <package>
yum list installed

# RedHat/CentOS (dnf)
dnf update
dnf install <package>
dnf remove <package>
dnf search <package>

# Arch Linux (pacman)
pacman -Syu  # Update system
pacman -S <package>
pacman -R <package>
pacman -Ss <package>  # Search
```

## Useful Commands

```bash
# History
history
history | grep <command>
!<number>  # Execute history number
!!  # Last command
!$  # Last argument

# Alias
alias ll='ls -la'
alias la='ls -A'
alias ..='cd ..'
unalias <alias-name>

# Symbolic link
ln -s <target> <link-name>

# Compare files
diff <file1> <file2>
cmp <file1> <file2>

# Checksum
md5sum <file>
sha256sum <file>

# Date and time
date
date +"%Y-%m-%d %H:%M:%S"

# Clear screen
clear
Ctrl+L

# Exit
exit
logout
```

## System Administration

```bash
# Run as root
sudo <command>
su -  # Switch user

# Service management (systemd)
systemctl start <service>
systemctl stop <service>
systemctl restart <service>
systemctl status <service>
systemctl enable <service>
systemctl disable <service>
systemctl list-units --type=service

# Service management (sysvinit)
service <service> start
service <service> stop
service <service> restart
service <service> status

# Cron
crontab -e  # Edit crontab
crontab -l  # List crontab
crontab -r  # Remove crontab

# Logs
journalctl  # systemd logs
journalctl -u <service>
journalctl -f  # Follow
tail -f /var/log/syslog
```
