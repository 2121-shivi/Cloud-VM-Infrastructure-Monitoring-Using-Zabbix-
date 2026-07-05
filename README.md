# ☁️ Cloud VM Infrastructure Monitoring and Alerting using Zabbix

![Platform](https://img.shields.io/badge/Platform-Ubuntu%2022.04-orange)
![Monitoring](https://img.shields.io/badge/Monitoring-Zabbix-red)
![Database](https://img.shields.io/badge/Database-MySQL-blue)
![Web Server](https://img.shields.io/badge/Web%20Server-Apache-green)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## 📖 Project Overview

This project demonstrates the deployment and implementation of a **Cloud VM Infrastructure Monitoring and Alerting System** using **Zabbix**. The monitoring environment was deployed on **VMware Cloud Director (VCD)** using three Ubuntu virtual machines.

The system continuously monitors cloud infrastructure, collects real-time performance metrics, detects abnormal conditions using triggers, and automatically sends email notifications to administrators whenever a problem occurs.

---

## 🎯 Project Objectives

- Deploy a centralized monitoring solution using Zabbix.
- Monitor multiple cloud-hosted virtual machines.
- Track CPU, memory, disk, and host availability.
- Configure trigger-based alert generation.
- Send automated email notifications using Gmail SMTP.
- Visualize infrastructure health through custom dashboards.
- Demonstrate proactive cloud infrastructure monitoring.

---

## 🏗️ Infrastructure

| Virtual Machine | IP Address | Purpose |
|-----------------|------------|----------|
| Zabbix Server | 192.168.0.2 | Central Monitoring Server |
| Client-1 | 192.168.0.3 | Monitored Host |
| Client-2 | 192.168.0.4 | Monitored Host |

---

## ⚙️ Technologies Used

- Ubuntu 22.04 LTS
- VMware Cloud Director (VCD)
- Zabbix 7.x
- MySQL
- Apache2
- Gmail SMTP
- Linux

---

## 🚀 Features

- ✅ Multi-VM Infrastructure Monitoring
- ✅ CPU Monitoring
- ✅ Memory Monitoring
- ✅ Disk Space Monitoring
- ✅ Host Availability Monitoring
- ✅ Real-Time Dashboards
- ✅ Trigger-Based Alerts
- ✅ Email Notifications
- ✅ Problem & Recovery Notifications
- ✅ Historical Performance Data
- ✅ Cloud Infrastructure Monitoring

---

## 📊 Monitoring Parameters

The following system metrics are monitored:

- CPU Utilization
- System Load
- Memory Usage
- Disk Utilization
- Disk Space Availability
- Host Availability
- Network Status
- System Uptime

---

## 🚨 Alert Configuration

The following alerts were configured:

- High CPU Utilization
- High System Load
- Host Down Detection
- Low Disk Space
- Email Alert Notification
- Recovery Notification

---

## 📧 Email Notification

Gmail SMTP was configured to automatically send notifications whenever a trigger entered a **Problem** or **Recovery** state.

Notification Features:

- Problem Alerts
- Recovery Alerts
- Gmail SMTP Integration
- Administrator Email Notifications

---

## 📈 Dashboard

A custom dashboard named **Cloud VM Infrastructure Monitoring** was created to provide centralized infrastructure visibility.

Dashboard Widgets:

- VM Availability
- CPU Utilization
- Current Alerts
- Infrastructure Status
- Clock Widget

---

## 📂 Repository Structure

```text
Cloud-VM-Infrastructure-Monitoring-Using-Zabbix/
│
├── README.md
├── SETUP_GUIDE.md
├── Zabbix_Documentation.pdf
├── Zabbix_Screenshots.pdf
│   ├── VM_Creation.png
│   ├── Dashboard.png
│   ├── Hosts.png
│   ├── CPU_Alert.png
│   ├── Email_Notification.png
│   └── Recovery_Email.png
└── LICENSE
```


## 🧪 Project Demonstration

The project was successfully tested by:

- Generating high CPU usage using the **stress** tool.
- Monitoring host availability.
- Triggering automatic alerts.
- Receiving email notifications.
- Verifying recovery notifications after resolving the issue.

---

## 📚 Documentation

Complete project documentation is available in:

- **SETUP_GUIDE.md** – Complete installation and configuration guide.
- **Zabbix_Documentation.pdf** – Detailed project documentation with implementation steps and screenshots.

---

## 🎓 Learning Outcomes

This project provided practical experience in:

- Cloud Infrastructure Monitoring
- Linux System Administration
- Zabbix Deployment
- Infrastructure Alerting
- Dashboard Development
- Incident Detection
- Email Notification Configuration
- Performance Monitoring

---

## 👨‍💻 Author

**Shivani Sharma**

B.Tech Computer Science Engineering

Amity University

---

