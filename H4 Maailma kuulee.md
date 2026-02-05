# H4. Maailma kuulee
- Päivämäärä: 5.2.2026
- Tekijä: Niko
- Ympäristö: Dell Precision M4600, Linux Mint käyttöjärjestelmä jolla käytetäänb UpCloudista vuokrattua Debian Trixie 13 palvelinta. 1gb RAM muistia.

## x) Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla 5.2.2026 18:00 - 18:30
- Pilvipalvelimen vuokraus: Palvelimen valinnassa huomioidaan hinta ja sijainti. SSH-avainten käyttö jo luontivaiheessa parantaa tietoturvaa merkittävästi (salasanaton kirjautuminen).
- Palomuurin suojaus: Palomuuri (ufw) on kriittinen. On sallittava vain tarvittavat portit (kuten 22/SSH ja 80/HTTP) ja kytkettävä se päälle heti.
- Kotisivujen asennus: Apache-verkkopalvelimen asennuksella ja oletussivun muokkaamisella todennetaan, että palvelin vastaa julkisiin pyyntöihin.
- Päivitykset: Järjestelmän pitäminen ajan tasalla (apt update & upgrade) on perusedellytys tietoturvassa.

## x) Karvinen 2012/2017: First Steps on a New Virtual Private Server 5.2.2026 18:30 - 19:00
- SSH-yhteys: Kirjautuminen tapahtuu etänä komentoriviltä. SSH-avaimet ovat salasanoja turvallisempi vaihtoehto.
- Käyttäjien hallinta: Ei työskennellä root-käyttäjänä. Luodaan uusi käyttäjä, annetaan sille sudo-oikeudet ja lukitaan root-tunnus. Root tunnus mahdollistaa järjestelmän hallinnan sekä muokkaamisen "god modessa" jolloin voidaan tuhota vaikka koko palvelimen sisältö. Muistetaan, että Linux ei juuri kysele varmistuksia tehdäänkö jotain.
- Tietoturvan perusaskeleet: Päivitetään ohjelmistopaketit heti asennuksen jälkeen ja varmistetaan palomuurin tila.
- Testaus: Verkkopalvelimen toimivuus varmistetaan katsomalla IP-osoitetta selaimella, jolloin näkyviin tulee Apachen oletussivu.

## a) Palvelimen vuokraaminen 3.2.2026 14:00 - 16:45
- Tämä vaihe toteutettiin luentojen yhteydessä joten sitä ei dokumentoitu.

## b) Alkutoimet palvelimella 5.2.2026 19:25 - 20:20
- Kirjautuminen omalle palvelimelleni UpCloudin palvelussa. IP osoite otettu omalta sivultani kirjauduttani tunnuksillani sivustolle. Kirjautuminen tapahtuu komennolla ssh root@_IP osoite_.

- Seuraavaksi palvelimen päivittäminen _apt update && apt full-upgrade_. Näissä ei tarvita tässä vaiheessa sudo etuliitettä, koska alkuvaiheessa olemme kirjautuneet "roottina".
- Tämän jälkeen palomuurin asentaminen apt get-install ufw.
- Palomuurin asentamisen jälkeen sallimme ainakin portin 22 (SSH kirjautuminen) _ufw allow 22/tcp_. Oletusarvoisesti palomuuri hylkää kaiken ulkoa tulevan liikenteen joten mikäli käynnistämme palomuurin ennenkuin sallimme portin 22 SSH liikenteen, emme pääse enää käyttämään palvelintamme etänä. Toinen sallittava portti on 80 (HTTP liikenne) _ufw allow 80/tcp_ joka sallii salaamattoman verkkoliikenteen, eli internet selaimet voivat hakea palvelimelta HTML tiedostoja. Portin 80 voi sallia myöhemminkin.
- Miksi käytimme porttien avaamisessa tcp päätettä? Koska kyseessä on yhteydellinen protokolla (Transmission Control Protocol) eikä yhteydetön UDP (Universal Data Package). Näin sallimmme yhteydellisen protokollan käyttämisen mutta emme yhteydettömän. Tämä on tietoturvallisempaa tässä vaiheessa.
Palomuurin konfiguroinnin jälkeen käynnistämme palomuurin _ufw enable_ komennolla.

- Seuraavaksi käyttäjien lisääminen. Lähdin lisäämään itselleni käyttäjää sekä oikeuksia komennoilla:
  - adduser Niko (lisätään tämänniminen käyttäjä).
  - adduser Niko sudo (lisätään käyttäjä sudo ryhmään jotta on oikeus käyttää sudo komentoa myöhemmin)
 
- Seuraavaksi kirjautumaan uudella käyttäjällä palvelimelle: ssh Niko@_IP osoite_. -> Vaan eipä onnistunutkaan. Sain ilmoituksen _permission denied (public key)_. Pannahinen, mikä on ongelma? Julkisen avaimen puuttuminen uudelta käyttäjältä. Tero Karvisen sivuilta onneksi löytyi oikeat komennot, joita en luennolta enää millään muistanut. Tarvittavat komennot ovat:
  - _sudo cp -rvn /root/.ssh/ /home/Niko/_ (cp -> copy, -rvn -> recursive verbose no-clobber eli kopioi koko kansio ja sen sisältö, näytä mitä kopioidaan sekä älä ylikirjoita mitään. Lisäksi kerrotaan osoite mikä kansio kopioidaan ja minne).
  - sudo chown -R Niko:Niko /home/Niko/.ssh/ (chown -> change owner eli vaihdetaan omistajaa, -R -> Tehdään kaikille tiedostoille ja kansioille, Niko:Niko -> Asetetaan omistaja sekä ryhmä, lopuksi kerrotaan kansio jossa muutokset tehdään).
  - SSH kirjautuminen on erittäin tietoturvallista. On tärkeää, että käyttöoikeus PKI (Public Key Infrastructure) avaimeen on kunnossa. Jos SSH avainkansion omistaja on joku muu kuin kirjautuja, ei kirjautuminen onnistu. Käyttöoikeuden pitää olla käyttäjällä (ja mahdollisesti rootilla) jotta kukaan muu ei pääse muokkaamaan SSH kansion PKI avainta.
- Lopuksi kirjautuminen saatiin onnistumaan uudella Niko käyttäjällä. Testataan tunnuksen toimivuus päivittämällä järjestelmä _sudo apt upgrade -y_. Nyt sudo komento on tarpeellinen, koska olemme tavallinen käyttäjä ja tarvitsemme sudo oikeuksia erikseen.

- Seuraavaksi lukitaan root tunnus ja tehdään pieni "palvelimen koventamisen" toimenpide seuraavilla komennoilla:
  - sudo usermod --lock root (Tavallaan lukitsee root käyttäjätunnuksen muuttamalla rootin salasanan hash tietoa. Näin syötetyt salasanat eivät enää täsmää olemassaolevaan). Root tunnuksen käyttäminen ei siis ole mahdollista, vaan kaikki tehdyt toimenpiteet täytyy tehdä kirjautuneena käyttäjän, josta jää lokimerkintä.
  - sudo mv -nv /root/.ssh /root/DISABLED-ssh/ (SSH avain eli PKI avain siirretään pois oletuskansiosta. Näin se pysyy tallessa mutta ei ole siellä mistä järjestelmä sitä automaattisesti etsii).

## c) Webbipalvelimen asennus 5.2.2026 20:25 - 
