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

Avoin lähdekoodi tarkoittaa ohjelmistoja (esim. Linux), joiden lähdekoodi on vapaasti kaikkien nähtävissä, muokattavissa ja jaettavissa. Tämä mahdollistaa sen, että kehittäjät ympäri maailmaa voivat osallistua ohjelmistojen kehittämiseen. Avoimessa lähdekoodissa käyttäjien on mahdollista tarkastella miten ohjelma toimii, ja tehdä haluamiansa muutoksia koodiin. (Coursera Staff 2025).

Yhteistyö, läpinäkyvyys ja vapaus käyttää ohjelmistoa eri tarkoituksiin ovat avoimen lähdekoodin perusperiaatteita. Ohjelmistot ovat usein maksuttomia ja niitä voidaan muokata ilman suurempia rajoituksia linsenssistä riippuen. Avoin lähdekoodi on nykyään hyvin yleistä, ja suurin osa nykyaikaisista ohjelmistoista sisältää avoimen lähdekoodin komponentteja. (Coursera Staff 2025).

Kustannustehokkuus, joustavuus ja aktiivinen kehittäjäyhteisö ovat avoimen lähdekoodin etuja. Nämä mahdollistavat ohjelmistojen jatkuvan parantamisen. Haasteina ovat esimerkiksi mahdollisest tietoturva-aukot, yhteensopivuusongelmat ja se, ettei ohjelmistolla ole yhtä vastuussa olevaa ylläpitäjää. (Coursera Staff 2025).

Avoin lähdekoodi mahdollistaa nopean kehityksen ja innovoinnin, koska suuri joukko kehittäjiä voi osallistua ohjelmistojen parantamiseen. Tämä on varmasti yksi syy sille, minkä takia teknologia kehittyy nykyisin niin nopeasti. Toisaalta tämä on myös välttämätöntä, sillä ilman nykyaikaista teknologiaa ja digitaalista infraa, eivät internet ja monet digitaaliset palvelut toimisi nykyisessä laajuudessaan. 

Tulevaisuutta ajatellen haasteena voi olla ainakin se, että avoimen lähdekoodin käyttö voi vaatia enemmän teknistä osaamista, eikä ohjelmistoilla ole aina keskitettyä tukea tai vastuullista tahoa. Ainakin organisaatiot tarvitsevat yleensä valmiita ja tuettuja ratkaisuja. Toisaalta on hyvä, että avoin lähdekoodi vähentää riippuvuutta yksittäisistä yrityksistä. Tämä taas lisää itsenäisyyttä ja joustavuutta. 

Lopuksi voisi sanoa, että nykyiselle digitaaliselle infralle avoin lähdekoodi on välttämätön, jotta uutta teknologiaa voidaan kehittää nopeasti ja tarkastella mahdollisimman läpinäkyvästi ja luotettavasti. 

## Yhteenveto

Opin asentamaan Debian Linux:in virtuaalikoneeseen ja tutustuin GitBHubin käyttöön tehtävien raportoinnissa. Lisäksi tutustuin avoimeen lähdekoodiin. Avoin lähdekoodi mahdollistaa teknologian jatkuvan kehityksen ja joustavuuden, mutta vaatii käyttäjiltä teknistä osaamista eikä välttämättä sovi kaikkiin ympäristöihin.  

Käytännön harjoituksessa ymmärsin, kuinka virtuaalikone toimii erillisenä ympäristönä ilman vaikutusta pääjärjestelmääni. Opin myös muutaman peruskomennon harjoituksen testi-osiossa. 

## Lähteet

- Coursera Staff. 31.12.2025. What Is Open Source Software and Why Use OSS? Coursera. Luettavissa: https://www.coursera.org/articles/what-is-open-source-software. Luettu: 28.3.2026.
- Debianin asennus - video. Linux-palvelimet -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Katsottu 28.3.2026.
- Heinonen, J. How to Install Linux to Virtualbox? Luettavissa: https://github.com/johannaheinonen/johanna-test-repo/blob/main/module_1.md. Luettu 28.3.2026.
- VirtualBox Virtuaalikoneen luonti - video. Linux-palvelimet -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Katsottu 28.3.2026.


