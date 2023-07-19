---
title: "OpenVPN Client 3.4 Throws Unsupported Configuration Error"
date: 2023-04-18 T19:34:30-04:00
categories:
  - blog
tags:
  - openVPN
  - Tutorials
---

If you have recently updated your OpenVPN client to version 3, specifically v3.4
you may notice that when attempting to connect to your openVPN server, the client
throws back an error message like the one below. 

![OpenVPN Error](assets/images/OpenVPN%203.4%20Client%20Error.png "OpenVPN 3.4 Client Error")

The first thing is to check the client log. Look for the error UNKNOWN/Unsupported Configuration. 

What follows after the erorr in the log is what is is causing the issue. 

You will have to keep removing the lines which are causing the issue. In my case it was the following two lines:

```
--data-ciphers-fallback 'AES-256-CBC'
block-outside-dns
```

Once you remove these, make sure to check on ipleak.net your IP or DNS is not causing any leak 
of your ISP IP and you are good to go. 