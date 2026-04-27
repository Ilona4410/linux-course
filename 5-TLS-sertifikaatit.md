# TLS Sertifikaatit

## Johdanto

Tämän tehtävän tarkoituksena oli tutustua TLS-sertifikaattiin ja sen käyttöön palvelimella. Tavoitteena oli myös ymmärtää DNS:n toimintaa ja HTTP- ja HTTPS-liikenteen ominaisuuksia. 

## DNS

- Asensin tunnilla dig-työkalun komennolla sudo apt install dnsutils
- Testasin, että DNS toimii oiken ja domain osoittaa etäpalvelimeni julkiseen IP-osoitteeseen 65.52.72.83


  ```
  linuxuser@test026:~$ dig test026.linuxkurssi.xyz

  ; <<>> DiG 9.20.21-1~deb13u1-Debian <<>> test026.linuxkurssi.xyz
  ;; global options: +cmd
  ;; Got answer:
  ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 62844
  ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

  ;; OPT PSEUDOSECTION:
  ; EDNS: version: 0, flags:; udp: 65494
  ;; QUESTION SECTION:
  ;test026.linuxkurssi.xyz.	IN	A

  ;; ANSWER SECTION:
  test026.linuxkurssi.xyz. 1799	IN	A	65.52.72.83

  ;; Query time: 40 msec
  ;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
  ;; WHEN: Fri Apr 24 14:03:12 UTC 2026
  ;; MSG SIZE  rcvd: 68
  ```


**DNS-liikenteen tarkkailu tcpdump-komennolla**
- Avasin kaksi terminaalia. Toisessa komtento sudo tcpdump -i eth0 port 53 -n -v ja toisessa dig test026.linuxkurssi.xyz. Mitään liikennettä ei näkynyt. Tämä johtui varmaankin siitä, että olin kysynyt domainia jo aiemmin ja vastaus saatiin nyt välimuistista
- Kun kokeilin kyselyä dig test026.linuxkurssi.xyz @8.8.8.8, liikennettä tuli näkyviin


```
linuxuser@test026:~$ sudo tcpdump -i eth0 port 53 -n -v
tcpdump: listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
14:22:39.573927 IP (tos 0x0, ttl 64, id 5293, offset 0, flags [none], proto UDP (17), length 92)
208.24.0.33.41614 > 8.8.8.8.53: 266+ [1au] A? test026.linuxkurssi.xyz. (64)
14:22:39.600949 IP (tos 0x0, ttl 117, id 57200, offset 0, flags [none], proto UDP (17), length 96)
8.8.8.8.53 > 208.24.0.33.41614: 266 1/0/1 test026.linuxkurssi.xyz. A 65.52.72.83 (68)
```

- Eli, toinen kysely pakotettiin ulkoiselle Googlen DNS-palvelimelle, ja näin saatiin ohitettua paikallinen välimuisti -> liikennettä näkyviin


## Name-Based VirtualHost 

