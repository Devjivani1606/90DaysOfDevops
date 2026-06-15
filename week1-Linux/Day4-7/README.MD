# ⚙️ Linux Administration - Part 2

## Topics Covered

- System Commands
- User & Group Management
- File Permissions
- Package Management
- Compression & Archiving
- File Transfer
- Networking Commands
- GREP, AWK, SED
- Storage & LVM

---

# System Commands

System Info:

```bash
uname -a
```

Uptime:

```bash
uptime
```

Current User:

```bash
whoami
```

Logged In Users:

```bash
who
```

Find Command Location:

```bash
which docker
which python
```

---

# Sudo Commands

Shutdown:

```bash
sudo shutdown now
```

Restart:

```bash
sudo reboot
```

---

# Package Management

Update Packages:

```bash
sudo apt update
```

Upgrade Packages:

```bash
sudo apt upgrade
```

Install Package:

```bash
sudo apt install nginx
```

Remove Package:

```bash
sudo apt remove nginx
```

---

# User Management

View Users:

```bash
cat /etc/passwd
```

Add User:

```bash
sudo useradd devops
```

Set Password:

```bash
sudo passwd devops
```

Switch User:

```bash
su - devops
```

Delete User:

```bash
sudo userdel devops
```

---

# Group Management

View Groups:

```bash
cat /etc/group
```

Create Group:

```bash
sudo groupadd developers
```

Add User To Group:

```bash
sudo gpasswd -a devops developers
```

Delete Group:

```bash
sudo groupdel developers
```

---

# File Permissions

View Permissions:

```bash
ls -l
```

Permission Structure:

```text
-rwxr-xr--
```

Values:

```text
Read    = 4
Write   = 2
Execute = 1
```

Examples:

```bash
chmod 777 file.txt
chmod 755 script.sh
chmod 644 config.txt
```

Ownership:

```bash
chown ubuntu file.txt
chgrp developers file.txt
```

Default Permissions:

```bash
umask
```

---

# Compression & Archiving

ZIP:

```bash
zip -r backup.zip project/
```

Unzip:

```bash
unzip backup.zip
```

Create TAR:

```bash
tar -cvf backup.tar project/
```

Compress TAR:

```bash
tar -czvf backup.tar.gz project/
```

Extract:

```bash
tar -xzvf backup.tar.gz
```

---

# File Transfer

SCP:

```bash
scp file.txt user@server:/path
```

Using Key:

```bash
scp -i key.pem file.txt user@server:/path
```

RSYNC:

```bash
rsync -av source/ destination/
```

---

# Networking Commands

Ping:

```bash
ping google.com
```

IP Information:

```bash
ifconfig
ip addr
```

Connections:

```bash
netstat -tulnp
ss -tulnp
```

DNS Lookup:

```bash
nslookup google.com
```

Route Trace:

```bash
traceroute google.com
```

Domain Info:

```bash
whois google.com
```

Network Scanner:

```bash
nmap 192.168.1.0/24
```

---

# Advanced Commands

## GREP

```bash
grep "ERROR" app.log
grep -i error app.log
```

## AWK

```bash
awk '{print $1}' file.txt
awk '{print $1,$3}' file.txt
```

## SED

```bash
sed 's/error/warning/g' app.log
sed -i 's/error/warning/g' app.log
```

## WATCH

```bash
watch df -h
```

---

# Storage Management

View Disks:

```bash
lsblk
```

---

# LVM Concepts

## Physical Volume

```bash
pvcreate /dev/xvdf
pvs
```

## Volume Group

```bash
vgcreate data-vg /dev/xvdf
```

## Logical Volume

```bash
lvcreate -L 10G -n app-lv data-vg
```

---

# Learning Outcome

✅ Linux Administration

✅ User & Group Management

✅ File Permissions

✅ Package Management

✅ Networking Commands

✅ GREP, AWK, SED

✅ Compression & Archiving

✅ LVM Fundamentals

# Next week challenge is 

- Git-Github basic
- hooks in Git
- Advace topic with Github Action