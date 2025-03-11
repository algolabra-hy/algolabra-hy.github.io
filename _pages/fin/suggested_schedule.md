---
layout: page
permalink: /schedule-fi
title: Harjoitustyön (suositus) Aikataulu  
title_long: Tarkempi ehdotus harjoitustyön aikataulusta
lang: fi # fi or en
ref: suggested_schedule # same as the markdown filename
---

Kurssilla on palautus jokaisen viikon (1-6) lauantaina, näiden deadlinet löytyvät kurssikalenterista moodlesta. 

## Viikko 1
- Aihe, käytettävä ohjelmointikieli ja työn laajuus päätetty.
    - Tutustu [aihe-ehdotuksiin]({% link _pages/fin/topics.md %}).
    - Juttele tarvittaessa ohjaajan kanssa, varsinkin jos sunnittelemasi aihe ei ole ehdotusten listalla. 
    - Ohjaaja tarkistaa määritelydokumentin ja antaa palautetta tarvittaessa. 
- [Harjoitustyön repositorio]({% link _pages/fin/git.md %}) alustettu ja rekisteröity [Labtooliin](https://study.cs.helsinki.fi/labtool/).
    - Muista myös sallia [issuet]({% link _pages/fin/git.md %}#issuiden-salliminen).
- [Projektinhallinta]({% link _pages/fin/project_maintenance_frontpage.md %}#projektin-hallinta) kunnossa.
    - Tämä tarkoittaa, että repositorion pitäisi olla tehtynä ja labtooliin rekisteröitynä. Tämän lisäksi jonkinlainen tapa kääntää koodia
      ja hallita riippuvuuksia pitäisi olla. Pythonin kanssa on syytä käyttää Poetrya, joka on muillakin opiskelijoilla yleensä käytössä ja heille tuttu väline.

**Viikko 1. Palautus** (katso päivä kurssikalenterista ja [ohjeet]({% link _pages/fin/documentation.md %}) palautuksista)
- [Viikkoraportti 1]({% link _pages/fin/documentation.md %}#viikkopalautukset)
- [Määrittelydokumetti]({% link _pages/fin/documentation.md %}#määrittelydokumentti)
    - **Tärkeää** Muista kirjoittaa määrittelydokumenttiin opinto-ohjelmasi ja projektin kieli!
    - Muista kirjoittaa määrittelydokumenttiin myös mikä on harjoitustyösi **ydin**, lisää ohjeita [määrittelydokumetin ohjeissa]({% link _pages/fin/documentation.md %}#määrittelydokumentti).


## Viikko 2
- Projektin ydinalueen kehitykseen pitäisi päästä **jo tällä viikolla**. 
    - Tämä tarkoittaa esimerkiksi, että jos teet pelin tekoälyä, itse tekoälyn kehitykseen pitäisi (mielellään) päästä jo tällä viikolla. 
    - Jos harjoitustyöösi kuuluu tietorakenteiden toteutusta, voit tässä vaiheessa käyttää kielesi valmiita rakenteita ja korvata ne myöhemmin.
- Projektin koodi on alusta asti [dokumentoitua]({% link _pages/fin/documentation.md %}#koodin-dokumentointi) 
- Projektin testien (ja [yksikkötestien]({% link _pages/fin/unit_testing.md %})) kehitys [edustavilla]({% link _pages/fin/testing_representative_inputs.md %}) syötteillä aloitettu.
    - Kehitä testejä samaan aikaan koodin kanssa. 
    - Testien on tarkoitus mitata koodin *oikeellisuutta*. Älä kuluta aikaa tarpeettomien testien kehitykseen, vaan mieti ensin minkälaisia testejä juuri oma työsi tarvitsee. 
        - [Testaus]({% link _pages/fin/testing_frontpage.md %}) sivuilla on materiaalia, mutta kaikki harjoitustyöt eivät tarvitse kaikkea sieltä löytyvää. 
    - Projektin [testikattavuus]({% link _pages/fin/unit_testing.md %}#onko-jo-testattu-tarpeeksi-testauskattavuus) seurattavissa. 

**Viikko 2. Palautus**
- [Viikkoraportti 2]({% link _pages/fin/documentation.md %}#viikkopalautukset)

## Viikko 3
- Projektin ydinalue kehittynyt
    - Projektilla on toimiva (ei tarvitse olla hiottu) käyttöliittymä. 
    - **Ydintoimintaa tukevat metodit kaikki valmiita**. 
    - Ideaalitapauksessa viikon aikana työtä pitäisi jo voida ajaa ja sen toiminnallisuutta havainnoida. 
- Koodin laatua ylläpidetään esim [pylintin]({% link _pages/fin/pylint.md %}) avulla.
- Projektin jo toteutetut päämetodit ovat kattavasti yksikkötestattuja [edustavilla]({% link _pages/fin/testing_representative_inputs.md %}) syötteillä. 
- [Testausdokumentin]({% link _pages/fin/documentation.md %}#testausdokumentti) kirjoitus aloitettu. 
    - Dokumentissa [testikattavuuden raportti]({% link _pages/fin/unit_testing.md %}#onko-jo-testattu-tarpeeksi-testauskattavuus)


**Viikko 3. Palautus**
- [Viikkoraportti 3]({% link _pages/fin/documentation.md %}#viikkopalautukset)


## Viikko 4
Tällä viikolla kannattaa keskittyä harjoitustyön valmisteluun vertaisarviointia varten. 
Varmista, että koodisi on sellaisessa kunnossa, että siitä voi antaa merkityksellistä palautetta.

- Ohjelman ydintoiminta melkein valmis. Mahdolliset omat tietorakenteet aloitettu. 
- Koodi hyvin [dokumentoitua]({% link _pages/fin/documentation.md %}#koodin-dokumentointi) ja kattavasti testattua. 
- [Toteutusdokumentin]({% link _pages/fin/documentation.md %}#toteutusdokumentti) teko aloitettu. 
- Mahdollisten [yksikkötestejä täydentävien]({% link _pages/fin/testing_frontpage.md %}#yksikkötestien-lisäksi) testien kehitys aloitettu.
    - Muista, että kaikkia mahdollisia eri testityyppejä ei tarvita. Mieti mitkä ovat oleellisia oman aiheesi oikeellisuuden testaamiseen. 
    - Kirjoita näistä [testausdokumenttiin]({% link _pages/fin/documentation.md %}#testausdokumentti).


**Viikko 4. Palautus** 
- [Viikkoraportti 4]({% link _pages/fin/documentation.md %}#viikkopalautukset)
- Ensimmäinen vertaisarviointi jaetaan viikon palautuksen jälkeen. 
    - Katso labtoolista linkki katselmoitavaan repoon. 
    - Muista sallia [issuet]({% link _pages/fin/git.md %}#issuiden-salliminen)
    - Vertaisarvioinnin deadline on sama kuin 5. viikkopalautuksella.
    - Ohjeet vertaisarviointiin [moodlessa]({{site.moodle}}). 

## Viikko 5
- Ensimmäinen vertaisarviointi tehty. 
- Oman harjoitustyön saaman palautteen hyödyntäminen
- [Toteutus-]({% link _pages/fin/documentation.md %}#toteutusdokumentti) ja [testausdokumentti]({% link _pages/fin/documentation.md %}#testausdokumentti) ajan tasalla. 
- Ohjelman ydintoiminta valmis. Mahdolliset omat tietorakenteet melkein valmiina. 
- Ohjelman testit kattavia. 

**Viikko 5. Palautus** 
- [Viikkoraportti 5]({% link _pages/fin/documentation.md %}#viikkopalautukset)



## Viikko 6:
- Toinen vertaisarviointi.
- Ohjelman viimeistelyä.
- Testien viimeistelyä. 
- [Dokumentaation]({% link _pages/fin/documentation.md %}) viimestelyä. 
    - Muista [käyttöohje]({% link _pages/fin/documentation.md %}#käyttöohje)

**Viikko 6. Palautus**
- [Viikkoraportti 6]({% link _pages/fin/documentation.md %}#viikkopalautukset)
- Toinen vertaisarviointi jaetaan viikon palautuksen jälkeen, tälle deadline muutama päivä arvioinnin jälkeen. 
    - Katso labtoolista linkki katselmoitavaan repoon. 
    - Muista sallia [issuet]({% link _pages/fin/git.md %}#issuiden-salliminen)
    - Vertaisarvioinnin deadline on viikon 7 torstaina.
    - Ohjeet vertaisarviointiin [moodlessa]({{site.moodle}}). 

## Lopullinen Palautus
(Tarkka päivä löytyy moodlen kalenterista)

**Dokumentaatio:**
- 100% selkeä ja kommentoitu koodi
- Valmiit dokumentit:
    - [Määrittelydokumetti]({% link _pages/fin/documentation.md %}#määrittelydokumentti) (ei tarvitse päivittää alkuperäisestä)
    - [Toteutusdokumentti]({% link _pages/fin/documentation.md %}#toteutusdokumentti)
    - [Testausdokumentti]({% link _pages/fin/documentation.md %}#testausdokumentti)
    - [Viikkoraportit]({% link _pages/fin/documentation.md %}#viikkopalautukset)
    - [Käyttöohje]({% link _pages/fin/documentation.md %}#käyttöohje)

**Ohjelma:**
-   Mielellään suoritettava ohjelma. 
-   Toiminnallisuudessa määrittelydokumenttiin kirjoitettu laajuus saavutettu.  
-   Työ valmis ja hiottu.

**Testaus:**
-   Koodin [kattava]({% link _pages/fin/testing_requirements.md %}) yksikkötestaus
-   Ohjelman testaus dokumentoitu testausdokumenttiin

{% include typo_instructions_fin.md %}
