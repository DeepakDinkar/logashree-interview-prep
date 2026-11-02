# 1. LINUX — Roadmap

> Every DevOps task runs on Linux. Containers are Linux. Know the filesystem, processes, permissions, networking and logs cold.

```
LINUX
│
├── 1. FILESYSTEM
│   ├── / (root)  /etc (config)  /var/log (logs)  /home  /tmp  /proc  /opt
│   ├── Paths — absolute vs relative
│   └── Navigation — cd, ls, pwd, find, locate
│
├── 2. FILES & TEXT
│   ├── View — cat, less, head, tail -f
│   ├── Edit — vi/vim, nano
│   ├── Search — grep, egrep, awk, sed
│   └── Manage — cp, mv, rm, touch, mkdir, ln -s
│
├── 3. PROCESSES
│   ├── View — ps aux, top, htop
│   ├── Control — kill, kill -9, nohup, &
│   ├── Jobs — bg, fg, jobs
│   └── Systemd — systemctl start/stop/status/enable, journalctl
│
├── 4. PERMISSIONS & USERS
│   ├── rwx — user / group / other
│   ├── chmod (755, 644), chown, chgrp
│   ├── sudo / su, /etc/passwd, /etc/sudoers
│   └── umask
│
├── 5. NETWORKING
│   ├── curl, wget — HTTP
│   ├── ss / netstat — ports
│   ├── ping, traceroute, dig, nslookup — DNS/reachability
│   ├── ssh, scp, rsync — remote
│   └── iptables / firewalld — firewall basics
│
├── 6. PACKAGES
│   ├── Debian/Ubuntu — apt, dpkg
│   ├── RHEL/Amazon Linux — yum, dnf, rpm
│   └── Services — enable on boot
│
├── 7. LOGS & MONITORING
│   ├── /var/log/* (syslog, messages, auth.log)
│   ├── journalctl -u <service>
│   ├── tail -f, grep, less
│   └── disk/mem — df -h, du -sh, free -m, top
│
└── 8. DISK & STORAGE
    ├── df, du, lsblk, mount
    ├── fstab — persistent mounts
    └── EBS volumes on EC2 (attach, mkfs, mount)
```

## 🔑 Must-know commands (interview reflex)
| Task | Command |
|------|---------|
| Follow a live log | `tail -f /var/log/app.log` |
| Find text in files | `grep -r "ERROR" /var/log` |
| Top CPU/mem processes | `top` / `ps aux --sort=-%mem \| head` |
| Kill a process | `kill -9 <PID>` |
| Disk usage | `df -h` (filesystem) · `du -sh *` (folder) |
| Open ports | `ss -tulpn` |
| Change permission | `chmod 755 script.sh` |
| Make file executable | `chmod +x script.sh` |
| Find big files | `find / -size +100M` |
| Count lines | `wc -l file` |
| Replace text in file | `sed -i 's/old/new/g' file` |

## 🎯 Interview focus
- Permissions math: `755 = rwxr-xr-x`, `644 = rw-r--r--`.
- `kill` (SIGTERM, graceful) vs `kill -9` (SIGKILL, forced).
- Hard link vs soft/symbolic link.
- How to troubleshoot "disk full", "high CPU", "service won't start".
- Linux signals, zombie/orphan processes.

→ Definitions: [`../Definitions/01-Linux-definitions.md`](../Definitions/01-Linux-definitions.md)
