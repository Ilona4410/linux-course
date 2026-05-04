# Linux työkoneena

## Johdanto

## Git

- Varmistin GitHubista, että sähköpostin yksityisyys on päällä
- Noreply-osoitteeni on 228961716+Ilona4410@users.noreply.github.com
- Gitin asennus komennolla sudo apt install git

- Gitin konfigurointi: käyttäjänimi ja sähköpostiosoite


  ```
  ilona@ilona:~$ git config --global user.name "Ilona"
  ilona@ilona:~$ git config --global user.email "12345678+username@users.noreply.github.com"
  ilona@ilona:~$ git config --list
  user.name=Ilona
  user.email=12345678+username@users.noreply.github.com
  ```


  - Loin SSH-avainparin komennolla ssh-keygen -t ed25519 -C "github key" ja poluksi /home/ilona/.ssh/github_key
    
  - Konfiguroin ~/.ssh/config -tiedostoa:


```
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/github_key
```


## Yhteenveto

## Lähteet
