# Web Server + Snort IDS Configuration

## About
The Web Server hosts the primary PHP-based application for the project.  
It is deployed in the **DMZ** network to allow access from both internal LAN and the public WAN (via firewall and port forwarding).  
The server runs **Apache2** for HTTP service and is integrated with **Snort IDS** for intrusion detection.  
This setup allows real-time detection of malicious activities targeting the web application.

---

## Snort Integration
Snort is installed on the same machine as the web server to:
- Detect common web attacks (SQL Injection, XSS, RFI, DoS).
- Monitor and log suspicious HTTP requests.
- Inspect traffic inline for application-layer threats.
- Provide early warning signs for potential intrusion attempts.

Snort runs in **IDS mode**, logging alerts to `/var/log/snort/alert` for review and integration with other monitoring systems.

---

## Configuration Flow
Follow the sequence below for a clean, working setup:

### 1. Change Hostname
Edit `/etc/hostname` and `/etc/hosts` to set the hostname:
```
web.dexter.local
```

### 2. Set Static IP
Edit `/etc/network/interfaces` to assign the static IP:
```
192.168.100.121
```

### 3. Install and Configure Apache2
- Install Apache2.
- Edit `/etc/apache2/apache2.conf` to harden configuration (e.g., disable directory listing).
- Edit `/etc/apache2/sites-available/000-default.conf` to point to your web root.
- Place PHP application files under `/var/www/html`.

### 4. Install and Configure Snort
- Edit `/etc/snort/snort.conf` to set network variables:
  ```
  ipvar HOME_NET 192.168.100.0/24
  ipvar EXTERNAL_NET any
  ```
- Edit `/etc/snort/rules/local.rules` to add detection rules.
- Enable `local.rules` in `snort.conf`.

### 5. Start Services
```
sudo systemctl restart apache2
sudo snort -A console -q -c /etc/snort/snort.conf -i <interface>
```

### 6. Testing
- From a LAN/WAN client, access the web application to confirm normal operation.
- Simulate malicious requests (SQLi, XSS) to verify Snort logs them in `/var/log/snort/alert`.

---

## Files in This Folder
- `hostname` → `/etc/hostname`
- `hosts` → `/etc/hosts`
- `interfaces` → `/etc/network/interfaces`
- `apache2.conf` → `/etc/apache2/apache2.conf`
- `default-ssl.conf` → `/etc/apache2/sites-available/default-ssl.conf`
- `snort.conf` → `/etc/snort/snort.conf`
- `local.rules` → `/etc/snort/rules/local.rules`

---

## Notes
- Always restart Apache after making changes:
  ```
  sudo systemctl restart apache2
  ```
- Snort runs manually in testing, but can be set up as a service for production.
- Keep Snort rules updated to detect the latest attack signatures.
