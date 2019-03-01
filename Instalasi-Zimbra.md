# Tutorial Install Zimbra Single Server

* Spesifikasi Hardware

```bash
 Processor Intel/AMD 64-Bit CPU 1.5 GHz
 RAM single server minimul 6/8 GB
 5 GB free disk untuk software dan logs
```

* Settingan Server

```bash
 Domain = cilebut.co.id
 IP address = 192.168.1.198
 Mail = mail.cilebut.co.id
```

Berikut langkah - langkah instalasi Zimbra Single Server :

Untuk proses instalasi menggunakan super user atau user root

```bash
zimbra@mail:~$ su -
password:
root@mail:~# 
```
* Merubah pengaturan hostname

```bash
 root@mail:~# vi /etc/hostname  
 mail.cilebut.co.id
 
 root@mail:~# vi /etc/hosts  
 192.168.1.198 mail.cilebut.co.id mail
```

* Memnonaktifkan Service Firewall dan Postfix

```bash
root@mail:~# systemctl stop firewalld
root@mail:~# systemctl disable firewalld

root@mail:~# systemctl stop postfix
root@mail:~# systemctl disable postfix
```

## Instalasi DNS 

* Install DNS

```bash
root@mail:~# yum install bind bind-utils -y
root@mail:~# systemctl start named

(Cek apakah sudah berjalan atau belum)
root@mail:~# systemctl status named
● named.service - Berkeley Internet Name Domain (DNS)
   Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2019-02-28 19:38:20 WIB; 42s ago
  Process: 7616 ExecStop=/bin/sh -c /usr/sbin/rndc stop > /dev/null 2>&1 || /bin/kill -TERM $MAINPID (code=exited, status=0/SUCCESS)
  Process: 7627 ExecStart=/usr/sbin/named -u named -c ${NAMEDCONF} $OPTIONS (code=exited, status=0/SUCCESS)
  Process: 7625 ExecStartPre=/bin/bash -c if [ ! "$DISABLE_ZONE_CHECKING" == "yes" ]; then /usr/sbin/named-checkconf -z "$NAMEDCONF"; else echo "Checking of zone files is disabled"; fi (code=exited, status=0/SUCCESS)
 Main PID: 7629 (named)
   CGroup: /system.slice/named.service
           └─7629 /usr/sbin/named -u named -c /etc/named.conf

(Diatas hasil dari service yang sudah berjalan dengan benar)

(Lalu dibuat permanent)
root@mail:~# systemctl enable named
```
* Konfigurasi DNS dan Deklarasi IP dan Domain

```bash
root@mail:~# vi /etc/named.conf
(Bisa dilihat isi filenya yang sudah di upload pada list diatas)

root@mail:~# cd /var/named/
(Buat file yang sudah dideklarasi pada di file named.conf)
```
Setelah di konfigurasi buat DNS, lakukan pengecekan kembali pada service DNS, 
apakah sudah berjalan dengan benar. Caranya yaitu:

```bash
root@mail:~# systemctl restart named
root@mail:~# systemctl status named
● named.service - Berkeley Internet Name Domain (DNS)
   Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2019-02-28 19:38:20 WIB; 42s ago
  Process: 7616 ExecStop=/bin/sh -c /usr/sbin/rndc stop > /dev/null 2>&1 || /bin/kill -TERM $MAINPID (code=exited, status=0/SUCCESS)
  Process: 7627 ExecStart=/usr/sbin/named -u named -c ${NAMEDCONF} $OPTIONS (code=exited, status=0/SUCCESS)
  Process: 7625 ExecStartPre=/bin/bash -c if [ ! "$DISABLE_ZONE_CHECKING" == "yes" ]; then /usr/sbin/named-checkconf -z "$NAMEDCONF"; else echo "Checking of zone files is disabled"; fi (code=exited, status=0/SUCCESS)
 Main PID: 7629 (named)
   CGroup: /system.slice/named.service
           └─7629 /usr/sbin/named -u named -c /etc/named.conf

(Kalo sudah seperti diatas sudah berjalan dengan benar)

(Langkah berikutnya untuk validasi dan pengecekan final, kita cek IP dan Domain sudah saling terhubung atau belum)
root@mail:~# nslookup mail.cilebut.co.id
Server:         192.168.1.198
Address:        192.168.1.198#53

Name:   mail.cilebut.co.id
Address: 192.168.1.198

root@mail:~# nslookup 192.168.1.198
Server:         192.168.1.198
Address:        192.168.1.198#53

192.1.168.198.in-addr.arpa      name = mail.cilebut.co.id.
```
## Instalasi Zimbra

