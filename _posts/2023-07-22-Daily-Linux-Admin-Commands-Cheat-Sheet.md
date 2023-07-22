---
title: "Daily Linux Systems Command Cheat Sheet"
date: 2023-04-22 T19:34:30-04:00
categories:
  - blog
tags:
  - Linux
  - cybersecurity
  - Tutorials
---

Below is a compact cheat sheet for CentOS and Ubuntu, including common tasks and commands for checking various aspects of the system. The commands are written in markdown format for both CentOS and Ubuntu.
Linux System Administration Cheat Sheet
Updates:

CentOS:

```
sudo yum check-update   # Check for available updates
sudo yum update         # Update the system
```
Ubuntu:

```
sudo apt update         # Update package lists
sudo apt upgrade        # Upgrade installed packages
```

Security Logs:

CentOS/Ubuntu:

```
sudo tail -n 50 /var/log/secure   # Check the tail of security logs
```

Firewall Logs:

CentOS/Ubuntu:

```
sudo tail -n 50 /var/log/firewalld   # Check the tail of firewall logs
```

Firewall Rules:

CentOS/Ubuntu:

```
sudo firewall-cmd --list-all   # View all firewall rules
```

Editing Firewall Rules:

CentOS/Ubuntu:

```
sudo firewall-cmd --permanent --add-service=<service>   # Add a rule to allow a service (e.g., ssh, http)
sudo firewall-cmd --permanent --remove-service=<service>   # Remove a rule for a service
sudo firewall-cmd --permanent --add-port=<port>/tcp   # Add a rule to allow a specific port
sudo firewall-cmd --reload   # Apply changes
```

Running Processes:

CentOS/Ubuntu:

```
ps aux   # List all running processes
```

Users:

CentOS/Ubuntu:

```
sudo cat /etc/passwd   # List all users
```

Fail2ban Logs:

CentOS/Ubuntu:

```
sudo tail -n 50 /var/log/fail2ban.log   # Check the tail of Fail2ban logs
```

System Mail:

CentOS/Ubuntu:

```
sudo mail   # Check system mail
```

System Security Check:

CentOS/Ubuntu:

```
sudo chkrootkit   # Check for rootkits
sudo rkhunter --check   # Run Rootkit Hunter
```

Server Load:

CentOS/Ubuntu:

```
uptime   # Show server load and uptime
```

Storage Usage:

CentOS/Ubuntu:

```
df -h   # Show disk usage of file systems
```

Other Useful Commands:

CentOS/Ubuntu:

```
top             # Display system tasks
netstat -tuln   # Display listening ports
ifconfig       # Show network interfaces (Ubuntu)
ip addr show   # Show network interfaces (CentOS)
```

Remember to use these commands with appropriate privileges (e.g., using sudo) where necessary to access restricted system files or settings.

Please note that some commands may require specific packages to be installed (e.g., fail2ban), and the availability of certain commands may depend on your system configuration. Always use caution and ensure that you have the necessary permissions before making changes to the system.
