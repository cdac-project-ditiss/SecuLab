# DHCP and DNS Server Configuration

## Configuring DHCP
---

**Package Name:** `dhcpd`  
**Configuration File:** `/etc/dhcp/dhcpd.conf`  
**Working Directory:** `/var/lib/dhcpd`  

### Steps:
```bash
yum install dhcp-server
sudo nano /etc/dhcp/dhcpd.conf
```

While editing `/etc/dhcp/dhcpd.conf`, you can also refer to:
```
/usr/share/doc/dhcp-server/dhcpd.conf.example
```

**Sample Configuration:**
```conf
subnet 192.168.100.0 netmask 255.255.255.0 {
    range 192.168.100.200 192.168.100.250;
    option domain-name-servers 192.168.100.50;
    option routers 192.168.100.1;
    default-lease-time 1200;
    max-lease-time 7200;
}
```

**Start and Configure Firewall:**
```bash
systemctl start dhcpd
firewall-cmd --add-port=67/udp --permanent
```

---

## Configuring DNS
---

**Package Name:** `bind`  
**Configuration File:** `/etc/named.conf`  
**Working Directory:** `/var/named`  

### Steps:
```bash
yum install bind
sudo nano /etc/named.conf
```

**Sample Configuration:**
```conf
options {
    listen-on port 53 { 127.0.0.1; 192.168.100.50; };
    listen-on-v6 port 53 { ::1; };
    directory       "/var/named";
    dump-file       "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    memstatistics-file "/var/named/data/named_mem_stats.txt";
    secroots-file   "/var/named/data/named.secroots";
    recursing-file  "/var/named/data/named.recursing";
    allow-query     { any; 192.168.100.0/24; };
    recursion yes;
    dnssec-validation yes;
    managed-keys-directory "/var/named/dynamic";
    geoip-directory "/usr/share/GeoIP";
    pid-file "/run/named/named.pid";
    session-keyfile "/run/named/session.key";
    include "/etc/crypto-policies/back-ends/bind.config";
};

logging {
    channel default_debug {
        file "data/named.run";
        severity dynamic;
    };
};

zone "." IN {
    type hint;
    file "named.ca";
};

include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";

zone "dexter.local" IN {
    type master;
    file "/var/named/dexter.local.zone";
    allow-update { none; };
};

zone "100.168.192.in-addr.arpa" IN {
    type master;
    file "/var/named/100.168.192.rev.dexter.local.zone";
    allow-update { none; };
};
```

---

### Creating Zone Files:
```bash
cd /var/named
cp named.localhost dexter.local.zone
nano dexter.local.zone
```

**Sample Zone File:**
```dns
$TTL 1D
@       IN SOA  ns1.dexter.local. admin.dexter.local. (
                                2025062601 ; serial
                                1D         ; refresh
                                1H         ; retry
                                1W         ; expire
                                3H )       ; minimum

@       IN      NS      ns1.dexter.local.
ns1     IN      A       192.168.100.50
files   IN      A       192.168.100.221
db      IN      A       192.168.100.122
mail    IN      A       192.168.100.123
@       IN      MX 10   mail.dexter.local.
web     IN      A       192.168.100.121
nagios  IN      A       192.168.100.120
fw      IN      A       192.168.100.1
```

**Set Group Ownership:**
```bash
chgrp named dexter.local.zone
```

---

### Configure `/etc/hosts`:
```conf
192.168.100.50     ns1.dexter.local
192.168.100.220    files.dexter.local
192.168.100.145    db.dexter.local
192.168.100.158    mail.dexter.local
192.168.100.228    web.dexter.local
```

### Configure `/etc/resolv.conf`:
```conf
nameserver 192.168.100.50
```

---

### Start Services and Open Firewall Ports:
```bash
firewall-cmd --add-port=53/udp --permanent
systemctl start named
systemctl status named
```

---

### Test DNS Resolution:
```bash
dig files.dexter.local
dig db.dexter.local
```
