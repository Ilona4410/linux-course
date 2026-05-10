# Shell Scripting - perusteet

## Johdanto

## Bash Shell 

- Aloitin tekemällä varmuuskopion Bash Shellin asetustiedostosta komennolla ```cp ~/.bashrc ~/.bashrc_backup```
- Muokkasin Bashin asetuksia alla kuva ja testi:

  <img width="732" height="373" alt="image" src="https://github.com/user-attachments/assets/fb9a13c9-7bf6-4ba8-9f1a-d96fb5890de8" />
  <img width="475" height="192" alt="image" src="https://github.com/user-attachments/assets/d783d7d5-0e37-482d-a5ca-9a59a8a505ee" />


- Lisäsin Bashin asetuksiin kaksi alias-komentoa ja testasin näitä:

  
  ```
  alias ll='ls -l'
  alias gs='git status'
  ```

  <img width="700" height="490" alt="image" src="https://github.com/user-attachments/assets/d79f447d-dcef-4712-b3c7-e3c9ee3ff6c2" />


- Seuraavaksi teihin muutoksia näihin: HISTSIZE ja HISTFILESIZE
    - HISTSIZE = Komentojen määrä, jotka Bash muistaa nykyisessä terminaalissa
    - HISTFILESIZE = Komentojen määrä, jotka tallennettaan


  ```
  HISTSIZE=2000
  HISTFILESIZE=4000
  ```

- Muutosten ansiosta minulla on nyt enemmän historiaa käytettävissä. Alla viimeisimmät komentoni:


  ```
  ilona@ilona:~$ tail ~/.bash_history
  sudo sh VBoxLinuxAdditions.run
  sudo reboot
  ping -i 0.1 8.8.8.8
  yes > /dev/null
  sudo tail -f /var/log/apache2/error-site2.log
  ssh linuxuser@65.52.72.83
  cp ~/.bashrc ~/.bashrc_backup
  ~/.bashrc 
  sudo ~/.bashrc 
  nano ~/.bashrc
  ```

  





## Yhteenveto

## Lähteet
