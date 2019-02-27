# Tutorial-Zimbra

## Caca Instalasi Zimbra Single Server

    Pada tutorial kali ini kita akan mencoba untuk install zimbra multi server, dimana sebelumnya kita sudah mencoba setting zimbra             standalone disini . 
    Dimana kalo setting standalone artinya semua service zimbra berjalan pada satu mesin yang sama, dan ketika satu mesin tersebut down
    maka kita tidak punya backup lagi dan artinya mail server kita tidak bisa di akses alias Down. 
    tentu tidak lucu server email corporate down karena masalah tersebut. maka untuk mengatasi masalah single point of failure, kita harus
    setting zimbra       
    multi server, artinya nanti untuk beberapa service kita pisah sesuai dengan fungsi dan kegunaan masing-masing. seperti zimbra-ldap,         zimbra-proxy, zimbra-mailbox, zimbra-mta dan lain sebagainya. Untuk lab kali ini akan kita install pada mesin virtual sebagai berikut :

* Zimbra LDAP
* Zimbra Proxy
* Zimbra Mailbox
* Zimbra MTA

