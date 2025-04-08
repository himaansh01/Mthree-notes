# Day 5 – Git Bash Commands & Concepts

## 🔧 Basic Git Commands

### 1. Check Current Directory
- `pwd`: Displays the current working directory.

### 2. Create & Navigate Directories
- `mkdir <folder_name>`: Creates a new directory.
- `cd <path>`: Changes to the specified directory.

---

## ⚙️ Git Configuration

- `git config --global user.name "Your Name"`: Sets your Git username globally.
- `git config --global user.email "your.email@example.com"`: Sets your Git email globally.

---

## 🛠️ Git Repository Initialization

- `git init`: Initializes a new Git repository in the current directory.
- `echo "text we want to save" > file_name.txt`: Creates a file and writes the given text into it.

---

## 📦 Git Stash – Temporarily Save Changes

- `git stash`: Saves uncommitted changes temporarily without committing.
- `git stash list`: Displays the list of stashed changes.
- `git stash apply`: Restores the most recent stash but keeps it in the stash list.
- `git stash pop`: Restores the most recent stash and removes it from the stash list.
- `git stash drop stash@{0}`: Deletes a specific stash (e.g., `stash@{0}`).
- `git stash clear`: Removes all stashed changes.
- `git stash push -m "message"`: Creates a named stash with a custom message.

---

## ⚔️ Scenario: Handling Merge Conflicts

**Issue:**  
- Changes were made to the `main` branch from the GitHub UI.  
- Local repository also has changes.  
- A `git pull` could cause a merge conflict.

### 👣 Steps Followed

1. **Switch to Feature Branch**  
   ```bash
   git checkout feature/intrest
