# H2. Komentaja pingviini
- Päivämäärä: 22.1.2026
- Tekijä: Niko
- Ympäristö: (Sama kuin kohdassa H1) Dell Precision M4600, Linux Mint käyttöjärjestelmä jossa asennettuna VirtualBox jossa Linux Debian 13.
## x) Command line basics:
Komentorivin merkitys:
Linuxin ja BSD:n komentorivi on säilynyt käytössä vuosikymmeniä (ennen Googlea ja Internetiä). Se on nopea, selkeä ja helppo automatisoida.
## Navigointi ja tiedostojen hallinta:
- _pwd_ (working directory), _ls_ (listaus) ja _cd_ (hakemiston vaihto) ovat perusliikkumista.
- Tiedostojen katseluun käytetään _less_-komentoa (välilyönti kääntää sivua, q lopettaa).
- Muokkaamiseen suositellaan nano- tai pico-editoreita (tallennus Ctrl-X y Enter).
- Tiedostojen poistamisessa _rm, rm -r_ on oltava tarkkana, sillä Linuxissa ei ole roskakoria.
## Etähallinta ja apu:
- _ssh user@host_ on turvallinen tapa hallita konetta etänä.
- _man-komento_ (esim. man ls) avaa manuaalisivun.
- Tabulaattori on tärkeä työkalu: se täydentää komennot ja tiedostonimet automaattisesti ja auttaa välttämään kirjoitusvirheitä.
## Pääkäyttäjäoikeudet:
- _sudo_-komentoa tulee käyttää vain silloin, kun on pakko (esim. ohjelmien asennus tai järjestelmäasetusten muuttaminen), noudattaen minimioikeuksien periaatetta.
## Oma huomio:
- TAB näppäimen käyttö "arvailun" ja virheiden vähentämiseksi on kätevä toiminto ja sen käytössä kannattaa harjaantua.

Ylläolevat havainnot tehty sivustosta (https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited). Sivusto luettu 22.1.2026.

## a) Micro editorin asennus 22.1.2026 19:45 - 19:50
- Editorin asentamiseen käytettiin komentoa _sudo apt-get install micro_. Ohjelma tarvitsee noin 15MB levytilaa ja ennen asentumistaan kysyy lupaa levytilan käyttöön (y/n). Tähän vastataan myöntävästi (y).

## b) Uudet komentoriviohjelmat 22.1.2026 19:50 - 20:30
- Kysyin Geminiltä vinkit kahteen asennettavaan ohjelmaan. Olin itse valinnut tree ohjelmiston asennettavaksi koska se vaikutti luennon perusteella kätevältä ohjelmalta. Ohjelmien asentaminen samanaikaisesti hoitui kätevästi komennolla _sudo apt-get install -y htop tree curl_. Komento koostuu elementeistä (Super User DO), apt (application), get (get/hae), install (install/asenna), (-y, yes/kyllä kaikkeen) sekä kolmesta asennettavasta ohjelmasta. Ennen asennusta kysytään salasanaa jotta asennuksen voi suorittaa ja lainata pääkäyttäjän (SUDO) oikeuksia. Asennetut ohjelmat olivat:
  - _Tree_ ("Visuaalisoi" kansiorakennetta UNIX pohjaiseen näkymään).
  - _Curl_ ((Client URL) jolla voi siirtää tietoa ja dataa palvelimien välillä sekä hakea tietoa).
  - _htop_ (Näyttää suoritettavat ohjelmat, prosessit ja niiden vaatimat resurssit samankaltaisesti kuin windows koneessa tehtävienhallinta).

<img width="819" height="512" alt="Kuvakaappaus 2026-01-22 19-56-28" src="https://github.com/user-attachments/assets/8c4617ce-39c1-4314-9ea1-48c4052fee79" />

Onnistunut asennus ei suoranaisesti kerro, että asennukset ovat onnistuneet. Riveiltä on mahdollista kuitenkin tulkita montako ohjelmaa on asennettu, poistettu tai päivitetty. Minulla oli ennestään asennettuna _tree_ sekä _curl_ ja uutena asennettiin _htop_.

<img width="826" height="516" alt="Kuvakaappaus 2026-01-22 19-58-12" src="https://github.com/user-attachments/assets/96edd9a5-7211-4f60-80c7-4ee289b66c66" />

Kokeiltaessa komentoa _tree_, kannattaa ensin _pwd_ (Print Working Direcotry) komennolla tarkastaa missä kansiossa olet. Tämän jälkeen komennolla _tree_ saat visualisoidumman näkymän kansiorakenteesta.

<img width="1256" height="764" alt="Kuvakaappaus 2026-01-22 20-00-17" src="https://github.com/user-attachments/assets/5b93c848-8193-4ae0-b975-677d38c20aeb" />

