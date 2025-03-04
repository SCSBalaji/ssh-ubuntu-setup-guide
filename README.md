# Ubuntu SSH Setup Guide

## 1. Project Title & Description
### Setting Up SSH Server on Ubuntu
This guide provides step-by-step instructions for installing, configuring, and troubleshooting SSH server on Ubuntu systems. Perfect for beginners who want to enable remote access to their Ubuntu machines.

## 2. Table of Contents
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Troubleshooting & FAQs](#troubleshooting--faqs)

## 3. Features
- Secure remote access to your Ubuntu machine
- Command-line based administration
- File transfer capabilities
- Port forwarding and tunneling options

## 4. Prerequisites
- Ubuntu operating system (any recent version)
- Internet connection for package installation
- Administrator (sudo) privileges
- Basic knowledge of terminal commands

## 5. Installation

### Step 1: Check if SSH client is already installed
```bash
ssh
```
> This command checks if the SSH client is installed. If a usage message appears, the client is present.

### Step 2: Check if SSH server is running
```bash
ssh localhost
```
> This connects to your local machine. If you see "do you want to continue" prompt, SSH server is running.

### Step 3: Install SSH server if not present
```bash
sudo apt install openssh-server -y
```
> This installs the OpenSSH server package with automatic confirmation.

### Step 4: Check SSH service status
```bash
sudo systemctl status ssh
```
> This displays the current status of the SSH service. Look for "Active: active (running)".

### Step 5: Enable and start SSH service if not active
```bash
sudo systemctl enable --now ssh
```
> This enables SSH service to start at boot and starts it immediately.

### Step 6: Configure firewall to allow SSH connections
```bash
sudo ufw allow ssh
```
> This adds an exception to the Ubuntu firewall to permit SSH traffic (default port 22).

## 6. Configuration

### Allowing Root Login (if needed)
If you encounter "permission denied" errors when trying to access as root:

```bash
sudo nano /etc/ssh/sshd_config
```
> This opens the SSH server configuration file for editing.

Find the line `#PermitRootLogin prohibit-password`, remove the comment (#) and change it to:
```
PermitRootLogin yes
```
> This enables root login via SSH (note: enabling root login has security implications).

Save the file (Ctrl+X, Y, Enter), then restart SSH service:
```bash
sudo systemctl restart ssh
```
> This applies the new configuration settings.

## 7. Usage

### Connect to your SSH server from another machine
```bash
ssh username@ipaddress
```
> This connects to the SSH server using the default port (22).

### Connect using a custom port
```bash
ssh username@ipaddress -p portnumber
```
> This connects to the SSH server using a specified port number.

### Find your IP address (if you don't know it)
```bash
ip addr show
```
or
```bash
hostname -I
```
> These commands display your network interfaces and IP addresses.

## 8. Troubleshooting & FAQs

### Permission denied errors
If you see "ssh login permission denied please try again":
1. Edit the SSH configuration file as shown in the Configuration section
2. Ensure you're using the correct username and password
3. Check that the SSH service is running properly

### Connection refused errors
If connection is refused:
1. Verify SSH service is running: `sudo systemctl status ssh`
2. Check firewall settings: `sudo ufw status`
3. Ensure you're using the correct IP address and port

### Secure your SSH server
For improved security:
1. Use SSH keys instead of passwords
2. Change the default port number
3. Disable root login when not needed
4. Configure fail2ban to prevent brute force attacks

## 11. Additional Resources
- [OpenSSH Documentation](https://www.openssh.com/manual.html)
- [Ubuntu SSH Documentation](https://ubuntu.com/server/docs/service-openssh)

---

This guide provides the essential steps to get SSH up and running on your Ubuntu system. For advanced configurations or specific use cases, refer to the official documentation linked above.
