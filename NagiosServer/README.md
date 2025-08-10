# Nagios Server (nagios.dexter.local)

## Overview
Nagios XI monitoring server for real-time monitoring of all project infrastructure.

## Purpose
- Monitor host and service availability.
- Send email alerts for downtime or threshold breaches.

## Configuration Flow
1. Set hostname
2. Configure static IP
3. Configure timezone data 
4. Install Nagios XI using provided tar.gz installer
5. Create admin user via Web UI
6. Deploy or manually install NCPA agents on hosts
7. Add hosts and services in Web UI
8. Configure email alerts and 2FA