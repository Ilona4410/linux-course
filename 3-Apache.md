# Apache2 web server

## Johdanto

### Asennus

#### Asensin Apache2 web serverin komennolla sudo apt install apache2 ja tarkistin, että tämä toimii normaalisti: 

```
ilona@ilona:~$ sudo systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/apache2.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-04-10 07:32:58 EEST; 23s ago
 Invocation: b54a6729ad80460c9907ae5bf651d0a2
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 2296 (apache2)
      Tasks: 55 (limit: 4479)
     Memory: 4.9M (peak: 5M)
        CPU: 34ms
     CGroup: /system.slice/apache2.service
             ├─2296 /usr/sbin/apache2 -k start
             ├─2297 /usr/sbin/apache2 -k start
             └─2315 /usr/sbin/apache2 -k start

huhti 10 07:32:58 ilona systemd[1]: Starting apache2.service - The Apache HTTP Server...
huhti 10 07:32:58 ilona apachectl[2294]: AH00558: apache2: Could not reliably determine the server's >
huhti 10 07:32:58 ilona systemd[1]: Started apache2.service - The Apache HTTP Server.
```
#### Seuraavaksi testasin, että selain näyttää Apache default sivun ja culr-komento näyttää tämän HTML-koodina:

<img width="416" height="350" alt="15" src="https://github.com/user-attachments/assets/5a3b90cd-59a1-4a82-b98c-807e4ce43a8c" />
<img width="517" height="238" alt="16" src="https://github.com/user-attachments/assets/a68d2ce7-9963-496f-98ba-e5fbeaa26a61" />

### Default-sivun muokkaus

#### Muokkasin default-sivua komennolla echo "This is the default page of my new web server" | sudo tee /var/www/html/index.html ja päivitin selaimen:

<img width="298" height="231" alt="17" src="https://github.com/user-attachments/assets/05d60487-0ae8-4425-accc-1cac7e647f3d" />

#### echo "This is the default page of my new web server" | sudo tee /var/www/html/index.html
- echo = kirjoittaa tekstin "This is the default page of my new web server"
- | (pipe) = yhdistetään komento seuraavaan
- sudo tee = kirjoittaa tiedostoon admin-oikeuksilla (Panovski 2026)
- /var/www/html/index.html = tiedosto

#### Muita tapoja tehtä sama: 
- nano-tekstieditorilla voidaan muokata tiedostoa = sudo nano /var/www/html/index.html
- sudo tee /var/www/html/index.html -> tekstin kirjoitus -> Ctrl + D

### /etc/hosts -tiedosto

#### Muokkasin /etc/hosts -tiedostoa lisäämällä domain-nimen ja IP-osoitteen

<img width="300" height="149" alt="18" src="https://github.com/user-attachments/assets/bc8bd36a-0011-48a0-8400-ae65cb01b764" />

### Palomuurin asennus ja konffaus

```
ilona@ilona:~$ sudo ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere                  
80/tcp                     ALLOW IN    Anywhere                  
443/tcp                    ALLOW IN    Anywhere                  
22/tcp (v6)                ALLOW IN    Anywhere (v6)             
80/tcp (v6)                ALLOW IN    Anywhere (v6)             
443/tcp (v6)               ALLOW IN    Anywhere (v6)  
```
#### Tein testin sulkemall 80/tcp-portin:

- Sivu avautui silti normaalisti (http://localhost/)
- Tästä voisi päätellä, että palomuuri ei estä localhostin sisäistä liikennettä

### Oman web-sivun luominen

1. Alla luomani HTML-tiedosto:

```
ilona@ilona:~$ cat ~/public-sites/index.html
<h1>Moi!</h1>
<p>Tämä on minun Apache-sivuni.</p>
```

2. Tarkistin oikeudet. Apachella täytyy olla tiedostooon lukuoikeudet r--, jotta se pystyy lukemaan tiedoston ja näyttämään sivun. Opin tämän tunnilla     tehdystä harjoituksesta. Lisäksi kansiossa täytyy olla -x, jotta Apache pääsee kansioon jossa tiedosto on

```
ilona@ilona:~$ ls -l ~/public-sites/index.html
-rw-rw-r-- 1 ilona ilona 38 11. 4. 14:11 /home/ilona/public-sites/index.html
ilona@ilona:~$ ls -ld ~/public-sites
drwxrwxr-x 2 ilona ilona 4096 11. 4. 14:11 /home/ilona/public-sites
```

3. Config-tiedoston luominen. Käytin mallina 000-default.conf-tiedostoa
   
<img width="418" height="286" alt="20" src="https://github.com/user-attachments/assets/791e5daa-7186-4988-b74e-19d1baf7e73c" />
<img width="308" height="132" alt="19" src="https://github.com/user-attachments/assets/24d92e28-bc69-4936-b2b8-3e0a67711060" />

4. Tässä valmis sivu:

<img width="267" height="149" alt="21" src="https://github.com/user-attachments/assets/578e8d43-3d39-4287-8104-745ab58e4836" />

5. Tarkistin logit ja kummassakaan ei ollut virheitä

```
ilona@ilona:~$ sudo tail -f /var/log/apache2/access.log
[sudo] password for ilona: 
127.0.0.1 - - [11/Apr/2026:13:55:50 +0300] "GET / HTTP/1.1" 304 248 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0"
ilona@ilona:~$ sudo tail -f /var/log/apache2/error.log
[Sat Apr 11 13:52:51.988044 2026] [mpm_event:notice] [pid 977:tid 977] AH00489: Apache/2.4.66 (Debian) configured -- resuming normal operations
[Sat Apr 11 13:52:51.988067 2026] [core:notice] [pid 977:tid 977] AH00094: Command line: '/usr/sbin/apa
```
-> Tästä syystä päätin tehdä pienen virheen config-tiedostoon ja katsoa miten se näkyy logeissa

- Tein typon config-tiedoston Directory-polkuun: Directory /home/ilona/public-sitesss/. Alla kuva mitä sivulla http://site1.com/ näkyi
  <img width="265" height="155" alt="22" src="https://github.com/user-attachments/assets/53e74881-9cd8-48bd-9f00-dc7883b3bced" />


 



## Yhteenveto

## Lähteet

- Panovski, D. 20.1.2026. Linux Tee Command with Examples. Linuxize. Luettavissa: https://linuxize.com/post/linux-tee-command/. Luettu: 10.4.2026.
