# Jellyfin Media Server Documentation

## Overview

In this project, I implemented Jellyfin on an Ubuntu Server to create a self-hosted media server environment.

Jellyfin is an open-source media server application that allows users to organize, manage and stream media such as:
- Music
- Movies
- TV shows
- Videos
- Photos

The Jellyfin server runs locally on the network and is accessible through a web browser or supported client applications.

Default Jellyfin Port:
```bash
8096
```

---

# Purpose

The purpose of using Jellyfin in this project is to:

- Learn how media servers work
- Host media files on a local network
- Stream music and videos across devices
- Practice Linux server administration
- Learn service installation and configuration
- Understand media library management
- Gain experience with self-hosted applications

---

# Setup Environment

| Component | Description |
|---|---|
| Server OS | Ubuntu Server 24 LTS |
| Virtualization Software | UTM |
| Host Machine | macOS |
| Client Devices | Mac, iPhone |
| Network Type | Bridged Network |

---

# Recommended Ubuntu Versions

Before installing Jellyfin, it is recommended to use a stable Ubuntu Server version.

New Ubuntu releases may sometimes experience repository or package compatibility issues.

The following Ubuntu versions are recommended for stable Jellyfin installation:

| Ubuntu Version | Stability | Recommended |
|---|---|---|
| Ubuntu 24.04 LTS | Very Stable | Yes |
| Ubuntu 22.04 LTS | Stable | Yes |
| Ubuntu 20.04 LTS | Stable | Yes |

LTS (Long Term Support) versions are recommended for server environments because they receive long-term security and stability updates.

---

# Installation and Configuration

## Step 1 — Update the System

Update package lists and upgrade existing packages:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Step 2 — Install Curl

Curl is required to download the Jellyfin installation script.

```bash
sudo apt install curl -y
```

---

## Step 3 — Download and Verify the Jellyfin Installation Script

Download the official Jellyfin repository installation script and verify its checksum.

```bash
curl -s https://repo.jellyfin.org/install-debuntu.sh -O
curl -s https://repo.jellyfin.org/install-debuntu.sh.sha256sum -O
sha256sum -c install-debuntu.sh.sha256sum
```

If the checksum verification is successful, the output should display:

```bash
OK
```

---

## Step 4 — Run the Installation Script

Execute the installation script using bash:

```bash
sudo bash install-debuntu.sh
```

This will:
- Add the Jellyfin repository
- Install Jellyfin
- Configure required packages
- Start the Jellyfin service

---

## Step 5 — Check Jellyfin Service Status

Verify that the Jellyfin service is running correctly:

```bash
sudo systemctl status jellyfin
```

If the service is active, the output should display:

```bash
active (running)
```
