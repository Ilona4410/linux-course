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

- Latasin/kopioin kussin repon omalle virtuaalikoneelleni komennolla ```git clone git@github.com:linux-spring-26/git-testing.git```
- Loin tiedoston ilona_testi.txt ja lisäsin sinne perusvinkin


  ```
  ilona@ilona:~/git-testing$ nano ilona_testi.txt
  ilona@ilona:~/git-testing$ git status
  On branch main
  Your branch is up to date with 'origin/main'.

  Untracked files:
  (use "git add <file>..." to include in what will be committed)
	ilona_testi.txt

  nothing added to commit but untracked files present (use "git add" to track)
  ilona@ilona:~/git-testing$ git push
  Enumerating objects: 4, done.
  Counting objects: 100% (4/4), done.
  Delta compression using up to 2 threads
  Compressing objects: 100% (3/3), done.
  Writing objects: 100% (3/3), 392 bytes | 392.00 KiB/s, done.
  Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
  remote: Resolving deltas: 100% (1/1), completed with 1 local object.
  To github.com:linux-spring-26/git-testing.git
  e8ebc3c..ab5a382  main -> main
  ```


- Oma julkaisuni näkyy osoitteessa https://github.com/linux-spring-26/git-testing



  






## Yhteenveto

## Lähteet
