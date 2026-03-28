# Johdanto

Tässä tehtävässä asensin Debian Linuxin VirtualBox VM:ään. Lisäksi loin GitHub repon raporttien tallentamista varten sekä tutustuin avoimen lähdekoodin (open source software) käsitteeseen artikkelin "What is Open Source Software and Why use OSS" pohjalta. Artikkelista tehdyn tiivistelmän lisäksi pohdin sitä, miten avoimen lähdekoodin ohjelmistot vaikuttavat nykyaikaiseen teknologiaan ja digitaaliseen infraan. 

Edellä kuvattujen tehtävien tarkoituksena oli oppia asentamaan Linux sekä ymmärtää GitHubin käyttöä raporttien tallentamiseen ja jakamiseen. Tavoitteena oli myös ymmärtää, mitä avoin lähdekoodi tarkoittaa ja mikä tämän rooli nykyään on teknologiassa. 

## Linuxin asentaminen omalle koneelle

Asennuksen ensimmäisessä vaiheessa asensin VirtualBoxin (https://www.virtualbox.org/wiki/Downloads) ja varmistin, että virtualisointituki (VT-x) oli käytössä tietokoneeni UEFI/BIOS-asetuksissa. 

Seuraavaksi latasin Debian Linux ISO-levykuvan debian-live-13.4.0-amd64-xfce.iso (https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/debian-live-13.4.0-amd64-xfce.iso). ISO-tiedosto sisälsi käyttöjärjestelmän asennustiedot ja liitin tämän virtuaalikoneeseen. 

Loin virtuaalikoneen määrittämällä tärkeimmät resurssit: keskusmuisti RAM, prosessoriytimet ja levytilan. Käytin määrittelyssä EFI-käynnistystä, joka vastaa nykyistä laiteympäristöä. 

<img width="416" height="214" alt="1" src="https://github.com/user-attachments/assets/34636f87-804b-415b-b984-119a335f2947" />


Ennen varsinaista asennusta testasin järjestelmää live-tilassa. Tämän avulla varmistin, että käyttöjärjestelmä käynnistyy oikein ja että verkkoyhteys toimii. Alla pari kuvaa testeistä. 

Tein varsinaisen asennuksen graafisella asennusohjelmalla. Tässä määrittelin kielen, aikavyöhykkeen, näppäimistön sekä käyttäjätiedot. Levyasetuksessa valitsin "Erase disk", jolla alustettiin virtuaalikoneen levy uutta asennusta varten. 

Asennuksen jälkeen käynnistin järjestelmän uudelleen kirjauduin sisään luomillani tunnuksilla. Lopuksi päivitin järjestelmän kahdella eri komennolla, jotta ohjelmistot olisivat ajan tasalla. Alla kuva. 
