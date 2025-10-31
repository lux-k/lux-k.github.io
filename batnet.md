---
layout: default
title: BatNet LXC Notes
---

# Running BattyBirdNet-Pi in LXC

This post documents how I configured **BattyBirdNet-Pi** to run inside an LXC container with an AudioMoth USB mic.

## Requirements
- Proxmox host
- LXC container (Debian 12)
- BattyBirdNet-Pi [https://github.com/rdz-oss/BattyBirdNET-Pi](https://github.com/rdz-oss/BattyBirdNET-Pi)
- [AudioMoth USB ](https://groupgets.com/products/audiomoth-usb-microphone)

### Deploy the LXC
- Deploy a LXC. I typically give 2 CPUs, 2GB RAM and 10GB of disk.
- Unprivilged.
- After the LXC is deployed, I like to allow root SSH and setup the timezone.
- apt-get update && apt-get upgrade

### Begin to modify the LXC
- Install curl, sudo: apt-get install curl sudo
- Add a user: adduser --uid 1000 batnet
- Put the user in the audio group: usermod -aG audio batnet
- Add the user to passwd-less sudo: visudo / add line: batnet ALL=(ALL) NOPASSWD: ALL
- Become the user: su - batnet
- Install (as batnet): curl -s https://raw.githubusercontent.com/rdz-oss/BattyBirdNET-Pi/main/newinstaller.sh | bash
- Wait awhile...
- Go to http://machine/batnet .. you should see a bat at the top

### LXC fun (passthrough)
