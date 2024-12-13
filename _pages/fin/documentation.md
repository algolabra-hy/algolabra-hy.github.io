---
layout: page
permalink: /documentation-fi
title: Dokumentaatio
title_long: Työn aikana tehtävät dokumentit
lang: fi # fi or en
ref: documentation # same as the markdown filename
---
Kaikki dokumentit palautetaan joko GitHubin tukemassa markdown-muodossa tai .pdf-muodossa
harjoitustyösi [repositoriossa]({% link _pages/fin/git.md %}). 
Mitään ei siis palauteta esim. sähköpostitse. 
Sijoita dokumentit omaan hakemistoonsa projektin juureen ja linkaa ne repositoriosi etusivulle.

## Viikkopalautukset
Osa kurssipisteistä tulee harjoitustyön viikottaisen edistymisen perusteella. 
Varmista viikottaisen deadlinen lähestyessä, että repositoriosi on ajantasalla ja 
isää sinne viikkoraportti. Edistymistä katsotaan vain kerran viikossa, mutta muutokset kannattaa 
pushata repositorioon vähintään joka kehityspäivän lopuksi.

# Viikkoraportin kirjoitus ja tuntikirjanpito
Raportti on noin puolesta sivusta kahteen sivua pitkä. Raportti palautetaan aina 
viikkopalautuksen yhteydessä sijoitettuna samaan kansioon muun dokumentaation 
kanssa ja nimetään selkeästi, esim. *Viikkoraportti 1*. 

Lisää viikkoraporttiin 
myös kuinka paljon aikaa käytit viikon aikana työhön. 
Käytetty tuntimäärä ei vaikuta arvosteluun.

Raportti tulee laatia käyttäen markdownia tai palauttaa pdf:nä.

Vastaa kirjoituksessa seuraaviin kysymyksiin:
1. Mitä olen tehnyt tällä viikolla?
1. Miten ohjelma on edistynyt?
1. Mitä opin tällä viikolla / tänään?
1. Mikä jäi epäselväksi tai tuottanut vaikeuksia? 
    - Vastaa tähän kohtaan rehellisesti, koska saat tarvittaessa apua tämän kohdan perusteella.
1. Mitä teen seuraavaksi?

Voit sisällyttää viikkoraporttin myös palautetta tai kysymyksiä kurssin ohjaajalle, 
kysymyksiin pyritään vastaamaan viikkopalautteessa.

**HUOM:**
Vaikka et olisi tehnyt mitään jollakin tietyllä viikolla, kannattaa viikkoraportti kuitenkin kirjoittaa niin että repositoriossa on muutoksia viikon ajalta. Voit jopa saada pisteitä. Muuten pisteitä tulee automaattisesti 0 vaikka projektista olisi muuten mahdollista saada viikkopisteitä.

Kolmen peräkkäisen viikon ajan muuttumaton repositorio tulkitaan kurssin keskeyttämiseksi!

## Harjoitustyön dokumentointi

Harjoitustyön dokumentaatio koostuu seuraavista 
osista:
- Koodin dokumentointi
- Määrittelydokumentti, 
- Toteutusdokumentti, 
- Testausdokumentti ja 
- Käyttöohje.

Dokumenttien merkitys kurssilla on melko vähäinen; olennainen asia on toimiva ja tehokas koodi. 
Jokaisen dokumentin pituus on n. 1-2 A4, poislukien mahdolliset kuvat ja taulukot (mikäli nämä sopivat aiheeseen).

### Koodin dokumentointi
Ohjelmakoodin ja rakenteen tulee olla selkeää. Metodien on oltava riittävän lyhyitä. Luokkien, muuttujien ja metodien on oltava kuvaavasti nimettyjä.

Koodin tulee olla kirjoitettu mahdollisimman selkeästi ja ymmärrettävästi. Kommentoi koodiasi kattavasti, mutta napakasti. Jokainen luokka, metodi ja attribuutti ei välttämättä kaipaa kommenttia, mutta kaikki olennainen ja vähemmän kuin itsestään selvä on oltava selostettu kommenteissa. Sisällytä metodien kommentteihin niiden parametrien ja paluuarvon merkitykset. Metodien sisäinen kommentointi ei ideaalitapauksessa ole tarpeen, sillä metodien tulee olla kuvaavasti nimettyjä, kompakteja, yksinkertaisia ja helposti hahmotettavia kokonaisuuksia. Mikäli metodin toimintaa kuitenkin on vaikea hahmottaa pelkän koodin ja metodin yleiskommentin perusteella, voidaan sen koodia kommentoida sisäisestikin.

