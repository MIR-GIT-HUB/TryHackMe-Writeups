# Daily Write-up: Linux Fundamentals Part 3 (TryHackMe)

## 📌 Overview
Mastered remote server architectures, background job control, and process/service administration inside Linux environments—critical skills for security monitoring and incident response.

---

## 🛠️ Key Concepts & Tools Learned

### 1. Lab Architecture & The Two-Machine Dynamic
* **The Reality**: Cybersecurity utilizes an Attacker machine (**AttackBox**) and a hidden target server (**Lab Machine**). 
* **Connection**: Bridges are built via **SSH** (`ssh username@target_ip`). Once inside, a single terminal seamlessly controls the remote target.
* **Layout Management**: Maximized efficiency by opening multiple terminal instances (e.g., `root@...177`) and snapping them side-by-side to monitor the attacker and target environments simultaneously.

### 2. File Transfers via Python Web Server (`200 OK`)
* **Concept**: Instead of physical media or email, Python turns a target folder into a temporary download station using `python3 -m http.server <port>`.
* **Execution**: Ran the server on Port `8000` on the remote server, and successfully used `wget http://<Target_IP>:8000/.flag.txt` from the AttackBox to pull down a hidden flag file.
* **The `200 OK` Status**: Confirmed successful network communication and retrieval of data across the private lab network.

### 3. Linux Process Management & Threat Hunting
* **Processes**: Active programs running in memory. Monitoring them allows defenders to spot unauthorized scripts, hidden malware, or resource hijacking.
* **`ps aux`**: Generates a static snapshot of all active processes across all users. Used this to hunt for out-of-place scripts running from non-standard directories.
* **`top`**: Displays a live, real-time administrative view of CPU and memory utilization.
* **Job Control**: 
  * `Ctrl + Z`: Pauses a foreground application instantly to reclaim the shell command line.
  * `fg`: Resumes a paused background task and brings it back to the screen center.

### 4. System Services (`systemctl`)
* **Start vs. Enable**: `systemctl start` turns a service on immediately for the current session. `systemctl enable` configures the service to boot automatically every time the computer powers up in the future.
* **Stop vs. Kill**: `systemctl stop` requests a graceful shutdown (saving data/cleaning cache). `systemctl kill` instantly terminates the main service and all its spawned child processes when a service freezes or goes rogue.

---

## 💡 Troubleshooting & Personal Takeaways
* **Gotcha (Port Definitions)**: Encountered a "timeout retrying" connection error while attempting a file download. Discovered the download command omitted the explicit port specification (`:8000`). Rectified this by matching the AttackBox `wget` request port precisely to the active Python server port, resulting in a successful `200 OK` status.
* **Security Mindset**: Learned that scanning user process lists (`ps aux`) is fundamental to incident response. Identifying anomalous paths (like binaries running from user home directories instead of `/usr/bin/`) is often the quickest way to catch an active intrusion on a server.
