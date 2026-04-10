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

#### Muokkasin defaul-sivua komennolla echo "This is the default page of my new web server" | sudo tee /var/www/html/index.html ja päivitin selaimen:

<img width="298" height="231" alt="17" src="https://github.com/user-attachments/assets/05d60487-0ae8-4425-accc-1cac7e647f3d" />

#### echo "This is the default page of my new web server" | sudo tee /var/www/html/index.html
- echo = kirjoittaa tekstin "This is the default page of my new web server"
- | (pipe) = yhdistetään komento seuraavaan
- sudo tee = kirjoittaa tiedostoon admin-oikeuksilla (Panovski 2026)
- /var/www/html/index.html = tiedosto





## Yhteenveto

## Lähteet

- Panovski, D. 20.1.2026. Linux Tee Command with Examples. Linuxize. Luettavissa: https://linuxize.com/post/linux-tee-command/. Luettu: 10.4.2026.
