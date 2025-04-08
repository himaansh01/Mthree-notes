# 🚀 Jenkins CI/CD Pipeline for Python & Docker Deployment

## 1. Overview

This project demonstrates how to automate the **build**, **test**, and **deployment** of a Python application using **Jenkins** and **Docker**. The CI/CD pipeline performs the following tasks:

- Clones the project from GitHub
- Sets up a Python virtual environment
- Builds the project into a Python wheel package
- Runs unit tests using `pytest`
- Builds a Docker image from the package
- Deploys the application as a container

---

## 2. Project Structure

```
my_python_project/
├── Dockerfile
├── Jenkinsfile
├── pyproject.toml
├── .gitignore
├── dist/
│   └── my_python_project-0.1.0-py2.py3-none-any.whl
├── src/
│   └── my_python_project/
│       └── main.py
└── tests/
    └── test_main.py
```

- `src/my_python_project/main.py` → Main Python application logic  
- `tests/test_main.py` → Unit tests  
- `Dockerfile` → Defines how the Docker image is built  
- `Jenkinsfile` → Jenkins pipeline configuration  
- `pyproject.toml` → Python project metadata  
- `dist/` → Contains the generated `.whl` package  

---

## 3. File Breakdown

### 3.1 `src/my_python_project/main.py`

```python
import time

def main():
    print("Hello from Jenkins CI/CD Pipeline!")
    while True:
        time.sleep(1)

if __name__ == "__main__":
    main()
```

---

### 3.2 `tests/test_main.py`

```python
import unittest
from my_python_project.main import main
import io
import sys

class TestMain(unittest.TestCase):
    def test_main(self):
        captured_output = io.StringIO()
        sys.stdout = captured_output
        main()
        sys.stdout = sys.__stdout__
        self.assertEqual(captured_output.getvalue().strip(), "Hello from Jenkins CI/CD Pipeline!")

if __name__ == "__main__":
    unittest.main()
```

---

### 3.3 `Dockerfile`

```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY dist/*.whl ./
RUN pip install *.whl

CMD ["python", "-m", "my_python_project.main"]
```

---

### 3.4 `Jenkinsfile`

```groovy
pipeline {
    agent any

    environment {
        REPO_URL = "git@github.com:Tamanna247/my_python_project.git"
        WORKDIR = "${WORKSPACE}/my_python_project"
        VENV_PATH = "${WORKSPACE}/venv"
        DOCKER_IMAGE = "my-python-app:latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                cleanWs()
                sh '''
                    echo "Current directory: $PWD"
                    if [ -d "$WORKDIR" ]; then
                        echo "Directory already exists, removing it"
                        rm -rf "$WORKDIR"
                    fi
                    git clone $REPO_URL "$WORKDIR"
                    echo "Repository cloned successfully!"
                    ls -la "$WORKDIR"
                '''
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                    python3 -m venv "$VENV_PATH"
                    . "$VENV_PATH/bin/activate"
                    pip install --upgrade pip build pytest
                '''
            }
        }

        stage('Build Wheel') {
            steps {
                dir('my_python_project') {
                    sh '''
                        . "$VENV_PATH/bin/activate"
                        python3 -m build --wheel
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                dir('my_python_project') {
                    sh '''
                        . "$VENV_PATH/bin/activate"
                        export PYTHONPATH=$PYTHONPATH:$(pwd)/src
                        pytest tests/
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('my_python_project') {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop my-python-container || true
                    docker rm my-python-container || true
                    docker run -d --name my-python-container $DOCKER_IMAGE
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Repository cloned, built, and deployed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check the logs for details.'
        }
    }
}
```

---

### 3.5 `pyproject.toml`

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "my_python_project"
version = "0.1.0"
dependencies = []

[project.scripts]
myapp = "my_python_project.main:main"

[tool.hatch.build.targets.wheel]
packages = ["src/my_python_project"]
```

---

### 3.6 `.gitignore`

```
__pycache__/
*.py[cod]
*.class
dist/
build/
*.egg-info/
venv/
```

---

## 4. Key Accomplishments

1. **Jenkins + GitHub Setup**
   - Configured SSH access to GitHub
   - Switched from HTTPS to SSH for secure cloning

2. **Resolved Jenkins Pipeline Issues**
   - Created and activated a Python virtual environment
   - Handled module import issues by setting `PYTHONPATH`
   - Executed tests using `pytest`

3. **Build & Test**
   - Packaged the Python code into a wheel
   - Validated application behavior with unit tests

4. **Containerization & Deployment**
   - Built Docker image using the wheel package
   - Deployed the app as a container from Jenkins

5. **Verification**
   - Checked container status: `docker ps -a`
   - Viewed logs: `docker logs my-python-container`

---

## ✅ Final Outcome

- Jenkins pipeline runs end-to-end successfully  
- Python application is deployed in a Docker container  
- Fully automated CI/CD process for building, testing, and deploying  
