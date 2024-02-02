---
layout: page
permalink: /performancetest
title: Suorituskykytestaus
title_long: Suorituskykytest
inheader: no
---
_Nämä ohjeet on kirjoittanut Jeremias Berg_

{% include no_requirement.md %}

Käydään tässä läpi, miten ns suorituskykytesteillä voidaan testata asioita, joihin voi olla vaikea päästä kiinni yksikkö tai invarianttitestien kautta. Vaikka esimerkki tässä on eri, seuraava olettaa tuntemusta [yksikkötestauksesta](/unittest) ja [invarianttitestuksesta](/invarianttest), varsinkin [Poetryn](/poetry) käytöstä.


## Quicksortin testaus
Tarkastellaan seuraava quicksort algoritmin implementointia ja sen testejä. 

```python
def valitse_pivot(taulukko):
    arvo = min(taulukko)
    indeksi = taulukko.index(arvo)
    if indeksi != 0:
        taulukko[0], taulukko[indeksi] = taulukko[indeksi], taulukko[0]
    return taulukko[0]

def quicksort_vaarin_implementoitu(taulukko):
    if len(taulukko) <= 1:
        return taulukko
    else:
        pivot = valitse_pivot(taulukko)
        vasen = [x for x in taulukko[1:] if x < pivot]
        oikea = [x for x in taulukko[1:] if x >= pivot]
        return quicksort_vaarin_implementoitu(vasen) + [pivot] + quicksort_vaarin_implementoitu(oikea)
```
Tässä siis melko simppeli quicksortin implementaatio, inspiraationa on käytetty [tätä](https://www.geeksforgeeks.org/python-program-for-quicksort/) Geeksfor Geeksin ohjetta. Varmista, että ymmärrät miten algoritmi toimii. 
Voit jo nyt miettiä, mikä bugi tässä implementaatiossa on. 

Oletetaan, että kunnollisina koodareina olemme tehneet seuraavat testit:
```python
import unittest
import hypothesis.strategies as st
from hypothesis import given , settings , example
from sort import quicksort

class TestSort(unittest.TestCase):  
    @given(taulukko=st.lists(st.integers()))
    @example([10, 9,7, 4, 1, 1, -2], [-2, 1, 1, 4, 7, 9, 10], []) 
    @settings(max_examples=15000)
    def test_quicksort_jarjestaa_listan_hypothesis(self, taulukko):
        kirjasto_jarjestys = sorted(taulukko)
        oma_jarjestys = quicksort_vaarin_implementoitu(taulukko)
        self.assertEqual(oma_jarjestys, kirjasto_jarjestys)

```
Tässä siis yksi testi joka testaa invarianttia <span style="color:blue">"oma quicksort implementaatiomme laittaa listan saman järjestykseen kuin pythonin kirjaston järjestysalgoritmi"</span>. Tähän testiin on @example komennolla lisätty muutama reunatapaus kuten tyhjä lista, käännetty lista, sekä jo jrjestyksessä oleva lista. 

Kokeillaan testejä (jos projektin alustaminen tuntuu epäselvältä, katso esimerkki [yksikkötestauksen luvusta](/unittest)): 
```
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % coverage run --branch -m pytest src; coverage html
=========================================== test session starts ============================================
platform darwin -- Python 3.9.6, pytest-7.4.4, pluggy-1.3.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/sorttaus
plugins: hypothesis-6.92.6
collected 1 items                                                                                          

src/tests/sort_test.py ....                                                                          [100%]

============================================ 1 passed in 0.26s =============================================
Wrote HTML report to htmlcov/index.html
```
Ja tarkastetaan kattavuus
![]({{ "/images/performancetest-0.png" | absolute_url }})

Eli toisin sanoen, voimme testiemme perusteella todeta, että 15000 eri listalla oma implementaatiomme quicksortista palauttaa saman järjestyksen kuin pythonin oma kirjastojärjestys. Tämän lisäksi testien kattavuus on 100%. Nyt olisi houkuttelevaa todeta, että olemme implementoineet quicksortin oikein. 

## Suorituskykytestaus
Kuten osa jo varmaan on huomannut, tämä implementaatio quicksortista on (keinotekoisesti) muokattu olemaan erittäin huono. Koska pivotiksi valitaan aina listan pienin alkio, jokaisessa rekursiivisessa kutsussa osalista vasen on tyhjä, jolloin tämä algoritmin ajoaika on aina neliöllinen listan pituuden suhteen. Tarkastellaan seuraavaksi muutamaa tapaa, millä tämän bugin voisi huomata automatisoiduilla testeillä. 

**Huom** Seuraavassa on tärkeää huomata, että suorituskykytestien suunnitellu on huomattavan paljon haasteellisempaa, kuin [yksikkötestien](/unittest) ja [invarianttitestien](/invarianttest). Tämä johtuu siitä, että koodin ajanotto ei ole determinististä. Saman metodin ajaminen moneen kertaan samalla syötteellä voi kestää eri määrän aikaa, riippuen esim processorin muusta käytöstä. Tämä tarkoittaa, että suorituskykytestien kirjoituksessa täytyy olla tarkkana sen kanssa, että testit todellakin testaavat sitä, mitä on tarkoitus. 

### Vertailu toiseen (huonompaan) algoritmiin 

Tira kurssilta tiedetään, että bubblesort algoritmin aikavaativuus on (useimmilla taulukoilla) huonompi kuin quicksortin. Voisimme siis testata oman quicksortimme oikeellisuutta vertaamalla sen ajoaikaa bubblesorttiin. 

Implementoidaan ensin bubblesort sort.py luokkaan (käyttäen [Geeks for Geeksin](https://www.geeksforgeeks.org/python-program-for-bubble-sort/) ohjeita inspiraationa)

```python 
def bubblesort(taulukko):
    n = len(taulukko)
    for i in range(n-1):
        for j in range(0, n-i-1):
            if taulukko[j] > taulukko[j + 1]:
                taulukko[j], taulukko[j + 1] = taulukko[j + 1], taulukko[j]
```

Jos quicksorttimme on oikein implementoitu, olettaisimme sen olevan nopeampi kuin bubblesort useimilla taulukoille. Pyritään seuraavaksi luomaan testi joka mittaa tätä. 
Apuna metodien ajanottoon käytetään ```timeit``` kirjastoa. Ensimmäinen yritys testistä on seuraavanlainen:
```python
taulukot_aikatesti = st.lists(st.integers())
@given(taulukko=taulukot_aikatesti)
@settings(max_examples=100)
def test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis(self, taulukko):
    kopio = taulukko.copy()
    bubblesort_aika = timeit.timeit(lambda: bubblesort(kopio), number=1)
    quicksort_aika = timeit.timeit(lambda: quicksort_vaarin_implementoitu(taulukko), number=10)
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
```
Tässä ensin luodaan kokeiltavasta taulukosta kopio, ja sen jälkeen kutsutaan timeit metodia joka mittaa, kauanko molempien järjestysalgoritmien ajamiseen menee. Timeit metodi haluaa ensimmäiseksi parametrikseen kutsuttavan metodin, joten teemme ns. nimettömän lambda funktion joka kutsuu järjestysalgoritmia. Timeit funktion parametri ```number``` määrittelee kuinka monta kertaa funktiota kutsutaan ajan mittauksen aikana. Tässä siis kutsutaan kumpaakin järjestysalgoritmia kerran.  

Kokeillaan: 
``` 
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % pytest src 
......(rivejä puuttuu)......
=================================== FAILURES ===================================
_____ TestSort.test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis _____

self = <tests.sort_test.TestSort testMethod=test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis>

    @given(taulukko=taulukot_aikatesti)
>   @settings(max_examples=100)

src/tests/sort_test.py:36: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
src/tests/sort_test.py:41: in test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
E   AssertionError: 1.208000000030296e-06 not greater than or equal to 2.458999999954692e-06
E   Falsifying example: test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis(
E       self=<tests.sort_test.TestSort testMethod=test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis>,
E       taulukko=[0, 0],
E   )
E   Explanation:
E       These lines were always and only run by failing examples:
E           /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/
lib/python3.9/unittest/case.py:1234
=========================== short test summary info ============================
FAILED src/tests/sort_test.py::TestSort::test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis - 
AssertionError: 1.208000000030296e-06 not greater than or equal to 2.458999...
========================= 1 failed, 4 passed in 0.20s ==========================

```
Tässä siis hypothesis on todennut, että kun kokeillaan listalla [0,0] niin bubblesortilla meni 0.0000012... sekunttia järjestämiseen kun taas quicksortilla 0.0000024....

Tämän testin luotettavuutta kuitenkin heikentää se, että **ajanmittaus on epädeterminististä**. Timeit metodin ilmoittavat ajoajat ovat niin pieniä, että tulokset voivat hyvinkin riippua kohinasta.

Kokeillaan mitä tapahtuu, kun käsketään timeittia mittamaan useamman kuin yhden kerran. Muutetaan äskeisessä testissä timeit metodin numbers parametri olemaan 10.
```
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % pytest src 
....(rivejä puuttuu)....
========================================================= FAILURES ==========================================================
___________________________ TestSort.test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis ____________________________

self = <tests.sort_test.TestSort testMethod=test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis>

    @given(taulukko=taulukot_aikatesti)
>   @settings(max_examples=100)

src/tests/sort_test.py:36: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
src/tests/sort_test.py:41: in test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
E   AssertionError: 4.7080000000199185e-06 not greater than or equal to 1.0874999999965773e-05
E   Falsifying example: test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis(
E       self=<tests.sort_test.TestSort testMethod=test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis>,
E       taulukko=[0, 0],
E   )
E   Explanation:
E       These lines were always and only run by failing examples:
E           /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/
unittest/case.py:1234
E           /Users/jezberg/Documents/teaching/tiralabra/sorttaus/src/sort.py:12
E           /Users/jezberg/Documents/teaching/tiralabra/sorttaus/src/sort.py:41
================================================== short test summary info ==================================================
FAILED src/tests/sort_test.py::TestSort::test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis - AssertionError:
 4.7080000000199185e-06 not greater than or equal to 1.0874999999965773e-05
================================================ 1 failed, 4 passed in 0.21s ================================================
```
Edelleenkään testi ei mene läpi. Nyt timeit kirjasto on ajanut molemmat metodit 10 kertaa, jonka (ainakin periaatteessa) pitäisi 
vähentää kohinaa. Kuitenkin, tässä testissä kuitenkin edelleen vastaesimerkkinä erittäin lyhyt lista. Täten ei ehkä kannata 
vielä uskoa, että koodissamme olisi jotain vialla. 

### Edustava testisyöte
Edellinen testi osoittaa edustavien testisyötteiden tärkeyden. Kun aikaisemmin halusimme testata invarianttia "quicksort järjestää listan oikein" on tärkeää, että käytetyt syötteet kattavat kaikki listojen reunatapaukset kuten: jo järjestetyt, monta samaa numeroa sisäätävät, tyhjät etc. listat. 

Nyt haluamme kuitenkin testata tehokkuutta. Aikaisemman testimme ongelma on, että invariantti <span style="color:blue">"quicksort on aina nopeampi kuin insertionsort"</span>  ei päde oikeissa implementaatioissa koska ajanmittaus on epädeterminististä. Vaihdetaan siis taktiikkaa ja testataan invarianttia <span style="color:blue">"quicksort on nopeampi kuin insertion sort listoilla joiden järjestäminen vaatii työtä"</span>. 

Seuraavaksi pitäisi miettä, mitä tarkoittaa että listan järjestäminen vaatii työtä. Tässä kannattaa miettiä, mikä on helppo approximaatio vaikeasti järjestettävälle listalle. Tarkemmin sanottuna, voisimme kirjoittaa oman hypothesis strategian, 
joka luo listoja, jossa on paljon alkioita väärin päin. Tämä vaatii kuitenkin työtä joka on pois harjoitustyön itsensä kehityksestä. 
Parempi tapa onkin miettiä, olisiko joku toinen syötteen generointi joka olisi "tarpeeksi vaikea".
Kokeillaan ensin luoda listoja joissa on vähintään 50 alkiota joista mitkään eivät ole samoja.
Tämä onnistuu erittäin pienellä muutoksella:
```python
taulukot_aikatesti = st.lists(st.integers())    
taulukot_aikatesti_isot = st.lists(st.integers(), min_size=50, unique=True)
@given(taulukko=taulukot_aikatesti_isot)
@settings(max_examples=100)
def test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis(self, taulukko):
    kopio = taulukko.copy()
    bubblesort_aika = timeit.timeit(lambda: bubblesort(kopio), number=10)
    quicksort_aika = timeit.timeit(lambda: quicksort_vaarin_implementoitu(taulukko), number=10)
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
```
Tässä siis lisätään kaksi parametria taulukoiden strategian generointiin. ```min_size```
parametri vaatii, että luotavassa taulukossa on vähintään 50 alkiota. ```unique``` parametri vaatii, että kaikki taulukoiden alkiot ovat uniikkeja. Toisin sanoen, että taulukossa ei ole kahta samaa numeroa. 

Kokeillaan:
```
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % pytest src 
.....(rivejä puuttuu)...
================================================================== FAILURES ===================================================================
____________________________________ TestSort.test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis _____________________________________

self = <tests.sort_test.TestSort testMethod=test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis>

    @given(taulukko=taulukot_aikatesti_isot)
>   @settings(max_examples=100)

src/tests/sort_test.py:36: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
src/tests/sort_test.py:41: in test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
E   AssertionError: 0.0005241249999983211 not greater than or equal to 0.0009875829999970165
E   Falsifying example: test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis(
E       self=<tests.sort_test.TestSort testMethod=test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis>,
E       taulukko=[12,
E        21,
E        -21,
E        23,
E        24,
E        -24,
E        25,
E        22,
E        -22,
E        -23,
E        -20,
E        0,
E        20,
E        -19,
E        1,
E        19,
E        -18,
E        18,
E        -17,
E        17,
E        -16,
E        16,
E        -15,
E        -6,
E        11,
E        15,
E        -14,
E        -1,
E        14,
E        -13,
E        13,
E        -12,
E        -11,
E        -10,
E        10,
E        -9,
E        9,
E        -8,
E        8,
E        -7,
E        7,
E        6,
E        -5,
E        5,
E        -4,
E        4,
E        -3,
E        3,
E        -2,
E        2],
E   )
E   Explanation:
E       These lines were always and only run by failing examples:
E           /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/unittest/case.py:1234
=========================================================== short test summary info ===========================================================
FAILED src/tests/sort_test.py::TestSort::test_quicksort_vaara_on_nopeampi_kuin_bubblesort_hypothesis - AssertionError: 0.0005241249999983211 not greater than or equal to 0.0009875829999970165
=================================================== 1 failed, 1 passed in 81.62s (0:01:21) ====================================================
```
Näyttää paremmalta, testi ei mene läpi ja tällä kerralla hypothesis löytää vastaesimerkin jolla olettaisimme, että quicksort on insertion sorttia nopeampi. Nyt pitäisi herätä huoli siitä, että koodissamme on tosiaan jotain väärin. 

## Korjataan quicksort
Testin perusteella alamme siis etsimään bugia. Onneksi keinotekoisesti lisätyt bugit on helppo korjata. Valitaan pivotti "sattumanvaraisesti" olemaan osataulukon ensimmäinen alkio. 
```python
def quicksort_oikein_implementoitu(taulukko):
    if len(taulukko) <= 1:
        return taulukko
    else:
        pivot = taulukko[0]
        vasen = [x for x in taulukko[1:] if x < pivot]
        oikea = [x for x in taulukko[1:] if x >= pivot]
        return quicksort_oikein_implementoitu(vasen) + [pivot] + quicksort_oikein_implementoitu(oikea)
```
ja sen testi
```python 
taulukot_aikatesti = st.lists(st.integers())
taulukot_aikatesti_isot = st.lists(st.integers(), min_size=50, unique=True)
@given(taulukko=taulukot_aikatesti_isot))
@settings(max_examples=100)
def test_quicksort_oikea_on_nopeampi_kuin_bubblesort_hypothesis(self, taulukko):
    kopio = taulukko.copy()
    bubblesort_aika = timeit.timeit(lambda: bubblesort(kopio), number=10)
    quicksort_aika = timeit.timeit(lambda: quicksort_oikein_implementoitu(taulukko), number=10)
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
```
Ja kokeillaan: 
```
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % pytest src 
============================================================= test session starts =============================================================
platform darwin -- Python 3.9.6, pytest-7.4.4, pluggy-1.3.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/sorttaus
plugins: hypothesis-6.92.6
collected 5 items                                                                                                                             

src/tests/sort_test.py .....                                                                                                            [100%]

============================================================== 2 passed in 1.65s ==============================================================
```
Eli tuntuisi toimivan. Olipas kuitenkin haastavaa.... 

### Sanity check
Tarkastetaan vielä, mitä käy jos yritämme testata oikein implementoitua quicksorttia lyhyillä listoilla. Toisin sanoen, lisätään ```@example``` komennolla aikaisemmin hylätty lista [0,0] testeihin. 
```python    
taulukot_aikatesti_isot = st.lists(st.integers(), min_size=50, unique=True)
@given(taulukko=taulukot_aikatesti_isot)
@example([0,0])
@settings(max_examples=100)
def test_quicksort_oikea_on_nopeampi_kuin_bubblesort_hypothesis(self, taulukko):
    kopio = taulukko.copy()
    bubblesort_aika = timeit.timeit(lambda: bubblesort(kopio), number=10)
    quicksort_aika = timeit.timeit(lambda: quicksort_oikein_implementoitu(taulukko), number=10)
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
```

Kokeillaan:
```
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % pytest src 
...(rivejä puuttuu)----
================================================================== FAILURES ===================================================================
____________________________________ TestSort.test_quicksort_oikea_on_nopeampi_kuin_bubblesort_hypothesis _____________________________________

self = <tests.sort_test.TestSort testMethod=test_quicksort_oikea_on_nopeampi_kuin_bubblesort_hypothesis>

    @given(taulukko=taulukot_aikatesti)
>   @example([0,0])

src/tests/sort_test.py:37: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
../../../../Library/Caches/pypoetry/virtualenvs/sorttaus-TVo7_s5m-py3.9/lib/python3.9/site-packages/hypothesis/core.py:1241: in _raise_to_user
    raise the_error_hypothesis_found
src/tests/sort_test.py:43: in test_quicksort_oikea_on_nopeampi_kuin_bubblesort_hypothesis
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
E   AssertionError: 5.332999999996257e-06 not greater than or equal to 8.459000000016204e-06
E   Falsifying explicit example: test_quicksort_oikea_on_nopeampi_kuin_bubblesort_hypothesis(
E       self=<tests.sort_test.TestSort testMethod=test_quicksort_oikea_on_nopeampi_kuin_bubblesort_hypothesis>,
E       taulukko=[0, 0],
E   )
=========================================================== short test summary info ===========================================================
FAILED src/tests/sort_test.py::TestSort::test_quicksort_oikea_on_nopeampi_kuin_bubblesort_hypothesis - AssertionError: 5.332999999996257e-06 not greater than or equal to 8.459000000016204e-06
========================================================= 1 failed, 1 passed in 0.14s =========================================================
```
Eli näin lyhyellä listalla myös oikein implementoitu quicksort on hitaampi kuin bubblesort, joka osoittaa syötteen miettimisen tärkeyden. 


## Lisähuomoita
Vaikka tässä esimerkissä riitti muuttaa yksittäisen taulukon generointia, hypothesis taipuu monimutkaisempiikin testeihin. Alla esimerkki testistä, joka järjestää korkeintaan 100 taulukkoa ja vaatii, että quicksort on bubblesorttia nopeampi vähintään puolella. 

```python
taulukko = st.lists(st.integers()) 
@given(taulukko_lista=st.lists( taulukko, max_size=100 ) )
def test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort(self, taulukko_lista):
    quicksort_win = 0
    bubblesort_win = 0
    for taulukko in taulukko_lista:
        kopio = taulukko.copy()
        bubblesort_aika = timeit.timeit(lambda: bubblesort(kopio), number=10)
        quicksort_aika = timeit.timeit(lambda: quicksort_vaarin_implementoitu(taulukko), number=10)
        if bubblesort_aika > quicksort_aika:
            quicksort_win += 1
        else:
            bubblesort_win += 1 
    self.assertGreaterEqual(quicksort_win -bubblesort_win, (len(taulukko_lista) / 2))
```
# Pitääkö mitata aikaa?
Tässä on toivottavasti huomattu, että ajoaikaa mittaavilla testeillä voidaan periaatteessa saada kiinni hienovaraisempia bugeija kuin invariantti ja yksikkötestauksella. Tämä vaatii kuitenkin tarkkuutta ja testien muuttamista hieman epädeterministisiksi. Tässä on omat haasteensa. 

Toinen (ja usein parempi) tapa on miettiä, voiko toivottuja asioita testata deterministisesti ilman ajoajan mittaamista. Järjestysalgoritmien tapauksessa voidaan miettiä, voisiko olla joku toinen (detemrinistinen) parametri joka erottaa bubblesortin ja quicksortin. Tälläinen löytyy esim miettimällä _miksi_ quicksortin aikavaatimus on yleensä n*log(n) kun bubblesortin on neliöllinen. Kuten tira kurssilta muistetaan, tämä johtuu siitä, että quicksortin ei yleensä tarvitse verrata kaikkia listan alkioita pareittan toisiinsa, sen sijaan jokaisella kierroksella verrataan kaikkia osalistan alkioita vain pivottiin. Parempi tapa testata metodiamme olisikin (ehkä) muuttaa quicksortin implementaatiota niin, että se palauttaa tehtyjen vertailujen määrän. 
Tämä arvo on deterministinen listoille, mutta senkin testaamisessa pitää olla tarkkana. Mille tahansa pivotin valintasäännölle on olemassa listoja joilla sekä quicksort, että bubblesort tekee neliöllisen määrän vertailuja.  

Jätetään tämän tutkiminen kotitehtäväksi. 

## Yhteeenveto 
Verrattuna muihin testityyppeihin, suorituskykytestien suunnittelussa pitää olla tietoinen siitä, että ajannittaus on epädeterminististä. Näimpä testit kannattaa suunnitella niin, että ne sallivat pienen heiton. Huomasimme myös, että hypothesiksen laajemmassa käytössä pitää alkaa olla tarkkana sen kanssa, minkälaista syötettä testataan ja mittaako se todella niitä asioita mitä halutaan. Oikein käytettynä tällä lailla voidaan kuitenkin saada kiinni bugeja joita muilla tekniikoilla ei saa. 

Tärkeä huomio on, että myös monimutkaisemmissa testeissä kannattaa keskittyä yhden asian testaamiseen.
Näimme, että järkevissä suorituskykytesteissä tarvitaan vähän isompia listoja joilla järjestysalgoritmeilla on "enemmän tekemistä". Rajatapusten, kuten jo järjestetyjen ja tyhjien listojen testaus on kuitenkin oleellista, aikaisemmissa esimerkeissä tämän hoitaa testimme ```test_quicksort_jarjestaa_listan_hypothesis```. Ei siis kannata testata sekä oikeellisuutta, että tehokkuutta samalla testillä.  

Vaikka quicksort, ja järjestys algoritmit muutenkin, ovat harjoitustyötä varten liian helppoja, samoja ideoita voi hyvin soveltaa myös harjoitustyöhön sopivissa aiheissa. Monet reitinhakualgoritmit voivat olla väärin implementoituja, mutta silti palauttaa lyhyimmän reitin. Mieti miten polunetsintäsi pitäis toimia, ja suunnitele testit testaamaan niitä heuristiikkoja. Polunetsinnässäkään ei tarvitse (välttämättä) luottaa ajoaikaan, sen sijaan voit laskea esimerkiksi vierailtujen solmujen määrän.


{% include typo_instructions.md %}
