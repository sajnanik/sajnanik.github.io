---
title: "Linux Server Hardening 101 - Using Fail2ban: Ban failed security attempts"
date: 2023-04-21 T19:34:30-04:00
categories:
  - blog
tags:
  - Linux
  - Cybersecurity
  - Tutorials
  - Linux Hardening 101
---

Fail2ban, a versatile and powerful intrusion prevention tool, has garnered both acclaim and caution in the realm of server security. As a guardian of our digital fortresses, it relentlessly watches for malicious actors attempting to breach our defenses, often resulting in the swift banning of suspicious IP addresses. However, in certain scenarios, Fail2ban's zealous protection might inadvertently catch legitimate users in its crossfire. As a result, some administrators hesitate to embrace it, fearing that it might lead to locking out users who may have merely forgotten their passwords. This article explores the benefits of Fail2ban, why it might not always be implemented, and how it can be effectively utilized in isolated server environments with known user IPs or static VPNs, creating a fine balance between enhanced security and user convenience.


# Installing Fail2ban on CentOS and Ubuntu:

## CentOS:

### Install Fail2ban:

```
sudo yum install epel-release
sudo yum install fail2ban
```

## Enable and start Fail2ban service:

```
    sudo systemctl enable fail2ban
    sudo systemctl start fail2ban
```

## Ubuntu:

### Install Fail2ban:

```
sudo apt update
sudo apt install fail2ban
```

## Enable and start Fail2ban service:

```
    sudo systemctl enable fail2ban
    sudo systemctl start fail2ban
```

# Configuring Fail2ban:

The Fail2ban configuration file is located at /etc/fail2ban/jail.conf. Before you do anything, create a copy in the same directory and name it /etc/fail2ban/jail.local. You will be editing this LOCAL file. You can create and edit this file as follows:

## Create a copy and open the configuration file:

```
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban/jail.local
```

Each service which will be protected by fail2Ban is called a Jail. So for example to protect ssh service, you will edit the SHH jail, which will be under  [sshd]


Customize the settings according to your needs. For example, to enable the SSH jail, modify the [sshd] section as follows:

# Find the jail and add the enabled true parameter like below. 

```
    [sshd]
    enabled = true
```

# Setting Parameters for Blocked IP:

You can adjust the ban parameters to fine-tune Fail2ban's behavior. This will be at the beginning of the file.  Key parameters include:

- maxretry: The number of failed login attempts before banning an IP.
- bantime: The duration (in seconds) an IP will be banned (set to -1 for indefinite).
- findtime: The time window (in seconds) within which maxretry attempts are counted.

# Checking Fail2ban Logs and Banned IP List:

To check if Fail2ban has banned any IPs and view the bans, use the following commands:

## View Fail2ban logs:

```
sudo tail -n 50 /var/log/fail2ban.log
```

## List banned IP addresses:

```
    sudo fail2ban-client status
```
	
## To remove a specific IP ban, you can use:

```
sudo fail2ban-client set <jail_name> unbanip <ip_address>
```
## Finally, to search the banned IPs: 

```
grep "Ban " /var/log/fail2ban.log
```

Conclusion:

Fail2ban is an indispensable tool for securing servers and preventing unnecessary bans caused by malicious activities. By automatically detecting and blocking suspicious IP addresses, Fail2ban ensures enhanced server security, reduces support ticket loads, and minimizes user inconvenience. With straightforward installation, configuration, and monitoring, Fail2ban serves as the guardian of your server's safety, giving you peace of mind and greater control over your server environment.


Within minutes, I already was starting to ban multiple IPs trying to bruteforce into my systems. See below in the fail2ban log file. 

