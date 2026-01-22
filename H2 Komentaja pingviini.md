# H2. Komentaja pingviini
Päivämäärä: 22.1.2026
Tekijä: Niko
Ympäristö: (Sama kuin kohdassa H1) Dell Precision M4600, Linux Mint käyttöjärjestelmä jossa asennettuna VirtualBox jossa Linux Debian 13.
## x) Command line basics:
Komentorivin merkitys: Linuxin ja BSD:n komentorivi on säilynyt käytössä vuosikymmeniä (ennen Googlea ja Internetiä), koska se on nopea, ilmaisuvoimainen ja helppo automatisoida.
## Navigointi ja tiedostojen hallinta:
- pwd (working directory), ls (listaus) ja cd (hakemiston vaihto) ovat perusliikkumista.
- Tiedostojen katseluun käytetään less-komentoa (välilyönti kääntää sivua, q lopettaa).
- Muokkaamiseen suositellaan nano- tai pico-editoreita (tallennus Ctrl-X y Enter).
- Tiedostojen poistamisessa (rm, rm -r) on oltava tarkkana, sillä Linuxissa ei ole roskakoria.
## Etähallinta ja apu:
- ssh user@host on turvallinen tapa hallita konetta etänä.
- man-komento (esim. man ls) avaa manuaalisivun.
- Tabulaattori on tärkeä työkalu: se täydentää komennot ja tiedostonimet automaattisesti ja auttaa välttämään kirjoitusvirheitä.
## Pääkäyttäjäoikeudet:
- sudo-komentoa tulee käyttää vain silloin, kun on pakko (esim. ohjelmien asennus tai järjestelmäasetusten muuttaminen), noudattaen minimioikeuksien periaatetta.
## Oma huomio:
- TAB näppäimen käyttö "arvailun" ja virheiden vähentämiseksi on kätevä toiminto ja sen käytössä kannattaa harjaantua.

Ylläolevat havainnot tehty sivustosta (https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited). Sivusto luettu 22.1.2026.

## a) Micro editorin asennus 22.1.2026 19:45
- Editorin asentamiseen käytettiin komentoa _sudo apt-get install micro_. Ohjelma tarvitsee noin 15MB levytilaa ja ennen asentumistaan kysyy lupaa levytilan käyttöön (y/n). Tähän vastataan myöntävästi (y).

## b) Uudet komentoriviohjelmat 22.1.2026 19:50 - 20:30
- Kysyin Geminiltä vinkit kahteen asennettavaan ohjelmaan. Olin itse valinnut tree ohjelmiston asennettavaksi koska se vaikutti luennon perusteella kätevältä ohjelmalta. Ohjelmien asentaminen samanaikaisesti hoitui kätevästi komennolla _sudo apt-get install -y htop tree curl_. Komento koostuu elementeistä (Super User DO), apt (application), get (get/hae), install (install/asenna), (-y, yes/kyllä kaikkeen) sekä kolmesta asennettavasta ohjelmasta. Ennen asennusta kysytään salasanaa jotta asennuksen voi suorittaa ja lainata pääkäyttäjän (SUDO) oikeuksia. Asennetut ohjelmat olivat:
  - Tree ("Visuaalisoi" kansiorakennetta UNIX pohjaiseen näkymään).
  - Curl ((Client URL) jolla voi siirtää tietoa ja dataa palvelimien välillä sekä hakea tietoa).
  - htop (Näyttää suoritettavat ohjelmat, prosessit ja niiden vaatimat resurssit samankaltaisesti kuin windows koneessa tehtävienhallinta).

<img width="819" height="512" alt="Kuvakaappaus 2026-01-22 19-56-28" src="https://github.com/user-attachments/assets/8c4617ce-39c1-4314-9ea1-48c4052fee79" />

Onnistunut asennus ei suoranaisesti kerro, että asennukset ovat onnistuneet. Riveiltä on mahdollista kuitenkin tulkita montako ohjelmaa on asennettu, poistettu tai päivitetty. Minulla oli ennestään asennettuna tree sekä curl ja uutena asennettiin htop.

<img width="826" height="516" alt="Kuvakaappaus 2026-01-22 19-58-12" src="https://github.com/user-attachments/assets/f4c4a1c5-3b94-445c-ab24-f9219da43872" />

Kokeiltaessa komentoa tree, kannattaa ensin pwd (Print Working Direcotry) komennolla tarkastaa missä kansiossa olet. Tämän jälkeen komennolla tree saat visualisoidumman näkymän kansiorakenteesta.

<img width="1068" height="705" alt="Kuvakaappaus 2026-01-22 19-59-10" src="https://github.com/user-attachments/assets/6f407e99-06e5-4094-a539-51dfd0c62a30" />

Kokeiltaessa komentoa curl täytyy hieman jo tietää mitä tietoa haluaa etsiä internetistä tai toiselta palvelimelta. Tämä komento oli itselleni vieras ja tähän etsin vinkkejä internetistä mitä komennolla voisi tehdä. Päädyin kokeilemaan sääennusteen hakemista, joka oli hauska ja mielenkiintoinen kokeilu. Lopputulos ei tosin ole visuaalisesti aivan yhtä miellyttävä kuin se, että tarkastaisi puhelimella Forecan sivut. Tulos on kuitenkin ymmärrettävä ja saatiin testattua, että komennolla saadaan haettua tietoa ulkopuolelta. Komentona käytettiin _curl wttr.in/Helsinki_. (www.geeksforgeeks.org).

<img width="1256" height="764" alt="Kuvakaappaus 2026-01-22 20-00-17" src="https://github.com/user-attachments/assets/dbc8c96e-4739-4b25-ae82-ece19451b980" />

Kokeiltaessa komentoa htop (Hisham's top, nimetty kehittäjänsä mukaan) saatiin esille aktiivisesti, noin sekunnin välein, päivittyvä listaus prosesseista ja niiden resurssien käytöstä.

<img width="1255" height="644" alt="Kuvakaappaus 2026-01-22 20-05-03" src="https://github.com/user-attachments/assets/7df13d54-38f5-467d-9841-b0945dd890cf" />

## c) FHS - Filesystem Hierarchy Standard
/ (Juurihakemisto)

/home (Käyttäjien kotihakemistot ovat täällä)

/home/nhi (Kyseisen käyttäjän kansiot ja tiedostot ovat täällä)

/etc (Kaikki tietokoneen ja käyttöjärjestelmän tiedostot ovat täällä)

/media (Esimerkiksi USB muistitikku näkyy täällä)

/var/log (Järjestelmän lokitiedot)
