---
title: "Free Wireguard VPN with Oracle"
date: 2023-12-10T22:30:25+11:00
draft: false
categories: [vpn]
tags: [oracle, wireguard, vpn]
images: []
description: Instructions on how to create a wireguard VPN for free with oracle cloud.
---
The following is a summary of my youtube video.

If you need an in depth explanation, please watch the video.

Wireguard is a very fast, and simple to use VPN. With this tutorial, you can set up your own free Wireguard VPN server. You will not be able to change the location of the VPN - make sure you choose the right location when you are setting up your free oracle account. This tutorial is about sensible defaults, not about tweaking the VPN for maximum security. [PiVPN](https://www.pivpn.io/) is an excellent way of installing Wireguard (or OpenVPN), with a good set of sensible configurations, and the option of auto updates.

1. Create an Ubuntu VM. I like to generate the key pair with PuTTYgen.
2. Enable port 51820 on the subnet
3. log into the VM with SSH. I prefer PuTTY.
4. Change to root user with `sudo su`
5. Update the repository listing with `apt update`
6. Upgrade packages with `apt upgrade`
7. Install PIVPN with `curl -L https://install.pivpn.io | bash `
8. Follow the prompts - disable IPv6. Choose wireguard. Choose ubuntu user. Choose your preferred DNS provider. Enable auto updates.
9. Create a user with `pivpn add`. Create a user for every device/person
10. Use `pivpn -qr` to easily transfer a user account key to a mobile device (you must install wireguard on the device first)
11. To transfer the certificates onto your computer. Log into the VM with WinSCP. You can then download the wireguard app for windows/mac.

Make sure you periodically restart the VM so that updates can be installed fully.
