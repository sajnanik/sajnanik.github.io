---
title: "Updating & Patching Linux Systems"
date: 2022-04-24 T19:34:30-04:00
categories:
  - blog
tags:
  - Linux
  - Cybersecurity
  - Tutorials
  - Linux Hardening 101
---
# Updating & Patching Linux Systems
Linux is an Open Source system, which means its available to both, good users & threat actors. Thanks to a large community of IT users, the system is constantly worked on and patches & security updates are released. The moment a new vulnerability is known, it has to published, which brings it to everyones light. 

This is why its very crucial to update and patch your Linux Installations. 

## Keeping Your System Current

Updating your Linux system manually is straightforward. Here's how to do it:
 - **Package List Update:**
   Start by updating the package list to fetch the latest available software versions:
```
sudo apt update
```
- **Upgrade Installed Packages:** 
Once the package list is updated, proceed to upgrade the installed packages:
```
sudo apt upgrade
```
- **Upgrade the Kernel (if needed):** 
To update the Linux kernel, which is a critical component of the OS, use:
```
sudo apt install linux-generic
```
## Enabling Automatic Updates

Enabling automatic updates can streamline the patching process and enhance system security. However, it's important to strike a balance between convenience and control:

- **Considerations for Automatic Updates:**
    
    -   **Security Updates:** Enable automatic updates for security patches to minimize vulnerabilities.
    -   **Regular Monitoring:** Regularly review update logs to ensure updates are proceeding smoothly.
    -   **Testing Environment:** For critical systems, consider testing updates in a controlled environment before deploying them to production.
    
- **Enabling Automatic Updates:** In Ubuntu, you can enable automatic updates using the `unattended-upgrades` package:
```
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades
```

**Note:** While automatic updates can offer convenience and security benefits, there are certain scenarios where you might want to reconsider enabling them. It's important to carefully evaluate your system's requirements and potential risks before deciding to implement automatic updates.

Updating and patching your Linux systems is a fundamental responsibility for maintaining security and performance. By regularly updating packages and enabling automatic updates for critical components, you're actively safeguarding your systems from potential threats. Remember, finding the right balance between automation and manual control is essential for maintaining a secure and stable environment.
