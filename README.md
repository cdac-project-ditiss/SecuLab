# SecuLab – Deployment of a Secure and Monitored Infrastructure Using Virtualization

Implemented a basic enterprise-style network infrastructure using VMware, consisting of layered architecture with DMZ and internal LAN. Configured essential servers including Web, Mail, DNS, DHCP, Database, and File Server using Debian and Rocky Linux. Integrated Nagios XI for service monitoring and alerting via email. SSL certificates were generated using XCA to enable secure communication between services. Included Snort-based IDS and FortiGate firewall (evaluation VM) to demonstrate traffic inspection, port forwarding, and policy-based access control.

Group Members

| Name            | Batch | Roll Number | PRN Number   | Phone Number | Email                      |
| --------------- | ----- | ----------- | ------------ | ------------ | -------------------------- |
| Chinmay Patil   | C2    | 89533       | 250244223012 | 8459100845   | chinmaypatilblog@gmail.com |
| Manu Sharma     | C2    | 89844       | 250244223028 | 8826375952   | msharma20103@gmail.com     |
| Vaishnavi Mehar | C2    | 89451       | 250244223054 | 8698581486   | meharvaishnavi6@gmail.com  |
| Aparna Korade   | C2    | 89688       | 250244223023 | 9834588768   | aparnakorade.ajk@gmail.com |


### **Sequence for Project Setup**

1. ### `01_DHCP_and_DNS_Server.md`
    - Sets up hostname, static IP
    - Provides dynamic IPs to clients (via DORA process)
    - Resolves all internal domain names (e.g., `web.dexter.local`, `mail.dexter.local`, etc.)

2. ### `02_Mail_Server.md`
    - Configures Postfix & Dovecot for sending/receiving internal mail
    - Important for Nagios alerts and user notifications

3. ### `03_File_Server.md`
    - Central location for internal file sharing and uploads
    - Used by users or admins to exchange resources

4. ### `04_Database_Server.md`
    - Hosts the database required by the PHP web application
    - Access restricted to internal network and web server only

5. ### `05_Web_Server.md`
    - Configures Apache + PHP web application
    - Connected to DB server internally
    - Resides in DMZ, externally accessible through firewall port forwarding

6. ### `06_Snort_IDS_on_Web_Server.md`
    - Configures Snort IDS on the same machine as the web server
    - Helps detect threats to the web app (SQLi, XSS, floods, etc.)        

7. ### `07_Nagios_XI_Monitoring_Server.md`
    - Monitors all above servers and services
    - Sends alerts via email
    - Uses agent-based and agentless methods for health checks

8. ### `08_Firewall_FortiGate_Setup.md`
    - Final security layer
    - Controls traffic between WAN and LAN/DMZ
    - Configures port forwarding, DMZ, access control, and security policies