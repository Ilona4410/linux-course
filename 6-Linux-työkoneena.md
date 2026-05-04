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
  
- Konfiguroin ~/.ssh/config -tiedostoa, jotta SSH-avain toimii:


  ```
  Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github_key
  ```

- Tallensin julkisen avaimen GitHubiin ja testasin yhteyttä: 

  ```
  ilona@ilona:~$ cat ~/.ssh/github_key.pub
  ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICIREaz3OZPNTvj4BLIikZ2vehgfs39eTxpYwcTLGFgl github key
  ilona@ilona:~$ ssh -T git@github.com
  The authenticity of host 'github.com (140.82.121.4)' can't be established.
  ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
  This key is not known by any other names.
  Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
  Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
  Hi Ilona4410! You've successfully authenticated, but GitHub does not provide shell access.
  ```






## Yhteenveto

## Lähteet
