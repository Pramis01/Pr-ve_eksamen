# Security Documentation

## Why UFW is Used

UFW (Uncomplicated Firewall) is a firewall management tool for Linux systems.

Using a firewall is important because it helps control which network traffic is allowed to access the server. It also helps improve understanding of how services communicate using different network ports.

In this project, UFW is used to:
- Allow only necessary services
- Block unwanted incoming connections
- Improve server security
- Manage open ports easily
- Create and manage firewall rules

UFW is beginner-friendly because its commands are simple and easy to understand compared to more advanced firewall tools.

By allowing only required ports and blocking unnecessary traffic, the risk of unauthorized access to the server is reduced.

Example:
```bash
sudo ufw allow 8096/tcp
```

This command allows Jellyfin traffic through port 8096.

---

# Open Ports Used in This Project

This project uses multiple services that require specific ports to be opened.

| Service | Port | Purpose |
|---|---|---|
| SSH | 22 | Remote server administration |
| Apache | 80 | Web server access |
| Samba | 445 | File sharing |
| Jellyfin | 8096 | Media server |

Only the required ports are opened to improve security.

If a service is no longer needed, its port can be disabled or blocked.

Example:
```bash
sudo ufw deny 22
```

or completely disable UFW:
```bash
sudo ufw disable
```

Disabling unused ports helps reduce the risk of attacks such as unauthorized SSH login attempts.

---

# Why SSH is Useful

SSH (Secure Shell) is a secure protocol used for remote server administration.

SSH allows administrators to connect to the server remotely through a terminal without requiring physical access to the machine.

Benefits of SSH:
- Secure encrypted connection
- Remote server management
- Easy administration from another device

SSH supports encrypted authentication methods such as:
- Password authentication
- SSH key authentication

SSH key authentication is considered more secure because the connection is encrypted and more resistant to brute-force attacks.

---

# Samba Permissions

In this project, Samba permissions are configured to allow users to read, write and execute files inside shared folders.

Since this is a home lab environment, the shared public folder is configured with read and write permissions to make file sharing easier between devices.

Example permissions:
```bash
chmod -R 755 /data/media
```

This allows:
- Reading files
- Writing files
- Executing files/directories

Permissions can be customized depending on the security requirements of the environment.

For example:
- Public folders can allow read/write access
- Private folders can be configured as read-only
- Sensitive files can be restricted to specific users only

Using proper file permissions helps protect important or confidential data from unauthorized modification or deletion.

---

# Security Considerations

Even in a home lab environment, security is important.

This project demonstrates:
- Basic firewall management
- Port security
- Remote administration security
- Access control
- File permission management

These practices help improve understanding of real-world Linux server administration and cybersecurity fundamentals.