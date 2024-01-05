---
layout: page
permalink: /testing
title: Harjoitustyön Testaaminen
title_long: Harjoitustyön Testaaminen
inheader: yes
---

Täältä löydät harjoitustyön testaamiseen liittyvää materiaalia. Sivut ovat vielä rakenteilla ja hyödyllisistä materiaaleista saa mielellään vinkata Jeremiakselle. 


## Yksikkötestaus ja Riippuvuuksien Injektointi
Mikäli yksikkötestaus ei ole entuudestaan tuttua kannattaa ensin lukea Ohjelmistotuotanto kurssin [yksikkötestaus ohjeet](/unittest). Myös materiaalista [riippuvuuden injektoinnista pythonille](/riippuvuuksien_injektointi_python) tai [javalle](/riippuvuuksien_injektointi)
voi olla hyötyä. Riippuvuuksien injektointi on ohjelmointitekniikka joka tekee testaamisesta helpompaa. 

## Monimutkaisten algoritmien testauksesta. 
Harjoitustyössä toteutetaan monimutkaisia algoritmeja. Näiden testaaminen voi olla haasteellista, usein yksikkötestit yksinään eivät riitä. Monimutkaisten algoritmien testaaminen vaatii hyvää ymmärrystä algoritmin toiminnasta. Mitä tarkoittaa että algoritmisi toimii oikein? 
- Pelejä pelaavan botin oikeellisuus ei ole että se "pelaa hyvin". Miinaharavabotti ei saa koskaan osua miinaan silloin, kun ruutua pidetään turvallisena. Shakkibotti ei saa tehdä laittomia siirtoja, ja sen on osattava tehdä matti, mikäli se on mahdollista sillä laskentasyvyydellä, jota käytetään. 
- Reitinhaku algoritmin oikeellisuus ei ole vain että se löytää lyhyimmän reitin. Esimerkiksi A* haku jonka heuristiikka on käänteellinen löytää lyhyimmän reitin, siihen menee vaan paljon kauemmin aikaa kun pitäisi. 
- Pakkausalgoritmin oikeelisuuteen ei riitä, että purettu tiedosto on sama kuin pakattu. Tämän lisäksi esim pakatun tiedoston koon täytyy olla odotuksien mukainen. 
- Neuroverkkojen oikeellisuuden testaamiseen ei riitä, että verkko klassifioi jonkun yksittäisen esimerkkitapauksen oikein. Sen sijaan täytyy testata toimiiko backpropagation oikein? Pineneekö virhe jokaisella inputilla? Voiko yhden kokoisen treenisetin saada 0 erroriin? Lue lisää [Sebastian Björkqvistin blogista](https://www.sebastianbjorkqvist.com/blog/writing-automated-tests-for-neural-networks/).

Monimutkaisille algoritmeille voi olla vaikea keksiä kuvaavia esimerkkisyötteitä joita testata. Voimmeko olla varmoja, että esimerkkisyötteemme testaavat kaikki haarat? Entä jos koodimme bugaa vain yli tuhannen kokoisilla syötteillä? Yksi tapa (ainakin osittain) lisätä testiemme luotettavuutta on ns. [invariantti testaus](/invarianttest).

**Huom** Verrattuna yksikkötesteihin, monimutkaisempien ominaisuuksien oikeellisuus- ja suorituskyvyn testit voivat kestää melko kauan. Niinpä niitä ei välttämättä kannata ajaa yksikkötestien kanssa joka kerralla. Sen sijaan testeistä kannattaa laittaa muutama edustava (esim automaattisesti löydetty) tapaus yksikkötesteihin ja ajaa loput erillisenä testiohjelmalla. Toisin sanoen, harjoitustyössä tarvitaan *sekä* yksikkötestejä, että monimutkaisempia testejä. 


## Lisää materiaalia
- [Pylint](/pylint) on python koodin stattiseen analysiin tarkoitettu työkalu joka helpottaa koodin laadun ylläpitoa. 
- [Neuroverkkojen testauksesta](https://www.sebastianbjorkqvist.com/blog/writing-automated-tests-for-neural-networks/) Sebastian Björkqvistin blogikirjoitus.

{% include typo_instructions.md %}
