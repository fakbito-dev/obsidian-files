# Bash_Commands

**Domain**:: #CLI
**Expertise**:: `⚡️ Intermediate `
**Last Used**:: 2025-05-31
**Related**:: [[Computer science|computer science]]
**Tags**:: #cheatsheet #reference #bash #shell

```mermaid
graph TD
    U[Bash_Commands] --> C[Core Commands]
    U --> S[Shortcuts & Aliases]
    U --> T[Troubleshooting]
    U --> E[Examples]
    U --> A[Advanced Patterns]
```

## Core Syntax & Operations

```bash
### List directory contents
ls
ls -l      # Detailed list
ls -a      # Show hidden files
ls -lh     # Human-readable sizes

# Create directory
mkdir dirname
mkdir -p parent/child  # Create nested directories

# Copy files
cp file.txt destination/
cp -r dir/ destination/  # Copy directories recursively

# Move/rename files
mv old.txt new.txt

# Delete files/folders
rm file.txt
rm -r dirname  # Delete directory recursively
rm -rf dirname # Force delete (caution!)

# Find files
find . -name "*.log"  # Search by name
grep -r "pattern" /path  # Search content in files

# Create file
touch newfile.txt
```

### **Process Management**

```bash
# List running processes
ps aux
ps aux | grep "processname"

# Monitor processes
top
htop  # Interactive viewer (install separately)

# Kill process
kill 1234         # By PID
killall processname
pkill -f "pattern"
```

### **System Information**

```bash
# System info
uname -a          # Kernel info
df -h             # Disk space
free -h           # Memory usage
lscpu             # CPU information

# Hardware info
lshw              # Detailed hardware (requires install)
dmidecode         # BIOS/hardware info
```

### **Network Tools**

```bash
# Ping test
ping google.com
ping -c 4 8.8.8.8  # Limited packets

# Network configuration
ifconfig          # Deprecated, use 'ip a'
ip a              # Show IP addresses
netstat -tulpn    # Listening ports

# DNS lookup
nslookup google.com
dig google.com

# Download files
wget https://example.com/file
curl -O https://example.com/file
```

### **Package Management**

```bash
# Debian/Ubuntu (apt)
sudo apt update
sudo apt install package
sudo apt remove package

# RedHat/CentOS (yum/dnf)
sudo yum install package
sudo dnf upgrade

# Search packages
apt search pattern
yum search pattern
```

### **User & Permissions**

```bash
# Run as superuser
sudo command

# File permissions
chmod 755 file.sh     # Numeric mode
chmod +x script.sh    # Make executable
chown user:group file # Change ownership

# User management
sudo adduser username
sudo passwd username
```

### **Scripting & Automation**

```bash
# Create executable script
#!/bin/bash           # Shebang line
echo "Hello World!"

# Variables
name="John"
echo "Hello $name"

# Conditional
if [ $age -gt 18 ]; then
    echo "Adult"
fi

# Loops
for i in {1..5}; do
    echo $i
done
```

### **Useful Aliases**

```bash
# Add to ~/.bashrc
alias ll='ls -alF'
alias cls='clear'
alias ..='cd ..'
alias grep='grep --color=auto'
```

### **Powerful Pipeline Examples**

```bash
# Find large files (>100MB)
find . -type f -size +100M

# Count lines in files
wc -l file.txt

# Process text
cat file.txt | sort | uniq -c | sort -nr

# Monitor log files
tail -f /var/log/syslog | grep "error"
```

### **Environment Variables**

```bash
export PATH="$PATH:/my/custom/path"
printenv              # List all variables
echo $HOME            # Show specific variable
```

### **Profile Customization**

```bash
nano ~/.bashrc        # Edit configuration
source ~/.bashrc      # Reload settings
```

## Productivity Shortcuts

```bash
# Navigation
alias ..='cd ..'
alias ...='cd ../..'
alias ll='ls -alF'

# History
!$       # Last argument of previous command
!ssh     # Run last ssh command
ctrl+r   # Search history
```

## Common Patterns

### Basic Usage

```bash
# Find and process files
find . -name "*.log" -exec grep "ERROR" {} \;

# Backup with date stamp
cp file.txt file.txt.bak_$(date +%Y%m%d)
```

### Composite Workflow

```bash
# Analyze log files
grep "ERROR" /var/log/syslog |
awk '{print $6}' |
sort |
uniq -c |
sort -nr > error_report.txt
```

## Debugging Guide

```bash
# Trace script execution
bash -x script.sh

# Check exit codes
echo $?

# Common error:
ERROR: "Permission denied"
FIX: "chmod +x file.sh && ./file.sh"
```

## Real-World Examples

### Development Workflow

```bash
# Build and run project
make clean &&
make all &&
./bin/app --test
```

### Automation Script

```bash
#!/usr/bin/env bash
# Auto-clean temp files older than 30 days
find /tmp -type f -mtime +30 -exec rm {} \;
```

## Advanced Techniques

```bash
# Parallel processing
parallel -j 4 convert {} {.}.png ::: *.jpg

# Process substitution
diff <(sort file1) <(sort file2)
```

## Configuration Snippets

### Minimal Setup

```bash
# ~/.bashrc essentials
export PATH="$PATH:$HOME/bin"
export EDITOR=nano
```

### Optimized Setup

```bash
# Enhanced prompt
PS1='\[\e[1;32m\]\u@\h\[\e[m\]:\[\e[1;34m\]\w\[\e[m\]\$ '
```

## Cross-Tool Integration

```bash
# With Python
python3 -c "import sys; print(sys.argv[1].upper())" "$variable"

# With jq (JSON processing)
curl -s api.example.com/data | jq '.results[].name'
```

## Version-Specific Notes

| Version | Changes            | Compatibility |
| ------- | ------------------ | ------------- |
| 4.x+    | Associative arrays | Linux/macOS   |
| 5.1+    | `EPOCHSECONDS` var | Linux only    |

## Pro Tips

```bash
# Rapid prototyping
debug() { echo "=== DEBUG: $*" >&2; }  # Quick debug function

# Safety nets
set -euo pipefail  # Exit on error/undefined vars
trap "echo 'Error at line $LINENO'" ERR
```

> **Remember**: Always test destructive commands with `echo` first

## Reference Links

1. [Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
2. [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
3. [Bash Hackers Wiki](https://wiki.bash-hackers.org/)
