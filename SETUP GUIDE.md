# Cloud VM Infrastructure Monitoring Using Zabbix
## Setup Guide

---

# Environment Details

| Component | Details |
|-----------|----------|
| Platform | VMware Cloud Director (VCD) |
| Operating System | Ubuntu 22.04 LTS |
| Monitoring Tool | Zabbix 7.0 |
| Database | MySQL |
| Web Server | Apache2 |
| Frontend | Zabbix Web Interface |

---

# Infrastructure

| Machine | Hostname | IP Address | Purpose |
|---------|----------|------------|---------|
| Zabbix Server | zabbix-server | 192.168.0.2 | Monitoring Server |
| Client VM 1 | client-1 | 192.168.0.3 | Monitored Linux Host |
| Client VM 2 | client-2 | 192.168.0.4 | Monitored Linux Host |

---

# Part 1 — Zabbix Server Installation

## Step 1 — Update System

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Step 2 — Install MySQL

```bash
sudo apt install mysql-server -y
sudo systemctl status mysql
```

---

## Step 3 — Secure MySQL

```bash
sudo mysql_secure_installation
```

---

## Step 4 — Create Database

Login to MySQL

```bash
sudo mysql -u root -p
```

Execute

```sql
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;

CREATE USER 'zabbix'@'localhost' IDENTIFIED BY 'zabbix123';

GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';

FLUSH PRIVILEGES;

EXIT;
```

---

## Step 5 — Add Zabbix Repository

```bash
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu22.04_all.deb

sudo dpkg -i zabbix-release_latest_7.0+ubuntu22.04_all.deb

sudo apt update
```

---

## Step 6 — Install Zabbix Packages

```bash
sudo apt install zabbix-server-mysql \
zabbix-frontend-php \
zabbix-apache-conf \
zabbix-sql-scripts \
zabbix-agent -y
```

---

## Step 7 — Import Database Schema

```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql -u zabbix -p zabbix
```

---

## Step 8 — Configure Zabbix Server

Edit

```bash
sudo nano /etc/zabbix/zabbix_server.conf
```

Update

```text
DBPassword=zabbix123
```

---

## Step 9 — Restart Services

```bash
sudo systemctl restart zabbix-server
sudo systemctl restart apache2
sudo systemctl restart zabbix-agent

sudo systemctl enable zabbix-server
sudo systemctl enable apache2
sudo systemctl enable zabbix-agent
```

---

## Step 10 — Verify Services

```bash
systemctl status zabbix-server

systemctl status apache2

ss -tulpn | grep 10051
```

---

# Part 2 — Web Frontend Setup

Open browser

```
http://192.168.0.2/zabbix
```

Complete the installation wizard.

Login using

```
Username : Admin
Password : zabbix
```

Change the default password after the first login.

---

# Part 3 — Client Agent Installation

Perform the following steps on both **Client-1** and **Client-2**.

---

## Step 1 — Update Repository

```bash
sudo apt update
```

---

## Step 2 — Install Agent

```bash
sudo apt install zabbix-agent -y
```

---

## Step 3 — Verify Installation

```bash
zabbix_agentd --version
```

---

## Step 4 — Configure Agent

Edit

```bash
sudo nano /etc/zabbix/zabbix_agentd.conf
```

### Client-1

```text
Server=192.168.0.2
ServerActive=192.168.0.2
Hostname=client-1
```

### Client-2

```text
Server=192.168.0.2
ServerActive=192.168.0.2
Hostname=client-2
```

---

## Step 5 — Restart Agent

```bash
sudo systemctl restart zabbix-agent
```

---

## Step 6 — Enable Agent

```bash
sudo systemctl enable zabbix-agent
```

---

## Step 7 — Verify Agent

```bash
systemctl status zabbix-agent

ss -tulpn | grep 10050
```

---

# Part 4 — Add Hosts

Navigate to

```
Data Collection
→ Hosts
→ Create Host
```

Configure the hosts.

| Parameter | Client-1 | Client-2 |
|------------|----------|----------|
| Host Name | client-1 | client-2 |
| Host Group | Linux Servers | Linux Servers |
| IP Address | 192.168.0.3 | 192.168.0.4 |
| Template | Linux by Zabbix Agent | Linux by Zabbix Agent |

Save the configuration.

Verify that the Availability indicator shows **Green ZBX**.

---

# Part 5 — Dashboard Configuration

Create a dashboard named

```
Cloud VM Infrastructure Monitoring
```

Add the following widgets:

- VM Availability
- CPU Utilization
- Current Alerts
- Infrastructure Status
- India Time Clock

---

# Part 6 — Trigger Configuration

Configured triggers include:

- High CPU Usage
- High Load Average
- Low Disk Space
- Host Unreachable

These triggers automatically generate alerts whenever predefined thresholds are exceeded.

---

# Part 7 — Email Notification Setup

Configure Gmail SMTP.

| Setting | Value |
|----------|-------|
| SMTP Server | smtp.gmail.com |
| Port | 587 |
| Security | STARTTLS |
| Authentication | Gmail App Password |

Associate the Email Media Type with the Admin user.

Enable **Report Problems** and **Report Recovery** actions.

---

# Part 8 — Alert Testing

## CPU Stress Test

Install stress utility

```bash
sudo apt install stress -y
```

Generate CPU load

```bash
stress --cpu 4 --timeout 300
```

Expected Result

- High CPU trigger activated
- Alert generated
- Dashboard updated
- Email notification received

---

## SSH Failed Login Monitoring

Create a log monitoring item

```text
log[/var/log/auth.log,Failed password]
```

Generate failed login attempts.

Expected Result

- Failed login detected
- Event appears in Latest Data
- Trigger generated
- Email notification sent

---

# Part 9 — Troubleshooting

| Problem | Resolution |
|----------|------------|
| Host not found | Corrected Hostname in `zabbix_agentd.conf`. |
| Active check not supported | Configured item as Active Check. |
| Permission denied on `/var/log/auth.log` | Added `zabbix` user to the `adm` group and restarted the agent. |
| Gmail login denied | Enabled 2FA and used a Gmail App Password. |
| Email not received | Configured Email Media for the Admin user and enabled trigger actions. |

---

# Final Outcome

The project successfully implemented a centralized monitoring solution using Zabbix to monitor multiple cloud-based virtual machines. The system continuously collected infrastructure metrics, displayed real-time dashboards, generated automated alerts, monitored security events, and delivered email notifications for both problem and recovery events.

```

This is a professional, GitHub-ready `SETUP_GUIDE.md` that aligns with your completed project and complements the detailed PDF documentation you've already prepared. It is based on the setup and workflow documented in your project report. :contentReference[oaicite:1]{index=1}
