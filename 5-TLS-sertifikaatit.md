# TLS Sertifikaatit

## Johdanto

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





  ```
  linuxuser@test026:~$ curl http://test026.linuxkurssi.xyz/
  <h1>Moi kaikki</h1>
  linuxuser@test026:~$ curl http://test026.linuxkurssi.xyz/file1.txt
  <h1>Toinen testi</h1>
  linuxuser@test026:~$ curl http://test026.linuxkurssi.xyz/editorfile.txt
  <h1>kolmas testi</h1>
  ```


  


## Yhteenveto

## Lähteet