- Loin tiedoston index.html komennolla nano /home/linuxuser/public-sites/index.html
- Loin toisen tiedoston komennolla nano /home/linuxuser/public-sites/file1.txt
- Koitin luoda kolmannen tiedoston komennolla sudo -u edituser nano /home/linuxuser/public-sites/editorfile.txt, mutta minulla ei vielä ollut edituseria
- Loin edituserin komennolla sudo adduser edituser ja koitin tehdä tiedostoa uudestaan, mutta minulta puuttui oikeudet. Alla mitä tein:


  ```
  linuxuser@test026:~$ sudo usermod -aG edituser linuxuser
  linuxuser@test026:~$ sudo chgrp edituser /home/linuxuser/public-sites
  linuxuser@test026:~$ chmod g+w /home/linuxuser/public-sites
  linuxuser@test026:~$ chmod g+x /home/linuxuser/public-sites
  linuxuser@test026:~$ ls -ld /home/linuxuser/public-sites
  drwxrwxr-x 2 linuxuser edituser 4096 Apr 24 14:44 /home/linuxuser/public-sites
  ```
  
    - sudo usermod -aG edituser linuxuser = liitin käyttäjät samaan ryhmään
    - sudo chgrp edituser /home/linuxuser/public-sites = kansio ryhmälle edituser
    - chmod g+w /home/linuxuser/public-sites = ryhmälle kirjoitusoikeus
    - chmod g+x /home/linuxuser/public-sites = ryhmälle pääsy kansioon
    - ls -ld /home/linuxuser/public-sites = tarkistus (drwxrwxr-x)
    - chmod o+x /home/linuxuser = pääsy myös ylempiin kansioihin
      -> Sain luotua tiedoston ja kirjoitettua tähän sudo -u edituser nano /home/linuxuser/public-sites/editorfile.txt

 - Sain komennolla ```curl http://test026.linuxkurssi.xyz/``` index.html-tiedoston auki, eli tiedoston nimeä ei tarvittu, koska Apache haki tämän automaattisesti
 - Eli index.html tulee automaattisesti ja muut tiedostot täytyy avata niiden nimellä URL-osoitteessa



  ```
  linuxuser@test026:~$ curl http://test026.linuxkurssi.xyz/
  <h1>Moi kaikki</h1>
  linuxuser@test026:~$ curl http://test026.linuxkurssi.xyz/file1.txt
  <h1>Toinen testi</h1>
  linuxuser@test026:~$ curl http://test026.linuxkurssi.xyz/editorfile.txt
  <h1>kolmas testi</h1>
  ```


## TLS Certificate 

- Asensin Certbotin komennolla sudo apt install certbot python3-certbot-apache
- Loin TLS-sertifikaatin:


  ```
  linuxuser@test026:~$ sudo certbot --apache
  Saving debug log to /var/log/letsencrypt/letsencrypt.log
  Enter email address or hit Enter to skip.
   (Enter 'c' to cancel): 

  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  Please read the Terms of Service at:
  https://letsencrypt.org/documents/LE-SA-v1.6-August-18-2025.pdf
  You must agree in order to register with the ACME server. Do you agree?
  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  (Y)es/(N)o: y
  Account registered.

  Which names would you like to activate HTTPS for?
  We recommend selecting either all domains, or all domains in a VirtualHost/server block.
  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  1: test026.linuxkurssi.xyz
  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  Select the appropriate numbers separated by commas and/or spaces, or leave input
  blank to select all options shown (Enter 'c' to cancel): 
  Requesting a certificate for test026.linuxkurssi.xyz

  Successfully received certificate.
  Certificate is saved at: /etc/letsencrypt/live/test026.linuxkurssi.xyz/fullchain.pem
  Key is saved at:         /etc/letsencrypt/live/test026.linuxkurssi.xyz/privkey.pem
  This certificate expires on 2026-07-24.
  These files will be updated when the certificate renews.
  Certbot has set up a scheduled task to automatically renew this certificate in the background.

  Deploying certificate
  Successfully deployed certificate for test026.linuxkurssi.xyz to /etc/apache2/sites-available/test026.linuxkurssi.xyz-le-ssl.conf
  Congratulations! You have successfully enabled HTTPS on https://test026.linuxkurssi.xyz

  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  If you like Certbot, please consider supporting our work by:
   * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   * Donating to EFF:                    https://eff.org/donate-le
  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  ```


- Selaimessa näkyy lukko:
  <img width="263" height="202" alt="35" src="https://github.com/user-attachments/assets/4c4de639-e8bf-4f36-8e83-eb459100a868" />


- TLS-sertifikaatti tarkistus crt.sh-palvelussa
  <img width="493" height="119" alt="36" src="https://github.com/user-attachments/assets/e99ac507-0ac1-4fd5-8d9a-36ac5f55caee" />

