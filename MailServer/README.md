# Mail Server (mail.dexter.local)

## Overview
Mail server configured using Postfix and Dovecot to provide internal and external mail delivery for project services.

## Purpose
- Send/receive email for users and system alerts.
- Provide secure IMAP/SMTP access.

## Configuration Flow
1. Set hostname
2. Configure static IP
3. Install Postfix (SMTP) and Dovecot (IMAP/POP3)
4. Configure virtual domains and mailboxes
5. Generate and install SSL certificates
6. Configure mail clients (Thunderbird)
7. Test sending and receiving emails