# 🚀 Day-11: Jenkins Pipeline – Python Project with Docker

---

## 🛠️ Step-by-Step: Jenkins CI/CD Pipeline for a Python Project

---

### ✅ Step 1: Create Project Directory

```bash
mkdir my_python_project && cd my_python_project
```
Creates and navigates into `my_python_project`.

---

### ✅ Step 2: Initialize Git Repository

```bash
git init
```
Initializes an empty Git repository.

---

### ✅ Step 3: Create `pyproject.toml`

```bash
cat << EOF > pyproject.toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "my_python_project"
version = "0.1.0"
description = "A simple Python app"
authors = [{name="Your Name", email="your@email.com"}]

[project.scripts]
myapp = "my_python_project.main:main"
EOF
```
Defines project configuration and CLI script.

---

### ✅ Step 4: Create Main Python App

```bash
mkdir -p src/my_python_project
cat << EOF > src/my_python_project/main.py
def main():
    print("Hello from my Python project!")

if __name__ == "__main__":
    main()
EOF
```
Creates `main.py` with an entry point.  
⚠️ Common mistake fixed: `__name__` and `__main__`.

---

### ✅ Step 5: Create Basic Test File

```bash
mkdir tests
cat << EOF > tests/test_main.py
import unittest
from io import StringIO
import sys
from my_python_project.main import main

class TestMain(unittest.TestCase):
    def test_output(self):
        captured = StringIO()
        sys.stdout = captured
        main()
        sys.stdout = sys.__stdout__
        self.assertEqual(captured.getvalue().strip(), "Hello from my Python project!")

if __name__ == "__main__":
    unittest.main()
EOF
```
Creates a unit test to validate the main output.  
⚠️ Fixes: `sys.stdout` used correctly, `__name__ == "__main__"`.

---

### ✅ Step 6: Create a Dockerfile

```bash
cat << EOF > Dockerfile
FROM python:3.9-slim
COPY dist/*.whl /app/
RUN pip install /app/*.whl
ENTRYPOINT ["myapp"]
EOF
```
Defines a minimal image with the built `.whl` package.

---

### ✅ Step 7: Create `.gitignore`

```bash
cat << EOF > .gitignore
__pycache__/
*.pyc
*.pyo
*.pyd
dist/
build/
*.egg-info/
venv/
EOF
```
Prevents untracked/compiled files from cluttering the repo.

---

### ✅ Step 8: Build the Python Wheel

```bash
pip install build
python -m build --wheel
```
Generates the `.whl` distribution package.

---

### ✅ Step 9: Commit Initial Project

```bash
git add .
git commit -m "Initial project setup with Python code and Dockerfile"
```

---

### ✅ Step 10: Create Jenkinsfile

```bash
cat << EOF > Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-username/my_python_project.git'
            }
        }

        stage('Build Wheel') {
            steps {
                sh 'pip install build'
                sh 'python -m build --wheel'
            }
        }

        stage('Test') {
            steps {
                sh 'pip install pytest'
                sh 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my_python_project:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker rm -f my_python_project || true'
                sh 'docker run -d --name my_python_project my_python_project:latest'
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Pipeline Failed.'
        }
    }
}
EOF
```

---

### ✅ Step 11: Commit Jenkinsfile

```bash
git add Jenkinsfile
git commit -m "Add Jenkinsfile for CI/CD pipeline"
```

---

### ✅ Step 12: Show Project Structure

```bash
echo "Project structure created:"
ls -R
```

---

## 🔁 Additional Jenkins Pipeline: Repository Cloning

```groovy
pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                cleanWs()
                sh 'echo "Current directory: $PWD"'
                sh 'git clone https://github.com/jineshranawatcode/my_python_project.git'
                sh 'ls -la my_python_project'
            }
        }

        stage('Verify Clone') {
            steps {
                dir('my_python_project') {
                    sh 'ls -la'
                    sh 'git status'
                }
            }
        }
    }
    post {
        success {
            echo "✅ Repository cloned successfully to workspace!"
        }
        failure {
            echo "❌ Failed to clone repository."
        }
    }
}
```

---

## 🧠 Key Takeaways

✅ **Project Initialization**: Python structure, `pyproject.toml`, Dockerfile  
✅ **Testing**: `unittest` & `pytest` used for automation  
✅ **Git & GitHub**: Project tracked with Git and GitHub  
✅ **CI/CD Pipeline**: Jenkins automates build, test, Dockerize, and deploy  
✅ **Docker**: Project containerized using a slim Python image  
✅ **Pipeline Workspace Management**: Jenkins handles workspace and repository clones

---

```diff
+ End-to-end CI/CD pipeline with Python, Docker, and Jenkins successfully set up!
```
