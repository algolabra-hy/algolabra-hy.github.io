---
layout: page
permalink: /projektinhallinta
title: Yleisiä Ohjeita
title_long: Ohjeita
inheader: yes
---

Näillä sivuilla löytyy ohjeita eri projektinhallintaa helpottaville työkaluille. 
Nämä ovat tarkoitettu lähinnä opiskelijoille, joille nämä työkalut eivät ole entuudestaan 
tuttuja, harjoitustyössä ei ole pakko käyttää juuri näitä jos joku muu työkalu tuntuu luontevammalta. 

Näillä sivuilla on paljon varsinkin Ohjelmistotuotannon kurssin materiaaleista lainattua ja lyhennettyä.

## Ihan Ensiksi
- Kurssin aikana kaikki harjoitustyöt luodaan git repositorioina GitHub sivuille. Mikäli tämä ei ole tuttua, kannattaa tustua [näihin ohjeisiin](/git). 
  - **Huom** harjoitustyön vertaisarviointi suoritetaan GitHubin issueina. Tätä varten harjoitustyön repossa täytyy [sallia issuet](/git#issuiden-salliminen).
- Harjoitustyön aikana vertaisarvioinnit ja viikottaiset palautteet saadaan [Labtoolin](https://study.cs.helsinki.fi/labtool/) kautta. Harjoitustyön repositorion luomisen jälkeen kaikkien opiskelijoiden täytyy rekisteröityä Labtooliin ad-tunnuksillaan oikealle kurssille. 

## Yleiskatsaus 
- [Yleiskatsaus Harjoitustyön rakenteesta](/yleiskatsaus) käy läpi tärkeimpiä harjoitustyöhön liittyviä ohjeita. 
- [Esimerkkejä Harjoitöistä](/esimerkkeja) sivulla löytyy esimerkkejä jo toteutetuista harjoitustöistä.
    - Näihin saa tutustua, huomaa kuitenkin, että muiden koodia ei saa esittää omanaan. 

## Aiheista
Löytyy ehdotuksia kurssin moodle sivuilta. 

## Projektin Hallinta
Alla muutama hyväksi havaittu työkalu projektinhallintaan. 

### Pythonilla Tehtävät Harjoitustyöt
- [Poetry](/poetry) on Python projektien riippuvuuksien hallintaan kehitetty työkalu.
    - Muutamia Poetryn asentamiseen ja käyttöön liittyviä yleisiä ongelmia käsitellään [täällä](/ongelmia).
- [Pylint](/pylint) on Python koodin stattiseen analysiin tarkoitetty työkalu jonka avulla koodin tason korkeana pitäminen helpottuu. 

### Javalla Tehtävät Harjoitustyöt
- [Gradle](/gradle/) on lähinnä Javalle tarkoitettu työkalu joka automatisoi ohjelman kääntämiseen ja testaamiseen liittyviä tehtäviä. Gradlea voi (periaatteessa) käyttää [Python kehitykseen](https://github.com/PrzemyslawSwiderski/python-gradle-plugin). Suosittelemme kuitenkin Poetrya. 

{% include typo_instructions.md %}

