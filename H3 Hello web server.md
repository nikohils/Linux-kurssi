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
## b) Lokirivit
Käytin komentoa _sudo tail -1 /var/log/apache2/access.log_ saadakseni lokitiedot nettisivustani. Tulokseksi sain kuitenkin vain lokitietoja joita oli tallentunut tiistaina 27.1. tehdessämme tehtävää. Kokeilin seuraavia asioita ongelmaan:
- Latasin sivun uusiksi muutamilla eri tavoilla (sisältäen ctrl + F5) näppäinyhdistelmän.
- Avasin nettisivut selaimessa jolla en ollut käsitellyt nettisivua. En kuitenkaan saanut lokitiedostoa päivittymään.
- Komennolla _systemctl status apache2 _kokeilin onko palvelin varmasti käynnissä, johon sain tiedon _running._
Tässä vaiheessa en enää keksinyt ongelmaa, vaan turvauduin tekoälyn apuun (Gemini). Siltä sain vihjeeksi tarkastaa tiedoston jota apache muokkaa. Tähän käytettiin komentoa _ls -ltr /var/log/apache2/_. Sain kolme tiedostoa jotka olivat access.log, error.log sekä other_vhosts_access.log joista viimeisin oli päivittynyt oikea aikaisesti. Kokeilin aiempaa _sudo tail -1 /var/log/apache2/other_vhosts_access.log_ komentoa tähän tiedostoon ja sain lokitiedon joka kohtasi tämä hetken kanssa. Pyysin Geminiä selittämään minulle tilanteen. Sain vastaukseksi seuraavaa:
_- Oletusasetukset: Apachen asennuksen mukana tulee globaali asetus (löytyy yleensä tiedostosta /etc/apache2/conf-enabled/other-vhosts-access-log.conf). Se sanoo palvelimelle: "Jos pyyntö tulee nimellä tai IP-osoitteella, jolle ei ole määritetty omaa, erillistä lokitiedostoa, kirjoita se tänne."_
_Log-prioriteetti: Jos oletus-konfiguraatiossa (000-default.conf) ei ole erikseen määritelty CustomLog-direktiiviä osoittamaan access.log-tiedostoon, tai jos kutsut palvelinta tavalla, jota Apache ei täysin yhdistä tiettyyn sivustoon, se turvautuu tähän "kaikkien muiden" lokiin._
Tästä sain havainnon, että apachelle pitää kertoa mikäli lokitiedot halutaan tiettyyn paikkaan. Tai sitten on vain tiedettävä se, minne lokit menevät.


