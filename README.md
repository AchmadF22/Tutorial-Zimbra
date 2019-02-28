# Tutorial Instalasi Zimbra Single Server di CentOS 7

## Apa itu Zimbra ??

Zimbra merupakan sebuah produk groupware produk Zimbra, Inc, yang terletak di San Mateo, California, Amerika Serikat. Perusahaan ini dibeli oleh Yahoo pada September 2007. Perangkat lunak ini terdiri dari komponen klien dan server. Zimbra tersedia dalam dua versi, yaitu Open Source, dan Komersil. Versi perangkat lunak ini tersedia dari Zimbra untuk diunduh dan digunakan dengan bebas, serta dari mitra resmi Zimbra.(Wikipedia, 2013)

Zimbra terdiri dari dua yaitu Zimbra Collaboration Suite Network Edition dan Zimbra Collaboration Suite Open Source Edition. Perbedaannya? Perbedaannya tentu terletak pada fasilitas yang diberikan terutama yang berhubungan dengan *proprietary* lain (connector untuk Microsoft Outlook misalnya) dan support yang diberikan.

Zimbra Collaboration Suite kompatibel dengan klien seperti Microsoft Outlook dan Apple Mail, baik melalui kepemilikan konektor, serta open-source Novell Evolution, sehingga email, kontak, dan kalender dapat disetarakan dari ZCS ini ke server. Zimbra juga menyediakan dua arah asli *sync* ke banyak perangkat mobile (Nokia Eseries, BlackBerry, Windows Mobile, iPhone dengan perangkat lunak 2,0).

## Perbedaan Zimbra dengan Mail Server Lain

* Tersedia dalam dua lisensi, support komersil dan *open source*
* Jauh lebih ringan dibandingkan Exchange, jauh lebih lengkap dibandingkan Mdaemon, Qmail maupun Postfix
* Tidak memerlukan lisensi untuk server
* Bisa berjalan pada service port RQM 22, postfix 25, HTTP 80, POP3 110, IMAP 143, LDAP 389, HTTPS 443
* Terdapat fitur calender, sharing folder file, tasks, chat, ssl sni, web administrator
* Sudah terintegrasi dengan anti spam, anti virus dan webmail
* Bisa diakses lokal maupun publik
* Mendukung berbagai tipe dan distro Linux

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
