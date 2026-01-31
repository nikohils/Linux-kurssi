# H3. Hello web server
- Päivämäärä: 29.1.2026
- Tekijä: Niko
- Ympäristö: (Sama kuin kohdassa H1) Dell Precision M4600, Linux Mint käyttöjärjestelmä jossa asennettuna VirtualBox jossa Linux Debian 13.
## x) Tiivistelmät 29.1.2026 19:15 - 19:45
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
## b) Lokirivit 29.1.2026 19:45 - 20:30
Käytin komentoa _sudo tail -1 /var/log/apache2/access.log_ saadakseni lokitiedot nettisivustani. Tulokseksi sain kuitenkin vain lokitietoja joita oli tallentunut tiistaina 27.1. tehdessämme tehtävää. Kokeilin seuraavia asioita ongelmaan:
- Latasin sivun uusiksi muutamilla eri tavoilla (sisältäen ctrl + F5) näppäinyhdistelmän.
- Avasin nettisivut selaimessa jolla en ollut käsitellyt nettisivua. En kuitenkaan saanut lokitiedostoa päivittymään.
- Komennolla _systemctl status apache2 _kokeilin onko palvelin varmasti käynnissä, johon sain tiedon _running._
Tässä vaiheessa en enää keksinyt ongelmaa, vaan turvauduin tekoälyn apuun (Gemini). Siltä sain vihjeeksi tarkastaa tiedoston jota apache muokkaa. Tähän käytettiin komentoa _ls -ltr /var/log/apache2/_. Sain kolme tiedostoa jotka olivat access.log, error.log sekä other_vhosts_access.log joista viimeisin oli päivittynyt oikea aikaisesti. Kokeilin aiempaa _sudo tail -1 /var/log/apache2/other_vhosts_access.log_ komentoa tähän tiedostoon ja sain lokitiedon joka kohtasi tämä hetken kanssa. Pyysin Geminiä selittämään minulle tilanteen. Sain vastaukseksi seuraavaa:
- _- Oletusasetukset: Apachen asennuksen mukana tulee globaali asetus (löytyy yleensä tiedostosta /etc/apache2/conf-enabled/other-vhosts-access-log.conf). Se sanoo palvelimelle: "Jos pyyntö tulee nimellä tai IP-osoitteella, jolle ei ole määritetty omaa, erillistä lokitiedostoa, kirjoita se tänne."_
- _Log-prioriteetti: Jos oletus-konfiguraatiossa (000-default.conf) ei ole erikseen määritelty CustomLog-direktiiviä osoittamaan access.log-tiedostoon, tai jos kutsut palvelinta tavalla, jota Apache ei täysin yhdistä tiettyyn sivustoon, se turvautuu tähän "kaikkien muiden" lokiin._
- Tästä sain havainnon, että apachelle pitää kertoa mikäli lokitiedot halutaan tiettyyn paikkaan. Tai sitten on vain tiedettävä se, minne lokit menevät.

<img width="1206" height="212" alt="Kuvakaappaus 2026-01-29 16-51-58" src="https://github.com/user-attachments/assets/8a5e2c5f-8856-4837-9148-9958f24591ca" />

Ylläolevassa kuvassa näkyy lokimerkintä jonka sain. Lokitiedoston merkinnöistä sain selville seuraavaa pohdittuani vähän aikaa näkemääni:
- zxcv.example.com:80 -> Koneeseeni asettama käyttäjänimi johon pyyntö kohdistui. Portti on 80 eli salaamaton HTTP liikenteen portti.
- 127.0.0.1 -> Asiakkaan/vierailijan IP osoite. Koska vierailin omalla palvelimellani omalta koneeltani, näkyy tässä LocalHost osoite.
- - - -> Liittyvät tunnistautumistietoihin jos ne ovat käytössä.
- 29/Jan/2026:16:28:28 +0200 -> Pyynnön aikaleima ja aikavyöhyke.
- GET /favicon.ico HTTP/1.1 -> Pyydetty sivuston kuvaketta (Karvisen luennolla mainittu favicon) käytetty HTTP/1.1 protokollaa.
- 404 -> favicon pyynnön perässä ilmaisee, ettei kuvaketta ole löytynyt "Not found".
- 487 -> Vastauksen koko tavuina.
- http://localhost/ -> Sivun osoite josta pyyntö saanut alkunsa.
- Mozilla/5.0 -> Käytetty selain.
- X11; Linux x86_64 -> Käytetty käyttöjärjestelmä sekä prosessoriarkkitehtuuri ja 64 bittinen järjestelmä.

## c) Etusivu uusiksi 31.1.2026 06:00 - 06:50
Tämä tehtävähän tehtiin jo oppitunnilla eikä tässä pitänyt olla mitään hankalaa. Muutaman nukutun yön jälkeen kuitenkin tuntui, että pää oli formatoinut hankitun osaamisen ja tiedon. Jouduin vaihtelemaan kansioita useasti, tarkastamaan tiedostoja, palaamaan aiemmin opetettuun ja muistelemaan, että mitä tehtiin ja miksi. Dokumentaation tekeminen suoritetuista tempuista jäi uupumaan, koska prosessointiteho meni tehtävänannon sisäistämiseen sekä aiemmin opitun kertaamiseen.

<img width="565" height="70" alt="Kuvakaappaus 2026-01-31 06-40-27" src="https://github.com/user-attachments/assets/aae86910-da17-46ee-bb7c-6cd0ae92a6c5" />

Ohessa näkyy tehtävänannossa mainittu hattu.conf tiedoston luonti.

<img width="864" height="71" alt="Kuvakaappaus 2026-01-31 06-42-13" src="https://github.com/user-attachments/assets/2c915cb5-db12-4278-997b-e97b7864fd7d" />

Ohessa näkyy tehtävänannossa mainittu tieto uudesta serverinimestä.

<img width="507" height="188" alt="Kuvakaappaus 2026-01-31 06-45-03" src="https://github.com/user-attachments/assets/40c2dc48-8661-4604-b96b-dea8c75e2329" />

Ohessa näkyy curl komennolla haettu tieto sivuston sisällöstä.

## e) Validi HTML5 sivu 31.1.2026 06:55 - 
Muokattiin index.html tiedostoa HTML koodilla siten, että sivusto saatiin jo tekemään jotakin normaalin nettisivun kaltaisia temppuja. Sivustossa käytettiin otsikointia (h1) sekä tekstiriviä (p). Merkistöksi asetettiin UTF-8 jotta myös ääkköset näkyvät.

<img width="975" height="358" alt="Kuvakaappaus 2026-01-31 06-56-19" src="https://github.com/user-attachments/assets/1259c9f8-796f-4f7a-b397-c1261880f5bd" />

Seuraavaksi todennettiin selaimessa nettisivun toimivuus.

<img width="1192" height="353" alt="Kuvakaappaus 2026-01-31 06-56-38" src="https://github.com/user-attachments/assets/b13bf541-b7b7-41ab-9b43-f79219e70414" />

Lopuksi vielä curl komennolla otettu 
