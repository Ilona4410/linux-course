# Komentorivi

## Johdanto

## 1. Basic Commands 

## 2. Grep and Pipe

## 3. btop

## 4. Install Your Own Command-Line Application 

## Virhetilanne ja ratkaisu - (copy-paste)

Kurssin ensimmäisellä luennolla kävi ilmi, että minulla sekä muutamalla muulla ei toiminut kopiointi ja liittäminen oman koneen ja VM:n välillä. Päätin korjata tämän ongelman ennen, kuin alan harjoitella komentoja. Opettajan neuvosta varmistin, että Shared Clipboard ja Drag-and-Drop -asetukset ovat Bidirectional. Googlasin ongelmaa ensin hakusanoilla "VirtualBox Guest Additions Debian copy paste not working" ja löysin Tech Infokartin YouTube videon "Fix VirtualBox Copy-Paste Not Working: Windows 11 to Ubuntu 24.04 (2026)". Tämän jälkeen koitin liittää Guest Additions CD Imagen, mutta sain virheilmoituksen, jonka mukaan Debianin ISO-levykuva oli kiinni CD-asemassa. Ratkaisin tämän ChatGPT 5.3 -kielimallin avulla poistamalla ISO-tiedoston virtuaalikoneen asetuksista, jolloin CD-asema vapautui. Tämän jälkeen tuli uusi virhe: "Machine has no optical drives" eli CD-asema ei ollut käytössä, koska se jäi tyhjäksi. Ratkaisin tämän lisäämällä uuden tyhjän CD-aseman Storage-asetuksissa "Add Optical Drive". Tämän jälkeen sain onnistuneesti liitettyä Guest Additions CD Imagen. 

Tech Infokartin YouTube videossa Guest Additions asennettiin graafisesti, mutta omasta näkymästäni puuttui kohta "Run Software". Tästä syystä pyysin ChatGPT 5.3 -kielimallilta komennot tekemään sama komentorivillä. 

#### Suoritin seuraavat komennot ja sain copy-pasten toimimaan:
- cd /media/ilona/VBox_GAs_7.2.6 (hakemistoon siirtyminen)
- sudo apt update (pakettilistan päivitys)
- sudo apt install build-essential dkms linux-headers-$(uname -r) (pakettien asennus)
- sudo sh VBoxLinuxAdditions.run (asennusskriptin suorittaminen)
- sudo reboot (järjestelmän uudelleenkäynnistys<9

Opin tästä, että kopiointi ja liittäminen ovat VM:lle lisäominaisuuksia, ja näiden saaminen vaatii erillisten lisäosien asentamista. CD-asema, ISO-levykuva ja optinen asema sekä näiden merkitys ei kuitenkaan ihan selvinnyt. Opin kuitenkin hiukan komentorivin käyttöä.

