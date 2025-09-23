# Nslookup Command Installation and Usage

## 📌 Introduction
nslookup is a network administration command-line tool used for querying the Domain Name System (DNS) to obtain domain name or IP address mapping, or other DNS records.  
It is available on *Windows, macOS, and most Linux distributions*.  

If it’s missing on your Linux system, follow the installation steps below.

---

## ⚙ Installation

### 1. Check Your Linux Distribution
We will cover installation steps for:
- Ubuntu, Debian, Linux Mint, Kali Linux  
- CentOS, Fedora, Red Hat  
- Arch Linux, Manjaro  

### 2. Open Terminal
You need *administrative privileges* (sudo access).

### 3. Install Based on Your Distro

#### ▶ Ubuntu, Debian, Kali Linux, Linux Mint

# Nslookup - Quick Guide

## ⚙ Installation

```bash
# Ubuntu, Debian, Kali, Linux Mint
sudo apt-get update
sudo apt-get install dnsutils

# CentOS, Fedora, Red Hat
sudo dnf install bind-utils

# Older CentOS, Fedora, Red Hat
sudo yum install bind-utils

# Arch Linux, Manjaro
sudo pacman -S dnsutils

# Nslookup - Interactive Example

# Start nslookup in interactive mode
nslookup

# Inside interactive mode, run multiple queries
> example.com
> -type=MX example.com
> -type=NS example.com

# Exit interactive mode
> exit
