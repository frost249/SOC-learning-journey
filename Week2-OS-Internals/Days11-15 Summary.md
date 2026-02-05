# Week 2 Progress: Days 11–15 Summary

Period: February 1–5, 2026  
Total Hours: ~13 hours  
Status: Complete (needs more practice)

---

## What I Accomplished

## Linux Command Line Mastery

### Skills Acquired
- Navigate Linux filesystem efficiently
- Understand file permissions and ownership
- Analyze authentication logs
- Parse logs using grep and awk
- Created basic Bash scripts for security monitoring

### Commands Practiced
```bash
# Navigation & File Operations
cd /var/log
ls -lah
cat /var/log/auth.log
tail -f /var/log/syslog

# Log Analysis
grep "Failed password" /var/log/auth.log
grep "Failed" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c

# File Permissions
chmod 755 script.sh
chown user:group file.txt

# Process & Network
ps aux
netstat -tulpn
```

### Logs Analyzed
- /var/log/auth.log  → Authentication events (SSH, sudo)
- /var/log/syslog   → System logs
- /var/log/kern.log → Kernel messages

---

## Bash Scripts Created

### Script 1: failed_logins.sh
```bash
#!/bin/bash
# Count failed SSH login attempts

echo "Failed SSH Login Report"
echo "======================="
grep "Failed password" /var/log/auth.log | \
  awk '{print $(NF-3)}' | \
  sort | uniq -c | sort -rn
```

### Script 2: port_scanner_detector.sh
```bash
#!/bin/bash
# Template 2: Port Scan Detector

echo "=== Port Scan Detection ==="

# Check for multiple connection attempts from same IP
netstat -tuln | grep ESTABLISHED | \
  awk '{print $5}' | \
  cut -d: -f1 | \
  sort | uniq -c | sort -rn | \
  awk '$1 > 5 {print "Possible scan from: " $2 " (" $1 " connections)"}'
```

---

## Network Scanning (Nmap Basics)

### Skills Practiced
- Basic host and service scanning
- Understanding open vs closed ports
- Observing scan behavior and scan limitations

### Commands Executed
```bash
# Basic scan
nmap scanme.nmap.org

# Service/version scan
nmap -sV scanme.nmap.org

# TCP SYN scan
nmap -sS scanme.nmap.org

# Scan localhost
nmap 127.0.0.1
```

### Observations
- Identified common open ports such as:
  - 22/tcp (SSH)
  - 80/tcp (HTTP)
  - 443/tcp (HTTPS)
- Observed filtered ports and timeouts
- Encountered retransmission cap warnings:
  - Learned this can occur due to rate limiting, firewalls, or IDS/IPS

---

## OverTheWire Bandit
- Completed Levels 0–12
- Topics reinforced:
  - SSH
  - File permissions
  - Hidden files
  - grep and find

---

## Windows Event Log Analysis

### Skills Acquired
- Navigate Event Viewer efficiently
- Understand critical Windows Event IDs
- Filter logs for specific security events
- Identify brute-force login attempts
- Understand process creation auditing

### Critical Event IDs Practiced

| Event ID | Log      | Meaning                     | SOC Use Case              |
|--------|----------|-----------------------------|---------------------------|
| 4624   | Security | Successful logon            | Track user access         |
| 4625   | Security | Failed logon                | Detect brute force        |
| 4688   | Security | Process created             | Process visibility        |
| 4672   | Security | Special privileges assigned | Privileged access         |
| 4720   | Security | User account created        | Account monitoring        |
| 4726   | Security | User account deleted        | Account removal           |
| 7036   | System   | Service state change        | Service monitoring        |

---

### Logon Types Understood
- Type 2  → Interactive
- Type 3  → Network
- Type 5  → Service
- Type 10 → Remote Desktop (RDP)
- Type 11 → Cached credentials

---

## Hands-On Experiments

### Failed Login Detection
- Generated multiple failed logons
- Identified Event ID 4625 in Security log
- Reviewed failure reason, source IP, and logon type
- Screenshot captured

### Process Creation Auditing
```cmd
auditpol /set /subcategory:"Process Creation" /success:enable
```
- Launched Calculator, Notepad, and Opera
- Observed Event ID 4688
- Identified parent-child process relationships

### User Account Management
```cmd
net user testuser Password123! /add
net user testuser /delete
```
- Observed Event IDs 4720 and 4726

---

## Network Commands Practiced
```cmd
ipconfig /all
netstat -ano
netstat -ano | find "ESTABLISHED"
netstat -ano | find "LISTENING"
```

---

## Challenges Faced

### Windows Process Auditing
- Event 4688 disabled by default
- Enabled using auditpol
- Created reference table for Event IDs

### Bash Scripting
- awk and piping initially confusing
- Improved by breaking commands into parts

---

## Key Learnings

### Brute Force Detection

#### Linux
```bash
grep "Failed password" /var/log/auth.log | \
awk '{print $(NF-3)}' | sort | uniq -c | \
awk '$1 >= 5 {print $2}'
```

#### Windows
- Filter Event ID 4625
- Look for repeated failures from same source
- Check for successful 4624 following failures

---

## Comparison: Linux vs Windows

| Aspect        | Linux              | Windows            |
|--------------|--------------------|--------------------|
| Log Location | /var/log           | Event Viewer       |
| Analysis     | grep, awk          | Log filtering      |
| Processes    | ps aux, top, htop        | Task Manager       |
| Services     | systemctl          | services.msc      |

---

## What’s Working
- Hands-on practice with real systems
- Screenshot-based documentation
- Breaking concepts into smaller tasks
- Gamified learning via Bandit

---

## What Needs Improvement
- Increase daily study hours
- More practice correlating logs
- Build a basic detection reference list
- Comprehensive understanding of logs

---

Date Documented: February 5, 2026  
Next Update: Week 3 – Splunk installation and log aggregation