Download paket Zimbra terlebih dahulu 

```bash
root@mail:~# wget https://files.zimbra.com/downloads/8.6.0_GA/zcs-8.6.0_GA_1153.RHEL7_64.20141215151110.tgz
root@mail:~# tar -xzf zcs-8.6.0_GA_1153.RHEL7_64.20141215151110.tgz
root@mail:~# cd zcs-8.6.0_GA_1153.RHEL7_64.20141215151110
```
Sekarang, kita akan install the ZCS package

```bash
[root@mail zcs-8.6.0_GA_1153.RHEL7_64.20141215151110]# ./install.sh

Operations logged to /tmp/install.log.14668
Checking for existing installation...
    zimbra-ldap...NOT FOUND
    zimbra-logger...NOT FOUND
    zimbra-mta...NOT FOUND
    zimbra-dnscache...NOT FOUND
    zimbra-snmp...NOT FOUND
    zimbra-store...NOT FOUND
    zimbra-apache...NOT FOUND
    zimbra-spell...NOT FOUND
    zimbra-convertd...NOT FOUND
    zimbra-memcached...NOT FOUND
    zimbra-proxy...NOT FOUND
    zimbra-archiving...NOT FOUND
    zimbra-core...NOT FOUND


PLEASE READ THIS AGREEMENT CAREFULLY BEFORE USING THE SOFTWARE.
ZIMBRA, INC. ("ZIMBRA") WILL ONLY LICENSE THIS SOFTWARE TO YOU IF YOU
FIRST ACCEPT THE TERMS OF THIS AGREEMENT. BY DOWNLOADING OR INSTALLING
THE SOFTWARE, OR USING THE PRODUCT, YOU ARE CONSENTING TO BE BOUND BY
THIS AGREEMENT. IF YOU DO NOT AGREE TO ALL OF THE TERMS OF THIS
AGREEMENT, THEN DO NOT DOWNLOAD, INSTALL OR USE THE PRODUCT.

License Terms for the Zimbra Collaboration Suite:

http://www.zimbra.com/license/zimbra-public-eula-2-5.html

Do you agree with the terms of the software license agreement? [N] Y

Checking for installable packages

Found zimbra-core
Found zimbra-ldap
Found zimbra-logger
Found zimbra-mta
Found zimbra-dnscache
Found zimbra-snmp
Found zimbra-store
Found zimbra-apache
Found zimbra-spell
Found zimbra-memcached
Found zimbra-proxy


Select the packages to install

Install zimbra-ldap [Y]

Install zimbra-logger [Y]

Install zimbra-mta [Y]

Install zimbra-dnscache [Y] N

Install zimbra-snmp [Y]

Install zimbra-store [Y]

Install zimbra-apache [Y]

Install zimbra-spell [Y]

Install zimbra-memcached [Y]

Install zimbra-proxy [Y]
Checking required space for zimbra-core
Checking space for zimbra-store
Checking required packages for zimbra-store
zimbra-store package check complete.

Installing:
    zimbra-core
    zimbra-ldap
    zimbra-logger
    zimbra-mta
    zimbra-snmp
    zimbra-store
    zimbra-apache
    zimbra-spell
    zimbra-memcached
    zimbra-proxy

The system will be modified.  Continue? [N] Y

Removing /opt/zimbra
Removing zimbra crontab entry...done.
Cleaning up zimbra init scripts...done.
Cleaning up /etc/ld.so.conf...done.
Cleaning up /etc/security/limits.conf...done.

Finished removing Zimbra Collaboration Server.

(Proses di potong)

DNS ERROR resolving MX for mail.cilebut.co.id
It is suggested that the domain name have an MX record configured in DNS
Change domain name? [Yes]
Create domain: [mail.cilebut.co.id] cilebut.co.id
        MX: mail.example.local (192.168.1.198)

        Interface: 127.0.0.1
        Interface: ::1
        Interface: 192.168.1.198
done.
Checking for port conflicts

(Berikut tampilan menu)
Main menu

   1) Common Configuration:
   2) zimbra-ldap:                             Enabled
   3) zimbra-logger:                           Enabled
   4) zimbra-mta:                              Enabled
   5) zimbra-snmp:                             Enabled
   6) zimbra-store:                            Enabled
        +Create Admin User:                    yes
        +Admin user to create:                 admin@cilebut.co.id
******* +Admin Password                        UNSET
        +Anti-virus quarantine user:           virus-quarantine.fsbv7fj6r0@cilebut.co.id
        +Enable automated spam training:       yes
        +Spam training user:                   spam.7xlmrmrh3@cilebut.co.id
        +Non-spam(Ham) training user:          ham.rt_1on1o@cilebut.co.id
        +SMTP host:                            mail.cilebut.co.id
        +Web server HTTP port:                 8080
        +Web server HTTPS port:                8443
        +Web server mode:                      https
        +IMAP server port:                     7143
        +IMAP server SSL port:                 7993
        +POP server port:                      7110
        +POP server SSL port:                  7995
        +Use spell check server:               yes
        +Spell server URL:                     http://mail.cilebut.co.id:7780/aspell.php
        +Enable version update checks:         TRUE
        +Enable version update notifications:  TRUE
        +Version update notification email:    admin@cilebut.co.id
        +Version update source email:          admin@cilebut.co.id
        +Install mailstore (service webapp):   yes
        +Install UI (zimbra,zimbraAdmin webapps): yes

   7) zimbra-spell:                            Enabled
   8) zimbra-proxy:                            Enabled
   9) Enable VMware HA:                        no
  10) Default Class of Service Configuration:
   s) Save config to file
   x) Expand menu
   q) Quit

Address unconfigured (**) items  (? - help) 6


Store configuration

   1) Status:                                  Enabled
   2) Create Admin User:                       yes
   3) Admin user to create:                    admin@cilebut.co.id
** 4) Admin Password                           UNSET
   5) Anti-virus quarantine user:              virus-quarantine.fsbv7fj6r0@cilebut.co.id
   6) Enable automated spam training:          yes
   7) Spam training user:                      spam.7xlmrmrh3@cilebut.co.id
   8) Non-spam(Ham) training user:             ham.rt_1on1o@cilebut.co.id
   9) SMTP host:                               mail.cilebut.co.id
  10) Web server HTTP port:                    8080
  11) Web server HTTPS port:                   8443
  12) Web server mode:                         https
  13) IMAP server port:                        7143
  14) IMAP server SSL port:                    7993
  15) POP server port:                         7110
  16) POP server SSL port:                     7995
  17) Use spell check server:                  yes
  18) Spell server URL:                        http://mail.cilebut.co.id:7780/aspell.php
  19) Enable version update checks:            TRUE
  20) Enable version update notifications:     TRUE
  21) Version update notification email:       admin@cilebut.co.id
  22) Version update source email:             admin@cilebut.co.id
  23) Install mailstore (service webapp):      yes
  24) Install UI (zimbra,zimbraAdmin webapps): yes

Select, or 'r' for previous menu [r] 4

Password for admin@example.local (min 6 characters): [SBmeBXtA] password

Store configuration

   1) Status:                                  Enabled
   2) Create Admin User:                       yes
   3) Admin user to create:                    admin@cilebut.co.id
   4) Admin Password                           set
   5) Anti-virus quarantine user:              virus-quarantine.fsbv7fj6r0@cilebut.co.id
   6) Enable automated spam training:          yes
   7) Spam training user:                      spam.7xlmrmrh3@cilebut.co.id
   8) Non-spam(Ham) training user:             ham.rt_1on1o@cilebut.co.id
   9) SMTP host:                               mail.cilebut.co.id
  10) Web server HTTP port:                    8080
  11) Web server HTTPS port:                   8443
  12) Web server mode:                         https
  13) IMAP server port:                        7143
  14) IMAP server SSL port:                    7993
  15) POP server port:                         7110
  16) POP server SSL port:                     7995
  17) Use spell check server:                  yes
  18) Spell server URL:                        http://mail.cilebut.co.id:7780/aspell.php
  19) Enable version update checks:            TRUE
  20) Enable version update notifications:     TRUE
  21) Version update notification email:       admin@cilebut.co.id
  22) Version update source email:             admin@cilebut.co.id
  23) Install mailstore (service webapp):      yes
  24) Install UI (zimbra,zimbraAdmin webapps): yes

Select, or 'r' for previous menu [r] 21

Version update destination address: [admin@cilebut.co.id] admin@cilebut.co.id

Store configuration

   1) Status:                                  Enabled
   2) Create Admin User:                       yes
   3) Admin user to create:                    admin@cilebut.co.id
   4) Admin Password                           set
   5) Anti-virus quarantine user:              virus-quarantine.fsbv7fj6r0@cilebut.co.id
   6) Enable automated spam training:          yes
   7) Spam training user:                      spam.7xlmrmrh3@cilebut.co.id
   8) Non-spam(Ham) training user:             ham.rt_1on1o@cilebut.co.id
   9) SMTP host:                               mail.cilebut.co.id
  10) Web server HTTP port:                    8080
  11) Web server HTTPS port:                   8443
  12) Web server mode:                         https
  13) IMAP server port:                        7143
  14) IMAP server SSL port:                    7993
  15) POP server port:                         7110
  16) POP server SSL port:                     7995
  17) Use spell check server:                  yes
  18) Spell server URL:                        http://mail.cilebut.co.id:7780/aspell.php
  19) Enable version update checks:            TRUE
  20) Enable version update notifications:     TRUE
  21) Version update notification email:       admin@cilebut.co.id
  22) Version update source email:             admin@cilebut.co.id
  23) Install mailstore (service webapp):      yes
  24) Install UI (zimbra,zimbraAdmin webapps): yes

Select, or 'r' for previous menu [r] 22

Version update source address: [admin@centos7.unixmen.local] admin@cilebut.co.id

Store configuration

   1) Status:                                  Enabled
   2) Create Admin User:                       yes
   3) Admin user to create:                    admin@cilebut.co.id
   4) Admin Password                           set
   5) Anti-virus quarantine user:              virus-quarantine.fsbv7fj6r0@cilebut.co.id
   6) Enable automated spam training:          yes
   7) Spam training user:                      spam.7xlmrmrh3@cilebut.co.id
   8) Non-spam(Ham) training user:             ham.rt_1on1o@cilebut.co.id
   9) SMTP host:                               mail.cilebut.co.id
  10) Web server HTTP port:                    8080
  11) Web server HTTPS port:                   8443
  12) Web server mode:                         https
  13) IMAP server port:                        7143
  14) IMAP server SSL port:                    7993
  15) POP server port:                         7110
  16) POP server SSL port:                     7995
  17) Use spell check server:                  yes
  18) Spell server URL:                        http://mail.cilebut.co.id:7780/aspell.php
  19) Enable version update checks:            TRUE
  20) Enable version update notifications:     TRUE
  21) Version update notification email:       admin@cilebut.co.id
  22) Version update source email:             admin@cilebut.co.id
  23) Install mailstore (service webapp):      yes
  24) Install UI (zimbra,zimbraAdmin webapps): yes

Select, or 'r' for previous menu [r] r

Main menu

   1) Common Configuration:
   2) zimbra-ldap:                             Enabled
   3) zimbra-logger:                           Enabled
   4) zimbra-mta:                              Enabled
   5) zimbra-snmp:                             Enabled
   6) zimbra-store:                            Enabled
   7) zimbra-spell:                            Enabled
   8) zimbra-proxy:                            Enabled
   9) Enable VMware HA:                        no
  10) Default Class of Service Configuration:
   s) Save config to file
   x) Expand menu
   q) Quit

*** CONFIGURATION COMPLETE - press 'a' to apply
Select from menu, or press 'a' to apply config (? - help) a
Save configuration data to a file? [Yes] Yes
Save config in file: [/opt/zimbra/config.23920] Yes
Saving config in /opt/zimbra/config.23920...done.
The system will be modified - continue? [No] Yes

(Proses instalasi dipotong)

Creating galsync account for default domain...done.

You have the option of notifying Zimbra of your installation.
This helps us to track the uptake of the Zimbra Collaboration Server.
The only information that will be transmitted is:
        The VERSION of zcs installed (8.6.0_GA_1153_RHEL7_64)
        The ADMIN EMAIL ADDRESS created (admin@cilebut.co.id)

Notify Zimbra of your installation? [Yes] no
Notification skipped
Setting up zimbra crontab...done.


Moving /tmp/zmsetup01032015-084819.log to /opt/zimbra/log


Configuration complete - press return to exit

(Proses instalasi sudah selesai)
```
Selanjutnya pengecekkan *service* zimbra

```bash
root@mail:~# su - zimbra
[zimbra@mail ~]$ zmcontrol status
Host mail.cilebut.co.id
        amavis                  Running
        antispam                Running
        antivirus               Running
        ldap                    Running
        logger                  Running
        mailbox                 Running
        memcached               Running
        mta                     Running
        opendkim                Running
        service webapp          Running
        snmp                    Running
        spell                   Running
        stats                   Running
        zimbra webapp           Running
        zimbraAdmin webapp      Running
        zimlet webapp           Running
        zmconfigd               Running
```
Tahap terakhir cek zimbra via web browser

```bash
(cek admin)
https://(IP Address):7071

(cek client)
https://(IP Address)
```
Penjelasan:
hahaha
hahaaha

