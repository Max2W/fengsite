---
title: "Enabling WSL in Windows 10"
author: "Feng Wang"
date: '2020-05-10'
comments: no
images: null
slug: enabling-wsl-in-windows-10
tags:
- WSL
- Ubuntu
categories: []
---

#### Using the GUI for enabling Windows features

1. Open the Start Menu and search Turn Windows features on or off 
2. Select Windows Subsystem for Linux 
3. Click OK 
4. Restart your computer when prompted

#### Using PowerShell

1. Open PowerShell as Administrator and run:  
    ```Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux```
2. Restart your computer when prompted 

#### Installing Ubuntu on WSL via the Microsoft Store (Recommended)

1. The following Ubuntu releases are available as apps on the Microsoft Store: 

- Ubuntu 16.04 LTS (Xenial) is the first release available for WSL. It supports the x64 architecture only. (offline installer: x64) 
- Ubuntu 18.04 LTS (Bionic) is the current LTS release and the first one supporting ARM64 systems, too. (offline installers: x64, ARM64) 
- Ubuntu (without the release version) always follows the recommended release, switching over to the next one when it gets the first point release. Right now it installs Ubuntu 18.04. 

2. Each app creates a separate root file system in which Ubuntu shells are opened but app updates don’t change the root file system afterwards. Installing a different app in parallel creates a different root file system allowing you to have both Ubuntu LTS releases installed and running in case you need it for keeping compatibility with other external systems. You can also upgrade your Ubuntu 16.04 to 18.04 by running ‘do-release-upgrade’ and have three different systems running in parallel, separating production and sandboxes for experiments. 

REF： [https://wiki.ubuntu.com/WSL](https://wiki.ubuntu.com/WSL) 