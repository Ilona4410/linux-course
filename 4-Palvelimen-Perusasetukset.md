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



## Yhteenveto

## Lähteet
