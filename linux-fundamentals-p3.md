# Daily Write-up: Linux Fundamentals Part 3 (TryHackMe)

## 📌 Overview
Explored advanced Linux utilities, text editing, and remote server interaction models essential for system administration and security operations.

---

## 🛠️ Key Concepts & Tools Learned

### 1. The Two-Machine Dynamic (Architecture)
* **Concept**: Cybersecurity training environments utilize an Attacker computer and an isolated target Lab Machine (Server). 
* **Workflow**: The target machine sits headlessly in the cloud. Access is established by building an encrypted network bridge using **SSH** (`ssh username@target_ip`). 
* **Control**: Once connected, control shifts seamlessly inside a single terminal from the local AttackBox to the remote target.

### 2. Terminal Text Editors
* Moved beyond basic `echo` and pipe operators (`>`, `>>`) to manage multi-line data efficiently.
* **`nano`**: A straightforward terminal text editor. 
  * *Controls*: `Ctrl + O` (Save/Write Out), `Ctrl + X` (Exit).

### 3. Session Management & Backgrounding
* Learned that interrupting or closing an SSH session will securely terminate the connection.
* **Best Practice**: To safely "minimize" a running task without losing the terminal or getting logged out, use `Ctrl + Z` to pause the job, followed by the `bg` command to push it into the background.

---

## 💡 Gotchas & Troubleshooting (Personal Takeaways)
* **Session Persistence**: Experienced an accidental logout while trying to background a process. Learned the proper lifecycle of Linux background jobs (`Ctrl + Z` + `bg`) to maintain session persistence over SSH.
