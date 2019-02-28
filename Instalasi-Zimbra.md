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

* Install Paket DNS

```bash
root@mail:~# yum install bind bind-utils -y
root@mail:~# systemctl start named

(Cek apakah sudah berjalan atau belum)

root@mail:~# systemctl status named
root@mail:~# systemctl enable named
```
* Setting konfigurasi buat DNS
```bash
root@mail:~# vi /etc/named.conf
(Bisa dilihat isi filenya yang sudah di upload sesuai dengan nama named.conf)
```
