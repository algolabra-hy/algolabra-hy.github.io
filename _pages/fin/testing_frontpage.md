---
layout: page
permalink: /testing-fi
title: Harjoitustyön testaaminen
title_long: Harjoitustyön testaaminen
inheader: yes
dropdown: true
lang: fi # fi or en
ref: testing_frontpage # same as the markdown filename
children:
  - title: Yleiskatsaus testaamisesta (lue tämä ensin)
    permalink: /testing-fi
  - title: Testauksen vaatimuksesta 
    permalink: /testreqs-fi
  - title: Yksikkötestaaminen
    permalink: /unittest-fi
  - title: Riippuvuuden injektointi
    permalink: /dependency-injection-fi
  - title: Testisyötteiden edustavuus
    permalink: /testing-representative-inputs-fi
---

Täältä löydät harjoitustyön testaamiseen liittyvää materiaalia. 

## Testauksen vaatimuksista
Lue harjoitustyön [testauksen vaatimuksista]({% link _pages/fin/testing_requirements.md %}) kurssin arvostelussa.


## Yksikkötestaus ja riippuvuuksien injektointi
Mikäli yksikkötestaus ei ole entuudestaan tuttua kannattaa ensin lukea Ohjelmistotuotanto kurssin [yksikkötestaus ohjeet]({% link _pages/fin/unit_testing.md %}). Myös materiaalista [riippuvuuden injektoinnista]({% link _pages/fin/dependency_injection_python.md %})
voi olla hyötyä. Riippuvuuksien injektointi on ohjelmointitekniikka joka tekee testaamisesta helpompaa. 

## Monimutkaisten algoritmien testauksesta. 
Harjoitustyössä toteutetaan monimutkaisia algoritmeja. Näiden testaaminen voi olla haasteellista, usein yksikkötestit eivät riitä. Monimutkaisten algoritmien testaaminen vaatii hyvää ymmärrystä algoritmin toiminnasta. Mitä tarkoittaa että algoritmisi toimii oikein? 
- Pelejä pelaavan botin oikeellisuus ei ole että se "pelaa hyvin". Miinaharavabotti ei saa koskaan osua miinaan silloin, kun ruutua pidetään turvallisena. Shakkibotti ei saa tehdä laittomia siirtoja, ja sen on osattava tehdä matti, mikäli se on mahdollista sillä laskentasyvyydellä, jota käytetään. 
- Reitinhaku algoritmin oikeellisuus ei ole vain että se löytää lyhyimmän reitin. Esimerkiksi A* haku, jonka heuristiikka on käänteellinen, löytää lyhyimmän reitin mutta siihen menee vaan paljon kauemmin aikaa kuin pitäisi. 
- Pakkausalgoritmin oikeellisuuteen ei riitä, että purettu tiedosto on sama kuin pakattu. Tämän lisäksi esim pakatun tiedoston koon täytyy olla odotuksien mukainen. 
- Neuroverkkojen oikeellisuuden testaamiseen ei riitä, että verkko klassifioi ison osan testisetistä oikein. Tämän lisäksi pitäisi testata, onko sen rakenne oikein? Toimiiko backpropagation oikein?

### Testisyötteiden edustavuus
Monimutkaisille algoritmeille voi olla vaikea keksiä kuvaavia esimerkkisyötteitä joita testata. Voimmeko olla varmoja, että esimerkkisyötteemme testaavat kaikki haarat? Entä jos koodimme bugaa vain yli tuhannen kokoisilla syötteillä? Varsinkin monimutkaisten algoritmien testaamisessa on oleellista, että käytetyt syötteet ovat edustavia. 

Testisyötteiden edustavuudesta lisää [täällä]({% link _pages/fin/testing_representative_inputs.md %}).

### Yksikkötestien lisäksi 
Vaikka yksikkötesteillä ja edustavilla syötteillä päästään jo pitkälle, harjoitustyön [vakuuttavaan]({% link _pages/fin/testing_requirements.md %}) testaukseen vaaditaan usein muitakin testaustekniikkoja. Esimerkkejä tälläisistä
tekniikoista ovat: 
- [Integraatiotestaus](https://en.wikipedia.org/wiki/Integration_testing)
- [Päästä päähän testaus](https://www.browserstack.com/guide/end-to-end-testing)
- [Invarianttitestaus]({% link _pages/fin/invariant_testing.md %}), ja
- [Suorituskykytestaus]({% link _pages/fin/performance_testing.md %})

**Huomaa** kuitenkin, että näitä kaikkia ei tarvitse käyttää. Tärkeintä on miettiä omaan harjoitustyöhön sopivat testit. Kurssin henkilökunta auttaa tarvittaessa. 
 Verrattuna yksikkötesteihin, monimutkaisempien ominaisuuksien oikeellisuus- ja suorituskyvyn testit voivat kestää melko kauan. Niinpä niitä ei välttämättä kannata ajaa yksikkötestien kanssa joka kerralla. Sen sijaan testeistä kannattaa laittaa muutama edustava (esim automaattisesti löydetty) tapaus yksikkötesteihin ja ajaa loput erillisenä testiohjelmalla. Toisin sanoen, harjoitustyössä tarvitaan *sekä* yksikkötestejä, että monimutkaisempia testejä. 


## Lisää materiaalia
- [Pylint]({% link _pages/fin/pylint.md %}) on Python koodin stattiseen analysiin tarkoitettu työkalu joka helpottaa koodin laadun ylläpitoa. 
- [Neuroverkkojen testauksesta](https://www.sebastianbjorkqvist.com/blog/writing-automated-tests-for-neural-networks/) Sebastian Björkqvistin blogikirjoitus.
- [Range Minimum Querie esimerkki](https://github.com/TiraLabra/Testing-and-rmq) repositorio jossa esimerkkejä hieman monimutkaisempien algoritmien testaamisesta. 

{% include typo_instructions_fin.md %}
