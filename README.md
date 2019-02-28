# Tutorial-Zimbra

## Caca Instalasi Zimbra Single Server

zimbra collaboration suite (ZCS) adalah server email yang bersifat opensource dan free dan memiliki fitur yang sangat bagus untuk enterprise , kampus ataupun komunias.sebenernya zimbra itu hampir sama dengan mail server yang lainnya seperti sendmail,postfix ataupun qmail. dan sebenarnya zimbra memakai mail servernya postfix, namun zimbra memiliki fitur lebih lengkap sehingga sangat recommend untuk kampus, perusahaan ataupun perusahaan yang memiliki user banyak.
    
## Rekomendasi

* Spesifikasi Hardware
```bash
  Processor Intel/AMD 64-Bit CPU 1.5 GHz
  RAM single server minimul 6/8 GB
  5 GB free disk untuk software dan logs
```
* Settingan Server
```bash
  Domain = cilebut.co.id
  IP address = 192.168.1.192
  Mail = mail.cilebut.co.id
```

Berikut langkah - langkah instalasi Zimbra Single Server :

Pertama setting hostname:
```bash
root@ubuntu:~# nano /etc/hostname  
mail.routecloud.idn


