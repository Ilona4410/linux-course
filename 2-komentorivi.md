# Komentorivi

## Johdanto

## Virhetilanne ja ratkaisu - (copy-paste)

Kurssin ensimmäisellä luennolla kävi ilmi, että minulla sekä muutamalla muulla ei toiminut kopiointi ja liittäminen oman koneen ja VM:n välillä. Päätin korjata tämän ongelman ennen, kuin alan harjoitella komentoja. Opettajan neuvosta varmistin, että Shared Clipboard ja Drag-and-Drop -asetukset ovat Bidirectional. Googlasin ongelmaa ensin hakusanoilla "VirtualBox Guest Additions Debian copy paste not working" ja löysin Tech Infokartin YouTube videon "Fix VirtualBox Copy-Paste Not Working: Windows 11 to Ubuntu 24.04 (2026)". Tämän jälkeen koitin liittää Guest Additions CD Imagen, mutta sain virheilmoituksen, jonka mukaan Debianin ISO-levykuva oli kiinni CD-asemassa. Ratkaisin tämän ChatGPT 5.3 -kielimallin avulla poistamalla ISO-tiedoston virtuaalikoneen asetuksista, jolloin CD-asema vapautui. Tämän jälkeen tuli uusi virhe: "Machine has no optical drives" eli CD-asema ei ollut käytössä, koska se jäi tyhjäksi. Ratkaisin tämän lisäämällä uuden tyhjän CD-aseman Storage-asetuksissa "Add Optical Drive". Tämän jälkeen sain onnistuneesti liitettyä Guest Additions CD Imagen. 

Tech Infokartin YouTube videossa Guest Additions asennettiin graafisesti, mutta omasta näkymästäni puuttui kohta "Run Software". Tästä syystä pyysin ChatGPT 5.3 -kielimallilta komennot tekemään sama komentorivillä. 

#### Suoritin seuraavat komennot ja sain copy-pasten toimimaan:
- cd /media/ilona/VBox_GAs_7.2.6 (hakemistoon siirtyminen)
- sudo apt update (pakettilistan päivitys)
- sudo apt install build-essential dkms linux-headers-$(uname -r) (pakettien asennus)
- sudo sh VBoxLinuxAdditions.run (asennusskriptin suorittaminen)
- sudo reboot (järjestelmän uudelleenkäynnistys)

Opin tästä, että kopiointi ja liittäminen ovat VM:lle lisäominaisuuksia, ja näiden saaminen vaatii erillisten lisäosien asentamista. CD-asema, ISO-levykuva ja optinen asema sekä näiden merkitys ei kuitenkaan ihan selvinnyt. Opin kuitenkin hiukan komentorivin käyttöä.

## 1. Basic Commands 

Tässä tehtävässä loin tehtävänannon mukaisen hakemistorakenteen tiedostoineen & tietoineen. 

### Loin ensin uuden kansion kotihakemistoon ja tämän alle kansiot. Loin neljä tiedostoa docs-kansioon. Alla kuva ja käytetyt komennot:

<img width="400" height="235" alt="image" src="https://github.com/user-attachments/assets/54d9fd53-7124-40c1-991e-b1976233b6ce" />

- mkdir practice
- mkdir practice/docs
- mkdir practice/images practice/backups practice/archive
- cd practice/docs
- touch notes1.txt notes2.txt notes3.txt notes4.txt

### Tämän jälkeen muokkasin luotuja tiedostoja lisäämällä näihin 10 eläintä ja 10 hedelmää/vihannesta + nimesin tiedot uudelleen: 

- nano notes1.txt
- nano notes2.txt
```
ilona@ilona:~/practice/docs$ mv notes2.txt vegetables.txt
ilona@ilona:~/practice/docs$ tree
.
├── animals.txt
├── notes3.txt
├── notes4.txt
└── vegetables.txt

1 directory, 4 files
ilona@ilona:~/practice/docs$ cat animals.txt
Koira
Kissa
Hiiri
Jänis
Hirvi
Hamsteri
Kala
Karhu
Delffiini
Lammas
ilona@ilona:~/practice/docs$ cat vegetables.txt
Omena
Punajuuri
Banaani
Peruna
Mustikka
Porkkana
Inkivääri
Salaatti
Bataatti
Sipuli
```
### Tein tiedostoista varmuuskopiot backups-kansioon ja muokkasin animals.txt-tiedostoa poistamalla eläinten nimiä. Poistin vegetables.txt-tiedoston :

- cp animals.txt ../backups/
- cp vegetables.txt ../backups/
- nano animals.txt (Ctrl + K rivin poisto)
- rm vegetables.txt

### Sitten palautin tiedostot varmuuskopioista docs-kansioon. Lopuksi tein arkistoinnin ja pakkauksen sekä loin uuden test-kansion johon purin arkiston. 

- tar -czvf archive/backup.tar.gz backups/
- mkdir test
- tar -xzvf archive/backup.tar.gz -C test/

<img width="306" height="363" alt="image" src="https://github.com/user-attachments/assets/1822ef13-8882-4b56-816c-ae500df6d0ba" />


## 2. Grep and Pipe

## 3. btop

## 4. Install Your Own Command-Line Application 

## Yhteenveto

## Lähteet

- Tech Infokart 24.4.2026. Fix VirtualBox Copy-Paste Not Working: Windows 11 to Ubuntu 24.04 (2026). Video. Katsottavissa: https://www.youtube.com/watch?v=c0Grtq7GAXs. Katsottu: 1.4.2026.
