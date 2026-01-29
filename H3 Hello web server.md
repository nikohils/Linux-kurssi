# H2. Komentaja pingviini
- Päivämäärä: 29.1.2026
- Tekijä: Niko
- Ympäristö: (Sama kuin kohdassa H1) Dell Precision M4600, Linux Mint käyttöjärjestelmä jossa asennettuna VirtualBox jossa Linux Debian 13.
## x) Tiivistelmät
The Apache software foundation 2023
- **Toimintaperiaate**: Name-based virtual hosting mahdollistaa useiden eri verkkosivustojen isännöinnin samassa IP-osoitteessa. Palvelin erottaa sivustot toisistaan selaimen lähettämän HTTP "Host"-otsikon perusteella.
- **Oletussivosto**: Jos pyyntö ei täsmää mihinkään määritettyyn ServerName- tai ServerAlias-asetukseen, Apache käyttää konfiguraatiotiedoston ensimmäistä listattua virtuaali-isäntää oletuksena.
- **Keskeiset asetukset**: Tärkeimmät asetukset ovat <VirtualHost>, ServerName (sivuston nimi), ServerAlias (vaihtoehtoiset nimet) ja DocumentRoot (tiedostopolku).
- **Keskeinen suositus:** Dokumentaatio suosittelee käyttämään aina nimeen perustuvia virtuaali-isäntiä (IP-pohjaisten sijaan), ellei ole erityistä teknistä syytä toimia toisin, sillä se säästää IP-osoitteita.
Tero Karvinen
- **Käytännön toteutus**: Opas näyttää, miten uusi sivusto lisätään Debian/Ubuntu-pohjaisessa järjestelmässä luomalla asetustiedosto hakemistoon /etc/apache2/sites-available/.
- **Käyttäjäoikeudet**: Karvinen korostaa hyvää tapaa sijoittaa verkkosivut käyttäjän kotihakemistoon (esim. public_html), jolloin niitä voi muokata ilman pääkäyttäjän (sudo) oikeuksia.
- ## a) Testaus
Tämä vaihe tehtiin harjoitteena luennon aikana joten vaiheesta ei ole dokumentaatiota.
## b)
