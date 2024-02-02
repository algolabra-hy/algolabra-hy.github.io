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
Jokaisessa harjoitustyössä vaaditaan vähintään automaattiset [yksikkötestit](unittest) jotka testaavat työn **toimintalogiikaa**. Käyttöliittymää ja I/O:ta (esimerkiksi tiedostojen lukua) *ei* tarvitse testata, eikä niiden testauksesta saa arvostelussa lisäpisteitä. 

Yleisesti ottaen hyvien testien tarkoitus on varmistaa, että oma algoritmi on oikein implementoitu. Mitä tämä täsmälleen tarkoittaa
riippuu aiheesta. Alla muutamia aihespecifisiä esimerkkejä. Lisää tulee kunkin toteutuksen aiheehdotus sivuille.

- Onko neuroverkkosi rakenne sellainen kun pitäisi?
- Tekeekö pelitekoälysi aina laillisia siirtoja?
- Löytääkö shakkibottisi matin jos sellainen on omalla laskentasyvyydellä?
- Tarkastaako reitinhakusi juuri ne solmut jotka pitäisi eikä niitä enempää?

Toinen tärkeä osa vakuuttavia testejä on "oikeilla" syötteillä testaaminen. Useat harjoitustyössä 
toteutetut algoritmit ovat tarpeeksi monimutkaisia, että bugeja voi olla vaan isoilla syötteillä.
RSA:han liittyvissä harjoitustöissä realistinen alkulukujen koko ei esimerkiksi ole 13 tai edes 61403. 
Vakuuttavissa testeissä on siis sekä "ihmiselle ymmärrettaviä" syötteitä, että "realistisia" syötteitä.
Tämän takia yksikkötestit eivät yleensä riitä vakuuttaviin testeihin, tarvitaan myös esim. [integraatio](https://en.wikipedia.org/wiki/Integration_testing) tai [päästä-päähän](https://www.techtarget.com/searchsoftwarequality/definition/End-to-end-testing) testausta. 

Alla olevassa taulukossa annetaan hieman tarkempaa osviittaa siitä, mitä harjoitustyön testeiltä vaaditaan. 
Kukin työ arvioidaan kuitenkin aina kokonaisuutena ja esimerkiksi aiheen vaativuus voi hieman vaikuttaa arvosteluun.
Ohjaajalta kannattaa kysyä tarpeen mukaan.  
Taulukossa sana "metodi" viittaa toimintalogiikan metodeihin. 

---

| Taso (pistemäärä)                 | Kuvaus |
| :---------------------------------  |--------: |
| riittämätön/hylätty (0)           | <span style="font-size:0.9em;">Testejä ei ole ollenkaan tai ne eivät testaa oikeellisuuteen liityviä asioita.</span> |
| *heikko (1)*                    |  <span style="font-size:0.9em;">*Projektin pääfunktioita testataan muutamalla syötteellä. Valittujen syötteiden edustavuudessa puutteita.*</span>        |
| keskinkertainen <br> (2-4)           | <span style="font-size:0.9em;">Keskeisimmät metodit on testattu muutamalla edustavalla syötteellä. Testien dokumentaatiosta käy ilmi niiden tarkoitus.</span> |
| *tyydyttävä (5-7)*                |  <span style="font-size:0.9em;">*Kaikki keskeiset metodit on testattu. Käytettävät syötteet ovat edustavia. Testit ovat toistettavia ja selkeitä.*</span>       |
| *vakuuttava / erinomainen (8-10)* | <span style="font-size:0.9em;">*Kaikki[^1] metodit on testattu. Testauksessa käytetään niitä oman harjoitustyön aiheeseen sopivia tekniikoita[^2] jotka täydentävät yksikkötestejä ja ovat oikeelisuuden testaamisen kannalta oleellisia. Testit ovat erittäin selkeitä ja niiden kattavuus laaja. Käytettävät syötteet ovat erittäin edustavia, kattaen sekä oletetut syötteet, että reunatapaukset.*</span>  |

---



{% include typo_instructions.md %}


# Lisähuomautukset
[^1]: poislukien erittäin yksinkertaiset metodit kuten getterit ja setterit jotka eivät muokkaa syötteitään mitenkään.
[^2]: Tälläiset tekniikat voivat olla esimerkiksi empiirinen testaus, [integraatio](https://en.wikipedia.org/wiki/Integration_testing) testaus, [päästä-päähän](https://www.techtarget.com/searchsoftwarequality/definition/End-to-end-testing) testaus, [invariantti](/invarianttest) testaus, [suorituskyky](/performancetest) testaus. **Huomaa** kuitenkin että näitä kaikkia ei missään nimessä vaadita. Tärkeintä on tehdä omalle harjoitustyölle sopivat testit, ohjaaja auttaa tarvittaessa.   
