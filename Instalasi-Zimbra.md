# Tutorial Install Single Server Zimbra

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

* Merubah pengaturan hostname :
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
        MX: mail.example.local (192.168.1.192)

        Interface: 127.0.0.1
        Interface: ::1
        Interface: 192.168.1.192
done.
Checking for port conflicts
