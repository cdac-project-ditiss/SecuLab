# Database Server (db.dexter.local)

## Overview
The database server stores and manages application data for the project. It is only accessible from the internal LAN and the Web Server for security reasons.

## Purpose
- Provide secure MySQL/MariaDB database services.
- Restrict database access to the web server and authorized LAN developers.

## Configuration Flow
1. Set hostname
2. Configure static IP
3. Install and configure MariaDB/MySQL
4. Create application database and user with restricted host access
5. Import database schema/data
6. Test database access from Web Server