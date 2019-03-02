# Tutorial Instalasi Zimbra di CentOS 7

## Apa itu Zimbra ??

Zimbra merupakan sebuah produk groupware produk Zimbra, Inc, yang terletak di San Mateo, California, Amerika Serikat. Perusahaan ini dibeli oleh Yahoo pada September 2007. Perangkat lunak ini terdiri dari komponen klien dan server. Zimbra tersedia dalam dua versi, yaitu Open Source, dan Komersil. Versi perangkat lunak ini tersedia dari Zimbra untuk diunduh dan digunakan dengan bebas, serta dari mitra resmi Zimbra.([Wikipedia](https://id.wikipedia.org/wiki/Zimbra), 2019)

Zimbra terdiri dari dua yaitu Zimbra Collaboration Suite Network Edition dan Zimbra Collaboration Suite Open Source Edition. Perbedaannya? Perbedaannya tentu terletak pada fasilitas yang diberikan terutama yang berhubungan dengan *proprietary* lain (connector untuk Microsoft Outlook misalnya) dan support yang diberikan.

Zimbra Collaboration Suite kompatibel dengan klien seperti Microsoft Outlook dan Apple Mail, baik melalui kepemilikan konektor, serta open-source Novell Evolution, sehingga email, kontak, dan kalender dapat disetarakan dari ZCS ini ke server. Zimbra juga menyediakan dua arah asli *sync* ke banyak perangkat mobile (Nokia Eseries, BlackBerry, Windows Mobile, iPhone dengan perangkat lunak 2,0).

## Perbedaan Zimbra dengan Mail Server Lain

* Tersedia dalam dua lisensi, mendukung komersil dan *open source*
* Jauh lebih ringan dibandingkan Exchange, jauh lebih lengkap dibandingkan Mdaemon, Qmail maupun Postfix
* Tidak memerlukan lisensi untuk server
* Bisa berjalan pada service port RQM 22, postfix 25, HTTP 80, POP3 110, IMAP 143, LDAP 389, HTTPS 443
* Terdapat fitur calender, sharing folder file, tasks, chat, ssl sni, web administrator
* Sudah terintegrasi dengan anti spam, anti virus dan webmail
* Bisa diakses lokal maupun publik
* Mendukung berbagai tipe dan distro Linux

## Spesifikasi Instalasi Zimbra Single dan Multi Server

* Kebutuhan untuk testing atau percobaan
```bash
 > Intel atau AMD 64 bit CPU 1.5 Ghz
 > Minimal RAM 8 GB ( bisa di sesuaikan 2 GB atau 4 GB juga cukup )
 > Sisakan 5 GB penyimpanan space hdd untuk software dan logs zimbra
```
* Kebutuhan untuk penerapan atau implementasi
```bash 
 > Intel atau AMD 64 bit CPU 2.0 Ghz
 > Minimal RAM 8GB
 > Sisakan 10 GB penyimpanan space hdd untuk software dan logs zimbra
 > Menambah jumlah penyimpanan hdd untuk penyimpanan mail
 > Menonaktifkan atau disable firewall sistem operasi
```

## Tahapan Instalasi

Dibawah ini tahapan instalasi **zimbra zingle server dan multi server** 
- [Instruksi untuk **Zimbra Single Server**](https://github.com/AchmadF22/Tutorial-Zimbra/blob/master/Instalasi-Zimbra.md)
- [Instruksi untuk **Zimbra Multi Server**](https://github.com/AchmadF22/Tutorial-Zimbra/blob/master/Instalasi-Zimbra.md)

