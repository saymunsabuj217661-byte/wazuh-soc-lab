# Wazuh SOC Lab Installation Documentation

## Phase 1: GitHub Repository & Project Setup

**Date:** 11 July 2026

---

## Objective

Prepare the development environment and create a GitHub repository for documenting and managing the Wazuh SOC Lab project.

---

## Step 1: Create GitHub Repository

Repository Name:
```
wazuh-soc-lab
```

Visibility:
- Public

Status:
- Completed

---

## Step 2: Install Git

Installed Git for Windows.

Version:

```
git version 2.55.0.windows.2
```

Status:
- Completed

---

## Step 3: Install Visual Studio Code

Installed Visual Studio Code.

Purpose:

- Configuration Editing
- Documentation
- Git Integration

Status:
- Completed

---

## Step 4: Configure Git

Configured Username

```bash
git config --global user.name "Saymun Islam Sabuj"
```

Configured Email

```bash
git config --global user.email "saymunsabuj21766.1@gmail.com"
```

Status:
- Completed

---

## Step 5: Clone GitHub Repository

```bash
git clone https://github.com/saymunsabuj217661-byte/wazuh-soc-lab.git
```

Status:
- Completed

---

## Step 6: Create Project Structure

Created folders:

- agents
- architecture
- configs
- docs
- logs
- rsyslog
- screenshots
- scripts
- wazuh

Status:
- Completed

---

## Step 7: Create README

Created README.md file.

Status:
- Completed

---

## Step 8: Create .gitignore

Created .gitignore file.

Status:
- Completed

---

## Step 9: First Commit

```bash
git add .

git commit -m "Initial project structure"
```

Status:
- Completed

---

## Step 10: Push to GitHub

```bash
git push -u origin main
```

Status:
- Completed

---

## Verification

```bash
git status
```

Output:

```
On branch main

Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

Status:
- Successful

# Phase 2 - Ubuntu Server Preparation

## Objective

Prepare the Ubuntu Server virtual machine for Wazuh SIEM deployment.

## VM Configuration

- Hypervisor: VMware Workstation Pro
- VM Name: soc-server
- Operating System: Ubuntu Server 22.04.5 LTS
- RAM: 8 GB
- CPU: 4 vCPU
- Disk: 100 GB
- Network: NAT

## Static Network Configuration

- Interface: ens33
- IP Address: 192.168.10.132/24
- Gateway: 192.168.10.2
- DNS:
  - 8.8.8.8
  - 1.1.1.1

## Verification

Commands used:

```bash
hostnamectl
ip a
ip route
ping -c 4 8.8.8.8
ping -c 4 google.com
```

## Status

Completed

## Screenshots

### 1. VMware Virtual Machine Configuration

![VM Settings](../screenshots/phase-02/01-vm-settings.png)

### 2. Network Configuration

![Network Configuration](../screenshots/phase-02/02-network-configuration.png)

### 3. Connectivity Test

![Connectivity Test](../screenshots/phase-02/03-connectivity-test.png)

### 4. System Information

![System Information](../screenshots/phase-02/04-system-information.png)