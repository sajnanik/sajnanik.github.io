---
title: "Disabling Root User & using privileges when required"
date: 2022-04-23 T19:34:30-04:00
categories:
  - blog
tags:
  - Linux
  - Cybersecurity
  - Tutorials
  - Linux Hardening 101
---
# Disabling Root User & using privileges when required

One effective security practice is to disable the root user and create a separate user with the ability to elevate privileges when necessary. This approach minimizes the risk of unauthorized access and enhances overall system security. This falls under User account Management practices.

User account management is a crucial aspect of Linux server administration. Properly managing user accounts helps enhance security, control access, and maintain the integrity of your systems. In this guide, we'll cover essential user account management tasks along with the corresponding commands.

## Understanding the Basics
In Linux, each user account represents a unique identity and has its own set of permissions, settings, and resources. Understanding the basics of users in Linux is crucial for effective system administration and security.

The administrator user, who has power over everything is the user named root. You would not want all services running under this user. You can imagine the things which could go wrong if threat actors gained access to your server.  **Whats more, if you are trying to hack the server, you will attempt to login with what default user? the root user.**

- **User IDs (UIDs):** Every user is assigned a unique User ID (UID). UIDs are numerical identifiers used by the system to differentiate between users. The root user typically has a UID of 0, and regular users have higher UID numbers.
- **Home Directories:** Each user has a home directory where they can store personal files, configuration files, and settings. The home directory is usually located at `/home/username`.
- **User Groups:** User groups are collections of users with similar permissions and privileges. Users can be members of one or more groups. Groups help simplify permission management and access control.
-   **User Privileges:** By default, non-root users have limited privileges to ensure system security. The `sudo` command allows authorized users to execute commands with elevated privileges.
-   **Superuser (Root):** The root user is a special user with complete administrative access and unrestricted permissions. Root can perform any action on the system, which is both powerful and risky.

-   **User Management Commands:**
    
    -   `adduser` or `useradd`: Add new users.
    -   `passwd`: Change or set user passwords.
    -   `userdel`: Remove user accounts.
    -   `usermod`: Modify user account properties.
    -   `groups`: Display a user's group memberships.
    -   `id`: Display a user's UID and GIDs.

## Disabling the Root User

The root user, often referred to as the superuser, has unrestricted access to the entire system. Disabling this account prevents potential attackers from exploiting it directly. Here's how you can disable the root user:

- **Create a New User:**
   First, create a new user with administrative privileges. You can do this using the `adduser` command:

```
sudo adduser adminuser
```
**adminuser** can be replaced with any username you prefer.

- **Grant Sudo Privileges:** To allow the new user to execute commands with elevated privileges, add them to the sudo group:
```
sudo usermod -aG sudo adminuser
```
-   **Set a Strong Password:** Set a strong password for the new user using the `passwd` command:
```
sudo passwd adminuser
```    
-   **Test Sudo Access:** Log in as the new user and test their sudo access:
```
su - adminuser
sudo ls
```
so now, the command sudo allows you to elevate user permissions to be root. Earlier, for example the command to upgrade the system would have been directly imputed as `apt upgrade`. Now instead, you will have to add the sudo prefix like `sudo apt upgrade`

## Enforcing Security and Accountability

By disabling the root user and creating a dedicated user with the ability to elevate privileges, you're taking a proactive step toward better security. With this setup, you'll be able to track actions back to individual users, preventing misuse of the root account and maintaining better accountability.
