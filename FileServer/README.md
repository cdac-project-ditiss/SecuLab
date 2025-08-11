# 📂 File Server (Samba)

## Overview
The File Server is configured using *Samba* to allow seamless file sharing between Linux and Windows clients within the internal LAN. This enables centralized storage and controlled access to shared resources, ensuring secure and organized data management across the network.

In this project, the file server plays a key role in enabling users from different client systems to upload, download, and collaborate on shared files. The server has been configured with specific share directories, access permissions, and authentication to ensure that only authorized users can access sensitive data.

---

## Purpose
- Provide centralized storage accessible to multiple clients.
- Control access to shared files with authentication and permissions.
- Enable cross-platform sharing between Linux and Windows systems.
- Enhance team collaboration by having a single, secure file repository.

---

## Configuration Flow
The configuration process for the file server is carried out in the following sequence:

1. *Set Hostname*
   - Assign a unique hostname to identify the file server in the network.

2. *Set Static IP Address*
   - Configure a static IP so that clients can consistently connect to the server without IP changes.

3. *Install Samba*
   - Install and configure Samba packages required for file sharing.

4. *Create Shared Directories*
   - Define directories that will be accessible to network users.

5. *Set Directory Permissions*
   - Configure Linux file permissions and Samba-specific access controls.

6. *Configure Samba Users*
   - Add Linux users and map them as Samba users for authentication.

7. *Edit Samba Configuration File*
   - Update /etc/samba/smb.conf with share definitions, permissions, and access restrictions.

8. *Restart Samba Services*
   - Restart smbd and nmbd to apply changes.

9. *Test Access from Clients*
   - Verify that the share is accessible from both Linux and Windows clients.

---

## Key Configuration Files
- /etc/hostname → Defines the hostname for the file server.
- /etc/hosts → Maps the hostname to the server IP.
- /etc/network/interfaces or /etc/sysconfig/network-scripts/ifcfg-* (depending on OS) → Static IP configuration.
- /etc/samba/smb.conf → Main Samba configuration file defining shares and permissions.

---

## Verification
- *Linux Clients* → Use smbclient or mount the share via mount -t cifs.
- *Windows Clients* → Access via \\<file_server_hostname>\<share_name> in File Explorer.
- Ensure authentication prompts and access control work as intended.

---
