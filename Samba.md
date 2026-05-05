# Samba File Server Documentation

## Overview

In this project, I implemented Samba on an Ubuntu server to enable file sharing within a local network. Samba allows different operating systems, such as macOS and Linux, to access shared folders using the SMB protocol.

---

## Purpose

The purpose of using Samba is to:

* Share files between devices on a local network
* Allow clients to access server storage remotely
* Demonstrate file server functionality in a client-server environment

---

## Setup Environment

* Server: Ubuntu (running in UTM virtual machine)
* Client: Mac (Finder)
* Network: Local network using server IP address

---

## Installation and Configuration

### Install Samba on Ubuntu

```bash
sudo apt update
sudo apt install samba -y
```
![Install Samba](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-1.png)
---

### Check Samba Status

```bash
systemctl status smbd
```

The service should show as `active (running)`.
![Check status Samba](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-2.png)

---

### Move default config file to Backup
```bash
sudo systemctl stop smbd
```
![Move the deafult config file to backup](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-3.png)
![Move the deafult config file to backup](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-4.png)
![Move the deafult config file to backup](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-5.png)
---

### Stop Samba 
```bash
sudo systemctl stop smbd
```
![Check status Samba](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-6.png)
---

### Create a new Config File
Now we need to create two config file 1. smb.conf 2. Shares.conf
To create a file 
remember you need to be on the /etc/samba directory
```bash
sudo nano smb.conf
```
copy the code from the image
![smb.conf](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-7.png)
ctrl+0 Enter ctrl+x
---
Create another file 
```bash
sudo nano shares.conf
```
[smb.conf](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-8.png)
copy the code from the image
![smb.conf](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-9.png)
---

### Create Shared Directory

```bash
sudo mkdir -p /share/public_files
sudo mkdir /share/private_files
```

This directory will be used for file sharing.

![shared directory](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-10.png)
![shared directory](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-11.png)
---

### Create Samba User

Create a smbuser (Note: THe user name must be same name which we have used on the config file):

```bash
sudo useradd --system --nocreate-home --group smbgroup -s /binfalse smbuser
```
![samba user](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-13.png)
![samba user](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-13.1.png)
![samba user](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-13.2.png)

---
### Create Samba group

Create a samba group:
```bash
sudo groupadd --system smbgroup
```
![samba group](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-12.png)
![samba group](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-.12.1png)
![samba group](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-.12.2png)

### Grant owner role

Give owner role for the directory:
```bash
sudo chown -R smbuser:smbgroup /share
```
![grant permission](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-14.png)
---

### Directory Permission

modify permission for directory;
```bash
sudo chmod -R g+w /share
```
![grant permission](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-15.png)
---
### Start Samba Service

```bash
sudo systemctl start smbd
```
![Start Samba](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-16.png)
---

## Firewall Configuration

Allow Samba traffic:

```bash
sudo ufw allow 445/tcp
```

---

## Connecting from Mac

In Finder, connect to the server:

![Connect to the server](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-17.png)

```text
smb://server-ip/Shared
```
![Connect with your ip](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-18.png)

Login with:

* Guest: 
![Login ](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-19.png)
![Folder1](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-20.png)
![Folder2](Samba-FTS_Bilder_Dokumentasjon/Samba-FTS-21.png)
---

## How It Works

* Client connects to server using SMB protocol
* Samba authenticates the user
* Access is granted to the shared folder
* Files can be read and written depending on permissions

---

## Testing and Verification

* Connect from Mac using SMB
* Upload and download files
* Verify access is restricted to authorized users

---

## Troubleshooting

If connection fails:

* Check Samba status:

```bash
systemctl status smbd
```

* Restart service:

```bash
sudo systemctl restart smbd
```

* Check firewall:

```bash
sudo ufw status
```

* Verify correct path and permissions

---

## Conclusion

Samba provides a reliable way to share files across different operating systems in a local network. It demonstrates how a file server can be implemented and secured using user authentication and firewall rules.
