# Komentorivin perusteet (Lähde: Karvinen 2020:https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited)

## Liikkuminen ja katselu
$ pwd - näyttää työhakemiston

$ ls - listaa työhakemiston tiedostot

$ cd terosdir/ - cd (kansion nimi) siirtyy alihakemistoon

$ cd .. - siirtyy hakemistossa yhden ylöspäin

$ less tero.txt - näyttää tekstitiedoston less-näkymässä. Välilyönti = seuraava sivu, b = edellinen sivu, / = haku, q = sulje

$ ls /etc|less - ls /etc listaa kansion /etc sisällön. Pystyviiva | avaa rivit näkymään, jossa pystyy etsimään ja selaamaan

## Tiedostojen käsittely
$ nano FOO.TXT - helpoimmat tekstieditorit pico ja nano. Tiedoston pääte voi olla mikä vaan, tekstitiedosto ei välttämättä ole .txt

$ mkdir NEWFOLDER - luo uusi kansio

$ mv OLDNAME NEWNAME - Jos NEWNAME on tiedosto, nimi muutetaan. Jos NEWNAME on kansio, OLDNAME siirretään sinne

$ cp -r ORIGINAL COPY - kopioi (kopioi myös kansion sisällön)

$ rmdir EMPTYDIR - poistaa tyhjän kansion

$ rm JUNK - poistaa tiedoston

$ rm -r FOLDEROFJUNK - poistaa kansion ja sen sisällön HUOM. rm:stä ei saa palautettua tiedostoja!

## SSH etähallinta
$ ssh tero@example.com - avaa turvallisen etäkomentorivin. Komennolla w näkee muut kirjautuneet käyttäjät. Komennolla exit takaisin omalle koneelle

$ scp -r FOLDER tero@example.com:public_html/ - kopioi kansion etäkoneen hakemistoon

## Ohjeet (Help)
$ man ls - avautuu less-näkymään

$ ls --help
$ wget -h - esim. komennoista joissa sisäänrakennettu ohje

## Historia ja muokkaus
$ ls /etc/re[tab][tab]
reportbug.conf  resolvconf/     resolv.conf - Tab kahdesti näyttää vaihtoehdot

$ history - näyttää historian

## Tärkeät hakemistot
/ – juurihakemisto. /home/tero/ – käyttäjän tero kotihakemisto. /etc/ - järjestelmän asetukset. /var/log/ - lokit

## Hallinnolliset komennot ja oikeudet
- Vähimmän oikeuden periaatteen mukaisesti tulisi käyttää normaalia käyttäjää. Korotetu oikeudet vain tarvittaessa sudo -komennolla
- Ohjelmien turvallisesti asentaminen: pakettienhallinta. $ sudo apt-get update - päivittää saatavilla olevien pakettien listan

$ sudo apt-get -y install nethack-console - asentaa ohjelman


