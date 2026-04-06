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
#### GPL-2 lisenssin tutkiminen grep-, pipe- ja wc-komennoilla

- Koko tiedostossa on 338 riviä
  ```
  ilona@ilona:~$ wc -l /usr/share/common-licenses/GPL-2
  338 /usr/share/common-licenses/GPL-2
  ```
- Komennolla grep GNU /usr/share/common-licenses/GPL-2 näytetään kaikki rivit, jotka sisältävät sanan GNU
  
- Rivien lukumäärä joissa sana GNU, saadaan yhdistämällä grep, wc ja pipe
  ```
  ilona@ilona:~$ grep GNU /usr/share/common-licenses/GPL-2 | wc -l
  8
  ```
- Kaikki rivit, jotka sisältävät sanan license saadaan komennolla:
  ```
  ilona@ilona:~$ grep license /usr/share/common-licenses/GPL-2
  ```
- Jotta edellisestä komennosta saadaan case sensitive ja näkyviin vain rivit joissa sana license pienillä kirjaimilla:
  ```
  ilona@ilona:~$ grep -i license /usr/share/common-licenses/GPL-2
  ```
- Oma kyselyni, jolla selvitin, kuinka monella rivillä mainitaan sana permission pienillä kirjaimilla:
  ```
  ilona@ilona:~$ grep -i permission /usr/share/common-licenses/GPL-2 | wc -l
  4
  ```
#### GPL-2 lisenssin pääkohdat 

- Ohjelmiston käyttö, kopiointi, muokkaus ja jakaminen ovat sallittu
- Lähdekoodin täytyy kuitenkin olla saatavilla
- Muokatut versiot täytyy jakaa samalla lisenssillä
- Lisenssin avulla voidaan varmistaa, että ohjelmisto pysyy avoimena kaikille
- Ohjelman käyttö tapahtuu aina omalla vastuulla, eikä sille ole takuuta
  
(GNU, 2026)

## 3. btop

### Asennus

- Btop on työkalu resurssien hallintaan. Se näyttää reaaliaikaisesti mm. CPU:n, muistin ja verkon tilan
- Asensin ohjelman komennolla sudo apt-get install btop
- Käynnistin ohjelman komennolla btop
  
  <img width="819" height="511" alt="image" src="https://github.com/user-attachments/assets/71629fb0-a1f4-4c60-907c-2dd16a22f06a" />
  <img width="823" height="519" alt="image" src="https://github.com/user-attachments/assets/2c9c5f57-57c1-4f95-8a73-6266aef8b924" />

- Komento which btop näyttää ohjelman sijainnin
  ```
  ilona@ilona:~$ which btop
  /usr/bin/btop
  ```
  
- Koko järjestelmän asetukset sijaitsevat /etc ja käyttäjäkohtaiset asetukset ~/.config

### Konfiguraatio

- Komento dpkg -L btop näyttää kaikki btop:in asentamat tiedostot
- Tein asetustiedostosta varmuuskopion: cp ~/.config/btop/btop.conf ~/.config/btop/btop.conf.orig
- Muokkasin asetuksia: update_ms (päivitysnopeus), proc_tree = True (prosessinäkymä puurakenteiseksi)
- Kokeilin tehdä tarkoitksella virheen (proc_tree = Truuuuue). Väärin kirjoitettu asetus ei mennyt läpi, vaan jäi default-asetukseen
- Tein oman muutoksen config-tiedostossa ja muutin väriteemaa: color_theme = "TTY"

### Load Generation

- Tässä tehtävässä kokeilin kuormittaa CPU:ta ja verkkoa sekä katsoa, mitä btop:ssa näkyy
- Kun pingasin Googlea (ping -i 0.1 8.8.8.8) huomasin, että network activity kasvoi
- Kun ajoin komennon yes > /dev/null, CPU nousi korkealle 

## 4. Install Your Own Command-Line Application 

- Asensin tässä tehtävässä CLI-ohjelman nimeltä htop. Löysin tämän reddit keskustelupalstalta jonka otsikko oli: "What are some CLI apps that someone should not miss when using Linux?"
- Asensin ohjelman komennolla sudo apt install htop
  
<img width="1093" height="685" alt="image" src="https://github.com/user-attachments/assets/4318a02f-1d21-4dca-adb4-4c656a58aa53" />

- Htop:lla voi seurata järjestelmän tilaa ja selvittää ongelmia
- Kuvassa näkyvä PERCENT_CPU näyttää sen, mikä kuormittaa konetta eniten
- PERCENT_MEM taas näyttää, mikä käyttää eniten RAM:ia
- Jos kone käy hitaalla tai jokin toimii muuten huonosti, voi syyn selvittää melko helposti htop:n avulla

## Yhteenveto

Kurssin toisella viikolla tutustuin komentorivin käyttöön ja peruskomentoihin. Opin liikkumaan hakemistossa ja harjoittelin tiedostojen ja kansioiden hallintaa sekä varmuuskopiointia. Opin myös, mitä grep-, wc- ja pipe-komennoilla voi tehdä. 

Tutustuin myös btop-työkaluun, jonka avulla on mahdollista seurata reaaliajassa resurssien käyttöä. Lisäksin muokkasin ensimmäistä kertaa konfiguraatio-tiedostoa. Latasin myös omavalintaisen CLI-ohjelman ja tutustuin tämän käyttöön. 

Tiivistettynä voisi sanoa, että opin komentorivin käyttöä ja tutustuin kahteen eri ohjelmaan, jolla voidaan hallita ja tarkkailla järjestelmän toimintaa.

## Lähteet

- Tech Infokart 24.4.2026. Fix VirtualBox Copy-Paste Not Working: Windows 11 to Ubuntu 24.04 (2026). Video. Katsottavissa: https://www.youtube.com/watch?v=c0Grtq7GAXs. Katsottu: 1.4.2026.
- GNU Operating System Supported by the Free Software Foundation. GNU General Public License, version 2. Luettavissa: https://www.gnu.org/licenses/old-licenses/gpl-2.0.html. Luettu: 4.4.2026.
- reddit 2021. What are some CLI apps that someone should not miss when using Linux?. Luettavissa: https://www.reddit.com/r/linuxquestions/comments/pghfap/what_are_some_cli_apps_that_someone_should_not/. Luettu: 6.4.2026.

