# 📖 Shell Scripting — Definitions & Examples

> Roadmap: [`../Roadmap/03-Shell-Scripting.md`](../Roadmap/03-Shell-Scripting.md)

### 📚 Reference docs
- [Bash Guide for Beginners (TLDP)](https://tldp.org/LDP/Bash-Beginners-Guide/html/) · [Advanced Bash Scripting Guide](https://tldp.org/LDP/abs/html/)
- [GNU Bash manual](https://www.gnu.org/software/bash/manual/bash.html)
- [Google Shell Style Guide](https://google.github.io/styleguide/shellguide.html)
- [ShellCheck](https://www.shellcheck.net/) (lint your scripts) · [explainshell](https://explainshell.com/)
- [crontab.guru](https://crontab.guru/) (cron syntax) · [awk](https://www.gnu.org/software/gawk/manual/gawk.html) · [sed](https://www.gnu.org/software/sed/manual/sed.html)

---

## Core concepts

**Shebang** — `#!/bin/bash` first line tells the OS which interpreter to use.

**Exit code** 🔥 — `$?` holds the last command's status. `0` = success, non-zero = failure.

**Variable** — `NAME="value"` (no spaces around `=`); use `$NAME` or `${NAME}`.

**Command substitution** — capture output: `now=$(date)`.

**Positional parameters** — `$1 $2` args, `$@` all args, `$#` count, `$0` script name.

**set -euo pipefail** 🔥 (start every prod script with it)
- `-e` exit on any error · `-u` error on undefined variable · `-o pipefail` fail if any piped command fails.

**Test operators** — numeric `-eq -ne -gt -lt -ge -le`; file `-f` (file) `-d` (dir) `-e` (exists); string `-z` (empty) `-n` (non-empty) `==`.

**Redirection** 🔥 — `>` overwrite, `>>` append, `<` input, `2>` stderr, `2>&1` merge stderr→stdout, `/dev/null` discard.

**Pipe** — `|` sends stdout of one command to stdin of the next: `cat log | grep ERROR | wc -l`.

**awk vs sed vs grep** 🔥
- **grep** — search lines matching a pattern.
- **sed** — stream edit / substitute: `sed 's/old/new/g'`.
- **awk** — column/field processing: `awk '{print $1}'` or `awk -F, '{sum+=$2} END{print sum}'`.

**trap** — run cleanup on exit/signal: `trap 'rm -f /tmp/lock' EXIT`.

**Cron** — scheduler; `crontab -e` to edit, `crontab -l` to list. `0 2 * * *` = 2 AM daily.

**$@ vs $*** — both expand all args; quoted `"$@"` keeps each arg separate (correct), `"$*"` joins into one string.

---

## 🔑 Example scripts (be ready to write live)

**Count errors in a log:**
```bash
grep -c "ERROR" /var/log/app.log
# or group by type
awk '/ERROR/ {print $5}' app.log | sort | uniq -c | sort -rn
```

**Disk usage alert:**
```bash
#!/bin/bash
set -euo pipefail
usage=$(df / | awk 'NR==2{print $5}' | tr -d '%')
if [ "$usage" -gt 80 ]; then
  echo "WARNING: disk ${usage}%"
fi
```

**Loop over servers, health check:**
```bash
for host in web1 web2 web3; do
  if curl -sf "http://$host/health" >/dev/null; then
    echo "$host OK"
  else
    echo "$host DOWN"
  fi
done
```

**Backup + timestamp:**
```bash
tar -czf "backup-$(date +%F).tar.gz" /app/data
```

---

## 🎯 Likely interview Qs
- What does `$?` return? What is `set -euo pipefail`?
- Difference between `>` and `>>`; what is `2>&1`?
- awk vs sed vs grep.
- Write a script to: count errors / rotate logs / check disk / backup a dir.
- How do you schedule a script? (cron)
