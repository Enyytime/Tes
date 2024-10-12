## Find your topology here!

- Link: https://drive.google.com/drive/folders/1ECQD6-cQkg0DzyflG-jSxJZaGaxg0KSU?usp=sharing

- Topology distribution for groups: https://docs.google.com/spreadsheets/d/1QKEZjixTStNbdXznOalJoJS0UQ6ed23o51pP8t8eAIM/edit?gid=1757558734#gid=1757558734

## Put your topology config image here!

`Put image in here`
![image](https://github.com/user-attachments/assets/d6c6a306-edc3-401f-a254-af52cd3b0543)

# ALL OF THE SCRIPTS ARE ALL BELOW AT THE MOST BOTTOM AFTER NUMBER 20
## Also i put the script in root, but just incase
<br>

## Soal 1

> Topologi terdiri dari node Wortel yang berupa DNS Master*. Selain itu, terdapat pula node Pokcoy sebagai DNS Slave*, yang bertugas sebagai cadangan dari node Wortel.
> <br> </br>
> Selanjutnya terdapat node Tomat dan Taoge yang bekerja sebagai Client*, tiga buah Web Server* yaitu Bayam, Buncis, dan Brokoli, serta Mayur sebagai Router*. Buatlah topologi sesuai dengan pembagian topologi [di sini](https://docs.google.com/spreadsheets/d/1QKEZjixTStNbdXznOalJoJS0UQ6ed23o51pP8t8eAIM/edit?usp=sharing) dan konfigurasi topologi [di sini](https://drive.google.com/drive/folders/1ECQD6-cQkg0DzyflG-jSxJZaGaxg0KSU?usp=sharing). Pastikan bahwa setiap node dapat terhubung ke Internet.

> _The topology consists of a Wortel node which is a DNS Master*. In addition, there is also a Pokcoy node as a DNS Slave*, which serves as a backup for the Wortel node._
> <br> </br>
> _Furthermore, there are Tomat and Taoge nodes that work as Client*, three Web Servers*, namely Bayam, Buncis, and Brokoli, then finally Mayur as Router*. Make a topology according to the topology division [here](https://docs.google.com/spreadsheets/d/1QKEZjixTStNbdXznOalJoJS0UQ6ed23o51pP8t8eAIM/edit?usp=sharing) and the topology configuration [here](https://drive.google.com/drive/folders/1ECQD6-cQkg0DzyflG-jSxJZaGaxg0KSU?usp=sharing). Make sure that each node can connect to the Internet._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/af21b525-37d6-48bb-aeb3-652917bcff13)


- Explanation

  `No need for explanation as we just follow what is the picture is telling us to do`

<br>

## Soal 2

> Tambahkan konfigurasi untuk domain bayam.yyy.com yang mengarah ke IP node Bayam di DNS Master. Dengan cara yang sama, buat konfigurasi domain brokoli.yyy.com yang mengarah ke IP node Brokoli dan domain buncis.yyy.com yang mengarah ke IP node Buncis. Simpan semua konfigurasi dalam folder Jarkom. Selama pengerjaan soal, ubah yyy menjadi kode kelompok masing-masing (contoh: A02).
> <br> </br>
> Jangan lupa update konfigurasi kedua client agar dapat berkomunikasi dengan semua domain tersebut.


> _Add a configuration for bayam.yyy.com domain that points to the Bayam node IP in the DNS Master. In the same way, create a brokoli.yyy.com domain configuration that points to the Brokoli node IP and a buncis.yyy.com domain that points to the Buncis node IP. Save all configurations in a folder called Jarkom. For this practicum, substitute yyy with the code of each group (ex: A02).
> <br> </br> 
> Don't forget to update the configuration of both clients so that they can communicate with the domains._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/1f16b466-145e-4861-9002-65cc477d86e2)
  ![image](https://github.com/user-attachments/assets/501953bd-62aa-4dc7-901a-bcc8b2bed52f)
  ![image](https://github.com/user-attachments/assets/e5b6f4ce-459e-4b9c-949f-249d8eabd9f5)
  ![image](https://github.com/user-attachments/assets/10d82705-b9d3-4a53-8770-89392390e241)
  ![image](https://github.com/user-attachments/assets/66ef67d4-d731-4527-ac75-ed945af614c4)
  ![image](https://github.com/user-attachments/assets/46070b49-7f36-431e-bb12-998b5b749f05)







- Explanation

  `Put your explanation in here`
### 1st step
first thing, go to `WortelDNSMaster` you have to make the domain in the `nano /etc/bind/named.conf.local` then configure it by writing 3 zones for `brokoli`, `bayam`, and `buncis` and fill them with their respective IP inside `named.conf.local`
```
zone "bayam.U25.com" {
    type master;
    file "/etc/bind/jarkom/bayam.U25.com";
};

zone "brokoli.U25.com" {
    type master;
    file "/etc/bind/jarkom/brokoli.U25.com";
};

zone "buncis.U25.com" {
    type master;
    file "/etc/bind/jarkom/buncis.U25.com";
};
```
make a jarkom file insdies /etc/bind
```
mkdir /etc/bind/jarkom

```
### 2nd Step
then you can configure it by copying a file called `dc.local` in the `/etc/bind` to the jarkom file we just made and name it `brokoli`, `bayam`, and `buncis`
```
cp /etc/bind/db.local /etc/bind/jarkom/brokoli.U25.com
cp /etc/bind/db.local /etc/bind/jarkom/bayam.U25.com
cp /etc/bind/db.local /etc/bind/jarkom/buncis.U25.com
```
then open `brokoli`, `bayam`, and `buncis` and then fill it accordingly
with ```nano /etc/bind/db.local /etc/bind/jarkom/brokoli.U25.com```
#### Bayam
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     bayam.U25.com. root.bayam.U25.com. (
                        2024011025      ; Serial
                        7200            ; Refresh
                        1800            ; Retry
                        1209600         ; Expire
                        43200 ) ; Negative Cache TTL
;
@       IN      NS      bayam.U25.com.
@       IN      A       10.63.3.5
www     IN      CNAME   bayam.U25.com.
```
#### Buncis
```

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     buncis.U25.com. root.buncis.U25.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      buncis.U25.com.
@       IN      A       10.63.3.4
```
#### Brokoli
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     brokoli.U25.com. root.brokoli.U25.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      brokoli.U25.com.
@       IN      A       10.63.3.3
www     IN      CNAME   brokoli.U25.com.
```

### 3rd Step
makesure you go to to `TomatClient` or `TaugeClient` and configure the `cat /etc/resolv.conf` to fill it with the IP of `WortelDNSMaster`
IP of WortelDNSMaster
```
nameserver 10.63.2.2 
```
after that you can
```
ping brokoli.U25.com
```
<br>

## Soal 3

> Tambahkan domain alias berupa www.bayam.yyy.com pada alamat bayam.yyy.com dan www.brokoli.yyy.com pada alamat brokoli.yyy.com.

> _Add a domain alias in the form of www.bayam.yyy.com to the bayam.yyy.com address and www.brokoli.yyy.com to the brokoli.yyy.com address._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/e068ff86-55ca-4c14-9611-873f97a72941)
  ![image](https://github.com/user-attachments/assets/8af23cf2-7de4-41aa-9d3d-ed74a6b3f0b5)


- Explanation

  `Put your explanation in here`
### First Step
- Open the worteldnsmaster
- Open the brokoli configuration file
  ```
  /etc/bind/jarkom/brokoli.U25.com
  ```
- modify it accordingly by adding a CNAME record (Aliases)
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     brokoli.U25.com. root.brokoli.U25.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@               IN      NS      brokoli.U25.com.
@               IN      A       10.63.3.3
www             IN      CNAME   brokoli.U25.com.
```
- Final step, restart the DNS, adn then ping from TomatClient
```
service bind9 restart
```
```
ping www.brokoli.U25.com
```
![image](https://github.com/user-attachments/assets/6e16efb0-b5c6-4906-a4cb-41914e20992e)


### Repeat on bayam
## Soal 4

> Tambahkan record reverse domain untuk domain brokoli.yyy.com dan buncis.yyy.com.

> _Add a reverse domain record for brokoli.yyy.com and buncis.yyy.com domains._

**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/fe51a120-455b-44b8-80d1-732897df93c2)

- Explanation

  `Put your explanation in here`
### First Step
- first go to WortelDNSMaster
- then go to the `named.conf.local' files
```
nano /etc/bind/named.conf.local
```
- modify it accordingly, add this code, then save it
```
zone "3.63.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/3.63.10.in-addr.arpa";
};
```
- copy this file
```
cp /etc/bind/db.local /etc/bind/jarkom/3.63.10.in-addr.arpa
```
- edit `/etc/bind/jarkom/3.63.10.in-addr.arpa` file accordingly
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     ns.U25.com. root.U25.com. (
                              3         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.63.10.in-addr.arpa.   IN      NS      ns.U25.com.
3                       IN      PTR     brokoli.U25.com.
4                       IN      PTR     buncis.U25.com.

```
- restart the DNS
```
service bind9 restart
```
- To check if it works, go to the client and
```
apt-get update
apt-get install dnsutils

host -t PTR "10.63.3.2" // ip Brokoli
```
### Repeat Buncis
<br>

## Soal 5

> Ubah record SOA dari domain bayam.yyy.com sesuai dengan ketentuan berikut:
> - Lama waktu server slave menunggu untuk mengecek salinan baru server master adalah sebesar 2 jam.
> - Field yang mengatur revisi file zona ini diubah menjadi tanggal awal praktikum (format YYYYMMDD) kemudian diikuti dengan nomor kelompok (contoh untuk kelompok A02 maka nomornya 02).
> - Lamanya waktu server harus menunggu untuk meminta pembaruan lagi dari nameserver master yang tidak responsif sebesar 30 menit.
> - Lama waktu nama domain di-cache secara lokal sebelum kadaluarsa dan kembali ke nameserver otoritatif untuk informasi terbaru sebesar 12 jam.
> - Jika server slave tidak mendapatkan respons dari server master dalam waktu 2 minggu, server tersebut harus berhenti merespons kueri untuk zona tersebut.

> _Change the SOA record of the bayam.yyy.com domain according to the following conditions:_
> - The length of time the slave server waits to check for a new revision of the master server is 2 hours.
> - The field that regulates the revision of this zone file is changed to the start date of the practicum (YYYYMMDD format) then followed by the group number (ex: for A02 the group number would be 02).
> - The length of time the server has to wait to request another update from an unresponsive master nameserver is 30 minutes.
> - The length of time a domain name is cached locally before it expires and returns to an authoritative nameserver for up-to-date information is 12 hours.
> - If the slave server does not get a response from the master server within 2 weeks, it must stop responding to queries for that zone.

**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/da3c6846-e999-42b5-9cef-b0ba2cd296ac)

- Explanation

  `Put your explanation in here`
### First Step
- go to WortelDNSMaster
- go to Bayam's configuration
```
nano /etc/bind/jarkom/bayam.U25.com
```
- Just do this 
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     bayam.U25.com. root.bayam.U25.com. (
                        2024011025      ; Serial
                        7200            ; Refresh
                        1800            ; Retry
                        1209600         ; Expire
                        43200 ) ; Negative Cache TTL
;
@       IN      NS      bayam.U25.com.
@       IN      A       10.63.3.5
www     IN      CNAME   bayam.U25.com.
```
<br>

## Soal 6

> Untuk menangani request yang berlebih dari client ke ketiga alamat yang tadi dibuat, konfigurasikan node Pokcoy sebagai DNS Slave yang bekerja untuk DNS Master Wortel.

> _To handle excess requests from the client to the three addresses created, configure the Pokcoy node as the DNS Slave that works for Wortel DNS Master._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  - Brokoli i already modified so it's according to number 6, but the other's are correct
  ### named.conf from Wortel
  ![image](https://github.com/user-attachments/assets/71da47c0-2ef4-48bd-88c8-c1b608e6d5ac)
  ### named.conf from Pakcoy
  ![image](https://github.com/user-attachments/assets/dc12ad3d-81b2-4a11-bb9e-39dcf00b4e17)
  ### The SOA of wortel and pakcoy
  ![image](https://github.com/user-attachments/assets/0ce74f65-134f-419d-920e-7cfa51b6738f)

  ![image](https://github.com/user-attachments/assets/9d1567f5-4555-40d8-b9e9-737fd5442455)



- Explanation

  `Put your explanation in here`
#### First Step
- Go to WortelDNSMaster's Terminal
- open this file
```
nano /etc/bind/named.conf.local
```
### Second Step modify the code so it can be a DNS Slave
- Copy paste this, 
```
zone "bayam.U25.com" {
    type master;
    also-notify { 10.63.3.2; };
    allow-transfer { 10.63.3.2; };
    file "/etc/bind/jarkom/bayam.U25.com";
};

zone "brokoli.U25.com" {
    type master;
    also-notify { 10.63.3.2; };
    allow-transfer { 10.63.3.2; };
    file "/etc/bind/jarkom/brokoli.U25.com";
};

zone "buncis.U25.com" {
    type master;
    also-notify { 10.63.3.2; };
    allow-transfer { 10.63.3.2; };
    file "/etc/bind/jarkom/buncis.U25.com";
};

zone "3.63.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/3.63.10.in-addr.arpa";
};
```
### Third Step 
- Restart the DNS
```
service bind9 restart
```
- go to PakcoyDNSMaster's Terminal
- do some installation in Pakcoy
```
apt-get update
apt-get install bind9 -y
```
- open the `/etc/bind/named.conf.local` file
```
nano /etc/bind/named.conf.local
```
- then modify it accordingly inside Pakcoy's `/etc/bind/named.conf.local`
```
zone "brokoli.U25.com" {
    type slave;
    masters { 10.63.2.2; };
    file "/etc/bind/delegasi/brokoli.U25.com";
};

zone "buncis.U25.com" {
    type slave;
    masters { 10.63.2.2; };
    file "/var/lib/bind/buncis.U25.com";
};

zone "bayam.U25.com" {
    type slave;
    masters { 10.63.2.2; };
    file "/var/lib/bind/bayam.U25.com";
};
```
- restart
```
service bind9 restart
```
### Last step test it
- at WortelDNSMater stop the service
```
service bind9 stop
```
- go to Tomat or Tauge Client
- dont forget to add this in the `resolv.conf`
![image](https://github.com/user-attachments/assets/30828d33-2699-48ab-bdb0-5fabb48345df)
- then `ping brokoli.U25.com` or any other web servers
<br>

## Soal 7

> Karena membutuhkan tempat untuk menyimpan resep brokoli, buatlah subdomain berupa vitamin.brokoli.yyy.com dengan alias www.vitamin.brokoli.yyy.com dengan mendelegasikannya dari Wortel ke Pokcoy dengan alamat IP menuju Brokoli yang diatur di folder Vitamin.

> _Since we need a place to store Brokoli recipes, create a subdomain in the form of vitamin.brokoli.yyy.com with an alias of www.vitamin.brokoli.yyy.com by delegating it from Wortel to Pokcoy with an ip to the Brokoli node in a folder called Vitamin._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  - there's already number's 8 config,  but it's still work
  ![image](https://github.com/user-attachments/assets/2506bf27-3c42-4ca4-ac9e-39e6bcbb38bd)
  ![image](https://github.com/user-attachments/assets/5b80d751-f864-4412-9995-b75a71b8ad7a)
  ### same config for named.conf.options
  ![image](https://github.com/user-attachments/assets/03803d53-8cc5-4abf-858c-3dc75396d7b0)


- Explanation

  `Put your explanation in here`
### First Step
- go to WortelDNSMaster's Terminal
- open up `/etc/bind/jarkom/brokoli.U25.com`
- add `ns1`, with an ip of 10.63.3.2 (Pakcoy's ip), and `vitamin`, indicating that it's gonna be delegated to Pakcoy at the SOA Configuration
```
ns1             IN      A       10.63.3.2
vitamin         IN      NS      ns1
```
- Full result:
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     brokoli.U25.com. root.brokoli.U25.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@               IN      NS      brokoli.U25.com.
@               IN      A       10.63.3.3
www             IN      CNAME   brokoli.U25.com.
ns1             IN      A       10.63.3.2
vitamin         IN      NS      ns1

```
- Then edit the file /etc/bind/named.conf.options in WortelDNSMaster.
```
nano /etc/bind/named.conf.options
```
Then comment `dnssec-validation auto;` and add the following line to `/etc/bind/named.conf.options`
```
allow-query{any;};
```
![image](https://github.com/user-attachments/assets/24b8aaf6-f6fb-4329-8c9a-c8768f27694f)
- Then, restart bind9
```
service bind9 restart
```
- Then edit the /etc/bind/named.conf.local file, change Brokoli to:
```
zone "brokoli.U25.com" {
    type master;
    file "/etc/bind/jarkom/brokoli.U25.com";
    allow-transfer { 10.63.3.2; };
};
```
![image](https://github.com/user-attachments/assets/0323c3df-1f9d-4d25-811d-3575b614a85a)

### Second Step (Pakcoy's Step)
- Got to Pakcoy Terminal
- Then edit the file /etc/bind/named.conf.options in PakcoyDNSMaster.
```
nano /etc/bind/named.conf.options
```
Then comment `dnssec-validation auto;` and add the following line to `/etc/bind/named.conf.options`
```
allow-query{any;};
```
![image](https://github.com/user-attachments/assets/24b8aaf6-f6fb-4329-8c9a-c8768f27694f)
- Then edit the /etc/bind/named.conf.local file, change Brokoli to:
```
zone "vitamin.brokoli.U25.com" {
    type master;
    file "/etc/bind/delegasi/vitamin.brokoli.U25.com";
};
```
- Then create a directory with the name delegasi
```
mkdir /etc/bind/delegasi
```
- Copy db.local to the delegasi directory and edit the name to vitamin.brokoli.U25.com
```
cp /etc/bind/db.local /etc/bind/delegasi/vitamin.brokoli.U25.com
```
- Then edit the vitamin.brokoli.U25.com file to be like this
![image](https://github.com/user-attachments/assets/f35e48fd-aa76-433c-a454-f28d3d4cf66e)

### Testing
- restart bind
```
service bind9 restart
```
- go to Tomat and ping vitamin.brokoli.U25.com and www.vitamin.brokoli.U25.com
![image](https://github.com/user-attachments/assets/94b584d8-4b9f-4162-b4a5-6bfa54d4ade9)

<br>

## Soal 8

> Buatlah subdomain khusus untuk kandungan brokoli dengan akses k1.vitamin.brokoli.yyy.com dengan alias www.k1.vitamin.brokoli.yyy.com yang mengarah ke IP brokoli dan diatur di folder k1.  

> _Create a special subdomain for Brokoli content called k1.vitamin.brokoli.yyy.com with an alias called www.k1.vitamin.brokoli.yyy.com that point to Brokoli node and are organized in a folder called k1._

**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/f0181b48-bc6a-47fb-906e-02b92b811517)
![image](https://github.com/user-attachments/assets/51fa0743-3ead-4587-9fb3-42073b6cce4d)


- Explanation

  `Put your explanation in here`
### First Step
First thing you have to do is make a subdomain for `k1.vitamin.brokoli.U25.com` and then make the aliases `www.k1.vitamin.brokoli.U25.com` in the `/etc/bind/delegasi/vitamin.brokoli.U25.com`

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     vitamin.brokoli.U25.com. root.vitamin.brokoli.U25.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      vitamin.brokoli.U25.com.
@       IN      A       10.63.3.3
WWW     IN      CNAME   vitamin.brokoli.U25.com.
k1      IN      A       10.63.3.3
www.k1  IN      CNAME   k1.vitamin.brokoli.U25.com.
```
### Second Step
next you got to download apache, php on `Brokoli`. and lynx on `TomatClient`
```
apt-get update
apt-get install apache2
apt-get install php
```

### Third Step
Go back to `BrokoliWebServer`
- Create Directories for the Subdomain: First, create separate directories for  your subdomain (e.g.,k1.vitamin.brokoli.u25.com). These directories will hold the respective content for each domain.
- Copy file `000-default.conf` to `file k1.vitamin.brokoli.U25.com.conf`
```
cp 000-default.conf k1.vitamin.brokoli.U25.com.conf
```
Just an example from the module
![image](https://github.com/user-attachments/assets/224c9b6a-c299-4a4a-985b-d8f416692fee)

- Open the file, and then fill this
  ```
  <VirtualHost *:80>
        #ServerName www.example.com

        ServerName k1.vitamin.brokoli.U25.com
        ServerAlias www.k1.vitamin.brokoli.U25.com
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/k1.vitamin.brokoli.U25.com

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>
  ```
- just for testing we can do
```
echo "Hello, K1 Vitamin!" > /var/www/k1.vitamin.brokoli.U25.com/index.html
```
- then save the configuraiton
```
a2ensite k1.vitamin.brokoli.U25.com
```
- start the apache serve
```
service apache2 reload
```
![image](https://github.com/user-attachments/assets/dfe05e0f-05d9-4262-ac50-5c900b80bdf7)
### Testing
- Go to wortel. and then see the webserver with lynx
```
lynx k1.vitamin.brokoli.U25.com
```
<br>

## Soal 9

> Bayam, Brokoli, dan Buncis masing-masing berfungsi sebagai web server nginx yang menyajikan resep khusus untuk jenis sayuran yang mereka tangani. Untuk mengaktifkan web server pada masing-masing worker, lakukan deployment website menggunakan sumber yang tersedia di sayur_webserver_nginx. Tambahkan konfigurasi untuk log error ke file /var/log/nginx/error.log dan log access ke file /var/log/nginx/access.log.

> _Bayam, Brokoli, and Buncis each function as nginx web servers that serve special recipes for the type of vegetables they handle. To activate the web server on each worker, do the deployment using the resources available in sayur_webserver_nginx. Add configuration for error log to the file /var/log/nginx/error.log and access log to the file /var/log/nginx/access.log._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/911e5bad-cbf5-41c1-869f-0d4bd39b7e47)
  ![image](https://github.com/user-attachments/assets/d6feb61f-c246-45bd-9ea1-b32be024b457)


- Explanation

  `Put your explanation in here`
  ### First Step (Downloading)
- First thing download the necessary things that you needed in all of the web server
  ```
  apt-get update && apt install nginx php php-fpm -y
  ```
- then download the nescessary resources from `sayur_webserver_nginx`
```
wget --no-check-certificate "https://docs.google.com/uc?export=download&id=1tFDk7pKRQLd3BMUcyvfAfEL-drvIxdSl" -O sayur_webserver_nginx.zip
```
- download unzip
```
apt install unzip
```
- unzip it
```
unzip sayur_webserver_nginx.zip
```
### Configuring the NginX
- Make the necessary directory on every single webserver and do it accordinly 
```
// make it diffrent cuz idk will it crash with the apache or not
mkdir -p /var/www/Bayam // on BayamWebServer
mkdir -p /var/www/Brokoli // on BrokoliWebServer
mkdir -p /var/www/Buncis // on BuncisWebServer
```

- Deply the web files
```
cp -r sayur_webserver_nginx/* /var/www/Bayam
cp -r sayur_webserver_nginx/* /var/www/Brokoli
cp -r sayur_webserver_nginx/* /var/www/Buncis
```
### Editing the Conf Files
- CreateConfiguration:
```
nano /etc/nginx/sites-available/Brokoli
```
- Fill it accordingly
```
server {

        listen 80;

        root /var/www/Brokoli;

        index index.php;
        server_name _; 

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
                }

                error_log /var/log/nginx/error.log; 
                access_log /var/log/nginx/access.log; 
}
```
### Start the nginx 
- Configure what ever the hell is this
```
ln -s /etc/nginx/sites-available/Brokoli /etc/nginx/sites-enabled/
```
- check if the syntax is correct
```
nginx -t 
```
- run it
```
service nginx reload
or
service nginx start // for the first time
```
- start the php
```
service php7.2-fpm start
```
### Repeat on every web server
### Checking the error logs
- to check the error logs you can go to client and then lynx http://brokoli.u25.com
![image](https://github.com/user-attachments/assets/b63d8655-4403-4029-8c8e-5ba6a954fecf)
- it will only show you this cause there's an error where 1. it's conflictng, 2. the Hostname in the php file is no correct, 3. Opening the wrong file
1. Error 1 can be fixed by changing `server_name _` into `server_name brokoli.u25.com'
2. Error 2 can be fixed by changin the hostname switchcase in the index.php file to the right one
   ![image](https://github.com/user-attachments/assets/6f0b0738-dcb4-4d02-87e5-c752d3c7dd94)
   ![image](https://github.com/user-attachments/assets/b83d2b1e-a054-43f7-9646-ca95d4bb29cf)

4. Last error can change the `resep_1.php` to `resep1.php`
<br>

## Soal 10

> Pada masing masing worker nginx, akan terdapat beberapa hal yang perlu diperbaiki pada resource yang diberikan untuk bisa menampilkan resep saat halaman dimuat. Analisis kesalahan yang ada di resource melalui file /var/log/nginx/error.log dan perbaiki hingga halaman bisa menampilkan resep sesuai dengan worker nya.

> _On each nginx worker, there will be several things that need to be fixed in the resources provided to be able to display recipes when the page is loaded. Analyze the errors in the resource through the /var/log/nginx/error.log file and fix it until the page can display recipes according to its worker._

**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/f0c10b27-4334-4cc2-a47e-88b82c151ce8)

- Explanation

  `Put your explanation in here`
### Checking the error logs
- to check the error logs you can go to client and then lynx http://brokoli.u25.com
![image](https://github.com/user-attachments/assets/b63d8655-4403-4029-8c8e-5ba6a954fecf)
- it will only show you this cause there's an error where 1. it's conflictng, 2. the Hostname in the php file is no correct, 3. Opening the wrong file
1. Error 1 can be fixed by changing `server_name _` into `server_name brokoli.u25.com'
2. Error 2 can be fixed by changin the hostname switchcase in the index.php file to the right one
   ![image](https://github.com/user-attachments/assets/6f0b0738-dcb4-4d02-87e5-c752d3c7dd94)
   ![image](https://github.com/user-attachments/assets/b83d2b1e-a054-43f7-9646-ca95d4bb29cf)

4. Last error can change the `resep_1.php` to `resep1.php`
### Repeat on every server

<br>

## Soal 11

> Setelah website berhasil dideploy pada masing-masing worker (Bayam, Brokoli, dan Buncis) dan halaman dapat menampilkan resep sayuran yang sesuai,  buatlah custom access log ke file /var/log/nginx/access.log di masing-masing web server worker menggunakan format log tertentu seperti di bawah:
> - Tanggal dan waktu akses dalam format standar log.
Nama worker yang sedang dilayani (misalnya: Bayam, Brokoli, atau Buncis).
> - Alamat IP klien yang mengakses website.
> - Metode HTTP dan URI yang diakses oleh klien.
> - Status respons HTTP yang diberikan oleh server.
> - Jumlah byte yang dikirimkan dalam respons.
> - Waktu yang dihabiskan oleh server untuk menangani permintaan.
> <br> </br>
> Contoh format log yang sesuai: 
[01/Oct/2024:11:30:45 +0000] Jarkom Node Bayam Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned stat


> _After successfully deploying the website on each worker (Bayam, Brokoli, and Buncis) and ensuring the pages display the appropriate vegetable recipes, create a custom access log file at /var/log/nginx/access.log on each web server worker using a specific log format as described below:_
> - _Access date and time in standard log format._
> - _Name of the worker serving the request (e.g., Bayam, Brokoli, or Buncis)._
> - _Client IP address accessing the website._
> - _HTTP method and URI accessed by the client._
> - _HTTP response status provided by the server.__
> - _Number of bytes sent in the response.
> - _Time taken by the server to handle the request._
> <br> </br>
> _Example of the appropriate log format:
[01/Oct/2024:11:30:45 +0000] Jarkom Node Bayam Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds_


**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/351f77a3-e614-4f65-94ec-1751c1c425f8)
![image](https://github.com/user-attachments/assets/dc7d18f5-1a6a-41fe-8ff8-272ea1c84c15)
![image](https://github.com/user-attachments/assets/7567cc45-7c1e-4d83-8163-842d4ad9ada7)

- Explanation

  `Put your explanation in here`
### First Step
we can configure the custom log in the `nginx.conf` file
- Open the NGINX configuration file on each server `/etc/nginx/nginx.conf `
```
nano /etc/nginx/nginx.conf
```
- and then add this configuratioon to the `# Logging Setting` part
```
log_format custom_brokoli '$time_local Jarkom Node Bayam Access from $remote_addr using method "$request" '
                        'returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
```
![image](https://github.com/user-attachments/assets/e75dc856-2874-485b-b26a-ad6208f13f0a)
- after that we can go to the server configuration which is `etc/nginx/sites-available/Brokoli`
```
nano /etc/nginx/sites-available/Brokoli
```
- and then add
```
access_log /var/log/nginx/access.log custom_brokoli;
```
![image](https://github.com/user-attachments/assets/cebc407c-8bae-4f50-92f9-640dde2fe879)
### Second Step (testing)
- then we can restart the nginx
```
service nginx restart
```
- go back to TomatClient, and lynx
```
lynx http://brokoli.U25.com
```
- and then go to Brokoli or any client, and check the access log
```
tail /var/log/nginx/access.log
```
![image](https://github.com/user-attachments/assets/e4bdad1b-fe99-4a3c-bb8e-2ee3653bfa7a)

<br>

## Soal 12

> Informasi vitamin pada sayur brokoli akan ditampilkan pada subdomain vitamin.brokoli.yyy.com di node brokoli, buatlah DocumentRoot yang disimpan pada /var/www/vitamin.brokoli.yyy. Konfigurasikan webserver dengan nama server vitamin.brokoli.yyy.com dan server alias www.vitamin.brokoli.yyy.com. Lakukan konfigurasi Apache Web Server pada Brokoli dengan menggunakan sumber yang tersedia di [sini](https://docs.google.com/uc?export=download&id=1QbGkKXo3jt4c68AdVAkl1hD4LolTUPg2).

> _For information on vitamins in brokoli will be displayed on the vitamin.brokoli.yyy.com subdomain on the brokoli node, create a DocumentRoot stored in /var/www/vitamin.brokoli.yyy. Configure the web server with the server name vitamin.brokoli.yyy.com and server alias www.vitamin.brokoli.yyy.com. Configure the Apache Web Server on Brokoli using [this resource](https://docs.google.com/uc?export=download&id=1QbGkKXo3jt4c68AdVAkl1hD4LolTUPg2)._

**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/14e79ea4-264a-485f-b092-225c49e30187)

- Explanation

  `Put your explanation in here`
### First Step (apache2 and setups)
- first thing you have to do is install 'apache2'
```
apt-get install apache2
```
- download the necessary files
```
wget --no-check-certificate "https://docs.google.com/uc?export=download&id=1NhsaTLD4Zk06BZJCqdN_oqoxB3uIg2C7" -O assets.zip
```
- make a directori for the website
```
mkdir /var/www/vitamin.brokoli.U25
```
- unzip the assets
```
unzip assets.zip
```
- copy the existing file to the `vitamin.brokoli.U25' directory
```
cp -r vitamin.brokoli.yyy.com/* /var/www/vitamin.brokoli.U25
```
### Second Step (Confuguration)
- then you can make a configuration file for the server in '/etc/apache2/sites-available'
- and then do
```
cp 000-default.conf vitamin.brokoli.U25.com.conf
```
- then open it
```
nano /etc/apache2/sites-available/vitamin.brokoli.U25.conf
```
- fill it according to this configuration
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName vitamin.brokoli.U25.com
    ServerAlias www.vitamin.brokoli.U25.com

    DocumentRoot /var/www/vitamin.brokoli.U25

    <Directory /var/www/vitamin.brokoli.U25>
        Options +Indexes
        AllowOverride All
        Require all granted
    </Directory>

    <Directory /var/www/vitamin.brokoli.U25/nutrisi>
        Options +Indexes
        AllowOverride All
        Require all granted
    </Directory>

    # Enable Rewrite Engine
    RewriteEngine On

    # Check if the request is not a directory
    RewriteCond %{REQUEST_FILENAME} !-d

    # Rewrite rule to remove .php extension
    RewriteRule ^nutrisi/([^\.]+)$ /nutrisi/$1.php [NC,L]

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
### Third Step (Checking)
- and then you can restart the apache
```
service apache2 restart
```
- and then lynx to the web by using tomat client
```
lynx http://vitamin.brokoli.u25.com/
```
- go to vitamin_a
![image](https://github.com/user-attachments/assets/79348989-0038-4317-b3c1-7ce198dc340f)
![image](https://github.com/user-attachments/assets/1710b04f-e515-429a-82db-91887a0761e3)


<br>

## Soal 13

> Pada subdomain vitamin.brokoli.yyy.com, terdapat subfolder /nutrisi yang menyediakan informasi tentang berbagai vitamin dalam brokoli, seperti Vitamin A, C, dan K. Aktifkan directory listing untuk folder /nutrisi, dan buatlah rewrite rule di Apache untuk memperbaiki URL agar halaman seperti www.vitamin.brokoli.yyy.com/nutrisi/vitamin_a.php dapat diakses hanya dengan www.vitamin.brokoli.yyy.com/nutrisi/vitamin_a. Pastikan setiap halaman vitamin dapat diakses langsung melalui url yang telah disederhanakan.

> _On the vitamin.brokoli.yyy.com subdomain, there is a /nutrisi subfolder that provides information about various vitamins in brokoli, such as Vitamin A, C, and K. Activate directory listing for the /nutrisi folder, and create a rewrite rule in Apache to fix the URL so that pages like www.vitamin.brokoli.yyy.com/nutrisi/vitamin_a.php can be accessed only with www.vitamin.brokoli.yyy.com/nutrisi/vitamin_a. Make sure each vitamin page can be accessed directly through the simplified url._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/125e83f5-496e-48c5-b06f-81018610023a)
### bukti dengan curl
![image](https://github.com/user-attachments/assets/0bb418fe-16c4-4544-ade7-62bd17bc5705)


- Explanation

  `Put your explanation in here`
### First Step (setups)
- run this command
```
a2enmod rewrite
```
- restrat the apache
```
service apache2 restart
```
### Second Step Configuration
- make an `.htaccess` file in the `/var/www/vitamin.brokoli.U25` directory
```
nano /var/www/vitamin.brokoli.U25/.htaccess
```
- and fill this
```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^([^\.]+)$ $1.php [NC,L]
```
### Testin
- restart the apache
```
service apache2 restart
```
- go to tomat client to test if the rewriteing works
```
lynx http://vitamin.brokoli.u25.com/nutrisi/vitamin_a
```
![image](https://github.com/user-attachments/assets/ba4ee182-2644-48d0-a9dd-e22e282b026a)

<br>

## Soal 14

> Tambahkan alias untuk folder /public/images/ pada subdomain www.vitamin.brokoli.yyy.com agar folder tersebut dapat diakses langsung melalui url www.vitamin.brokoli.yyy.com/img.

> _Add an alias for the /public/images/ folder on the www.vitamin.brokoli.yyy.com subdomain so that the folder can be accessed directly through the url www.vitamin.brokoli.yyy.com/img._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/aefa8c8b-74b8-48a7-b9a8-7afa308d16b6)
  ![image](https://github.com/user-attachments/assets/b6efd225-98d5-4677-b376-0ca7b0e54ad7)


- Explanation

  `Put your explanation in here`
### First Step
- open up the confuguration file of the apace web server
```
nano /etc/apache2/sites-available/vitamin.brokoli.U25.com.conf
```
- Modify the conf according to this by adding an `Alias` Directory Routing
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName vitamin.brokoli.U25.com
    ServerAlias www.vitamin.brokoli.U25.com

    DocumentRoot /var/www/vitamin.brokoli.U25
    Alias "/img" "/var/www/vitamin.brokoli.U25/public/images/"

    <Directory "/var/www/vitamin.brokoli.U25/public/images/">
        Require all granted
    </Directory>

    <Directory /var/www/vitamin.brokoli.U25>
        Options +Indexes
        AllowOverride All
        Require all granted
    </Directory>

    <Directory /var/www/vitamin.brokoli.U25/nutrisi>
        Options +Indexes
        AllowOverride All
        Require all granted
    </Directory>

    # Enable Rewrite Engine
    RewriteEngine On

    # Check if the request is not a directory
    RewriteCond %{REQUEST_FILENAME} !-d

    # Rewrite rule to remove .php extension
    RewriteRule ^nutrisi/([^\.]+)$ /nutrisi/$1.php [NC,L]

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
### Second Step (Testing)
- save the configuration by restartig the apache
```
service apache2 restart
```
- go to tomatclient
```
lynx http://vitamin.brokoli.u25.com/img
```
<br>

## Soal 15

> Karena terdapat resep rahasia di file /secret/recipe_secret.txt pada subdomain www.vitamin.brokoli.yyy.com, konfigurasikan folder /secret agar tidak dapat diakses oleh pengguna (dengan menampilkan 403 Forbidden).

> _Because there is a secret recipe in the /secret/recipe_secret.txt file on the www.vitamin.brokoli.yyy.com subdomain, configure the /secret folder so that it cannot be accessed by users (by displaying 403 Forbidden)._

**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/d5be2245-9110-4c91-971a-9c14a666267a)

- Explanation

  `Put your explanation in here`
### First and only step
simply add this to the apache configuration file
```
<Directory /var/www/vitamin.brokoli.U25/secret>
        Require all denied
</Directory>
```
then restart
```
service apache2 restart
```
![image](https://github.com/user-attachments/assets/14965188-3f93-4b4e-8909-b551bb842695)

<br>

## Soal 16

> Karena dinilai terlalu panjang coba ubah konfigurasi www.vitamin.brokoli.yyy.com/public/js menjadi www.vitamin.brokoli.yyy.com/js

> _Since it is considered too long, change the configuration from www.vitamin.brokoli.yyy.com/public/js to www.vitamin.brokoli.yyy.com/js._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/42f187df-7ef3-4293-b681-eeb1f4d839e3)
  ![image](https://github.com/user-attachments/assets/30e258cf-d1c3-4af1-987f-25a4b641df11)
  ![image](https://github.com/user-attachments/assets/d9d9ea6a-8255-4fb6-a4fa-d25ef1f5e227)


- Explanation

  `Put your explanation in here`
  ### First and only step
simply add this to the apache configuration file
```
Alias "/js" "/var/www/vitamin.brokoli.U25/public/js"

<Directory /var/www/vitamin.brokoli.U25/public/js>
      Require all granted
</Directory>
```
then restart
```
service apache2 restart
```
![image](https://github.com/user-attachments/assets/42f187df-7ef3-4293-b681-eeb1f4d839e3)

<br>

## Soal 17

> Supaya Web kita aman terkendali maka ubah konfigurasi www.k1.vitamin.brokoli.yyy.com menjadi hanya bisa di akses oleh port 9696 dan 8888

> _To keep our web secure, configure www.k1.vitamin.brokoli.yyy.com to only be accessible through ports 9696 and 8888._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ### (sudah ada konfigurasi untuk soal selanjut selanjutnya), tapi sudah memakai port
![image](https://github.com/user-attachments/assets/31c6a150-e66e-4d02-937e-ff8d3dbed2a0)

- Explanation

  `Put your explanation in here`
### First step
Go back to `BrokoliWebServer`
- Create Directories for the Subdomain: First, create separate directories for  your subdomain (e.g.,k1.vitamin.brokoli.u25.com). These directories will hold the respective content for each domain.
```
mkdir /var/www/k1.vitamin.brokoli.u25
```
- Copy file `000-default.conf` to `file k1.vitamin.brokoli.U25.com.conf`
```
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/k1.vitamin.brokoli.U25.com.conf
```
Just an example from the module
![image](https://github.com/user-attachments/assets/224c9b6a-c299-4a4a-985b-d8f416692fee)

- Open the file, and then fill this
```
<VirtualHost *:9696 *:8888>
    ServerAdmin webmaster@localhost
    ServerName k1.vitamin.brokoli.u25.com
    ServerAlias www.k1.vitamin.brokoli.u25.com

    DocumentRoot /var/www/k1.vitamin.brokoli.u25

    <Directory /var/www/k1.vitamin.brokoli.u25>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
- go to `/etc/apache2/ports.conf`
```
nano /etc/apache2/ports.conf
```
- and then add the following port
```
Listen 9696
Listen 8888
```
- and then
```
a2ensite k1.vitamin.brokoli.u25.com.conf
```
### Testing
- reload the apache2
```
service apache2 reload
```
- go back to tomat client, and write the following lynx
```
lynx http://k1.vitamin.brokoli.u25.com:9696
```

![image](https://github.com/user-attachments/assets/e09b9798-736b-44bb-ad14-f81adc287027)

<br>

## Soal 18

> Lanjutkan dari nomor sebelumnya buatlah autentikasi dengan username “Seblak” dan password “sehatyyy” dengan yyy adalah kode kelompok. Letakkan Document Root pada /var/www/k1.vitamin.brokoli.yyy.

> _Continuing from the previous point, create authentication with the username “Seblak” and the password “sehatyyy” where yyy is the group code. Set the Document Root to /var/www/k1.vitamin.brokoli.yyy._

**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/36d49ff9-d7b3-4bdb-b6e1-83e34c93b466)

- Explanation

  `Put your explanation in here`

### First step (configurin)
- first create a `.htpasswd` file in `/etc/apache2/` directory
```
htpasswd -c /etc/apache2/.htpasswd Seblak
```
- and then configure the password by typing `sehatu25` for the password
- go to the  `/etc/apache2/sites-available/k1.vitamin.brokoli.u25.com.conf` file
```
nano /etc/apache2/sites-available/k1.vitamin.brokoli.u25.com.conf
```
- and change the directory listing to this
```
<Directory /var/www/k1.vitamin.brokoli.u25>
        Options Indexes FollowSymLinks
        AllowOverride All
        AuthType Basic
        AuthName "Restricted Area"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
    </Directory>
```
### Second Step (testing)
- safe the configuration by restarting the apache
```
service apache2 restart
```
- go to tomat client, and open the web with lynx
```
lynx http://k1.vitamin.brokoli.u25.com:8888
```
 or
```
lynx http://k1.vitamin.brokoli.u25.com:9696
```
- and then you can fill in the username `seblak` and also the password `sehatu25`

![image](https://github.com/user-attachments/assets/c070dd1e-8fad-4711-803e-a2b0ef8b7dd2)

<br>

## Soal 19

> Konfigurasikan agar setiap kali IP Brokoli diakses dengan lynx, secara otomatis akan dialihkan ke www.brokoli.yyy.com (alias).

> _Configure it so that every time Brokoli's IP is accessed using lynx, it is automatically redirected to www.brokoli.yyy.com (alias)._

**Answer:**

- Screenshot

  `Put your screenshot in here`
![image](https://github.com/user-attachments/assets/fcb08c40-e835-4a74-94c4-a989567910c1)

- Explanation

  `Put your explanation in here`
### First Step
- make the `brokoli.u25.com.conf file`
```
nano /etc/apache2/sites-available/brokoli.u25.com.conf
```
- fill it accordingly to this
```
<VirtualHost *:80>
    ServerName brokoli.u25.com
    ServerAlias www.brokoli.u25.com
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/Brokoli

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
- and then type
```
a2ensite brokoli.u25.com.conf
```
- after that, to make it if you type the IP it redirects to the brokoli server you can make another `.conf` file
```
nano /etc/apache2/sites-available/brokoli-ip-alias.conf
```
- fill it accordingly
```

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/Brokoli

    # Replace '10.63.3.3' with Brokoli's actual IP address
    ServerName 10.63.3.3
    Redirect / http://www.brokoli.u25.com/

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
### Testing
```
a2ensite brokoli-ip-alias.conf
```
- go to tomat client, and open it with lynx
```
 lynx http://10.63.3.3
```
![image](https://github.com/user-attachments/assets/c9e9a5f8-a036-4ccf-b7e5-db31c2ccd8c4)

<br>

## Soal 20

> Karena jumlah pengunjung website www.vitamin.brokoli.yyy.com semakin meningkat dan terdapat banyak gambar random, ubah permintaan gambar yang mengandung substring "vitamin" agar diarahkan ke file vitamin.png.

> _Since the number of visitors to www.vitamin.brokoli.yyy.com is increasing and there are many random images, redirect image requests that contain the substring "vitamin" to the file vitamin.png._

**Answer:**

- Screenshot

  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/6a88f2b6-3c1c-4008-8a24-47c05ae8a2e6)
  ![image](https://github.com/user-attachments/assets/4f263192-1bd6-4bca-bf25-06e8bbed3387)
  ![image](https://github.com/user-attachments/assets/784ad351-d0b2-47b9-a648-4d2194d1fc06)

- Explanation

  `Put your explanation in here`
### First step
- open the `.htaccess` file
```
nano /var/www/vitamin.brokoli.U25/.htaccess
```
- add this part
```
RewriteCond %{REQUEST_URI} ^/public/images/.*vitamin.* [NC]
RewriteRule ^public/images/.*$ /public/images/vitamin.png [L,R=302]
```

### Testing
- save the configuration
```
service apache2 restart
```
- open up the link
```
lynx http://www.vitamin.brokoli.U25.com/public/images/tesvitamin.png
```
![image](https://github.com/user-attachments/assets/784ad351-d0b2-47b9-a648-4d2194d1fc06)
- it should go to vitamin.png

### Other solution
- or if we're referring to all the vitamin that's only inside the file we can do
```
RewriteRule ^/public/images/sayur-vitamin-k\.jpg$ /public/images/vitamin.png [L,R=301]
RewriteRule ^/public/images/makanan-vitamin-A-tertinggi\.jpg$ /public/images/vitamin.png [L,R=301]
RewriteRule ^/public/images/jenis-makanan-yang-mengandung-vitamin-c\.jpg$ /public/images/vitamin.png  [L,R=301]
```
- and then all of them will be redirected to download vitamin.php
<br>
  
## Scripts
### WortelDNS
#### /etc/bind/jarkom/3.63.10.in-addr.arpa
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     ns.U25.com. root.U25.com. (
                              3         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.63.10.in-addr.arpa.   IN      NS      ns.U25.com.
3                       IN      PTR     brokoli.U25.com.
4                       IN      PTR     buncis.U25.com.
```
#### /etc/bind/jarkom/brokoli.U25.com
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     brokoli.U25.com. root.brokoli.U25.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@               IN      NS      brokoli.U25.com.
@               IN      A       10.63.3.3
www             IN      CNAME   brokoli.U25.com.
ns1             IN      A       10.63.3.2
vitamin         IN      NS      ns1
```
#### /etc/bind/jarkom/bayam.U25.com
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     bayam.U25.com. root.bayam.U25.com. (
                        2024011025      ; Serial
                        7200            ; Refresh
                        1800            ; Retry
                        1209600         ; Expire
                        43200 ) ; Negative Cache TTL
;
@       IN      NS      bayam.U25.com.
@       IN      A       10.63.3.5
www     IN      CNAME   bayam.U25.com.

```
#### /etc/bind/jarkom/buncis.U25.com
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     buncis.U25.com. root.buncis.U25.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      buncis.U25.com.
@       IN      A       10.63.3.4
```
#### /etc/bind/named.conf.local
```
zone "bayam.U25.com" {
    type master;
    also-notify { 10.63.3.2; };
    allow-transfer { 10.63.3.2; };
    file "/etc/bind/jarkom/bayam.U25.com";
};

zone "brokoli.U25.com" {
    type master;
    file "/etc/bind/jarkom/brokoli.U25.com";
    allow-transfer { 10.63.3.2; };
};

zone "buncis.U25.com" {
    type master;
    also-notify { 10.63.3.2; };
    allow-transfer { 10.63.3.2; };
    file "/etc/bind/jarkom/buncis.U25.com";
};

zone "3.63.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/3.63.10.in-addr.arpa";
};
```
####/etc/bind/named.conf.options
```
options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        // dnssec-validation auto;
        allow-query{any;};
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
```
### Pakcoy
#### /etc/bind/k1/vitamin.brokoli.U25.com
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     vitamin.brokoli.U25.com. root.vitamin.brokoli.U25.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      vitamin.brokoli.U25.com.
@       IN      A       10.63.3.3
WWW     IN      CNAME   vitamin.brokoli.U25.com.
k1      IN      A       10.63.3.3
www.k1  IN      CNAME   k1.vitamin.brokoli.U25.com.
```
#### /etc/bind/named.conf.local
```
zone "vitamin.brokoli.U25.com" {
    type master;
    file "/etc/bind/k1/vitamin.brokoli.U25.com";
};

zone "buncis.U25.com" {
    type slave;
    masters { 10.63.2.2; };
    file "/var/lib/bind/buncis.U25.com";
};

zone "bayam.U25.com" {
    type slave;
    masters { 10.63.2.2; };
    file "/var/lib/bind/bayam.U25.com";
};

```
### Brokoli and the others web servers
### NGINX Part
#### /etc/nginx/sites-available/Brokoli
```
server {

        listen 80;

        root /var/www/Brokoli;

        index index.php;
        server_name brokoli.u25.com;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
                }

                error_log /var/log/nginx/error.log;
                access_log /var/log/nginx/access.log custom_brokoli;
}
```
#### nginx.conf (add this)
```
        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;
        log_format custom_brokoli '$time_local Jarkom Node Bayam Access from $remote_addr using method "$request" '
                        'returned status $status with $body_bytes_sent bytes sent in $request_time seconds';
```
#### apache
#### /etc/apache2/sites-available/vitamin.brokoli.U25.com.conf
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName vitamin.brokoli.U25.com
    ServerAlias www.vitamin.brokoli.U25.com

    DocumentRoot /var/www/vitamin.brokoli.U25
    Alias "/img" "/var/www/vitamin.brokoli.U25/public/images/"

    <Directory "/var/www/vitamin.brokoli.U25/public/images/">
        Require all granted
    </Directory>

    <Directory /var/www/vitamin.brokoli.U25>
        Options +Indexes
        AllowOverride All
        Require all granted
    </Directory>

    <Directory /var/www/vitamin.brokoli.U25/nutrisi>
        Options +Indexes
        AllowOverride All
        Require all granted
    </Directory>
    <Directory /var/www/vitamin.brokoli.U25/secret>
        Require all denied
    </Directory>

    Alias "/js" "/var/www/vitamin.brokoli.U25/public/js"

    <Directory /var/www/vitamin.brokoli.U25/public/js>
      Require all granted
    </Directory>
    # Enable Rewrite Engine
    RewriteEngine On
    RewriteRule ^/public/images/sayur-vitamin-k\.jpg$ /public/images/vitamin.png [L,R=301]
    RewriteRule ^/public/images/makanan-vitamin-A-tertinggi\.jpg$ /public/images/vitamin.png [L,R=301]
    RewriteRule ^/public/images/jenis-makanan-yang-mengandung-vitamin-c\.jpg$ /public/images/vitamin.png  [L,R=301]
    RewriteRule ^/public/images/(.*vitamin.*)$ /public/images/vitamin.png [L]
# Check if the request is not a directory
    RewriteCond %{REQUEST_FILENAME} !-d

    # Rewrite rule to remove .php extension
#    RewriteRule ^nutrisi/([^\.]+)$ /nutrisi/$1.php [NC,L]

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
#### /etc/apache2/sites-available/k1.vitamin.brokoli.u25.com.conf 
```
<VirtualHost *:9696 *:8888>
    ServerAdmin webmaster@localhost
    ServerName k1.vitamin.brokoli.u25.com
    ServerAlias www.k1.vitamin.brokoli.u25.com

    DocumentRoot /var/www/k1.vitamin.brokoli.u25

    <Directory /var/www/k1.vitamin.brokoli.u25>
        Options Indexes FollowSymLinks
        AllowOverride All
        AuthType Basic
        AuthName "Restricted Area"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
#### /etc/apache2/sites-available/brokoli.u25.com.conf 
```
<VirtualHost *:80>
    ServerName brokoli.u25.com
    ServerAlias www.brokoli.u25.com
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/Brokoli

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    # Redirect to the desired URL if accessed via the IP

</VirtualHost>
```
####  /var/www/vitamin.brokoli.U25/.htaccess
```
RewriteEngine On


RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^([^\.]+)$ $1.php [NC,L]
```
## Problems

## Revisions (if any)
