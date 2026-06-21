# Linux Server Administration and Automation Lab

A hands-on Linux administration project built on an AWS EC2 Ubuntu server to demonstrate core Cloud and DevOps skills, including user management, SSH hardening, web server deployment, automation, monitoring, and service management.

## Project Overview

This project simulates common day-to-day responsibilities of a Linux System Administrator and DevOps Engineer in a production environment.

The lab environment was provisioned on an Amazon EC2 instance running Ubuntu Server 26.04 LTS and configured using native Linux administration tools.

## Features

* User and group management
* Group-based access control
* Shared directory configuration
* SSH key generation and SSH daemon configuration
* Nginx web server deployment
* Bash scripting for system health monitoring
* Automated task scheduling with Cron
* Service management using Systemd
* Basic server monitoring and troubleshooting

## Architecture

```text
Local Machine
      │
      │ SSH
      ▼
AWS EC2 (Ubuntu 26.04 LTS)
      │
      ├── User & Group Management
      ├── Shared Directory Permissions
      ├── SSH Configuration
      ├── Nginx Web Server
      ├── Bash Automation Scripts
      ├── Cron Jobs
      ├── Systemd Services
      └── System Monitoring
```

## Technologies Used

* AWS EC2
* Ubuntu Server 26.04 LTS
* Linux CLI
* Bash Scripting
* Nginx
* SSH
* Cron
* Systemd
* Git
* GitHub

## Project Structure

```text
linux-admin-lab/
├── README.md
├── scripts/
│   └── health-check.sh
├── systemd/
│   └── healthcheck.service
├── screenshots/
│   ├── users-groups.png
│   ├── shared-directory.png
│   ├── nginx-status.png
│   ├── cronjobs.png
│   └── systemd-logs.png
└── docs/
    └── architecture.md
```

## Implementation Steps

### 1. System Update

Updated package repositories and upgraded installed packages.

```bash
sudo apt update
sudo apt upgrade -y
```

### 2. User and Group Management

Created user groups and configured group memberships.

```bash
sudo groupadd devops
sudo groupadd developers

sudo useradd -m -s /bin/bash john
sudo useradd -m -s /bin/bash alice

sudo passwd john
sudo passwd alice

sudo usermod -aG devops john
sudo usermod -aG developers alice
```

Verified user information.

```bash
groups john
id john
```

### 3. Shared Directory Configuration

Created a shared directory accessible only to members of the `devops` group.

```bash
sudo mkdir /shared
sudo chown root:devops /shared
sudo chmod 770 /shared
```

Verified permissions.

```bash
ls -ld /shared
```

Tested access using the `john` user.

```bash
su - john

touch /shared/test.txt

ls -l /shared
```

### 4. SSH Configuration

Generated SSH keys and modified SSH daemon settings.

```bash
ssh-keygen

sudo nano /etc/ssh/sshd_config
```

Applied configuration changes.

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

Restarted the SSH service.

```bash
sudo systemctl restart ssh
```

### 5. Nginx Web Server Deployment

Installed and configured Nginx.

```bash
sudo apt install nginx -y

sudo systemctl enable nginx
sudo systemctl start nginx
```

Verified service status.

```bash
systemctl status nginx
```

Customized the default web page.

```bash
sudo nano /var/www/html/index.html
```

### 6. Bash Automation

Created a health monitoring script.

```bash
mkdir -p ~/scripts
cd ~/scripts

nano health-check.sh

chmod +x health-check.sh

./health-check.sh
```

Example checks performed by the script:

* CPU load
* Memory usage
* Disk usage
* Top running processes

### 7. Cron Job Scheduling

Configured automated execution of the health monitoring script.

```bash
crontab -e
```

Added the following cron job.

```cron
0 9 * * * /home/ubuntu/scripts/health-check.sh >> /home/ubuntu/health.log
```

Verified configuration.

```bash
crontab -l
```

### 8. Systemd Service Configuration

Created a custom Systemd service.

```bash
sudo nano /etc/systemd/system/healthcheck.service
```

Service definition:

```ini
[Unit]
Description=Health Check Service

[Service]
ExecStart=/home/ubuntu/scripts/health-check.sh
User=ubuntu

[Install]
WantedBy=multi-user.target
```

Enabled and started the service.

```bash
sudo systemctl daemon-reload

sudo systemctl start healthcheck

sudo systemctl enable healthcheck
```

Verified logs.

```bash
journalctl -u healthcheck
```

### 9. Monitoring and Troubleshooting

Used standard Linux monitoring commands.

```bash
top
free -h
df -h
uptime
journalctl -xe
systemctl list-units --type=service
```

## Key Learnings

* Linux user and group administration
* File permissions and ownership
* Group-based access control
* SSH configuration and security
* Web server deployment with Nginx
* Bash scripting and automation
* Task scheduling using Cron
* Service management with Systemd
* Basic Linux monitoring and troubleshooting

## Future Enhancements

* Automate backups using Bash scripts
* Upload backups to Amazon S3
* Configure firewall rules with UFW
* Integrate Amazon CloudWatch monitoring
* Add email notifications for health checks
* Containerize monitoring scripts using Docker

## Author

**Gokul M**

* GitHub: https://github.com/gokul-dev-ml
* LinkedIn: https://linkedin.com/in/gokul-m05
<img width="497" height="286" alt="Screenshot 2026-06-21 161903" src="https://github.com/user-attachments/assets/4c786694-c2b0-4610-b103-d2e6433a6148" />
<img width="491" height="283" alt="Screenshot 2026-06-21 161843" src="https://github.com/user-attachments/assets/9335577f-ce75-46b1-9c0e-5e8725b2a13b" />
<img width="1" height="1" alt="Screenshot 2026-06-21 161831" src="https://github.com/user-attachments/assets/f580b5a5-93a0-455f-8de3-ba9f3094c04d" />
<img width="2" height="1" alt="Screenshot 2026-06-21 161812" src="https://github.com/user-attachments/assets/13a06967-9020-4224-bb70-6713336a8b6d" />
<img width="496" height="285" alt="Screenshot 2026-06-21 161730" src="https://github.com/user-attachments/assets/9f38929a-57f7-4429-9ec1-e24c045389ac" />
<img width="494" height="284" alt="Screenshot 2026-06-21 161652" src="https://github.com/user-attachments/assets/873f26ab-cf0d-4a74-834b-fa926d394017" />
<img width="488" height="281" alt="Screenshot 2026-06-21 161528" src="https://github.com/user-attachments/assets/198a7e46-eb62-4695-9132-eacbc5310a89" />
<img width="493" height="214" alt="Screenshot 2026-06-21 160520" src="https://github.com/user-attachments/assets/655aff61-3a5a-4d6c-b965-ddf08642fadf" />
