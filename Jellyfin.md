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
---
# Configure Jellyfin

After installing Jellyfin, the next step is to configure media directories, permissions and libraries.

---

# Step 1 — Create Media Directories

Create dedicated folders for storing media files.

```bash
sudo mkdir -p /data/media/movies
sudo mkdir -p /data/media/tv
sudo mkdir -p /data/media/music
```

These folders will be used by Jellyfin libraries.

---

# Step 2 — Set Permissions

Give Jellyfin permission to access the media folders.

```bash
sudo chown -R jellyfin:jellyfin /data/media
sudo chmod -R 755 /data/media
```

Explanation:
- `chown` changes ownership to the Jellyfin user
- `chmod 755` gives read and execute permissions

This allows Jellyfin to read and organize media files correctly.

---

# Step 3 — Access Jellyfin in Browser

Find your server IP address:

```bash
ip a
```

Open a web browser and go to:

```bash
http://SERVER-IP:8096
```

Example:

```bash
http://192.168.1.10:8096
```

---

# Step 4 — Complete Initial Setup

When opening Jellyfin for the first time:

1. Create an administrator account
2. Select preferred language
3. Configure media libraries
4. Finish the setup wizard

---

# Step 5 — Add Media Libraries

To add media libraries:

1. Open Dashboard
2. Go to Libraries
3. Click "Add Media Library"
4. Choose media type
5. Select media folder path

Example for music library:

```bash
/data/media/music
```

Example for movies:

```bash
/data/media/movies
```

Example for TV shows:

```bash
/data/media/tv
```

---

# Step 6 — Add Media Files

After creating libraries:

- Copy music files into `/data/media/music`
- Copy movie files into `/data/media/movies`
- Copy TV shows into `/data/media/tv`

---

# Step 7 — Scan Libraries

After adding media files:

1. Go to Dashboard
2. Open Libraries
3. Click "Scan All Libraries"

Jellyfin will now:
- Detect media files
- Download metadata
- Generate posters and thumbnails

---

# Custom Jellyfin Theme (Optional)

Jellyfin supports custom CSS themes.

To change the default interface:

1. Go to Dashboard
2. Open General Settings
3. Find "Custom CSS"

The theme used in this project:

```css
@import url("https://cdn.jsdelivr.net/gh/lscambo13/ElegantFin@main/Theme/ElegantFin-jellyfin-theme-build-latest-minified.css");
```

This changes the default Jellyfin appearance with a cleaner custom design.

---

# Metadata Management

Jellyfin uses metadata to organize media information such as:
- Artist names
- Album covers
- Posters
- Genres
- Release dates

---

# How to Add Metadata Manually

This project uses MusicBrainz for music metadata.

## Step 1 — Open MusicBrainz

Visit:

```bash
https://musicbrainz.org
```

---

## Step 2 — Search for Music

Search for:
- Song name
- Artist
- Album

---

## Step 3 — Copy MBID

Open the song details page and copy the:

```bash
MusicBrainz ID (MBID)
```

---

## Step 4 — Edit Metadata in Jellyfin

Inside Jellyfin:

1. Open the song
2. Click the three dots
3. Select "Edit Metadata"
4. Go to External IDs
5. Paste the MusicBrainz Track ID

Jellyfin will automatically fetch:
- Album artwork
- Artist information
- Metadata details

---

# Adding Lyrics to Music

Jellyfin supports synchronized lyrics using `.lrc` files.

`.lrc` files contain:
- Song lyrics
- Timestamps for each line

This allows lyrics to sync with the music while playing.

---

# Create LRC Lyrics Files

## Step 1 — Open LRC Generator

Visit:

```bash
https://lrcgenerator.com
```

---

## Step 2 — Add Song Information

Enter:
- Song title
- Artist
- Album

---

## Step 3 — Add Lyrics

You can find lyrics from:
- Genius
- Official lyrics websites

Recommended:

```bash
https://genius.com
```

Copy and paste the lyrics into the generator.

---

## Step 4 — Synchronize Lyrics

1. Upload the MP3 file
2. Play the song
3. Click "Next Line" whenever the lyrics change

This creates synchronized timestamps.

---

## Step 5 — Save the LRC File

Important:
- The `.lrc` file and `.mp3` file must have the same filename.

Example:

```bash
song.mp3
song.lrc
```

Save the `.lrc` file inside the music folder.

---

# Install Lyrics Plugin

Inside Jellyfin:

1. Go to Dashboard
2. Open Plugins
3. Install:

```bash
LrcLib Lyrics
```

---

# Refresh Libraries

After adding lyrics:

1. Go to Libraries
2. Click "Scan All Libraries"

Jellyfin will now display synchronized lyrics during music playback.

---

# Features Implemented

- Media streaming
- Music libraries
- Movie libraries
- Metadata management
- Synchronized lyrics
- Custom Jellyfin theme
- Multi-device support
- Web-based administration

---

# Troubleshooting

## Jellyfin Cannot Detect Media

Check folder permissions:

```bash
sudo chown -R jellyfin:jellyfin /data/media
```

---

## Jellyfin Service Not Running

Restart the service:

```bash
sudo systemctl restart jellyfin
```

---

## Check Jellyfin Status

```bash
sudo systemctl status jellyfin
```

---

# Conclusion

This project helped improve understanding of:
- Linux server administration
- Media server management
- File permissions
- Metadata systems
- Self-hosted applications
- Networking and service configuration

Jellyfin proved to be a powerful open-source media server solution for home server environments.