JavaDoc-kommentointia käytetään kaikissa töissä, jotka toteutetaan Javalla. Jos käyttät NetBeansiä, se voit toteuttaa luokille ja metodeille JavaDoc-kommenttien pohjat. 
Python-ohjelmissa käytetään Ohjelmistotekniikka-kurssilla opetettuun tapaan [docstringeja](https://ohjelmistotekniikka-hy.github.io/python/viikko6#docstring-ja-koodin-dokumentointi). 
Muilla kielillä ohjelmoitaessa noudatetaan kyseisen kielen käytäntöjä.

### Määrittelydokumentti
Määrittelydokumentin pitää sisältää seuraavat tiedot:

- Mitä ohjelmointikieltä käytät?
- Kerro myös mitä muita kieliä hallitset siinä määrin, että pystyt tarvittaessa vertaisarvioimaan niillä tehtyjä projekteja.
- Mitä algoritmeja ja tietorakenteita toteutat työssäsi?
- Minkä ongelman ratkaiset?
- Mitä syötteitä ohjelma saa ja miten niitä käytetään?
- Tavoitteena olevat aika- ja tilavaativuudet (esim. O-analyysit)
    - Tästä kannattaa selvittää niin paljon kuin voitte. **Ei** ole tarkoitus todistaa tai mitata mitään itse. 
    - Käytä aika ja tilavaatimuuksia apuvälineenä ymmärtääksenne, miten työhön kannattaa asennoitua. 
      - Nämä kannattaa katsoa wikipediasta ja varmistaa, että ymmärrätte oman algoritmin kohdalla mistä ne tulevat. Miksi algoritmisi tarvitsee sen verran aikaa? 
- Viitteet

**Harjoitustyön Ydin.** Kuvaile määrittelydokumenttiin muutamalla lauseella, mikä on aiheesi *ydin*. 
**Käytä tähän aikaa** koska se auttaa harjoitustyön 
toteuttamisessa. Vaikka koko työhön tarvitaan muutakin kuin sen ytimeen liittyvää koodia, suurin osa kehitykseen käytettävästä ajasta pitäisi kuluttaa juurikin ytimen kehitykseen. Suunnittele ajankäyttösi niin.  
- Jos aiheesi on jonkin pelin tekoäly, aiheen ydin on *tekoäly*, ei esimerkiksi pelin 
suorittamiseen tarvittavat metodit. 
- Jos aiheesi on reitinhaku, sen ydin on reitinhaku algoritmit, ei esimerkiksi verkkojen visualisointiin 
tarvittavat metodit. 

Kurssin hallintoon liittyvistä syistä, määrittelydokumentissä tulee myös mainita opinto-ohjelma johon kuulut (esim. tietojenkäsittelytieteen kandidaatti (TKT) 
tai bachelor’s in science (bSc)). Määrittelydokumentissa tulee myös mainita projektin dokumentaatiossa käytetty kieli.

Tällä kurssilla määrittelydokumentti on kurssin alkuvaiheen apuväline, jota ei tarvitse päivittää kurssin aikana, ellei ohjaaja pyydä siihen täsmennyksiä. 
**Huomaa**, että ohjaaja on katsonut projektin laajuudeltaan ja vaativuudeltaan sopivaksi määrittelydokumentin perusteella. 
Oleellisesti suppeampi työ ei useimmiten riitä kurssin hyväksyttyyn suoritukseen.

### Toteutusdokumentti
Toteutusdokumentin tulee sisältää seuraavat:

- Ohjelman yleisrakenne
- Saavutetut aika- ja tilavaativuudet (esim. O-analyysit pseudokoodista)
- Suorituskyky- ja O-analyysivertailu (mikäli sopii työn aiheeseen)
- Työn mahdolliset puutteet ja parannusehdotukset
- **Laajojen kielimallien (ChatGPT yms.) käyttö. Mainitse mitä mallia on käytetty ja miten. Mainitse myös mikäli et ole käyttänyt. Tämä on tärkeää!**
- Viitteet

### Testausdokumentti
Testausdokumentin pitääs sisältää seuraavat:

- Yksikkötestauksen kattavuusraportti.
- Mitä on testattu, miten tämä tehtiin?
- Minkälaisilla syötteillä testaus tehtiin?
- Miten testit voidaan toistaa?
- Ohjelman toiminnan mahdollisen empiirisen testauksen tulosten esittäminen graafisessa muodossa. (Mikäli sopii aiheeseen)
- Ei siis riitä todeta, että testaus on tehty käyttäen automaattisia yksikkötestejä, vaan tarvitaan konkreettista tietoa testeistä, kuten:
  - Testattu, että tekoäly osaa tehdä oikeat siirrot tilanteessa, jossa on varma 4 siirron voitto. Todettu, että siirroille palautuu voittoarvo 100000.
  - Testattu 10 kertaan satunnaisesti valituilla lähtö- ja maalipisteillä, että JPS löytää saman pituisen reitin kuin Dijkstran algoritmi.
  - Kummallakin algoritmilla on pakattu 8 MB tekstitiedosto, purettu se ja tarkastettu, että tuloksena on täsmälleen alkuperäinen tiedosto.

[Testauksesta lisää]({% link _pages/fin/testing_frontpage.md %})

### Käyttöohje
Miten ohjelma suoritetaan, miten eri toiminnallisuuksia käytetään
Minkä muotoisia syötteitä ohjelma hyväksyy

{% include typo_instructions_fin.md %}