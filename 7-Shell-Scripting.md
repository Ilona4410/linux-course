# Shell Scripting - perusteet

## Johdanto

Tässä tehtävässä tutustuin Bash Shellin toimintaan ja konfigurointiin. Lisäksi pääsin harjoittelemaan ensimmäistä kertaa yksinkertaisen skriptin tekoa. 

Tavoitteenani oli ymmärtää, miten komentorivin toimintaa voidaan muokata ja kuinka pieniä toistuvia tehtäviä voidaan automatisoida skriptien avulla. 

## Bash Shell 

- Aloitin tekemällä varmuuskopion Bash Shellin asetustiedostosta komennolla ```cp ~/.bashrc ~/.bashrc_backup```
- Muokkasin Bashin asetuksia, alla kuva ja testi:

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

- Muutosten ansiosta komentorivi muistaa nyt enemmän komentoja. Alla viimeisimmät komentoni:


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


## Shell Script 

- Aloitin luomaan skriptin komennolla ```nano project_script.sh```

  <img width="628" height="189" alt="image" src="https://github.com/user-attachments/assets/c9ef5408-e46b-4baf-a821-20d4bc6a2420" />

- Asetin oikeudet komennolla ```chmod u+x project_script.sh```

  ```
  ilona@ilona:~$ ll project_script.sh
  -rwxrw-r-- 1 ilona ilona 127 10. 5. 18:26 project_script.sh
  ```

- Skriptin ajo komennolla ```./project_script.sh```. Alla tulos

  ```
  ilona@ilona:~$ cat project/info.txt
  Username: ilona
  Date: su 10.5.2026 18.28.57 +0300
  ```


## Yhteenveto

Onnistuin muokkaamaan Bash Shellin asetustiedostoa lisäämällä aloitusviestin ja kaksi alias-komentoa. Muutin myös HISTSIZE- ja HISTFILESIZE-arvoja, jolloin komentohistoria säilyttää enemmän aiempia komentoja. Loin myös Bash-skriptin, joka automatisoi kansion ja tiedoston luomisen sekä kirjoittaa tiedostoon käyttäjänimen ja päivämäärän.

Tämä oli kurssin viimeinen raportti/tehtäväkokonaisuus. Samalla tämä oli henkilökohtainen suosikkini kaikista tehtävistä. Harmikseni en ehtinyt tekemään kaikkia tämän viikon tehtäviä, mutta jään varmaan kokeilemaan näitä myöhemmin. Tykkäsin näistä tehtävistä, koska Bashin toiminta ja skripti tuntuivat jotenkin käytännöllisiltä ja helposti ymmärrettäviltä. 

## Lähteet

Heinonen, J. Linux Shell Scripting Basics. Luettavissa: https://github.com/johannaheinonen/johanna-test-repo/blob/main/module_7.md. Luettu: 10.5.2026.