```
2023-07-22 03:37:21,623 fail2ban.actions        [45906]: NOTICE  [sshd] Restore Ban 143.198.238.143
2023-07-22 03:37:21,651 fail2ban.actions        [45906]: NOTICE  [sshd] Restore Ban 186.155.214.147
2023-07-22 03:37:21,666 fail2ban.actions        [45906]: NOTICE  [sshd] Restore Ban 218.92.0.56
2023-07-22 03:39:17,614 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.112 - 2023-07-22 03:39:17
2023-07-22 03:39:19,705 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.112 - 2023-07-22 03:39:19
2023-07-22 03:39:22,125 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.112 - 2023-07-22 03:39:22
2023-07-22 03:39:22,432 fail2ban.actions        [45906]: NOTICE  [sshd] Ban 218.92.0.112
2023-07-22 03:39:58,496 fail2ban.actions        [45906]: NOTICE  [sshd] Unban 218.92.0.56
2023-07-22 03:42:42,735 fail2ban.actions        [45906]: NOTICE  [sshd] Unban 143.198.238.143
2023-07-22 03:42:56,782 fail2ban.actions        [45906]: NOTICE  [sshd] Unban 186.155.214.147
2023-07-22 03:43:10,900 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.118 - 2023-07-22 03:43:10
2023-07-22 03:43:13,168 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.118 - 2023-07-22 03:43:13
2023-07-22 03:43:15,699 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.118 - 2023-07-22 03:43:15
2023-07-22 03:43:16,025 fail2ban.actions        [45906]: NOTICE  [sshd] Ban 218.92.0.118
2023-07-22 03:43:36,345 fail2ban.filter         [45906]: INFO    [sshd] Found 61.177.172.136 - 2023-07-22 03:43:36
2023-07-22 03:43:39,045 fail2ban.filter         [45906]: INFO    [sshd] Found 61.177.172.136 - 2023-07-22 03:43:39
2023-07-22 03:43:40,833 fail2ban.filter         [45906]: INFO    [sshd] Found 61.177.172.136 - 2023-07-22 03:43:40
2023-07-22 03:43:41,275 fail2ban.actions        [45906]: NOTICE  [sshd] Ban 61.177.172.136
2023-07-22 03:43:51,340 fail2ban.filter         [45906]: INFO    [sshd] Found 186.155.214.147 - 2023-07-22 03:43:51
2023-07-22 03:43:53,175 fail2ban.filter         [45906]: INFO    [sshd] Found 186.155.214.147 - 2023-07-22 03:43:53
2023-07-22 03:43:53,311 fail2ban.actions        [45906]: NOTICE  [sshd] Ban 186.155.214.147
2023-07-22 03:43:55,966 fail2ban.filter         [45906]: INFO    [sshd] Found 143.198.238.143 - 2023-07-22 03:43:55
2023-07-22 03:43:58,015 fail2ban.filter         [45906]: INFO    [sshd] Found 143.198.238.143 - 2023-07-22 03:43:58
2023-07-22 03:45:21,940 fail2ban.filter         [45906]: INFO    [sshd] Found 143.198.238.143 - 2023-07-22 03:45:21
2023-07-22 03:45:22,045 fail2ban.actions        [45906]: NOTICE  [sshd] Ban 143.198.238.143
2023-07-22 03:45:23,794 fail2ban.filter         [45906]: INFO    [sshd] Found 143.198.238.143 - 2023-07-22 03:45:23
2023-07-22 03:46:07,372 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.56 - 2023-07-22 03:46:07
2023-07-22 03:46:09,460 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.56 - 2023-07-22 03:46:09
2023-07-22 03:46:11,773 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.56 - 2023-07-22 03:46:11
2023-07-22 03:46:12,128 fail2ban.actions        [45906]: NOTICE  [sshd] Ban 218.92.0.56
2023-07-22 03:54:30,068 fail2ban.filter         [45906]: INFO    [sshd] Found 180.101.88.247 - 2023-07-22 03:54:30
2023-07-22 03:54:32,168 fail2ban.filter         [45906]: INFO    [sshd] Found 180.101.88.247 - 2023-07-22 03:54:32
2023-07-22 03:54:34,572 fail2ban.filter         [45906]: INFO    [sshd] Found 180.101.88.247 - 2023-07-22 03:54:34
2023-07-22 03:54:34,797 fail2ban.actions        [45906]: NOTICE  [sshd] Ban 180.101.88.247
2023-07-22 03:58:25,590 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.22 - 2023-07-22 03:58:25
2023-07-22 03:58:27,647 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.22 - 2023-07-22 03:58:27
2023-07-22 03:58:30,023 fail2ban.filter         [45906]: INFO    [sshd] Found 218.92.0.22 - 2023-07-22 03:58:30
2023-07-22 03:58:30,315 fail2ban.actions        [45906]: NOTICE  [sshd] Ban 218.92.0.22
```
