# Raportti: Debian 13 asennus virtuaalikoneeseen
## Päivämäärä:
17.1.2026
## Tekijä:
Niko
## Ympäristö:
Vanha, alunperin Windows 10 asennuksella ollut, Dell Precision M4600. Intel core i7 2720QM (neljä ydintä), 16GB RAM muistia, Nvidia Quadro 2000M näytönohjain (jota tosin en ole saanut toimimaan koska suljetut ajurit ja varsin vanha ohjain).
Koneessa ollut noin puoli vuotta asennettuna Linux Mint. Tämänhetkinen asennus 22.2 Cinnamon, versiolla 6.4.8.
## Tiivistelmä:
Asensin tietokoneeseen virtuaalikoneen, johon asensin Debian 13 -käyttöjärjestelmän opintojakson harjoitusta varten. Asennuksessa kohtasin haasteita prosessoriarkkitehtuurin ja kirjautumisen kanssa, mutta sain haasteet ratkaistua varsin helposti. Lopputuloksena on toimiva Debian 13 asennus virtuaalikoneessa.
## Asennusprosessi:
1. Latasin Debian 13 ISO-tiedoston virallisilta sivuilta. Aluksi fläshäsin tiedoston USB-tikulle balenaEtcherillä, mutta totesin asennusvaiheessa, että VirtualBox osaa lukea suoraan .iso-tiedostoa, joka on nopeampaa. Palautin USB-tikun alkuperäiseen kokoonsa Linuxin Levyt-sovelluksella, joka on omasta mielestäni selkeäkäyttöisempi kuin Windowsin vastaava ohjelma.
2. Loin VirtualBoxissa uuden virtuaalikoneen seuraavilla asetuksilla:
   - Nimi: Debian 13
   - RAM muisti: 4096MB
   - Prosessorit: 4 ydintä (Dell M4600 i7 suoritin, neljä ydintä ja kahdeksan säiettä.
   - Levytila: 50GB VDI tiedosto.
3. Ensimmäinen virhetilanne tuli asennusvaiheen alussa ilmoituksella _"This kernel requires an x86-64 CPU, but only detected an i686 CPU."._
4. <img width="877" height="429" alt="kuva" src="https://github.com/user-attachments/assets/0625677d-11a7-4351-8ad9-56e21fab309d" />

  - Ensimmäisenä pääsi tietysti pari kirosanaa, että mikä tätä nyt heti vaivaa. Hetken katseltuani virheilmoitusta ja vaivattuani älynystyröitä tuli mieleen, että tämähän varmaan yrittää nyt asentaa sitä 32 bittistä         versiota.
  - Sammutin virtuaalikoneen, menin asetuksiin ja vaihdoin version 64 bittiseen muotoon. Tämä ratkaisi ongelman ja asennus lähti eteenpäin.
5. Asetukset valitsin pääpiirteittäin seuraaviksi
  - Kieleksi englanti
  - Näppäimistöasetteluksi suomi
  - Ohjattu levytilan käyttö
  - Käyttäjälle salasana
  - XFCE työpöytä
6. Toinen virhetilanne tuli virtuaalikoneen kirjautumisikkunassa Debian 13 asennuksen jälkeen.
  - Käytin asettamaani käyttäjätunnusta ja salasanaa mutta en päässyt kirjautumaan sisälle.
  - Testasin näppäimistöasettelun joka vastasi suomea. Käytössä ei tosin ollut pohjoismaisia merkkejä muutenkaan.
  - Lopulta käynnistin virtuaalikoneen uudelleen, joka nollasi tilanteen ja pääsin kirjautumaan käyttöjärjestelmään. Mysteeriksi jäi mikä tilanteessa oli pielessä.
7. Debian 13 on nyt asennettu ja se toimii Dell Precision M4600 -koneella riittävän sujuvasti. Seuraavaksi tutustutaan käyttöjärjestelmään tarkemmin ja asennetaan tarvittaessa lisäosia.
## Lähteet:
- Tero Karvinen 2006: Raportin kirjoittaminen. http://terokarvinen.com
- Debian projekti: Debian 13 (Trixie) asennusmedia.
- Keskustelu tekoälyassistentin (Gemini) kanssa 14.1.2026: Dell M4600 koneen suorituskyky Linux mintin, virtuaalikoneen ja Debian 13 asennuksen kanssa.
