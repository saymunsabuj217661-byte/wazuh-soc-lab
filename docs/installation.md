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


# Phase 3 – Centralized Rsyslog Installation

## Objective

Install and verify the Rsyslog service to prepare the Ubuntu server for centralized log collection.

## Commands

```bash
sudo apt update
sudo apt install rsyslog -y
rsyslogd -v
sudo systemctl status rsyslog
sudo systemctl enable rsyslog
sudo systemctl is-enabled rsyslog
```

## Expected Result

- rsyslog installed successfully.
- Service status: active (running).
- Service enabled at boot.

## Screenshots

![Rsyslog Version](../screenshots/phase-03/01-rsyslog-version.png)

![Rsyslog Status](../screenshots/phase-03/02-rsyslog-status.png)

![Rsyslog Enabled](../screenshots/phase-03/03-rsyslog-enabled.png)


## Step 2: Backup Rsyslog Configuration

Before making any configuration changes, a backup of the original `rsyslog.conf` file was created.

### Command

```bash
sudo cp /etc/rsyslog.conf /etc/rsyslog.conf.backup
ls -l /etc/rsyslog.conf*
```

### Result

- Backup file created successfully.
- Original configuration remains unchanged.
- Backup can be restored if needed.

### Screenshot

![Rsyslog Backup](../screenshots/phase-03/04-rsyslog-backup.png)

## Step 3: Enable Remote Syslog Reception

The Rsyslog server was configured to receive remote logs using UDP and TCP protocols on port 514.

### Configuration

Enabled modules:

```conf
module(load="imudp")
input(type="imudp" port="514")

module(load="imtcp")
input(type="imtcp" port="514")
```

### Verification

```bash
grep -E "imudp|imtcp|514" /etc/rsyslog.conf

sudo systemctl restart rsyslog

sudo ss -tulnp | grep 514
```

### Expected Result

- UDP port 514 is listening.
- TCP port 514 is listening.
- Rsyslog service is active.

### Screenshots

![Rsyslog UDP TCP Configuration](../screenshots/phase-03/05-rsyslog-udp-tcp-enabled.png)

![Rsyslog Restart Status](../screenshots/phase-03/06-rsyslog-status-after-restart.png)

![Port 514 Listening](../screenshots/phase-03/07-port-514-listening.png)
## Step 4: Configure Remote Log Storage

A dedicated directory was created to store logs received by the centralized rsyslog server.

### Create Log Directory

```bash
sudo mkdir -p /var/log/remote
sudo chmod 755 /var/log/remote
```

### Configure Remote Log Template

File:

```bash
/etc/rsyslog.d/remote.conf
```

Configuration:

```conf
$template RemoteLogs,"/var/log/remote/%HOSTNAME%/%PROGRAMNAME%.log"

*.* ?RemoteLogs
& stop
```

### Permission Configuration

```bash
sudo chown -R syslog:adm /var/log/remote
sudo chmod -R 755 /var/log/remote
```

### Verification

```bash
sudo systemctl restart rsyslog

logger "Phase 3 remote log test"

sudo find /var/log/remote -type f
```

### Expected Result

- Rsyslog service running successfully.
- Remote log directory created.
- Logs stored based on hostname and program name.

### Screenshots

![Remote Log Directory](../screenshots/phase-03/08-remote-log-directory.png)

![Rsyslog Final Status](../screenshots/phase-03/09-rsyslog-status-final.png)

![Remote Log Test](../screenshots/phase-03/10-remote-log-test.png)