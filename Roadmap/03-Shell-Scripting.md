# 3. SHELL SCRIPTING — Roadmap

> Glue of automation: health checks, deployments, log rotation, backups, cron jobs. Expect a "write a script to…" task.

```
SHELL SCRIPTING (Bash)
│
├── 1. BASICS
│   ├── #!/bin/bash (shebang)
│   ├── chmod +x, ./script.sh
│   ├── echo, printf, comments (#)
│   └── exit codes ($?)
│
├── 2. VARIABLES
│   ├── NAME="value"  (no spaces)
│   ├── $NAME, ${NAME}
│   ├── command substitution — $(date)
│   ├── positional — $1 $2 $@ $# $0
│   └── env vars — export, $PATH
│
├── 3. CONDITIONS
│   ├── if [ "$x" -gt 5 ]; then ... fi
│   ├── test operators — -eq -ne -gt -lt / -z -n / -f -d -e
│   ├── string — ==, !=
│   └── case ... esac
│
├── 4. LOOPS
│   ├── for f in *.log; do ...; done
│   ├── while read line; do ...; done < file
│   ├── until
│   └── break / continue
│
├── 5. FUNCTIONS
│   ├── greet() { echo "hi $1"; }
│   ├── return / local
│   └── reuse + source
│
├── 6. TEXT PROCESSING
│   ├── grep (search)
│   ├── awk (columns: awk '{print $1}')
│   ├── sed (replace: sed 's/a/b/g')
│   ├── cut, sort, uniq, wc, tr
│   └── pipes | and redirection > >> 2>&1
│
├── 7. ROBUSTNESS
│   ├── set -e (exit on error)
│   ├── set -u (undefined var = error)
│   ├── set -o pipefail
│   ├── trap (cleanup on exit)
│   └── logging + error handling
│
└── 8. SCHEDULING
    ├── cron — 0 2 * * * /path/script.sh
    ├── crontab -e / -l
    └── at (one-off)
```

## 🔑 Reflex snippets
```bash
#!/bin/bash
set -euo pipefail

# health check loop
for url in "$@"; do
  if curl -sf "$url" > /dev/null; then
    echo "UP   $url"
  else
    echo "DOWN $url"; exit 1
  fi
done
```

```bash
# delete logs older than 7 days
find /var/log/app -name "*.log" -mtime +7 -delete

# disk alert
usage=$(df / | awk 'NR==2 {print $5}' | tr -d '%')
[ "$usage" -gt 80 ] && echo "Disk > 80%!"
```

## 🎯 Interview focus
- `$?` = exit status of last command (0 = success).
- `set -euo pipefail` — why every production script starts with it.
- Difference between `$@` and `$*`, and quoting `"$@"`.
- `>` overwrite vs `>>` append; `2>&1` redirect stderr.
- awk vs sed vs grep — when each.
- Write: parse a log, count errors, backup a DB, rotate logs.

→ Definitions: [`../Definitions/03-Shell-definitions.md`](../Definitions/03-Shell-definitions.md)
