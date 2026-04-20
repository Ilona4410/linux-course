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


    <img width="437" height="259" alt="28" src="https://github.com/user-attachments/assets/2896c6f5-0031-4ec4-a3f2-0d3fa1ff13e5" />




  






## Yhteenveto

## Lähteet
