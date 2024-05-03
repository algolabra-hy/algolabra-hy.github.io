---
layout: page
permalink: /respresentativeinputs
title: Testisyötteiden Edustavuus
title_long: Edustavuus
inheader: no
---
_Nämä ohjeet on kirjoittanut Jeremias Berg_

Käydään tässä läpi hieman testeissä käytettävien syötteiden edustavuuden tärkeydestä esimerkin kautta.
Yleisempää asiaa edustavista syötteistä löytyy [testien vaatimus sivulta.](/testreqs#testien-tarkoituksesta-tällä-kurssilla)


Alla oleva esimerkki olettaa osaamista [yksikkötesteistä](/unittest) ja Python projektin 
alustamisesta [Poetrylla](/poetry).
Tämän osion tarkoitus on näyttää edustavien testisyötteiden valinnan 
tärkeyden ja kuinka, jopa järkevästi suunnitellut testit,
eivät välttämättä paljasta bugeja jos syötteet eivät ole edustavia. 

## Leveyssuuntainen Läpikäynti
Tutkitaan seuraavaa leveyssuuntaista läpikäyntiä lyhyimmän etäisyyden laskemiseen. 
Tämä on tehty [Geeks for Geeksin](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) artikkelin perusteella. 

```python
from collections import defaultdict
 
class Graph:
 
    def __init__(self, solmumaara):
        self.verkko = defaultdict(list)
        self.solmut = solmumaara
 
    def lisaaKaari(self, u, v):
        self.verkko[u].append(v)
 
    def BFS(self, lahto, maali): 
        vierailtu = [False] * (self.solmut + 1)
        jono = []
        jono.append((lahto, 0))
        vierailtu[lahto] = True

        while jono:
            (solmu, etaisyys) = jono.pop()
            if (solmu == maali):
                return etaisyys
            for naapuri in self.verkko[solmu]:
                if vierailtu[naapuri] == False:
                    jono.append((naapuri, etaisyys + 1))
                    vierailtu[naapuri] = True
        
        return -1 # reittiä ei ole
 
```
Tässä siis melko yksinkertainen koodi joka käyttää [leveyssuuntaista läpikäyntiä](https://en.wikipedia.org/wiki/Breadth-first_search) (BFS algoritmia) laskeakseen lyhyimmän reitin kahden solmun 
välillä painottamattomassa verkossa. Tässä implementaatiossa on kuitenkin bugi, 
katso pystytkö jo tässä vaiheessa huomaamaan sen?

# Yksikkötestit
Tehdään BFS algoritmille yksikkötestit. Jos testien tekeminen ja ajaminen ei tunnu tutulta, 
kannattaa tutustua aikaisempaan materiaaliin [yksikkötestauksesta](/unittest).

```python
import unittest
from bfs import Graph

class TestBFS(unittest.TestCase):
	def test_bfslaskeeetaisyydenoikein(self):
		verkko = Graph(3) 
		verkko.lisaaKaari(0, 1)
		verkko.lisaaKaari(0, 2)
		verkko.lisaaKaari(1, 3)
		verkko.lisaaKaari(2, 3)
		self.assertEqual(verkko.BFS(0, 3), 2)
```
Tämä tuntuu järkevältä testiltä. Tehdään verkko jossa tiedetään, että solmun 0
ja 3 välillä on kaksi askelta, ja kokeillaan, että BFS metodi on asiasta samaa mieltä. 

Kokeillaan:
```
(syotteidenedustavuus-py3.9) jezberg@LM2-500-27156 syotteidenedustavuus % pytest src 
============= test session starts ==============
platform darwin -- Python 3.9.6, pytest-8.0.0, pluggy-1.4.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/syotteidenedustavuus
collected 1 item                                                                                                                                                                           

src/tests/bfs_test.py .                                                                                                                                                              [100%]

============== 1 passed in 0.04s ===============
```

Eli menee läpi. Kuitenkin implementaatiossa on bugi, joten tämä testi ei yksinään riitä. 
Itse testissä ei ole mitään vikaa. BFS algoritmin tarkoitus on löytää 
lyhyin reitti kahden solmun välillä, joten testi joka tarkastaa, että näin tapahtuu 
on järkevä. Ongelmana tässä on, että tällä syötteellä bugia ei saa kiinni. 

Kuvitellaan, että emme 
tiedä, että koodissa on bugi. Hyvinä koodaajina tiedämme kuitenkin, 
että yhden esimerkin periaatteella ei pitkälle pötkitä ja tehdään toinenkin testi. 

```python
def test_bfslaskeeetaisyydenoikein_toinen(self):
	verkko = Graph(4)
	verkko.lisaaKaari(0, 1)
	verkko.lisaaKaari(0, 4)
	verkko.lisaaKaari(4, 2)
	verkko.lisaaKaari(1, 2)
	verkko.lisaaKaari(2, 3)
	self.assertEqual(verkko.BFS(0, 3), 3)
```
ja kokeillaan:
```
(syotteidenedustavuus-py3.9) jezberg@LM2-500-27156 syotteidenedustavuus % pytest src 
============= test session starts ==============
platform darwin -- Python 3.9.6, pytest-8.0.0, pluggy-1.4.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/syotteidenedustavuus
collected 2 items                                                                                                                                                                          

src/tests/bfs_test.py ..                                                                                                                                                             [100%]

============== 2 passed in 0.02s ===============
```
Edelleenkin menee läpi. 

# Syötteiden edustavuus
Tässä vaiheessa voisi olla houkuttelevaa luottavaisin mielin jatkaa kehitystä. 
Kannattaa kuitenkin pysähtyä miettimään millä syötteillä tässä testataan. 
Piirretään ensimmäisen testin verkko:

![]({{ "/images/verkko1.png" | absolute_url }})

ja toisen testin verkko:

![]({{ "/images/verkko2.png" | absolute_url }})

Molemmissa etsitään lyhyintä reittiä solmun 0 ja solmun 3 välillä. 
Näitä tarkastelemalla huomataan, että vaikka nämä ovat eri verkot, 
ne eivät itse asiassa testaa eri asioita meidän algoritmissamme. 
Molemmissa verkoissa kaikki reitit solmun 0 ja 3 välillä ovat yhtä pitkiä. 
Ts. nämä syötteet eivät ole **edustavia**. Toinen testi ei lisää testiemme 
vakuuttavuutta tai kattavuutta. 

# Toisenlainen testiverkko
Aikaisemmasta viisastuneena kehitetään testi jossa lähtö- ja maalisolmun välillä on 
eri pituisia reittejä: 
```python
def test_bfstoimiikunoneripituisiareitteja(self):
	verkko = Graph(5)
	verkko.lisaaKaari(0, 1)
	verkko.lisaaKaari(0, 2)
	verkko.lisaaKaari(1, 3)
	verkko.lisaaKaari(2, 5)
	verkko.lisaaKaari(2, 4)
	verkko.lisaaKaari(4, 3)
	self.assertEqual(verkko.BFS(0, 3), 2)
```
joka testaa verkkoa:

![]({{ "/images/verkko3.png" | absolute_url }})

Kokeillaan:
```
=================== FAILURES ===================
______________________________________________________________________ TestBFS.test_bfstoimiikunoneripituisiareitteja ______________________________________________________________________

self = <tests.bfs_test.TestBFS testMethod=test_bfstoimiikunoneripituisiareitteja>

    def test_bfstoimiikunoneripituisiareitteja(self):
    	verkko = Graph(5)
    	verkko.lisaaKaari(0, 1)
    	verkko.lisaaKaari(0, 2)
    	verkko.lisaaKaari(1, 3)
    	verkko.lisaaKaari(2, 5)
    	verkko.lisaaKaari(2, 4)
    	verkko.lisaaKaari(4, 3)
>   	self.assertEqual(verkko.BFS(0, 3), 2)
E    AssertionError: 3 != 2

src/tests/bfs_test.py:30: AssertionError
=========== short test summary info =============
FAILED src/tests/bfs_test.py::TestBFS::test_bfstoimiikunoneripituisiareitteja - AssertionError: 3 != 2
========= 1 failed, 2 passed in 0.04s ===========
```
Eli nyt menee pieleen. Tästä voimme alkaa metsästää bugiamme. 
Hetken debuggauksen jälkeen huomaamme, että 
BFS metodi ei poista jonon ensimmäistä alkiota, vaan viimeisen.
Täten implementoimme vahingossa syvyyssuuntaisen läpikäynnin. 

# Korjataan koodi
Hyvän testin avulla koodin korjaus on melko yksikertaista. Lisätään jonon pop metodin argumentti, joka pyytää poistamaan ensimmäisen alkion. 
```python
def BFS(self, lahto, maali): 
    vierailtu = [False] * (self.solmut + 1)
    jono = []
    jono.append((lahto, 0))
    vierailtu[lahto] = True

    while jono:
        (solmu, etaisyys) = jono.pop(0)
        if (solmu == maali):
            return etaisyys
        for naapuri in self.verkko[solmu]:
            if vierailtu[naapuri] == False:
                jono.append((naapuri, etaisyys + 1))
                vierailtu[naapuri] = True
       
    return -1 # reittiä ei ole
```
ja kokeillaan:

```
(syotteidenedustavuus-py3.9) jezberg@LM2-500-27156 syotteidenedustavuus % pytest src 
============= test session starts ==============
platform darwin -- Python 3.9.6, pytest-8.0.0, pluggy-1.4.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/syotteidenedustavuus
collected 3 items                                                                                                                                                                          

src/tests/bfs_test.py ...                                                                                                                                                            [100%]

============== 3 passed in 0.02s ===============
```

Hyvin valittujen testisyötteiden avulla löydettiin ja korjatiin muuten hankalasti löydettävissä oleva bugi. 

## Yhteenveto
Monimutkaisten algoritmien testauksessa testisyötteiden valinta on yhtä tärkeää kuin testien suunnittelu. Tässä käytettiin 
vain yhden tyyppistä testiä "annettuna verko jonka lyhyin reitti lähdön ja maalin välillä tunnetaan, 
testaa palauttaako metodimme saman arvon". Tällä testillä saatiin kiinni koodin bugi, mutta kuitenkin vain oikeanlaisella syötteellä. 

Vaikka omaa harjoitustyön kehityksessä ei aina voi tietää, että koodissa on bugeja, 
syötteiden edustavuuteen pitää silti aina kiinnittää huomiota. Testejä kannattaa kirjoittaa jo 
työn kehitysvaiheessa eikä vasta jälkikäteen. Aina kun törmäät bugiin, kirjoita testi joka hylkää koodin nykyisen version, ja korjaa vasta sitten. 

{% include typo_instructions.md %}


## Lisää huomioita

Palataan vielä hetkeksi bugiseen implementaatioon:

```python
def BFS(self, lahto, maali): 
    vierailtu = [False] * (self.solmut + 1)
    jono = []
    jono.append((lahto, 0))
    vierailtu[lahto] = True

    while jono:
        (solmu, etaisyys) = jono.pop()
        if (solmu == maali):
            return etaisyys
        for naapuri in self.verkko[solmu]:
            if vierailtu[naapuri] == False:
                jono.append((naapuri, etaisyys + 1))
                vierailtu[naapuri] = True
        
    return -1 # reittiä ei ole
 ```
Katsotaan sille seuraavaa testiä:
```python
def test_bfstoimiikunoneripituisiareitteja(self):
	verkko = Graph(5)
	verkko.lisaaKaari(0, 2)
	verkko.lisaaKaari(0, 1)
	verkko.lisaaKaari(1, 3)
	verkko.lisaaKaari(2, 5)
	verkko.lisaaKaari(2, 4)
	verkko.lisaaKaari(4, 3)
 	self.assertEqual(verkko.BFS(0, 3), 2)
```
Tämä on melkein sama kuin testi jolla saimme bugin kiinni. Tässäkin testataan verkkoa:

![]({{ "/images/verkko3.png" | absolute_url }})

Ainoa ero on järjestys jossa kaaret lisätään verkkoon. Tässä kaari (0,2) lisätään ennen kaarta (0,1).  
Kokeillaan:

```
(syotteidenedustavuus-py3.9) jezberg@LM2-500-27156 syotteidenedustavuus % pytest src 
============= test session starts ==============
platform darwin -- Python 3.9.6, pytest-8.0.0, pluggy-1.4.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/syotteidenedustavuus
collected 1 item                                                                                                                                                                           

src/tests/bfs_test.py .                                                                                                                                                              [100%]

============== 1 passed in 0.02s ===============
```
Eli nyt meneekin läpi. Nyt tässä nimittäin käy niin, että syvyyssuuntainen läpikäynti löytää (sattumalta) lyhyimmän reitin maaliin koska solmun 0 naapureista, se kokeilee ensin solmua 1. 

Toisin sanoen, buginen koodimme toimii jos lähdon ja maalin väliset reitit ovat kaikki yhtä pitkiä, ja joskus vaikka näin ei olisikaan. Ollaksemme täysin varmoja koodin oikeellisuudesta meidän 
pitäisi pystyä "keksimään" kaikki eri tyyppiset verkot, ja kokeilemaan niitä kaikkia.
Tämä ei kuitenkaan ole realistista, edes tässä helpossa tapauksessa, saati sitten vaikeempien harjoitustyön aiheiden testaamisessa. 

### Lisää testejä
Koska kaikkien edustavien syötteiden itse keksiminen ei ole realistista, tarvitaan muita testaustekniikkoja. Tässä kannattaa miettiä, mitä muuta metodimme pitäisi toteuttaa. 
Tuntuisi ilmeiseltä, että metodimme pitäisi palauttaa sama arvo, riippumatta siitä, missä järjestyksessä kaaret on lisätty verkkoon. Tehdään siis testi joka kokeilee tätä: 

```python
def test_bfseiriipukaarienjarjestyksesta(self):
	kaaret = []
	kaaret.append((0,2))
	kaaret.append((0,1))
	kaaret.append((1,3))
	kaaret.append((2,5))
	kaaret.append((2,4))
	kaaret.append((4,3))
	verkko = Graph(5)
	for (x, y) in kaaret:
		verkko.lisaaKaari(x,y)
	ensimmäinen_etaisyys = verkko.BFS(0,3)
	for kaari_permutaatio in list(itertools.permutations(kaaret)):
		verkko = Graph(5)
		for (x, y) in kaari_permutaatio:
			verkko.lisaaKaari(x,y)
		etaisyys = verkko.BFS(0,3)
		self.assertEqual(ensimmäinen_etaisyys, etaisyys)
```
Tässä siis kerätään kaaret listaan, ja sitten permutoidaan sitä ja tarkastetaan, että kaikilla järjestyksillä tulee sama tulos. Tämä testi hylkää odotetusti. 

Vaikka tämä on periaatteessa hyvä idea, yleisessä tapauksissa (järkevän kokoisilla verkoilla) 
kaikkien permutaatioiden testaaminen ei ole käytännöllistä. Sen sijaan kannattaa testata vain osaa permutaatioista. 

Testi "kaikilla kaarien järjestyksillä tulee sama tulos" voidaan nähdä ns [invariantti testinä](/invarianttest). Tälläisille testeille 
löytyy valmiita kirjastoja jotka mahdollistavat verkkojen sattumanvaraisen generoinnin melko helposti, jonka avulla taas pystymme löytämään 
entistä monimutkaisempia bugeja. Lisää näistä kirjastoista löytyy esim. [invarianttitestauksesta kertovasta materiaalista](/invarianttest)

