# ⏱️ CronJob_Python - Automated URL & Webhook Requester

<p align="center">
  <a href="README.md"><strong>🇺🇸 English (Current)</strong></a> &nbsp;|&nbsp; 
  <a href="README_VI.md"><strong>🇻🇳 Xem bản Tiếng Việt</strong></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-3776AB?logo=python&logoColor=white" alt="Python 3.8+" />
  <img src="https://img.shields.io/badge/Library-requests-blue" alt="Requests" />
  <img src="https://img.shields.io/badge/Platform-Windows_|_Linux_|_macOS-brightgreen" alt="Platform" />
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT" />
</p>

<p align="center">
  <b>A lightweight automation tool designed to periodically dispatch HTTP GET requests to a list of URLs for keep-alive pings, uptime monitoring, and scheduled webhook triggers on free cloud tiers (Render, Heroku, Supabase, Vercel...).</b>
</p>

---

## 📖 Overview

**CronJob_Python** is a minimalist automation script written in Python. It reads target URLs from `cron.txt`, sequentially sends HTTP GET requests via `requests`, and outputs real-time session logs (`Session`, target `URL`, and server `Response text`).

### Practical Use Cases:
- 🟢 **Keep-alive / Anti-Sleep**: Keep web apps hosted on free cloud tiers (Render, Koyeb, Glitch, Heroku) active 24/7 without entering hibernation.
- 🔄 **Webhook & Task Triggers**: Periodically trigger data sync routines, scrapers, automated emails, or database backups.
- 📡 **Basic Uptime Monitoring**: Verify the live status and response payloads of target web services.

---

## ✨ Key Features

- 📋 **External URL List**: Manage target URLs easily in `cron.txt` without editing source code.
- 🖥️ **Real-Time Logging**: Live terminal output showing session counter, request URL, and server response.
- ⏱️ **Customizable Delay**: Adjustable sleep interval between loop cycles (`limit = 5` seconds default).
- 🚀 **Low Resource Footprint**: Consumes minimal CPU and memory; runs smoothly even on entry-level VPS.

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- [Python 3.8+](https://www.python.org/downloads/) installed.
- Ensure **"Add Python to PATH"** was checked during Windows installation.

---

### 2. Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/kingbone2006/CronJob_Python.git
   cd CronJob_Python
   ```

2. **Install dependencies:**
   ```bash
   pip install requests
   ```

---

### 3. Configure URLs (`cron.txt`)

Add target URLs to `cron.txt` (one URL per line):

```text
https://my-app.onrender.com/api/ping
https://example.com/cron-task
https://api.mysite.com/health
```

---

### 4. Run

```bash
python 1.py
```

Console output:
```text
Phiên: 1
+ URL: https://my-app.onrender.com/api/ping
+ Response: {"status":"ok","timestamp":1726589000}
-------------------------------------
Phiên: 2
+ URL: https://example.com/cron-task
+ Response: Success
-------------------------------------
```

---

## 🔄 Running 24/7 in Background

### On Linux / VPS:
```bash
# Using nohup
nohup python3 1.py > cron.log 2>&1 &

# Or using PM2
pm2 start 1.py --name "cronjob" --interpreter python3
```

### On Windows:
Create a `run_silent.vbs` file to run silently in the background:
```vbs
Set WshShell = CreateObject("WScript.Shell")
WshShell.Run "python 1.py", 0, False
```

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).
