# 🧠 Day-7: Linux Commands & Shell Scripting

This document covers essential system commands, package management, file operations, networking tools, Git commands, archiving, and shell scripting in Linux.

---

## 📦 1. Basic System & Package Management

```bash
sudo apt update              # Updates package lists
sudo apt install ncal        # Installs ncal tool
ncal                         # Displays calendar in ncal format
ncal 12 2025                 # Calendar for December 2025
cal 2025                     # Calendar for year 2025
cal 1990                     # Calendar for year 1990
```

---

## 🖥️ 2. System Information

```bash
uname -a   # Complete system info
uname -s   # Kernel name only
```

---

## 📂 3. Finding File Locations

```bash
whereis python
whereis java
whereis ls
```

---

## ⚙️ 4. Process Management

```bash
ps aux                   # List all processes
kill -9 <PID>            # Force kill process by PID (e.g. kill -9 119675)
```

---

## 📁 5. File Operations

```bash
ls -lrt                  # List files sorted by time
wc -l name.txt           # Count lines
wc -w name.txt           # Count words
wc -c name.txt           # Count characters
cat name.txt             # Display contents
vi name.txt              # Edit file with vi
```

---

## 🔍 6. Searching Files & Directories

```bash
find -name "*.txt"                       # Find all .txt files
find . -type d                          # Find directories
find . -name "*.tmp" -exec rm {} \;     # Delete all .tmp files
```

---

## 📊 7. System Monitoring

```bash
top                # Real-time process viewer
du -sh *           # Disk usage of directories
ncdu .             # Interactive disk usage viewer (install with sudo apt install ncdu)
```

---

## 🌐 8. Networking Commands

```bash
ip a                          # Network interfaces
grep -Ril "ranawat"           # Search for keyword in files
telnet google.com             # Test connection (if telnet is installed)
dig google.com                # DNS lookup
iperf -s -f M                 # Run iperf in server mode
sudo tcpdump -i any           # Capture traffic on all interfaces
```

---

## 🔧 9. Git Commands

```bash
git pull                             # Pull latest changes
git reset --hard origin/main         # Reset to remote main branch
history | grep git                   # Show past git commands
```

---

## 🗜️ 10. File Compression & Archiving

```bash
tar -cvf etc.tar Invoice-9.pdf       # Archive file
tar -cvf etc1.tar .                  # Archive current directory
tar -xzvf etc1.tar                   # Extract archive
tar -cvf etc12.tar.gz .              # Create compressed archive
tar -xzvf etc12.tar.gz               # Extract .tar.gz
tar -tzvf etc12.tar.gz               # View archive contents
man tar                              # Show tar manual
```

---

## 💡 11. Shell Scripting & Variables

### 🧪 Creating Variables

```bash
namej="jinesh"
echo $namej
```

### 🔗 Concatenating

```bash
var_1="mannaliker"
var_2="himaansh"
echo "$var_1$var_2"
```

### 🚫 Readonly Variable

```bash
readonly var_2
# var_2="newvalue"  # Will throw error
```

### 🕒 Time-based Greeting

```bash
time=$(date +%H)
if [ $time -lt 12 ]; then
  message="Good morning user"
elif [ $time -lt 18 ]; then
  message="Good afternoon user"
else
  message="Good evening user"
fi
echo "$message $time"
```

### ❌ Unset Variables

```bash
unset var_age
echo "Age is after unsetting $var_age"
```

---

## 🔁 12. Loops in Shell Scripting

### 🔄 While Loop

```bash
i=1
while [ $i -lt 5 ]
do
  echo "himaansh"
  i=`expr $i + 1`
done
```

### 🔂 For Loop with Break

```bash
for a in 1 2 3 4 5 6 7 8 9
do
  if [ $a == 5 ]; then
    break
  fi
  echo "Iteration is $a"
done
```

---

## 🧩 13. Aliases

```bash
alias j1="ls -lrt"
j1              # Executes ls -lrt
alias c="clear"
c               # Clears terminal
```

---

## 🧹 14. File & Directory Removal

```bash
find . -name "*.tmp" -exec rm {} \;         # Remove temp files
rmdir [-rf / --ignore-fail-on-non-empty]    # Force delete folders
```

---

## 📚 15. Man Page Searching

```bash
/keyword     # Inside man page, search for term
n            # Jump to next match
```

---

## ✅ Key Takeaways

- **Package Management:** `apt install`, `apt update`
- **System Info:** `uname`, `top`, `ps aux`
- **Processes:** `kill`, `grep`, `find`
- **Networking:** `dig`, `iperf`, `tcpdump`
- **Git:** `git pull`, `git reset`
- **Compression:** `tar` variations
- **Shell Scripting:** Variables, loops, conditionals
- **Aliases:** Quick shortcuts
