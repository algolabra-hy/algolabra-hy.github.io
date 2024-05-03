---
layout: page
permalink: /testing
title: Harjoitustyön Testaaminen
title_long: Harjoitustyön Testaaminen
inheader: yes
---

Täältä löydät harjoitustyön testaamiseen liittyvää materiaalia. Sivut ovat vielä rakenteilla. Hyödyllisistä materiaaleista saa mielellään vinkata Jeremiakselle. 

## Ihan ensiksi
Lue harjoitustyön [testauksen vaatimuksista](/testreqs) kurssin arvostelussa.


## Yksikkötestaus ja riippuvuuksien injektointi
Mikäli yksikkötestaus ei ole entuudestaan tuttua kannattaa ensin lukea Ohjelmistotuotanto kurssin [yksikkötestaus ohjeet](/unittest). Myös materiaalista [riippuvuuden injektoinnista Pythonille](/riippuvuuksien_injektointi_python) tai [Javalle](/riippuvuuksien_injektointi)
voi olla hyötyä. Riippuvuuksien injektointi on ohjelmointitekniikka joka tekee testaamisesta helpompaa. 

## Monimutkaisten algoritmien testauksesta. 
Harjoitustyössä toteutetaan monimutkaisia algoritmeja. Näiden testaaminen voi olla haasteellista, usein yksikkötestit yksinään eivät riitä. Monimutkaisten algoritmien testaaminen vaatii hyvää ymmärrystä algoritmin toiminnasta. Mitä tarkoittaa että algoritmisi toimii oikein? 
- Pelejä pelaavan botin oikeellisuus ei ole että se "pelaa hyvin". Miinaharavabotti ei saa koskaan osua miinaan silloin, kun ruutua pidetään turvallisena. Shakkibotti ei saa tehdä laittomia siirtoja, ja sen on osattava tehdä matti, mikäli se on mahdollista sillä laskentasyvyydellä, jota käytetään. 
- Reitinhaku algoritmin oikeellisuus ei ole vain että se löytää lyhyimmän reitin. Esimerkiksi A* haku, jonka heuristiikka on käänteellinen, löytää lyhyimmän reitin mutta siihen menee vaan paljon kauemmin aikaa kuin pitäisi. 
- Pakkausalgoritmin oikeellisuuteen ei riitä, että purettu tiedosto on sama kuin pakattu. Tämän lisäksi esim pakatun tiedoston koon täytyy olla odotuksien mukainen. 
- Neuroverkkojen oikeellisuuden testaamiseen ei riitä, että verkko klassifioi ison osan testisetistä oikein. Tämän lisäksi pitäisi testata, onko sen rakenne oikein? Toimiiko backpropagation oikein?

### Testisyötteiden edustavuus
Monimutkaisille algoritmeille voi olla vaikea keksiä kuvaavia esimerkkisyötteitä joita testata. Voimmeko olla varmoja, että esimerkkisyötteemme testaavat kaikki haarat? Entä jos koodimme bugaa vain yli tuhannen kokoisilla syötteillä? Varsinkin monimutkaisten algoritmien testaamisessa on oleellista, että käytetyt syötteet ovat edustavia. 

Testisyötteiden edustavuudesta lisää [täällä](/respresentativeinputs).

### Yksikkötestien lisäksi 
Vaikka yksikkötesteillä ja edustavilla syötteillä päästään jo pitkälle, harjoitustyön [vakuuttavaan](/testreqs) testaukseen vaaditaan usein muitakin testaustekniikkoja. Esimerkkejä tälläisistä
tekniikoista ovat: 
- [Integraatiotestaus](https://en.wikipedia.org/wiki/Integration_testing)
- [Päästä päähän testaus](https://www.browserstack.com/guide/end-to-end-testing)
- [Invarianttitestaus](/invarianttest), ja
- [Suorituskykytestaus](performancetest)

**Huomaa** kuitenkin, että näitä kaikkia ei tarvitse käyttää. Tärkeintä on miettiä omaan harjoitustyöhön sopivat testit. Kurssin henkilökunta auttaa tarvittaessa. 
 Verrattuna yksikkötesteihin, monimutkaisempien ominaisuuksien oikeellisuus- ja suorituskyvyn testit voivat kestää melko kauan. Niinpä niitä ei välttämättä kannata ajaa yksikkötestien kanssa joka kerralla. Sen sijaan testeistä kannattaa laittaa muutama edustava (esim automaattisesti löydetty) tapaus yksikkötesteihin ja ajaa loput erillisenä testiohjelmalla. Toisin sanoen, harjoitustyössä tarvitaan *sekä* yksikkötestejä, että monimutkaisempia testejä. 


## Lisää materiaalia
- [Pylint](/pylint) on Python koodin stattiseen analysiin tarkoitettu työkalu joka helpottaa koodin laadun ylläpitoa. 
- [Neuroverkkojen testauksesta](https://www.sebastianbjorkqvist.com/blog/writing-automated-tests-for-neural-networks/) Sebastian Björkqvistin blogikirjoitus.
- [Range Minimum Querie esimerkki](https://github.com/TiraLabra/Testing-and-rmq) repositorio jossa esimerkkejä hieman monimutkaisempien algoritmien testaamisesta. 

{% include typo_instructions.md %}
