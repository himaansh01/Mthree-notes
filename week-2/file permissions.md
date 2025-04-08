# 🐧 Day-6: Linux Basics – File Management, Permissions, Navigation

---

## 📁 1. Listing & Managing Files

### 🔧 Commands
- `ls -lrt`  
  → Lists files in long format, sorted by modification time (oldest first).

- `rm -rf *`  
  → Deletes **everything** in the current directory.  
  ⚠️ **Use with caution — irreversible!**

- `touch {a..z}.txt`  
  → Creates 26 empty files named `a.txt` to `z.txt`.

- `cp -rf b.txt /mnt/c/`  
  → Forcefully copies `b.txt` to Windows path `/mnt/c/`.

- `cp -rf b.txt /mnt/c/Users/srs33/`  
  → Copies `b.txt` to a specific Windows directory via WSL.

- `cp -rf a /mnt/c/Users/srs33/`  
  → Copies entire folder `a` to Windows location.

- `rm -rf /mnt/c/Users/srs33/a`  
  → Removes the copied directory `a` from Windows path.

---

## 🔐 2. Permissions Management

### 🔧 Commands
- `chmod -R 777 a`  
  → Grants **read/write/execute** to everyone for folder `a`.

- `chmod -R 700 b`  
  → Grants **full access only to owner**, none to others.

- `chmod 720 b`  
  → Sets specific permissions:  
  - Owner: `7` → rwx  
  - Group: `2` → w  
  - Others: `0` → no access

---

## 📂 3. File & Directory Navigation

### 🔧 Commands
- `cd a`  
  → Move into directory `a`.

- `cd ..`  
  → Move one level up.

- `cd /mnt/c/Users/srs33/`  
  → Navigate to a specific Windows directory via WSL.

- `cd`  
  → Go to the home directory (`~`).

---

## 🔍 4. Searching Text in Files

### 🔧 Commands
- `grep -Ril "jinesh"`  
  → Recursively search for **"jinesh"** in current directory files (case-insensitive, filenames only).

- `grep -Ril "jinesh" /mnt/c/Users/srs33/`  
  → Same search inside a specific Windows folder.

- `man grep`  
  → Shows manual/help page for `grep`.

---

## 📜 5. Viewing & Editing Command History

### 🔧 Commands
- `history`  
  → Displays previously executed commands.

- `vi .bash_history`  
  → Opens history file in `vi` for viewing/editing.

---

## 💽 6. Disk Space & File System Info

### 🔧 Command
- `df -h`  
  → Shows disk usage in **human-readable** format (GB/MB/KB).

---

## 📘 7. Manual Pages (Help)

### 🔧 Commands
- `man ls`  
  → Help page for `ls`.

- `man grep`  
  → Help page for `grep`.

---

## ✅ Key Takeaways

| Category             | Commands                                                                 |
|----------------------|--------------------------------------------------------------------------|
| 📁 File Management    | `ls`, `rm`, `touch`, `cp`                                                |
| 🔐 Permissions        | `chmod 777`, `chmod 700`, `chmod 720`                                   |
| 📂 Navigation         | `cd`, `cd ..`, `cd /mnt/...`                                             |
| 🔍 Searching          | `grep -Ril`, `man grep`                                                  |
| 📜 History            | `history`, `vi .bash_history`                                            |
| 💽 Disk Space         | `df -h`                                                                  |
| 📘 Help               | `man <command>`                                                          |

---

```diff
+ Mastered essential Linux commands for file handling, permissions, and log searches!
```
