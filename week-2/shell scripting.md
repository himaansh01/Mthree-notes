# 🔐 Day-10: SSH Key Setup & Jenkins Installation

A walkthrough of setting up SSH for GitHub, essential system/network commands, and installing/configuring Jenkins (with optional Java 17 and Docker integration).

---

## 🔑 1. SSH Key Setup for GitHub Authentication

```bash
ssh-keygen -t ed25519 -C "ranawatjinesh@gmail.com"
# Generates SSH key with email label

eval "$(ssh-agent -s)"
# Starts the SSH agent

ssh-add ~/.ssh/id_ed25519
# Adds private key to agent

cat ~/.ssh/id_ed25519.pub
# Copy this to GitHub → Settings → SSH Keys

ssh -T git@github.com
# Tests SSH connection with GitHub
# Expected: "Hi <username>! You've successfully authenticated..."

git clone git@github.com:jineshranawatcode/c406firstproject.git
# Clone repo via SSH
```

---

## 🛠️ 2. System & Network Commands

```bash
su - jineshtry               # Switch user
lpq                         # Printer queue
dmesg | tail -50            # Kernel log tail (debugging)
dmesg | grep "USB"          # Filter USB logs
iperf -s -f M               # Bandwidth test server (MB/s)
sudo tcpdump -i any         # Capture all network traffic
telnet google.com           # (Deprecated) Port test
dig google.com              # DNS query
```

---

## 🚀 3. Jenkins Setup (Java 11)

### Step 1: Update & Install Java

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```

### Step 2: Add Jenkins Repo (Deprecated method)

```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

### Step 3: Install Jenkins

```bash
sudo apt update
sudo apt install jenkins -y
```

### Step 4: Start Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins   # Check for "active (running)"
```

---

## 🆕 4. Alternative Jenkins Repo (Modern Way)

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

## ☕ 5. Jenkins with Java 17 (LTS)

```bash
sudo apt install fontconfig openjdk-17-jre -y
sudo apt install jenkins -y
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
# Use this password to log in at first Jenkins launch
```

---

## 🐳 6. Docker Access for Jenkins

```bash
sudo usermod -aG docker jenkins   # Add Jenkins to Docker group
sudo systemctl restart jenkins    # Apply permission changes
```

---

## 🌐 7. Access Jenkins Web Interface

- Open your browser: `http://localhost:8080`
- Paste the initial admin password
- Follow the setup wizard
- Install suggested plugins
- Create your first admin user

---

## ✅ Key Takeaways

- **SSH Authentication**: Secure GitHub access using SSH keys  
- **System Monitoring**: `dmesg`, `tcpdump`, `iperf`, `dig` for diagnostics  
- **Jenkins Setup**: Installed via Java 11 and Java 17 methods  
- **Secure Repo Access**: Used modern GPG key and `signed-by=` syntax  
- **Docker Integration**: Enabled Jenkins to run Docker commands  
- **Web UI**: Jenkins is accessible via `http://localhost:8080` for full setup
