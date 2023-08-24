---
title: "Linux Server Hardening 101 : Using SSH Keys for remote access"
date: 2022-04-21 T19:34:30-04:00
categories:
  - blog
tags:
  - Linux
  - Cybersecurity
  - Tutorials
  - Linux Hardening 101
---

SSH keys are used for secure communication between a client and a server using the SSH (Secure Shell) protocol. SSH keys are a more secure alternative to traditional password-based authentication. The following information is tailored towards Ubuntu systems.

# Understanding the basics

## A Secure Foundation

SSH keys, based on asymmetric encryption, consist of a pair of keys: a private key and a corresponding public key. **The private key remains with you, confidential and is stored securely on the client's device**, while the **public key is stored on the remote servers you want to access**. Authentication occurs through cryptographic operations, lending a level of security far superior to plain text passwords.

## The Vulnerabilities of Traditional Authentication
While servers can be locked down and access can be limited or left behind a firewall and so on, ultimately there is a username and password somewhere. It may be hard for a threat actor to access your server, but when they do, traditional authentication methods, like username and password, possess inherent vulnerabilities that can be exploited by malicious actors. 

Brute force attacks, phishing attempts, and credential stuffing attacks are just a few of the tactics adversaries employ to gain unauthorized access. Moreover, passwords can be compromised through breaches or easily guessed if weak.

## The Strengths of SSH Keys

-   **Elimination of Passwords**: SSH keys negate the need for passwords entirely, thereby eliminating password-related vulnerabilities.
-   **Resistance to Brute Force**: Since private keys are not transmitted, there's no target for brute force attacks.
-   **Two-Factor Authentication (2FA)**: SSH keys can be used alongside passwords or passphrases, adding an extra layer of security.
-   **Limited Attack Surface**: Unlike passwords, which are typed into multiple systems, SSH keys are primarily used for one-to-few authentication, minimizing exposure.
-   **Centralized Key Management**: SSH keys can be centrally managed, making it easier to enforce policies and track access.
-   **Revocation and Rotation**: Keys can be revoked and rotated efficiently, minimizing the impact of lost or compromised keys.

## Weakness of SSH Keys

While the strengths are great, in terms of IT security, always focus on the weaknesses to understand your systems limitations. 

- **Loss or Theft of Private Key:** If your private key is lost or stolen, an attacker could potentially gain unauthorized access to systems that you have access to. It's important to protect your private key with a passphrase and store it securely.

-   **Passphrase Weakness:** If you use a weak or easily guessable passphrase to protect your private key, it can undermine the security provided by SSH keys. Use a strong passphrase to ensure better protection.
    
-   **Key Management Challenges:** Managing a large number of SSH keys across multiple systems can become complex. Proper key rotation, access revocation, and centralized key management are important to prevent unauthorized access.
    
-   **Single Point of Compromise:** If an attacker gains access to your private key and passphrase, they can potentially access all systems associated with that key, making it a single point of compromise.
    
-   **Lack of Immediate Deactivation:** Unlike passwords, which can be changed quickly, revoking access to a compromised SSH key might take longer, especially if the key is distributed across multiple systems.
    
-   **Limited User Accountability:** Since SSH keys don't require frequent authentication like passwords, it might be more difficult to trace actions back to a specific user, especially if passphrase-less keys are used.
    
-   **Key Distribution:** Distributing SSH keys securely to authorized users can be a challenge, particularly in large and dynamic environments.
    
-   **Initial Key Pair Creation:** If the process of generating and distributing the initial key pair is not done securely, it could introduce vulnerabilities.
    
-   **Unprotected Key Storage:** If your private key is stored in an insecure location or transmitted over unencrypted channels, it can be intercepted by attackers.

# **Implementing SSH Key Authentication**
Now that you are aware of the pros and cons of SSH keys, lets have a look at how to create one. 

-   **Key Generation**: Keys are generated using the `ssh-keygen` command. A private key is stored on the client machine, while the public key is deployed to the servers.
-   **Server Configuration**: Public keys are added to the `authorized_keys` file on remote servers to allow key-based authentication for authorized users.
-   **Passphrase Protection**: A passphrase can be added to the private key, enhancing security by requiring an additional layer of authentication.

The code below will generate an RSA keys with a bit length of 2048, you can also swap it for 4096 by changing the number. 
```
ssh-keygen -t rsa -b 2048
```
This command generates both the *private key (`id_rsa`)* and the *public key (`id_rsa.pub`)* in the `~/.ssh/` directory.

**Provide a Passphrase (Optional):** You'll be prompted to provide a passphrase for the private key. While optional, using a passphrase adds an extra layer of security. If you choose to use a passphrase, enter it when prompted.

**View Your Keys:** Once the keys are generated, you can view the contents of the public key using the `cat` command:
```
cat ~/.ssh/id_rsa.pub
```
**Using the Public Key in other remote servers:** To use the SSH key for authentication, you need to copy the public key to the remote server's `~/.ssh/authorized_keys` file. Copy the contents to your local computer on Notepad and create the same name file inside that directory in the destination server. 
**Make sure to delete the copied contents from your local computer.**

**Protect Private Key:** Ensure that your private key (`id_rsa`) is stored securely on your Ubuntu server. Set proper permissions to the private key file to restrict access:
```
chmod 600 ~/.ssh/id_rsa
```
If you are using a SSH Terminal with GUI you can probably load the private key to make the connection to your server. Alternatively, you can use the code below to connect using a bare terminal.  The -i specifies the location of the private key.

```
ssh -i ~/.ssh/id_rsa user@remote_server
```

From now onward, while you will create root users, you should disable those users, harden your server and install the same key on them to access without username/password and avoid having to remember or store the passwords locally. You can instead have one password for your private key which unlocks access to all your servers. 

Remember that SSH keys provide enhanced security for remote access, and their proper management is crucial. Always keep your private key secure and follow best practices for key rotation, passphrase usage, and key distribution.

