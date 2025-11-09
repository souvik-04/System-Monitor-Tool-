# 🖥️ System Monitor Tool

A **real-time terminal-based system monitoring tool** written in **C++**, built using the **ncurses** library.  
This project provides a clean, modular, and lightweight implementation for displaying **CPU**, **memory**, and **process information** in a Linux environment.

---

## 📘 Overview

The **System Monitor Tool** functions similarly to the `htop` command but is fully built from scratch in **C++** using **object-oriented programming principles**.  
It displays:
- CPU and memory utilization (as progress bars)
- Total and running processes
- System uptime
- Detailed list of processes with PID, user, CPU%, RAM usage, and command

The project is designed to help understand how Linux exposes system information via the `/proc` filesystem.

---

## ⚙️ Features

✅ Display **OS name**, **kernel version**, and **uptime**  
✅ Show **CPU** and **memory utilization** as live progress bars  
✅ List all running processes with **PID, user, CPU%, RAM**, and **command**  
✅ **Sort processes by memory usage** (default; can be changed to CPU usage)  
✅ Auto-refresh display every **1 second** (real-time updates)  
✅ **Modular, object-oriented** design for clarity and scalability  

---

## 🏗️ Project Structure
```
Linux-System-Monitor/
│
├── include/                 # Header files
│   ├── all_processes.h
│   ├── format.h
│   ├── linux_parser.h
│   ├── ncurses_display.h
│   ├── parser_consts.h
│   ├── parser_helper.h
│   ├── process.h
│   ├── processor.h
│   └── system.h
│
├── src/                     # Source code files
│   ├── all_processes.cpp
│   ├── format.cpp
│   ├── linux_parser.cpp
│   ├── main.cpp
│   ├── ncurses_display.cpp
│   ├── process.cpp
│   ├── processor.cpp
│   └── system.cpp
│
├── CMakeLists.txt           # CMake build configuration
├── Makefile                 # Alternative build method
├── LICENSE                  # License file
└── README.md                # Project documentation
```
---

## 🧩 Class Responsibilities

| Class | Responsibility |
|--------|----------------|
| **System** | Coordinates CPU, memory, and process info |
| **Processor** | Calculates CPU utilization |
| **Process** | Represents a single process |
| **All_Processes** | Manages and sorts all processes |
| **LinuxParser** | Reads and parses system data from `/proc` |
| **Format** | Formats data (e.g., uptime display) |
| **NCursesDisplay** | Displays system info using ncurses UI |

---

## 🧠 Architecture
```
/proc/stat ───▶ LinuxParser ───▶ Processor ───▶ System ───▶ NCursesDisplay
/proc/[pid]/stat ──▶ Process ──▶ All_Processes ──▶ System
```

---

## 🚀 Getting Started

### 1️⃣ Prerequisites
Ensure you have the following installed:

```bash
sudo apt update
sudo apt install -y build-essential cmake libncurses5-dev libncursesw5-dev
```
---

## If you’re using Windows, run this inside WSL (Ubuntu).
### 2️⃣ Build Instructions
## Clone the repository
```
git clone https://github.com/<your-username>/System-Monitor-Tool.git
cd System-Monitor-Tool
```

## Create and navigate to build folder
```
mkdir build && cd build
```
## Configure project
```
cmake ..
```
## Compile
```
make
```
### 3️⃣ Run the Program
```
./monitor
```
## 🧰 How It Works

The tool reads data from the /proc filesystem (/proc/stat, /proc/meminfo, /proc/[pid]/status, etc.)

LinuxParser extracts the raw values.

Processor calculates CPU utilization using deltas of idle and total times.

All_Processes gathers all process IDs and builds Process objects.

NCursesDisplay continuously redraws the UI every second with updated data.
