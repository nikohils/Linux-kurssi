# H4. Maailma kuulee
- Päivämäärä: 5.2.2026
- Tekijä: Niko
- Ympäristö: Dell Precision M4600, Linux Mint käyttöjärjestelmä jolla käytetäänb UpCloudista vuokrattua Debian Trixie 13 palvelinta. 1gb RAM muistia.

## x) Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla
- Pilvipalvelimen vuokraus: Palvelimen valinnassa huomioidaan hinta ja sijainti. SSH-avainten käyttö jo luontivaiheessa parantaa tietoturvaa merkittävästi (salasanaton kirjautuminen).
- Palomuurin suojaus: Palomuuri (ufw) on kriittinen. On sallittava vain tarvittavat portit (kuten 22/SSH ja 80/HTTP) ja kytkettävä se päälle heti.
- Kotisivujen asennus: Apache-verkkopalvelimen asennuksella ja oletussivun muokkaamisella todennetaan, että palvelin vastaa julkisiin pyyntöihin.
- Päivitykset: Järjestelmän pitäminen ajan tasalla (apt update & upgrade) on perusedellytys tietoturvassa.

## x) Karvinen 2012/2017: First Steps on a New Virtual Private Server
- SSH-yhteys: Kirjautuminen tapahtuu etänä komentoriviltä. SSH-avaimet ovat salasanoja turvallisempi vaihtoehto.
- Käyttäjien hallinta: Ei työskennellä root-käyttäjänä. Luodaan uusi käyttäjä, annetaan sille sudo-oikeudet ja lukitaan root-tunnus. Root tunnus mahdollistaa järjestelmän hallinnan sekä muokkaamisen "god modessa" jolloin voidaan tuhota vaikka koko palvelimen sisältö. Muistetaan, että Linux ei juuri kysele varmistuksia tehdäänkö jotain.
- Tietoturvan perusaskeleet: Päivitetään ohjelmistopaketit heti asennuksen jälkeen ja varmistetaan palomuurin tila.
- Testaus: Verkkopalvelimen toimivuus varmistetaan katsomalla IP-osoitetta selaimella, jolloin näkyviin tulee Apachen oletussivu.

## a) Palvelimen vuokraaminen
- Tämä vaihe toteutettiin luentojen yhteydessä joten sitä ei dokumentoitu.

## b) Alkutoimet palvelimella
- 
