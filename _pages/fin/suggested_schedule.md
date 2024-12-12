---
layout: page
permalink: /aikataulu
title: Harjoitustyön (suositus) Aikataulu  
title_long: Tarkempi ehdotus harjoitustyön aikataulusta
inheader: no
---

Kurssilla on palautus jokaisen viikon lauantaina, näiden deadlinet löytyvät kurssikalenterista moodlesta. 

## Viikko 1
- Aihe, käytettävä ohjelmointikieli ja työn laajuus päätetty.
    - Tutustu [aihe-ehdotuksiin](/aiheet).
    - Juttele tarvittaessa ohjaajan kanssa, varsinkin jos sunnittelemasi aihe ei ole ehdotusten listalla. 
    - Ohjaaja tarkistaa määritelydokumentin ja antaa palautetta tarvittaessa. 
- [Harjoitustyön repositorio](/git) alustettu ja rekisteröity [Labtooliin](https://study.cs.helsinki.fi/labtool/).
    - Muista myös sallia [issuet](/git#issuiden-salliminen).
- [Projektinhallinta](/projektinhallinta#projektin-hallinta) kunnossa.
    - Tämä tarkoittaa, että repositorion pitäisi olla tehtynä ja labtooliin rekisteröitynä. Tämän lisäksi jonkinlainen tapa kääntää koodia
      ja hallita riippuvuuksia pitäisi olla. Pythonilla tämä voi tarkoittaa poetrya, mutta jos jokin muu työkalu on
      tutumpi niin sitäkin saa käyttää. 

**Viikko 1. Palautus** (katso päivä kurssikalenterista ja [ohjeet](/dokumentaatio) palautuksista)
- [Viikkoraportti 1](/dokumentaatio#viikkopalautukset)
- [Määrittelydokumetti](dokumentaatio#määrittelydokumentti)
    - **Tärkeää** Muista kirjoittaa määrittelydokumenttiin opinto-ohjelmasi ja projektin kieli!
    - Muista kirjoittaa määrittelydokumenttiin myös mikä on harjoitustyösi **ydin**, lisää ohjeita [määrittelydokumetin ohjeissa](dokumentaatio#määrittelydokumentti).


## Viikko 2
- Projektin ydinalueen kehitykseen pitäisi päästä **jo tällä viikolla**. 
    - Tämä tarkoittaa esimerkiksi, että jos teet pelin tekoälyä, itse tekoälyn kehitykseen pitäisi (mielellään) päästä jo tällä viikolla. 
    - Jos harjoitustyöösi kuuluu tietorakenteiden toteutusta, voit tässä vaiheessa käyttää kielesi valmiita rakenteita ja korvata ne myöhemmin.
- Projektin koodi on alusta asti [dokumentoitua](/dokumentaatio#koodin-dokumentointi) 
- Projektin testien (ja [yksikkötestien](/unittest)) kehitys [edustavilla](/respresentativeinputs) syötteillä aloitettu.
    - Kehitä testejä samaan aikaan koodin kanssa. 
    - Testien on tarkoitus mitata koodin *oikeellisuutta*. Älä kuluta aikaa tarpeettomien testien kehitykseen, vaan mieti ensin minkälaisia testejä juuri oma työsi tarvitsee. 
        - [Testaus](/testing) sivuilla on materiaalia, mutta kaikki harjoitustyöt eivät tarvitse kaikkea sieltä löytyvää. 
    - Projektin [testikattavuus](/unittest#onko-jo-testattu-tarpeeksi-testauskattavuus) seurattavissa. 

**Viikko 2. Palautus**
- [Viikkoraportti 2](/dokumentaatio#viikkopalautukset)

## Viikko 3
- Projektin ydinalue kehittynyt
    - Projektilla on toimiva (ei tarvitse olla hiottu) käyttöliittymä. 
    - **Ydintoimintaa tukevat metodit kaikki valmiita**. 
    - Ideaalitapauksessa viikon aikana työtä pitäisi jo voida ajaa ja sen toiminnallisuutta havainnoida. 
- Koodin laatua ylläpidetään esim [pylintin](/pylint) avulla.
- Projektin jo toteutetut päämetodit ovat kattavasti yksikkötestattuja [edustavilla](/respresentativeinputs) syötteillä. 
- [Testausdokumentin](/dokumentaatio#testausdokumentti) kirjoitus aloitettu. 
    - Dokumentissa [testikattavuuden raportti](/unittest#onko-jo-testattu-tarpeeksi-testauskattavuus)


**Viikko 3. Palautus**
- [Viikkoraportti 3](/dokumentaatio#viikkopalautukset)


## Viikko 4
Tällä viikolla kannattaa keskittyä harjoitustyön valmisteluun vertaisarviointia varten. 
Varmista, että koodisi on sellaisessa kunnossa, että siitä voi antaa merkityksellistä palautetta.

- Ohjelman ydintoiminta melkein valmis. Mahdolliset omat tietorakenteet aloitettu. 
- Koodi hyvin [dokumentoitua](/dokumentaatio#koodin-dokumentointi) ja kattavasti testattua. 
- [Toteutusdokumentin](/dokumentaatio#toteutusdokumentti) teko aloitettu. 
- Mahdollisten [yksikkötestejä täydentävien](/testing#yksikkötestien-lisäksi) testien kehitys aloitettu.
    - Muista, että kaikkia mahdollisia eri testityyppejä ei tarvita. Mieti mitkä ovat oleellisia oman aiheesi oikeellisuuden testaamiseen. 
    - Kirjoita näistä [testausdokumenttiin](/dokumentaatio#testausdokumentti).


**Viikko 4. Palautus** 
- [Viikkoraportti 4](/dokumentaatio#viikkopalautukset)
- Ensimmäinen vertaisarviointi jaetaan viikon palautuksen jälkeen. 
    - Katso labtoolista linkki katselmoitavaan repoon. 
    - Muista sallia [issuet](/git#issuiden-salliminen)
    - Vertaisarvioinnin deadline on **kolme päivää** arvioiden jaon jälkeen.
    - Ohjeet vertaisarviointiin [moodlessa]({{site.moodle}}). 

## Viikko 5
- Ensimmäinen vertaisarviointi tehty. 
- Oman harjoitustyön saaman palautteen hyödyntäminen
- [Toteutus-](/dokumentaatio#toteutusdokumentti) ja [testausdokumentti](/dokumentaatio#testausdokumentti) ajan tasalla. 
- Ohjelman ydintoiminta valmis. Mahdolliset omat tietorakenteet melkein valmiina. 
- Ohjelman testit kattavia. 

**Viikko 5. Palautus** 
- [Viikkoraportti 5](/dokumentaatio#viikkopalautukset)



## Viikko 6:
- Toinen vertaisarviointi.
- Ohjelman viimeistelyä.
- Testien viimeistelyä. 
- [Dokumentaation](/dokumentaatio) viimestelyä. 
    - Muista [käyttöohje](/dokumentaatio#käyttöohje)

**Viikko 6. Palautus**
- [Viikkoraportti 6](/dokumentaatio#viikkopalautukset)
- Toinen vertaisarviointi jaetaan viikon palautuksen jälkeen, tälle deadline muutama päivä arvioinnin jälkeen. 
    - Katso labtoolista linkki katselmoitavaan repoon. 
    - Muista sallia [issuet](/git#issuiden-salliminen)
    - Vertaisarvioinnin deadline on **kolme päivää** arvioiden jaon jälkeen.
    - Ohjeet vertaisarviointiin [moodlessa]({{site.moodle}}). 

## Lopullinen Palautus
(Tarkka päivä löytyy moodlen kalenterista)

**Dokumentaatio:**
- 100% selkeä ja kommentoitu koodi
- Valmiit dokumentit:
    - [Määrittelydokumetti](dokumentaatio#määrittelydokumentti) (ei tarvitse päivittää alkuperäisestä)
    - [Toteutusdokumentti](/dokumentaatio#toteutusdokumentti)
    - [Testausdokumentti](/dokumentaatio#testausdokumentti)
    - [Viikkoraportit](/dokumentaatio#viikkopalautukset)
    - [Käyttöohje](/dokumentaatio#käyttöohje)

**Ohjelma:**
-   Mielellään suoritettava ohjelma. 
-   Toiminallisuudessa määrittelydokumenttiin kirjoitettu laajuus saavutettu.  
-   Työ valmis ja hiottu.

**Testaus:**
-   Koodin [kattava](/testreqs) yksikkötestaus
-   Ohjelman testaus dokumnetoitu testausdokumenttiin

{% include typo_instructions.md %}