Kokeiltaessa komentoa _curl_ täytyy hieman jo tietää mitä tietoa haluaa etsiä internetistä tai toiselta palvelimelta. Tämä komento oli itselleni vieras ja tähän etsin vinkkejä internetistä mitä komennolla voisi tehdä. Päädyin kokeilemaan sääennusteen hakemista, joka oli hauska ja mielenkiintoinen kokeilu. Lopputulos ei tosin ole visuaalisesti aivan yhtä miellyttävä kuin, että katsoisi puhelimella Forecan sivut. Tulos on kuitenkin ymmärrettävä ja saatiin testattua, että komennolla saa haettua tietoa ulkopuolelta. Komentona käytettiin _curl wttr.in/Helsinki_. (www.geeksforgeeks.org).

<img width="1255" height="644" alt="Kuvakaappaus 2026-01-22 20-05-03" src="https://github.com/user-attachments/assets/12f80c9a-4384-491b-b0af-6a758cbd6a38" />

Kokeiltaessa komentoa _htop_ (Hisham's top, nimetty kehittäjänsä mukaan) saatiin esille aktiivisesti, noin sekunnin välein, päivittyvä listaus prosesseista ja niiden resurssien käytöstä.

<img width="1068" height="705" alt="Kuvakaappaus 2026-01-22 19-59-10" src="https://github.com/user-attachments/assets/7665c3a1-d3cc-455f-9064-5cfb5c5b335a" />

## c) FHS - Filesystem Hierarchy Standard 24.1.2026 06:00 - 07:10.
/ (Juurihakemisto)
Tässä kansiossa on juuri kaikelle ja kaikki kansiot sekä tiedostot näkyvät sen alla.

<img width="825" height="518" alt="Kuvakaappaus 2026-01-24 06-06-01" src="https://github.com/user-attachments/assets/fd769699-78f2-4c45-8e43-fc8973230192" />

/home (Käyttäjien kotihakemistot ovat täällä)
Tämä kansio on kotikansio kaikille käyttäjille. Tällä koneella ei ole muita käyttäjiä kuin minä. _ls -F_ komennolla (ls, List ja -F, näyttää kansiot kenoviivalla) saan näkymän käyttäjien kansioihin home kansiossa.

<img width="828" height="519" alt="Kuvakaappaus 2026-01-24 06-06-55" src="https://github.com/user-attachments/assets/0543f857-4b78-4cd2-bbe6-0f161be51a4b" />

/home/nhi (Kyseisen käyttäjän kansiot ja tiedostot ovat täällä)
Olen kirjautuneena käyttäjänä nhi ja allaolevassa kuvassa on näkymä kaikkiin tiedostoihin omassa kansiossani. Komennolla _ls -a_ (-a, näyttää kaikki, myös piilotiedostot) saan näkyviin kaikki kansiot ja tiedostot kansiossa. Pisteellä alkavat ovat piilotettuja eivätkä ne näy normaalisti.

<img width="828" height="518" alt="Kuvakaappaus 2026-01-24 06-10-21" src="https://github.com/user-attachments/assets/98266383-6e12-48e7-b9e1-f04191addb4f" />

/etc (Kaikki tietokoneen ja käyttöjärjestelmän tiedostot ovat täällä)
Tässä kansiossa sijaitsee kaikki tietokoneen ja käyttöjärjestelmän toimimiseen liittyvä tieto. Tässä kansiossa ei kotikäyttäjän tarvitse juurikaan toimia. Komennoll _ls -F_ (-F, näyttää kansiot kenoviivalla) saan näkyviin kaikki kansiot etc kansion sisällä. Kansioita on niin paljon, etteivät ne mahdu yhteen näkymään kannettavan näytöllä.

<img width="1275" height="769" alt="Kuvakaappaus 2026-01-24 06-11-55" src="https://github.com/user-attachments/assets/4ffcbeb0-3060-4d8b-b399-4f2b573bca02" />

/etc kansiosta löytää tarvittaessa runsaasti tietoa monenlaisista asioista tietokoneen ja käyttöjärjestelmän osalta. Allaolevassa kuvassa haettu tieto käytössä olevasta käyttöjärjestelmästä _cat /etc/os-release_ komennolla (cat, Concatenate, tällä haetaan tiettyjä haluttuja tietoja, /etc, haluttu kansio, os-release, pyydetään tietoja käyttöjärjestelmästä).

<img width="1275" height="773" alt="Kuvakaappaus 2026-01-24 06-14-14" src="https://github.com/user-attachments/assets/d92a39d3-e3bf-440c-af41-902399aebc42" />

/media (Esimerkiksi USB muistitikku näkyy täällä)
Tässä kansiossa näkyvät irrotettavat medialaitteet kuten USB tikku tai ulkoinen kiintolevy. Minulla ei sellaisia tällä hetkellä ole kiinni.

/var/log (Järjestelmän lokitiedot)
Tässä kansiossa on lokitiedostot tietokoneen ja käyttöjärestelmän toiminnoista. Kotikäyttäjän ei oikeastaan tarvitse tässä kansiossa vierailla mutta ylläpitäjälle kansio on erittäin tärkeä. Etsin tietoa kyseisestä kansiosta ja mieleeni oli iskostunut tieto, että lokitiedostot tallentuvat kansioon _varlog_ tai _syslog_. Hämmennykseni oli suuri kun en löytänytkään kyseistä kansiota. Tässä kohtaa jouduin turvautumaan googleen selvittääkseni, mistä löydän lokitietoja. Apua sain debian julkaisun sivuilta seuraavasta osoitteesta: https://www.debian.org/releases/bookworm/arm64/release-notes/ch-information.en.html

Löysin tiedon, että ensisijaisesti lokitietoja löytyy _journal_ kansiosta sekä _dpkg.log_ tiedostosta. Käytin komentoa tail -n 1 /var/log/dpkg.log (tail, näyttää "hännän" tiedoston loppupäästä. -n 1, number ja vain yksi rivi näytetään, loppuosa on tiedostopolkua josta tietoa haetaan). Tästä selviää viimeisin lokitieto joka on, että järjestelmä on asentanut jonkin ajurin tai tiedoston.

<img width="1283" height="289" alt="Kuvakaappaus 2026-01-24 06-23-26" src="https://github.com/user-attachments/assets/73ab75a9-4fdc-470d-9333-69298f4c64ec" />

## d) The friendly M
Luennon jäljiltä jäin vielä miettimään erilaisia tapoja hakea ohjeita komentojen tekemiseen komentokehotteessa. Päätin kysyä Geminiltä vinkkejä asiaan ja sain seuraavia ideoita:
 
 - _man_ (Manual) Perinteinen tapa ohjeiden etsimiseen tietyille komennoille. Esimerkiksi _man grep_ tarjoaa tietoa/ohjeita juuri _grep_ komennon käyttämiseen

<img width="1277" height="769" alt="Kuvakaappaus 2026-01-24 07-24-09" src="https://github.com/user-attachments/assets/10fb635b-030f-41e5-a45a-4582e0dbf733" />

 - _apropos_ (aihepiirin mukainen haku) Jos et muista komennon nimeä mutta tiedät mitä haluat tehdä, voi _apropos_ komenolla etsiä komentoja jotka liittyvät asiaan jota haluat tehdä. Esimerkiksi _apropos "list directory_ tarjoaa vinkkejä millä komennoilla saat aiheeseen liittyviä asioita tehtyä. Tykästyin tähän toimintoon sen vuoksi, että välillä on todella hankalaa muistaa komentojen tarkka kirjoitusmuoto.

<img width="1277" height="776" alt="Kuvakaappaus 2026-01-24 07-26-46" src="https://github.com/user-attachments/assets/7aa33700-6e94-4fc4-98e1-01c92dcacbe0" />

 - _--help_ tarjoaa pikaohjeen asiaan eikä näytä koko ohjekirjaa. Esimerkiksi _ls --help_ tietoa ls komennosta.

<img width="1276" height="774" alt="Kuvakaappaus 2026-01-24 07-30-05" src="https://github.com/user-attachments/assets/8430ffc3-7701-4136-ae67-58ee2e534c26" />

 - _whatis_ on kätevä toiminto joka kertoo lyhyesti, yhdellä rivillä, mitä kyseinen komento tekee. Esimerkiksi _whatis grep_ tarjoaa lyhyen ja ytimekkään tiedon muistin tueksi, mitä komennolla tehdään.

<img width="1277" height="154" alt="Kuvakaappaus 2026-01-24 07-30-31" src="https://github.com/user-attachments/assets/ad76ac26-df62-414e-88e6-bc3ee9e59aac" />

Kätevä toiminto/komento jonka löysin on _-i_ (ignore case) joka ohittaa "case sensitive" toiminnon. Komentorivihän on muutoin totaalisen tarkka isoista ja pienistä kirjaimista. Tällä komennolla etsin tekstiä "debian" aiemmin esitellystä /etc kansiosta. _ grep -i "debian" /etc/os-release_

<img width="818" height="518" alt="Kuvakaappaus 2026-01-24 07-44-27" src="https://github.com/user-attachments/assets/f2dd8fc7-7d2d-4092-8aab-8cb493f3dc52" />

Etsin omaan kyttäjätunnukseeni liittyviä tietoja komennolla _grep "nhi" /etc/passwd_. Esille tullut tieto vahvisti minun olevan ensimmäinen ihmiskäyttäjä koneella (1000). Sitä aiemmat käyttäjät (<1000) on varattu käyttöjärjestelmälle.

<img width="821" height="515" alt="Kuvakaappaus 2026-01-24 07-50-24" src="https://github.com/user-attachments/assets/4eed5ca0-b241-49ef-9332-6017e8b386a1" />

## e) Pipe eli "putket"
Putket yhdistävät kaksi tai useamman komennon toisiinsa siten, että ne tekevät yhteistyötä. Putken " | " vasemmalla puolella oleva on ns. lähde ja oikealla puolella on komento. Jos haluaisin esimerkiksi etsiä tiedostoa ja käyttäisin pelkästään komentoa _ls "/kansionimi"_ saisin pahimmillaan satoja merkkejä ruudulle.
Käyttämällä "Putkia" voidaan rajata ruudulle ilmestyvää tietoa. Ei kirjoiteta aiemmin mainittua komentoa vaan sen sijaan _ls /kansionimi | grep "tiedostonimi"_ saadaan haettua vain kyseistä etsittyä tietoa. Tässä voi olla tarpeen huomioida vielä _-i_ komento jotta ruudulle ilmestyy tiedot isoilla ja pienillä kirjaimilla.
Tässä esimerkissä olen etsinyt koneeltani _grep_ komennolla kaikki .md päätteiset tiedostot (ne on tehty aiemmalla oppitunnilla). Käytin komentoa _ls -R | grep ".md"._ (ls meille olikin jo tuttu (listaus), -R 
Recursive käy läpi hakemiston siitä alkaen missä kansiossa olet. Voit siis aloittaa juuresta esimerkiksi. | merkki tarkoittaa putki/pipe komentoa. grep (global regular expression print) halutun tiedon etsimiseen, "" lainausmerkeillä erotellaan etsittävä tieto.
<img width="1033" height="558" alt="Kuvakaappaus 2026-01-25 06-15-29" src="https://github.com/user-attachments/assets/b4eb847c-80de-4a96-bf79-2f9e6d62a29f" />

## f) Rauta
Läksyjen mukaisesti siirryttiin tarkastelemaan tietokoneen rauta, eli hardware, puolta. Yritin ajaa komennon _sudo lshw -short -sanitize _ saadakseni tiedot näkyviin. Komentorivi ei kuitenkaan komentoa tunnistanut, joten asensin ensin lshw toiminnon komennolla _sudo apt install lshw_. Asennuksen jälkeen ajoin komennon uudelleen. Komento sisältää elementit _sudo_ (pääkäyttäjä), _lshw list hardware_, _-short_ lyhentää ja tiivistää listan siistimpään muotoon ja karsii tiedot keskeisiksi, _-sanitize_ poistaa esimerkiksi sarjanumerot ja huolehtii tiedon olevan yleispätevämpää eikä se sisällä arkaluonteisia tietoja.

<img width="1196" height="762" alt="Kuvakaappaus 2026-01-25 06-17-33" src="https://github.com/user-attachments/assets/6bbd1c44-22dd-4f76-aea5-4c44b847a794" />

### Mitä kone on "syönyt"?
Järjestelmä:
- Ensimmäisellä rivillä näkyy teksti virtualbox. Tällä saamme tiedon, että käyttöjärjestelmä toimii virtuaalikoneessa eikä suoraan isäntäkoneessa.

Muisti:
- Virtuaalikoneelle on annettu RAM muistia (Random Access Memory) 8GiB käyttöön. GiB on hieman eri termi kuin GB mutta peruskäyttäjälle riittää tieto, että se on suurinpiirtein 8GB.

Prosessori:
- Isäntäkoneen prosessorin tiedot Intel Core i7-2720QM 2.20GHz

Kiintolevy:
- Levytilaa on virtuaalisesti yhteensä noin 53 GB josta käytettävissä on vielä noin 41GB.

Verkko:
- Verkkokortti 82540M Gigabit ethernet controller.

Muut tiedot:
- Lisäksi näkyy esimerkiksi erilaisia väylä, portti ja painiketietoja. Nämä voivat joissakin tilanteissa olla tarpeellisia mutta tällä kertaa emme paneudu niihin tarkemmin.

# Lähteet:
- https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited
- Google Gemini (Asennettavien ohjelmien vinkki, komentojen selittäminen auki).
- https://www.geeksforgeeks.org/linux-unix/curl-command-in-linux-with-examples/ (Curl komento)
