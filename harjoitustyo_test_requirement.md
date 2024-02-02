---
layout: page
permalink: /testreqs
title: Harjoitustyön vaatimukset testeille
title_long: Mitä vaaditaan harjotustyön testeiltä
inheader: no
---


<div style="color:black; border-style: solid; border-width: thick; border-color: red; padding: 10px; margin-bottom: 15px; padding: 10px; background-color: #F1EFEF;">

<h4>Huom!</h4>

<p>
Alla asiaa herjoitustyön testien vaatimuksista. Painotamme kuitenkin, että testien 
päätarkoitus on auttaa työn kehityksessä. Suosittelemme vahvasti, että kirjoitatte testejä kehitystyön aikana eikä vasta jälkikäteen.
Aina kun löydätte jonkun bugin, sille kannattaa kirjoittaa testi. 
</p>

</div>

## Testien vaatimuksista - mitä pitää testata?
Jokaisessa harjoitustyössä vaaditaan vähintään automaattiset [yksikkötestit](unittest) jotka testaavat työn **toimintalogiikaa**. Käyttöliittymää ja esim. I/O:ta (esimerkiksi tiedostojen lukua) *ei* tarvitse testata, eikä niiden testauksesta saa arvostelussa lisäpisteitä. 

Yleisesti ottaen hyvien testien tarkoitus on varmistaa, että oma algoritmi on oikein implementoitu. Mitä tämä täsmälleen tarkoittaa
riippuu aiheesta. Alla muutamia aihespecifisiä esimerkkejä. Lisää tulee kunkin toteutuksen aiheehdotus sivuille.

- Onko neuroverkkosi rakenne sellainen kun kuvittelet sen olevan?
- Tekeekö pelitekoälysi aina laillisia siirtoja?
- Löytääkö shakkibottisi matin jos sellainen on omalla laskentasyvyydellä?
- Tarkastaako reitinhakusi juuri ne solmut jotka pitäisi eikä niitä enempää?

Toinen tärkeä osa vakuuttavia testejä on "oikeilla" syötteillä testaaminen. Useat harjoitustyössä 
toteutetut algoritmit ovat tarpeeksi monimutkaisia, että bugeja voi olla vaan isoilla syötteillä.
RSA:han liittyvissä harjoitustöissä realistinen alkulukujen koko ei esimerkiksi ole 13 tai edes 61403. 
Vakuuttavissa testeissä on siis sekä "ihmiselle ymmärrettaviä" syötteitä, että "realistisia" syötteitä.


Alla olevassa taulukossa annetaan hieman tarkempaa osviittaa siitä, mitä harjoitustyön testeiltä vaaditaan. 
Kukin työ arvioidaan kuitenkin aina kokonaisuutena ja esimerkiksi, aiheen vaatimus voi hieman vaikuttaa arvosteluun.
Ohjaajalta kannattaa kysyä, jos on epäselvää.  
Taulukossa sana "metodi" viittaa toimintalogiikan metodeihin. 

---

| Taso (pistemäärä)                 | Kuvaus |
| :---------------------------------  |--------: |
| riittämätön/hylätty (0)           | <span style="font-size:0.9em;">Testejä ei ole ollenkaan.</span> |
| *heikko (1-2)*                    |  <span style="font-size:0.9em;">*Muutamia metodeja testattu yksittäisillä syötteillä. <br>Syötteiden valinnassa suuria puutteita. Testeistä ei ilmene mitä testataan.*</span>        |
| keskinkertainen <br> (3-4)           | <span style="font-size:0.9em;">Suurinta osaa keskeisistä metodeista on testattu muutamalla yksittäisellä syötteellä. Testeistä käy ilmi niiden tarkoitus sekä mitä niillä testataan.</span> |
| *tyydyttävä (5-6)*                |  <span style="font-size:0.9em;">*Kaikki keskeiset metodit on testattu. Käytettävät syötteet kattavat metodeille oletetut normaalin kokoiset syötteet. Testeistä käy selkeästi ilmi niiden tarkoitus. Testit ovat toistettavia ja dokumentaatiosta käy ilmi miten ne toistetaan.*</span>       |
| hyvä (7-8)                      | <span style="font-size:0.9em;">Kaikki keskeiset metodit on kattavasti testattu. Testauksessa käytetään hyödyksi oman harjoitustyön aiheeseen sopivia tekniikoita[^1] täydentämään yksikkötestejä. Testien perusteella voimme olla melko varmoja ohjelman toimintalogiikan oikeellisuudesta.</span>       |
| *vakuuttava / erinomainen (9-10)* | <span style="font-size:0.9em;">*Kaikki[^2] metodit on kattavasti testattu. Testauksessa käytetään hyvin niitä oman harjoitustyön aiheeseen sopivia tekniikoita[^1] jotka täydentävät yksikkötestejä ja ovat oikeelisuuden testaamisen kannalta oleellisia. Testit ovat selkeitä ja niiden kattavuus laaja.*</span>  |

---
[^1]: Tälläiset tekniikat voivat olla esimerkiksi empiirinen testaus, [integraatio](https://en.wiki) testaus, [päästä-päähän](https://www.techtarget.com/searchsoftwarequality/definition/End-to-end-testing) testaus, [invariantti](/invarianttest) testaus, [suorituskyky](/performancetest) testaus. **Huomaa** kuitenkin että näitä kaikkia ei missään nimessä vaadita. Tärkeintä on tehdä omalle harjoitustyölle sopivat testit, ohjaaja auttaa tarvittaessa.   
[^2]: poislukien erittäin yksinkertaiset metodit kuten getterit ja setterit jotka eivät muokkaa syötteitään mitenkään.


{% include typo_instructions.md %}


# Lisähuomautukset
