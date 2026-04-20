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


```
linuxuser@test026:~$ sudo systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Wed 2026-04-15 06:33:33 UTC; 5 days ago
 Invocation: a2950ddfb1b24de690b65c5ff114d144
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 10732 (sshd)
      Tasks: 1 (limit: 423)
     Memory: 11.1M (peak: 154.9M)
        CPU: 6min 39.767s
     CGroup: /system.slice/ssh.service
             └─10732 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
 ``` 

## SSH-avainkirjautuminen

- Loin avaimen omalle virtuaalikoneelle ja annoin palvelimelle luvan hyväksyä sen. Salasanakirjautuminen -> avaimella kirjautuminen
- Komento omalla koneella ssh-keygen -> private key minulle ja public key jaettavaksi
- Kopioin avaimen palvelimelle ssh-copy-id linuxuser@65.52.72.83
- Testasin SSH-yhteyttä uudelleen komennolla ssh linuxuser@65.52.72.83 ja avainkirjautuminen onnistuis, ei kysynyt salasanaa

## Apachen asennus etäpalvelimelle

- Pakettilista päivitys komennolla sudo apt update ja Apachen asennus komennolla sudo apt install apache2
- Apache2 toimii, näkyy näkyy active (running):


  ```
  linuxuser@test026:~$ sudo systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/apache2.service; enabled; preset: enabled)
     Active: active (running) since Mon 2026-04-20 12:09:50 UTC; 1min 34s ago
 Invocation: fdbaffadc56d4db0b71d109dab967ee0
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 65131 (apache2)
      Tasks: 55 (limit: 423)
     Memory: 5.9M (peak: 7M)
        CPU: 60ms
     CGroup: /system.slice/apache2.service
             ├─65131 /usr/sbin/apache2 -k start
             ├─65132 /usr/sbin/apache2 -k start
             └─65162 /usr/sbin/apache2 -k start
  ```







## Yhteenveto

## Lähteet
