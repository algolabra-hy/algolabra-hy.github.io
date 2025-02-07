---
layout: page
permalink: /testreqs-fi
title: Harjoitustyön vaatimukset testeille
title_long: Mitä vaaditaan harjotustyön testeiltä
lang: fi # fi or en
ref: testing_requirements # same as the markdown filename
---

## Testien vaatimuksista - mitä pitää testata?
Jokaisessa harjoitustyössä vaaditaan vähintään automaattiset [yksikkötestit]({% link _pages/fin/unit_testing.md %}) jotka testaavat työn **toimintalogiikkaa**. 
Käyttöliittymää ja I/O:ta (esimerkiksi tiedostojen lukua) *ei* tarvitse testata, eikä niiden testauksesta saa arvostelussa lisäpisteitä. 

Yleisesti ottaen hyvien testien tarkoitus on varmistaa, että oma algoritmi on oikein toteutettu. Mitä tämä täsmälleen tarkoittaa
riippuu aiheesta. Alla muutamia esimerkkejä. Kurssin henkilökunta auttaa tarvittaessa.

- Onko neuroverkkosi rakenne sellainen kuin pitäisi?
- Tekeekö pelitekoälysi aina laillisia siirtoja?
- Löytääkö shakkibottisi matin jos sellainen on omalla laskentasyvyydellä?
- Tarkastaako reitinhakusi juuri ne solmut jotka pitäisi eikä niitä enempää?
- Toimiiko RSA salauksesi oikein sekä pienillä, että isoilla avaimilla? 
- Pakkaako ja purkaako tiedonpakkausalgoritmisi kaiken kokoisia tiedostoja oikein?

Toinen tärkeä osa vakuuttavia testejä on [edustavilla]({% link _pages/fin/testing_representative_inputs.md %}) syötteillä testaaminen. Useat harjoitustyössä 
toteutetut algoritmit ovat tarpeeksi monimutkaisia, että kaikkia bugeja ei löydy pienillä syötteillä. 
RSA:han liittyvissä harjoitustöissä realistinen alkulukujen koko ei esimerkiksi ole 13 tai edes 61403. 
Vakuuttavissa testeissä on siis sekä "ihmiselle ymmärrettäviä" syötteitä, että "realistisia" syötteitä.
Yleensä vakuuttaviin testeihin vaditaan yksikkötestaamisen lisäksi [edistyneempiä testaustekniikoita]({% link _pages/fin/testing_frontpage.md %}#yksikkötestien-lisäksi). Mieti itse mikä sopisi aiheeseesi ja kysy ohjaajalta tarvittaessa. Tyypillisesti [integraatio](https://en.wikipedia.org/wiki/Integration_testing) 
tai [päästä-päähän](https://www.techtarget.com/searchsoftwarequality/definition/End-to-end-testing) testaus riittää. 

## Testien tarkoituksesta tällä kurssilla
Tämän kurssin olennaisena osana on kokonaisen projektin, ja sen testien *itsenäinen* suunnittelu ja toteutus.
Takoitus on siis---ohjaajan avulla---itse miettiä minkälaiset testit tarvitaan, jotta voitaisiin olla (melko) varmoja 
siitä, että ohjelmasi on oikein toteutettu. Huomaa että tämä on eri asia kuin ohjelman tehokkuuden testaaminen. Muilla kursseilla 
testejä usein tarjotaan valmiina ja vaaditaan, että ohjelmasi pitää päästä juuri niistä läpi. Tällä 
kurssilla sen sijaan vaaditaan ymmärrystä siitä, mitä kussakin harjoitustyössä edes pitäisi testata. 
**Varaudu käyttämään testien suunnitteluun aikaa**. Mieti mitä ohjelmasi eri metodien pitäisi tehdä? Minkä kokoisilla syötteillä niiden pitäisi toimia? 
Mitä reunatapauksia pitäisi osata käsitellä? Huomaa, että esim.. testien määrä ei ole oleellinen asia. Edustaviin testeihin päästään usein 
muutamalla hyvin valitulla testillä ja syöttellä. Toisaalta suuri määrä sattumanvaraisesti tuotettuja testejä harvemmin riittää. 

Pyri siihen, että jokaisessa toteuttamassasi testissä osaat selittää (ainakin itsellesi) miksi tämä testi näillä syötteillä on mukana? 
**Ohjaaja auttaa tarvittaessa** ota yhteyttä jos testien kehitys ei etene. Varaudu kuitenkin siihen, että ohjaajakin kysyy mitä metodisi pitäisi tehdä ja 
minkä kokoisilla syötteillä sen pitäisi toimia? Sinun ei tarvitse osata tyhjentävästi vastata näihin kysymyksiin ennen kuin otat yhteyttä ohjaajaan, mutta
sinun täytyy miettiä näitä ja valmistautua kertomaan ohjaajalle oman näkökulmasi siitä, miksi testien suunnittelu ei etene. 


## Testien arvostelusta

Alla olevassa taulukossa annetaan hieman tarkempaa osviittaa siitä, mitä harjoitustyön testeiltä vaaditaan. 
Kukin työ arvioidaan kuitenkin aina kokonaisuutena ja esimerkiksi aiheen vaativuus voi hieman vaikuttaa arvosteluun.
Ohjaajalta kannattaa kysyä apua tarpeen mukaan.  
Taulukossa sana "metodi" viittaa toimintalogiikan metodeihin. 

---

| Taso (pistemäärä)                 | Kuvaus |
| :---------------------------------  |--------: |
| riittämätön/hylätty (0)           | <span style="font-size:0.9em;">Projektin päämetodeja ei testata ollenkaan tai niiden testit eivät testaa oikeellisuuteen liittyviä asioita.</span> |
| heikko (1)                    |  <span style="font-size:0.9em;">Projektin päämetodeja testataan muutamalla syötteellä. Valittujen syötteiden [edustavuudessa]({% link _pages/fin/testing_representative_inputs.md %}) puutteita.</span>        |
| keskinkertainen <br> (2-4)           | <span style="font-size:0.9em;">Keskeisimmät metodit on testattu muutamalla [edustavalla]({% link _pages/fin/testing_representative_inputs.md %}) syötteellä. Testien dokumentaatiosta käy ilmi niiden tarkoitus.</span> |
| tyydyttävä (5-7)                |  <span style="font-size:0.9em;">Kaikki keskeiset metodit on testattu. Käytettävät syötteet ovat edustavia. Testit ovat toistettavia ja selkeitä.</span>       |
| vakuuttava / erinomainen (8-10) | <span style="font-size:0.9em;">Testauksessa käytetään niitä omaan aiheeseen sopivia tekniikoita jotka ovat oikeelisuuden testaamisen kannalta oleellisia. Testit ovat erittäin selkeitä. Käytettävät syötteet ovat perusteltuja ja edustavia.</span>  |

---



{% include typo_instructions_fin.md %}