- Testasin sertifikaatin uusimisen komennolla certbot renew --dry-run


  ```
  linuxuser@test026:~$ sudo certbot renew--dry-run
  usage: 
  certbot [SUBCOMMAND] [options] [-d DOMAIN] [-d DOMAIN] ...

  Certbot can obtain and install HTTPS/TLS/SSL certificates.  By default,
  it will attempt to use a webserver both for obtaining and installing the
  certificate. 
  certbot: error: unrecognized arguments: renew--dry-run
  linuxuser@test026:~$ sudo certbot renew --dry-run
  Saving debug log to /var/log/letsencrypt/letsencrypt.log

  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  Processing /etc/letsencrypt/renewal/test026.linuxkurssi.xyz.conf
  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  Account registered.
  Simulating renewal of an existing certificate for test026.linuxkurssi.xyz

  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  Congratulations, all simulated renewals succeeded: 
  /etc/letsencrypt/live/test026.linuxkurssi.xyz/fullchain.pem (success)
  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  ```

  ## Monitoring – curl in verbose mode

- HTTPS-yhteys verbose-tilassa. Handshake-vaihe näkyy, eli asiakas ja palvelin muodostavat salatun yhteyden


  ```
  linuxuser@test026:~$ curl -v https://test026.linuxkurssi.xyz
  * Host test026.linuxkurssi.xyz:443 was resolved.
  * IPv6: (none)
  * IPv4: 65.52.72.83
  *   Trying 65.52.72.83:443...
  * ALPN: curl offers h2,http/1.1
  * TLSv1.3 (OUT), TLS handshake, Client hello (1):
  *  CAfile: /etc/ssl/certs/ca-certificates.crt
  *  CApath: /etc/ssl/certs
  * TLSv1.3 (IN), TLS handshake, Server hello (2):
  * TLSv1.3 (IN), TLS change cipher, Change cipher spec (1):
  * TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
  * TLSv1.3 (IN), TLS handshake, Certificate (11):
  * TLSv1.3 (IN), TLS handshake, CERT verify (15):
  * TLSv1.3 (IN), TLS handshake, Finished (20):
  * TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
  * TLSv1.3 (OUT), TLS handshake, Finished (20):
  * SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384 / X25519MLKEM768 / id-ecPublicKey
  * ALPN: server accepted http/1.1
  * Server certificate:
  *  subject: CN=test026.linuxkurssi.xyz
  *  start date: Apr 25 05:18:43 2026 GMT
  *  expire date: Jul 24 05:18:42 2026 GMT
  *  subjectAltName: host "test026.linuxkurssi.xyz" matched cert's "test026.linuxkurssi.xyz"
  *  issuer: C=US; O=Let's Encrypt; CN=E7
  *  SSL certificate verify ok.
  *   Certificate level 0: Public key type EC/prime256v1 (256/128 Bits/secBits), signed using ecdsa-with-SHA384
  *   Certificate level 1: Public key type EC/secp384r1 (384/192 Bits/secBits), signed using sha256WithRSAEncryption
  *   Certificate level 2: Public key type RSA (4096/152 Bits/secBits), signed using sha256WithRSAEncryption
  * Connected to test026.linuxkurssi.xyz (65.52.72.83) port 443
  * using HTTP/1.x
  > GET / HTTP/1.1
  > Host: test026.linuxkurssi.xyz
  > User-Agent: curl/8.14.1
  > Accept: */*
  > 
  * Request completely sent off
  * TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
  * TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
  < HTTP/1.1 200 OK
  < Date: Mon, 27 Apr 2026 10:55:49 GMT
  < Server: Apache/2.4.66 (Debian)
  < Last-Modified: Fri, 24 Apr 2026 14:42:53 GMT
  < ETag: "14-65035c7ae5d7f"
  < Accept-Ranges: bytes
  < Content-Length: 20
  < Content-Type: text/html
  < 
  <h1>Moi kaikki</h1>
  * Connection #0 to host test026.linuxkurssi.xyz left intact
  ```


