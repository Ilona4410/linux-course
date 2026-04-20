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

- ip a -komento:


  <img width="440" height="155" alt="27" src="https://github.com/user-attachments/assets/326226a7-e397-4c87-b8e2-af6039ec01bd" />

 - Testit:


   <img width="472" height="347" alt="29" src="https://github.com/user-attachments/assets/ec9ad74e-2810-4544-ab91-1200e6da3d72" />
   <img width="438" height="185" alt="30" src="https://github.com/user-attachments/assets/52288ab7-2646-4491-a7bd-a8b487e18cac" />


- Loin hakemiston ja tarkistin oikeudet:


  ```
  linuxuser@test026:~$ mkdir -p /home/linuxuser/public-sites
  linuxuser@test026:~$ ls -ld /home/linuxuser/public-sites
  drwxrwxr-x 2 linuxuser linuxuser 4096 Apr 20 12:37 /home/linuxuser/public-sites
  ```






  




  






## Yhteenveto

## Lähteet
