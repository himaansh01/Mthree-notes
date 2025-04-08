# 🐧 Day-9: Linux Commands & Ollama Setup

---

## 📅 Extracting Date & Time from Logs with `grep`

### Task: Extract timestamps where **"Database connection lost"** appears

#### 🔧 Command:
```bash
grep "Database connection lost" logfile.txt | grep -oP '^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2}'
```

#### 🧠 Explanation:
- `grep "Database connection lost"`: Filters lines containing the specific error.
- `grep -oP '^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2}'`: Extracts date and time using Perl-compatible regex.

#### 🧪 Example:
**logfile.txt**
```
2024-02-01 08:10:14 ERROR [app-server-1] Database connection lost
2024-02-01 08:30:22 ERROR [app-server-2] Database connection lost
```

**Output**
```yaml
2024-02-01 08:10:14
2024-02-01 08:30:22
```

---

## ⚠️ Extracting "WARN" Timestamps from Logs

#### 🔧 Command:
```bash
grep "WARN" logfile.txt | grep -oP '^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2}'
```

#### 🧪 Example:
**logfile.txt**
```
2024-02-01 08:30:22 WARN [app-server-2] High memory usage detected
2024-02-01 09:15:45 WARN [app-server-3] Disk space low
```

**Output**
```yaml
2024-02-01 08:30:22
2024-02-01 09:15:45
```

#### 💡 Alternative (Single Command using Lookahead):
```bash
grep -oP '^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2}(?=.*WARN)' logfile.txt
```

---

## 📊 Filtering Logs by CPU & Memory Usage using `awk`

#### 🔧 Command:
```bash
awk -F'[:,%]+' '$2 ~ /CPU Usage/ && $3 > 70 && $5 ~ /Memory Usage/ && $6 > 80' logfile.txt
```

#### 🧠 Explanation:
- `-F '[:,%]+'`: Splits on colon `:` or percent `%`.
- `$3 > 70`: CPU usage threshold.
- `$6 > 80`: Memory usage threshold.

#### 🧪 Example:
**logfile.txt**
```
2024-02-01 10:15:30 INFO CPU Usage: 72%, Memory Usage: 85%
2024-02-01 10:16:30 INFO CPU Usage: 68%, Memory Usage: 82%
2024-02-01 10:17:30 INFO CPU Usage: 75%, Memory Usage: 79%
2024-02-01 10:18:30 INFO CPU Usage: 80%, Memory Usage: 90%
```

**Output**
```
2024-02-01 10:15:30 INFO CPU Usage: 72%, Memory Usage: 85%
2024-02-01 10:18:30 INFO CPU Usage: 80%, Memory Usage: 90%
```

#### 💡 Alternative using `grep` + `awk`:
```bash
grep "CPU Usage" logfile.txt | grep "Memory Usage" | awk -F'[:,%]+' '$3 > 70 && $6 > 80'
```

---

## 🤖 Using Ollama in VS Code

### 1️⃣ Install Ollama
- **macOS/Linux**:
  ```bash
  curl -fsSL https://ollama.com/install.sh | sh
  ```
- **Windows**: Download from [ollama.com](https://ollama.com)

---

### 2️⃣ Verify Installation
```bash
ollama list
```

---

### 3️⃣ Start Ollama Server
```bash
ollama serve
```

---

### 4️⃣ VS Code Extensions
- ✅ REST Client
- ✅ Python extension

---

### 5️⃣ Test Ollama in Terminal
```bash
ollama run mistral
```

> Replace `"mistral"` with any installed model.

---

### 6️⃣ Use Ollama in a Python Script
**ollama_test.py**
```python
import requests

response = requests.post("http://localhost:11434/api/generate", json={
  "model": "mistral",
  "prompt": "Hello, Ollama!"
})
print(response.json()["response"])
```

```bash
python ollama_test.py
```

---

### 7️⃣ Use Ollama in Jupyter Notebook (VS Code)

- Install Jupyter:
  ```bash
  pip install jupyter
  ```

- Use inside `.ipynb`:
  ```python
  !curl -X POST http://localhost:11434/api/generate -d '{"model": "mistral", "prompt": "Explain AI"}'
  ```

---

## ✅ Summary

- Extracted **specific logs** using `grep -oP` with Perl regex
- Filtered system usage logs using **`awk`** and **`grep`**
- Set up and connected **Ollama LLM** in **VS Code** with Python + REST

---

```diff
+ Learning Progress: Efficient log parsing, system resource monitoring, and LLM integration!
```