- HTTP-yhteyden testauksessä näkyy 301 Moved Permanently, eli liikenne ohjattiin HTTPS-osoitteeseen. Palvelin siis pakottaa käyttämään salattua yhteyttä


  ```
  linuxuser@test026:~$ curl -v http://test026.linuxkurssi.xyz
  * Host test026.linuxkurssi.xyz:80 was resolved.
  * IPv6: (none)
  * IPv4: 65.52.72.83
  *   Trying 65.52.72.83:80...
  * Connected to test026.linuxkurssi.xyz (65.52.72.83) port 80
  * using HTTP/1.x
  > GET / HTTP/1.1
  > Host: test026.linuxkurssi.xyz
  > User-Agent: curl/8.14.1
  > Accept: */*
  > 
  * Request completely sent off
  < HTTP/1.1 301 Moved Permanently
  < Date: Mon, 27 Apr 2026 11:01:01 GMT
  < Server: Apache/2.4.66 (Debian)
  < Location: https://test026.linuxkurssi.xyz/
  < Content-Length: 369
  < Content-Type: text/html; charset=iso-8859-1
  < 
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
  <html><head>
  <title>301 Moved Permanently</title>
  </head><body>
  <h1>Moved Permanently</h1>
  <p>The document has moved <a href="https://test026.linuxkurssi.xyz/">here</a>.</p>
  <hr>
  <address>Apache/2.4.66 (Debian) Server at test026.linuxkurssi.xyz Port 80</address>
  </body></html>
  * Connection #0 to host test026.linuxkurssi.xyz left intact
  ```


- Redirectin poisto väliaikaisesti muokkaamalla config-tiedostoa sudo nano /etc/apache2/sites-available/test026.linuxkurssi.xyz.conf
  <img width="407" height="163" alt="37" src="https://github.com/user-attachments/assets/26ba86c4-0336-4304-8d05-0dcec7f9555c" />

- Apachen lataus uudelleen komennolla sudo systemctl reload apache2
- Testasin HTTP-yhteyttä uudelleen7


  ```
  linuxuser@test026:~$ curl -v http://test026.linuxkurssi.xyz
  * Host test026.linuxkurssi.xyz:80 was resolved.
  * IPv6: (none)
  * IPv4: 65.52.72.83
  *   Trying 65.52.72.83:80...
  * Connected to test026.linuxkurssi.xyz (65.52.72.83) port 80
  * using HTTP/1.x
  > GET / HTTP/1.1
  > Host: test026.linuxkurssi.xyz
  > User-Agent: curl/8.14.1
  > Accept: */*
  > 
  * Request completely sent off
  < HTTP/1.1 200 OK
  < Date: Mon, 27 Apr 2026 11:12:10 GMT
  < Server: Apache/2.4.66 (Debian)
  < Last-Modified: Fri, 24 Apr 2026 14:42:53 GMT
  < ETag: "14-65035c7ae5d7f"
  < Accept-Ranges: bytes
  < Content-Length: 20
  < Content-Type: text/html
  < 
  <h1>Moi kaikki</h1>
  * Connection #0 to host test026.linuxkurssi.xyz left intact
  ```


- Kun redirect otettiin pois käytöstä, HTTP-liikennettä ei enää ohjattu HTTPS. Sivun sisältö <h1>Moi kaikki</h1> näkyy eli liikenne ei ole salattu

  
## Yhteenveto

Onnistuin asentamaan ja konfiguroimaan TLS-sertifikaation palvelimelle. DNS toimi myös oikein ja domain osoitti palvelimen julkiseen IP-osoitteeseen.

Opin erityisesti HTTPS- ja HTTP-liikenteistä ja siitä, mikä vaikutus redirectillä on. Tehtävät auttoivat minua ymmärtämään, miten HTTPS suojaa liikennettä. 

## Lähteet

- Heinonen, J. Domain Name and TLS Cerfiticates. Luettavissa: https://github.com/johannaheinonen/johanna-test-repo/blob/main/module_5.md. Luettu: 27.4.2026.
