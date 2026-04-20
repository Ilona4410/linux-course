# Palvelimen perusasetukset

## Johdanto

## Järjestelmän päivitys ja salasananvaihto

- Kirjauduin etäpalvelimelle (Azure VM) komennolla ssh linuxuser@65.52.72.83
- Vaihdoin salasanan komennolla passwd
- Päivitin pakettilistan komennolla sudo apt update
- Suoritin alla näkyvän komennon:


  ```
  linuxuser@test026:~$ sudo apt upgrade
  Summary:                        
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 0
  ```

## SSH-serveri

- SSH-serveri toimii, näkyy active (running):



## SSH-avainkirjautuminen

- Loin avaimen omalle virtuaalikoneelle ja annoin palvelimelle luvan hyväksyä sen. Salasanakirjautuminen -> avaimella kirjautuminen
- Komento omalla koneella ssh-keygen -> private key minulle ja public key jaettavaksi
- Kopioin avaimen palvelimelle ssh-copy-id linuxuser@65.52.72.83
- Testasin SSH-yhteyttä uudelleen komennolla ssh linuxuser@65.52.72.83 ja avainkirjautuminen onnistuis, ei kysynyt salasanaa

## Apachen asennus etäpalvelimelle

- Pakettilista päivitys komennolla sudo apt update ja Apachen asennus komennolla sudo apt install apache2
- Apache2 toimii, näkyy näkyy active (running):


  <img width="440" height="181" alt="26" src="https://github.com/user-attachments/assets/6340d1eb-f5b1-4b9c-be65-f1610e5a8a9b" />


 - Testit:


   <img width="472" height="347" alt="29" src="https://github.com/user-attachments/assets/ec9ad74e-2810-4544-ab91-1200e6da3d72" />
   <img width="438" height="185" alt="30" src="https://github.com/user-attachments/assets/52288ab7-2646-4491-a7bd-a8b487e18cac" />


- Loin hakemiston ja tarkistin oikeudet:


  ```
  linuxuser@test026:~$ mkdir -p /home/linuxuser/public-sites
  linuxuser@test026:~$ ls -ld /home/linuxuser/public-sites
  drwxrwxr-x 2 linuxuser linuxuser 4096 Apr 20 12:37 /home/linuxuser/public-sites
  ```

## UFW:n asennus

- Asennus komennolla sudo apt install ufw
- SSH:n salliminen komennolla sudo ufw allow 22/tcp. Ilman tätä menettäisin SSH-yhteyden
- Sallin HTTP ja HTTPS:


  ```
  linuxuser@test026:~$ sudo ufw allow 80/tcp
  Rules updated
  Rules updated (v6)
  linuxuser@test026:~$ sudo ufw allow 443/tcp
  Rules updated
  Rules updated (v6)
  ```

- Palomuurin käyttöönotto ja tilan tarkistus:


  ```
  linuxuser@test026:~$ sudo ufw enable
  Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
  Firewall is active and enabled on system startup
  linuxuser@test026:~$ sudo ufw status verbose
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

## Networking

- Komento ip a näyttää localhostin, verkkokortin, IP-osoitteen ja broadcast-osoitteen. Ei näytä julkista osoitettani:


  <img width="440" height="155" alt="27" src="https://github.com/user-attachments/assets/326226a7-e397-4c87-b8e2-af6039ec01bd" />

**Packet inspection**

- Ngrep asennus komennolla sudo apt install ngrep

**HTTP-liikenteen kuuntelu**

- Komento sudo ngrep -d eth0 -W byline "" port 80
- Toisessa terminaalissa komento curl http://localhost


  <img width="439" height="268" alt="31" src="https://github.com/user-attachments/assets/393f4423-b2a5-40f2-a516-0257eb60c27e" />

- Viesteissä näkyy GET request, HTTP response (200 OK) ja headers (Host, User-Agent)
- HTTP-liikenne ei ole salattua
- Osa liikenteestä oli jotain taustaliikennettä, ei liittynyt toisen terminaalin komentooni

**SSH-liikenteen kuuntelu**

- Komento sudo ngrep -d eth0 -W byline "" port 22
- Toisessa terminaalissa komento ssh localhost
- Terminaalissa jossa kuuntelen liikennettä, vilisee merkkejä, ei näy mitään. SSH-liikenne on salattua


  <img width="429" height="236" alt="32" src="https://github.com/user-attachments/assets/7c2864ce-74d2-44b8-8d4e-3bac0a7679d6" />

**Ping-kuuntelu**

- Toisessa terminaalissa komento sudo ngrep -d eth0 -W byline "" icmp
- Toisesssa ping 8.8.8.8


  <img width="314" height="207" alt="33" src="https://github.com/user-attachments/assets/f95ee87b-6f77-4601-b89f-429626e2691f" />

- Tuloksessa näkyy ICMP-paketteja omalta VM:ltäni kohti Googlen osoitetta 8.8.8.8 sekä vastauksia takaisin

**Tcpdump**

- Toisessa terminaalissa komento sudo tcpdump -i eth0 icmp
- Toisessa ping 8.8.8.8


  <img width="423" height="106" alt="34" src="https://github.com/user-attachments/assets/c828b4f3-7e7d-41f3-b46f-8705f1eba607" />

- Tcpdump näyttää IP:t ja protokollat. Näyttää pakettien tiedot tarkemmin



  




  





  




  






## Yhteenveto

## Lähteet
