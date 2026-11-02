# 📖 Linux — Definitions & Examples

> Roadmap: [`../Roadmap/01-Linux.md`](../Roadmap/01-Linux.md)

### 📚 Reference docs
- [Linux Journey](https://linuxjourney.com/) — free structured course (start here)
- [The Linux Command Line (book, free PDF)](https://linuxcommand.org/tlcl.php)
- [Linux man pages](https://man7.org/linux/man-pages/) · [explainshell](https://explainshell.com/) (decode any command)
- [Red Hat / Amazon Linux docs](https://docs.aws.amazon.com/linux/) · [tldr pages](https://tldr.sh/)
- [systemd / systemctl](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html) · [journalctl](https://www.freedesktop.org/software/systemd/man/latest/journalctl.html)

---

## Core concepts

**Filesystem hierarchy** 🔥 — Linux is a single tree from `/`.
- `/etc` config · `/var/log` logs · `/home` users · `/tmp` temp · `/proc` live kernel/process info · `/opt` optional apps · `/bin`,`/usr/bin` binaries.
    Ans: `/usr/bin` = user commands, `/bin` = essential commands for single-user mode. `/usr/local/bin` = local custom binaries.

**Process** 🔥 — a running program with a PID.
- View: `ps aux`, `top`. Kill: `kill <PID>` (SIGTERM, graceful) vs `kill -9 <PID>` (SIGKILL, forced).
- **Zombie** — finished but parent hasn't read exit status. **Orphan** — parent died, adopted by init.

**Permissions** 🔥 — `rwx` for **user / group / other**.
- `chmod 755 file` = `rwxr-xr-x` (owner all, others read+execute).
- `644` = `rw-r--r--`. Math: r=4, w=2, x=1.
- `chmod +x script.sh` makes executable. `chown user:group file` changes owner.

**Standard streams** — stdin(0), stdout(1), stderr(2).
- `cmd > out.txt` redirect stdout · `2>&1` merge stderr into stdout · `>>` append.

**Signal** — software interrupt to a process. SIGTERM(15) graceful, SIGKILL(9) forced (can't be caught), SIGHUP(1) reload.

**Hard link vs symbolic (soft) link** 🔥
- Hard link = another name for the same inode (data); survives original deletion.
- Soft link (`ln -s`) = a pointer/shortcut to a path; breaks if target deleted.

**systemd / systemctl** — init system that manages services.
- `systemctl start|stop|status|restart|enable <svc>`. `enable` = start on boot. `journalctl -u <svc>` = its logs.

**Cron** — time-based scheduler. `0 2 * * * /script.sh` = 2 AM daily. Fields: min hour day month weekday.

---

## 🔑 Troubleshooting recipes (interview gold)
| Symptom | How you diagnose |
|---------|------------------|
| Disk full | `df -h` (which FS) → `du -sh /path/*` (what's big) → clean logs/`/tmp` |
| High CPU | `top` / `ps aux --sort=-%cpu \| head` |
| High memory | `free -m`, `ps aux --sort=-%mem` |
| Service down | `systemctl status x` → `journalctl -u x` |
| Port in use | `ss -tulpn \| grep :8080` |
| Can't reach host | `ping`, `curl -v`, `dig`, check Security Group |

**Example — free up disk:**
```bash
df -h                       # /var at 95%
du -sh /var/log/* | sort -h # app.log = 4G
> /var/log/app.log          # truncate (or logrotate)
```

---

## 🎯 Likely interview Qs (answers above)
- Explain `755` vs `644`. How to make a file executable.
- `kill` vs `kill -9`. What is a zombie process?
- Hard link vs soft link.
- How do you troubleshoot a server with high CPU / full disk?
- How to see what's listening on a port.
