---
layout: page
permalink: /projektinhallinta
title: Harjoitustyön projektinhallinta
title_long: Ohjeita
inheader: yes
dropdown: true
children:
  - title: Yleiskatsaus projektinhallinnasta (lue tämä ensin)
    permalink: /projektinhallinta
  - title: Kurssin kulku
    permalink: /yleiskatsaus
  - title: Esimerkkiaikataulu 
    permalink: /aikataulu
  - title: Aihe ehdotuksia
    permalink: /aiheet
  - title: Git ohjeet
    permalink: /git
  - title: Työkalut projektinhallintaan
    permalink: /yleista#projektin-hallinta
  - title: Tekoälyalusta pelitekoälyille
    permalink: /aiplatform
---


## Ihan ensiksi
- Kurssin aikana kaikki harjoitustyöt luodaan git repositorioina GitHub sivuille. Mikäli tämä ei ole tuttua, kannattaa tustua [näihin ohjeisiin](/git). 
  - **Huom** harjoitustyön vertaisarviointi suoritetaan GitHubin issueina. Tätä varten harjoitustyön repossa täytyy [sallia issuet](/git#issuiden-salliminen).
- Harjoitustyön aikana vertaisarvioinnit ja viikottaiset palautteet saadaan [Labtoolin](https://study.cs.helsinki.fi/labtool/) kautta. Harjoitustyön repositorion luomisen jälkeen kaikkien opiskelijoiden täytyy rekisteröityä Labtooliin ad-tunnuksillaan oikealle kurssille. 

## Yleiskatsaus 
- [Yleiskatsaus kurssin kulusta](/yleiskatsaus) käy läpi tärkeimpiä harjoitustyöhön liittyviä ohjeita. 
- [Viikottainen aikataulu](/aikataulu) käy läi tarkemmin harjoitustyön suositusaikataulun ja mitä viikkopalautuksiin kuuluu. 
- [Esimerkkejä harjoitustöistä](/esimerkkeja) sivulla löytyy esimerkkejä jo toteutetuista harjoitustöistä.
    - Näihin saa tutustua, huomaa kuitenkin, että muiden koodia ei saa esittää omanaan. 

## Aiheista
- Aiheenvallinasta lisää [aiheet](/aiheet) sivulla.

## Projektin hallinta
Alla muutama hyväksi havaittu työkalu projektinhallintaan. Nämä ovat tarkoitettu lähinnä opiskelijoille, joille nämä työkalut eivät ole entuudestaan tuttuja, harjoitustyössä ei ole pakko käyttää juuri näitä jos joku muu työkalu tuntuu luontevammalta. Näillä sivuilla on paljon varsinkin Ohjelmistotuotannon kurssin materiaaleista lainattua ja lyhennettyä.


### Pythonilla tehtävät harjoitustyöt
- [Poetry](/poetry) on Python projektien riippuvuuksien hallintaan kehitetty työkalu.
    - Muutamia Poetryn asentamiseen ja käyttöön liittyviä yleisiä ongelmia käsitellään [täällä](/ongelmia).
- [Pylint](/pylint) on Python koodin stattiseen analysiin tarkoitetty työkalu jonka avulla koodin tason korkeana pitäminen helpottuu. 

### Javalla tehtävät harjoitustyöt
- [Gradle](/gradle/) on lähinnä Javalle tarkoitettu työkalu joka automatisoi ohjelman kääntämiseen ja testaamiseen liittyviä tehtäviä. Gradlea voi (periaatteessa) käyttää [Python kehitykseen](https://github.com/PrzemyslawSwiderski/python-gradle-plugin). Suosittelemme kuitenkin Poetrya. 

{% include typo_instructions.md %}

