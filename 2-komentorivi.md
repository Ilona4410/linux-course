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

#### Loin ensin uuden kansion kotihakemistoon ja tämän alle kansiot. Loin neljä tiedostoa docs-kansioon. Alla kuva ja käytetyt komennot:

<img width="400" height="235" alt="image" src="https://github.com/user-attachments/assets/54d9fd53-7124-40c1-991e-b1976233b6ce" />

- mkdir practice
- mkdir practice/docs
- mkdir practice/images practice/backups practice/archive
- touch notes1.txt notes2.txt notes3.txt notes4.txt

#### Tämän jälkeen muokkasin luotuja tiedostoja lisäämällä näihin 10 eläintä ja 10 hedelmää/vihannesta + nimesin tiedot uudelleen: 

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
#### Tein tiedostoista varmuuskopiot backups-kansioon ja muokkasin animals.txt-tiedostoa poistamalla eläinten nimiä. Poistin vegetables.txt-tiedoston:

- cp animals.txt ../backups/
- cp vegetables.txt ../backups/
- nano animals.txt (Ctrl + K rivin poisto)
- rm vegetables.txt

#### Sitten palautin tiedostot varmuuskopioista docs-kansioon. Lopuksi tein arkistoinnin ja pakkauksen sekä loin uuden test-kansion johon purin arkiston

- cp ../backups/animals.txt .
- cp ../backups/vegetables.txt .
- tar -czvf archive/backup.tar.gz backups/
- mkdir test
- tar -xzvf archive/backup.tar.gz -C test/

<img width="306" height="363" alt="image" src="https://github.com/user-attachments/assets/1822ef13-8882-4b56-816c-ae500df6d0ba" />

## 2. Grep and Pipe

#### Grep-komennolla voidaan etsiä tekstiä tiedostosta

- grep apple fruits.txt  = Etsii tiedostosta rivit, joissa sana apple
- grep -i apple fruits.txt = Optio -i ei ota huomioon isoja ja pieniä kirjaimia
- grep -n apple fruits.txt = Optio -n näyttää rivin rivin numeron tuloksen edessä
- grep -ni apple fruits.txt = Kun yhdistetään -n ja -i, ei huomioida kirjainkokoa ja näytetään rivien numerot
- grep -v apple fruits.txt = Näyttää kaikki rivit, joissa ei olee sanaa apple sen täsmällisessä muodossa
  
```
ilona@ilona:~/practice/docs$ echo -e "apple\nbanana\norange\nApple pie" > fruits.txt
ilona@ilona:~/practice/docs$ cat fruits.txt 
apple
banana
orange
Apple pie
ilona@ilona:~/practice/docs$ grep apple fruits.txt  
apple
ilona@ilona:~/practice/docs$ grep -i apple fruits.txt  
apple
Apple pie
ilona@ilona:~/practice/docs$ grep -n apple fruits.txt 
1:apple
ilona@ilona:~/practice/docs$ grep -ni apple fruits.txt 
1:apple
4:Apple pie
ilona@ilona:~/practice/docs$ grep -v apple fruits.txt 
banana
orange
Apple pie
```
#### wc-komennolla voidaan selvittää, kuinka monta riviä, sanaa ja merkkiä tiedosto sitältää

```
ilona@ilona:~/practice/docs$ wc -l fruits.txt
4 fruits.txt
ilona@ilona:~/practice/docs$ wc -w fruits.txt 
5 fruits.txt
ilona@ilona:~/practice/docs$ wc -w fruits.txt 
5 fruits.txt
ilona@ilona:~/practice/docs$ wc -c fruits.txt
30 fruits.txt
```
#### Pipe (|). Tämän avulla voidaan yhdistää komentoja

- cat animals.txt | grep cat = Näyttää tiedoston sisällön ja suodattaa näkyviin rivit joissa sana teksti cat
- cat animals.txt | wc -l = Näyttää tiedoston ja laskee rivit
- cat animals.txt | sort | uniq = Näyttää tiedoston, sort muuttaa aakkosjärjestykseen ja uniq poistaa duplikaatit

```
ilona@ilona:~/practice/docs$ echo -e "dog\ncat\nhorse\ncow\ncatfish" > animals.txt 
ilona@ilona:~/practice/docs$ cat animals.txt 
dog
cat
horse
cow
catfish
ilona@ilona:~/practice/docs$ cat animals.txt | grep cat 
cat
catfish
ilona@ilona:~/practice/docs$ cat animals.txt | wc -l  
5
ilona@ilona:~/practice/docs$ cat animals.txt | sort | uniq 
cat
catfish
cow
dog
horse
```

## 3. btop

## 4. Install Your Own Command-Line Application 

## Yhteenveto

## Lähteet

- Tech Infokart 24.4.2026. Fix VirtualBox Copy-Paste Not Working: Windows 11 to Ubuntu 24.04 (2026). Video. Katsottavissa: https://www.youtube.com/watch?v=c0Grtq7GAXs. Katsottu: 1.4.2026.
