---
layout: page
permalink: /project-management-fi
title: Harjoitustyön Toteutus
title_long: Ohjeita
lang: fi # fi or en
ref: project_maintenance_frontpage # same as the markdown filename
---


## Ihan ensiksi
- Kurssin aikana kaikki harjoitustyöt luodaan git repositorioina GitHub sivuille. Mikäli tämä ei ole tuttua, kannattaa tustua [näihin ohjeisiin]({% link _pages/fin/git.md %}). 
  - **Huom** harjoitustyön vertaisarviointi suoritetaan GitHubin issueina. Tätä varten harjoitustyön repossa täytyy [sallia issuet]({% link _pages/fin/git.md %}#issuiden-salliminen).
- Harjoitustyön aikana vertaisarvioinnit ja viikottaiset palautteet saadaan [Labtoolin](https://study.cs.helsinki.fi/labtool/) kautta. Harjoitustyön repositorion luomisen jälkeen kaikkien opiskelijoiden täytyy rekisteröityä Labtooliin ad-tunnuksillaan oikealle kurssille. 

## Yleiskatsaus 
- [Yleiskatsaus kurssin kulusta]({% link _pages/fin/overview_full_course.md %}) käy läpi tärkeimpiä harjoitustyöhön liittyviä ohjeita. 
- [Viikottainen aikataulu]({% link _pages/fin/suggested_schedule.md %}) käy läi tarkemmin harjoitustyön suositusaikataulun ja mitä viikkopalautuksiin kuuluu. 


## Aiheista
- Aiheenvallinasta lisää [aiheet]({% link _pages/fin/topics.md %}) sivulla.

## Projektin hallinta
Alla muutama hyväksi havaittu työkalu projektinhallintaan. Nämä ovat tarkoitettu lähinnä opiskelijoille, joille nämä työkalut eivät ole entuudestaan tuttuja, harjoitustyössä ei ole pakko käyttää juuri näitä jos joku muu työkalu tuntuu luontevammalta. Näillä sivuilla on paljon varsinkin Ohjelmistotuotannon kurssin materiaaleista lainattua ja lyhennettyä.


### Pythonilla tehtävät harjoitustyöt
- [Poetry]({% link _pages/fin/poetry.md %}) on Python projektien riippuvuuksien hallintaan kehitetty työkalu.
- [Pylint]({% link _pages/fin/pylint.md %}) on Python koodin stattiseen analysiin tarkoitetty työkalu jonka avulla koodin tason korkeana pitäminen helpottuu. 

### Javalla tehtävät harjoitustyöt
- [Gradle]({% link _pages/fin/gradle.md %}) on lähinnä Javalle tarkoitettu työkalu joka automatisoi ohjelman kääntämiseen ja testaamiseen liittyviä tehtäviä. Gradlea voi (periaatteessa) käyttää [Python kehitykseen](https://github.com/PrzemyslawSwiderski/python-gradle-plugin). Suosittelemme kuitenkin Poetrya. 

{% include typo_instructions_fin.md %}

