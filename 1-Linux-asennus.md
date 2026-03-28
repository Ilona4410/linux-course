# Johdanto

Tässä tehtävässä asensin Debian Linuxin VirtualBox VM:ään. Lisäksi loin GitHub repon raporttien tallentamista varten sekä tutustuin avoimen lähdekoodin (open source software) käsitteeseen artikkelin "What is Open Source Software and Why use OSS" pohjalta. Artikkelista tehdyn tiivistelmän lisäksi pohdin sitä, miten avoimen lähdekoodin ohjelmistot vaikuttavat nykyaikaiseen teknologiaan ja digitaaliseen infraan. 

Edellä kuvattujen tehtävien tarkoituksena oli oppia asentamaan Linux sekä ymmärtää GitHubin käyttöä raporttien tallentamiseen ja jakamiseen. Tavoitteena oli myös ymmärtää, mitä avoin lähdekoodi tarkoittaa ja mikä tämän rooli nykyään on teknologiassa. 

## Linuxin asentaminen omalle koneelle

Asennuksen ensimmäisessä vaiheessa asensin VirtualBoxin (https://www.virtualbox.org/wiki/Downloads) ja varmistin, että virtualisointituki (VT-x) oli käytössä tietokoneeni UEFI/BIOS-asetuksissa. 

Seuraavaksi latasin Debian Linux ISO-levykuvan debian-live-13.4.0-amd64-xfce.iso (https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/debian-live-13.4.0-amd64-xfce.iso). ISO-tiedosto sisälsi käyttöjärjestelmän asennustiedot ja liitin tämän virtuaalikoneeseen. 

Loin virtuaalikoneen määrittämällä tärkeimmät resurssit: keskusmuisti RAM, prosessoriytimet ja levytilan. Käytin määrittelyssä EFI-käynnistystä, joka vastaa nykyistä laiteympäristöä. 

<img width="416" height="214" alt="1" src="https://github.com/user-attachments/assets/34636f87-804b-415b-b984-119a335f2947" />

Ennen varsinaista asennusta testasin järjestelmää live-tilassa. Tämän avulla varmistin, että käyttöjärjestelmä käynnistyy oikein ja että verkkoyhteys toimii. Alla pari kuvaa testeistä. 

<img width="548" height="443" alt="3" src="https://github.com/user-attachments/assets/ea3e6907-3bec-4a52-a455-fdd22043db84" />

<img width="416" height="310" alt="4" src="https://github.com/user-attachments/assets/822e8beb-f30d-4710-a601-37b44e474842" />


Tein varsinaisen asennuksen graafisella asennusohjelmalla. Tässä määrittelin kielen, aikavyöhykkeen, näppäimistön sekä käyttäjätiedot. Levyasetuksessa valitsin "Erase disk", jolla alustettiin virtuaalikoneen levy uutta asennusta varten. 

Asennuksen jälkeen käynnistin järjestelmän uudelleen kirjauduin sisään luomillani tunnuksilla. Lopuksi päivitin järjestelmän kahdella eri komennolla (sudo apt-get update ja sudo apt-get upgrade), jotta ohjelmistot olisivat ajan tasalla. Alla kuva. 

<img width="416" height="265" alt="2" src="https://github.com/user-attachments/assets/a8b1ee89-43d2-4f6b-bc50-b92d2a9c0c8b" />

## Avoin lähdekoodi (open source software)

Avoin lähdekoodi tarkoittaa ohjelmistoja (esim. Linux), joiden lähdekoodi on vapaasti kaikkien nähtävissä, muokattavissa ja jaettavissa. Tämä mahdollistaa sen, että kehittäjät ympäri maailmaa voivat osallistua ohjelmistojen kehittämiseen. Avoimessa lähdekoodissa käyttäjien on mahdollista tarkastella miten ohjelmaa ja toimii, ja tehdä haluamiansa muutoksia koodiin. (Coursera Staff 2025).

Yhteistyö, läpinäkyvyys ja vapaus käyttää ohjelmistoa eri tarkoituksiin ovat avoimen lähdekoodin perusperiaatteita. Ohjelmistot ovat usein maksuttomia ja niitä voidaan muokata ilman suurempia rajoituksia linsenssitä riippuen. Avoin lähdekoodi on nykyään hyvin yleistä, ja suurin osa nykyaikaisista ohjelmistoista sisältää avoimen lähdekoodin komponentteja. (Coursera Staff 2025).

Kustannustehokkuus, joustavuus ja aktiivinen kehittäjäyhteisö ovat avoimen lähdekoodin etuja. Nämä mahdollistavat ohjelmistojen jatkuvan parantamisen. Haasteina ovat esimerkiksi mahdollisest tietoturva-aukot, yhteensopivuusongelmat ja se, ettei ohjelmistolla ole yhtä vastuussa olevaa ylläpitäjää. (Coursera Staff 2025).

