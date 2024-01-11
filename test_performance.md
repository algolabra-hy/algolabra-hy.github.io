---
layout: page
permalink: /performancetest
title: Suorituskykytestaus
title_long: Suorituskykytest
inheader: no
---
_Nämä ohjeet on kirjoittanut Jeremias Berg_


Käydään tässä läpi, miten ns suorituskykytesteillä voidaan testata asioita, joihin voi olla vaikea päästä kiinni yksikkö tai invarianttitestien kautta. Vaikka esimerkki tässä on eri, seuraava olettaa tuntemusta [yksikkötestauksesta](/unittest) ja [invarianttitestuksesta](/invarianttest) sivuista.


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
    def test_quick_sort_jarjestaa_listan(self):
        lista = [1, 7, 4, 1, 10, 9, -2]
        jarjestetty = quicksort_vaarin_implementoitu(lista)
        self.assertEqual(jarjestetty, [-2,1,1,4,7,9,10])
    
    def test_quicksort_ei_muuta_jarjestettya_listaa(self):
        lista = [-2, 1, 1, 4, 7, 9, 10]
        jarjestetty = quicksort_vaarin_implementoitu(lista)
        self.assertEqual(jarjestetty, lista)
    
    def test_quicksort_jarjestaa_kaannety_listan(self):
        lista = [10, 9,7, 4, 1, 1, -2]
        jarjestetty = quicksort_vaarin_implementoitu(lista)
        self.assertEqual(jarjestetty, [-2,1,1,4,7,9,10])
    
    
    @given(taulukko=st.lists(st.integers()))
    @settings(max_examples=15000)
    def test_quicksort_jarjestaa_listan_hypothesis(self, taulukko):
        kirjasto_jarjestys = sorted(taulukko)
        oma_jarjestys = quicksort_vaarin_implementoitu(taulukko)
        self.assertEqual(oma_jarjestys, kirjasto_jarjestys)

```
Tässä siis ensin testataan muutamaa yksittäistä tapausta ja sen jälkeen tehdään vielä invarianttitesti joka testaa, että oman algoritmimme palauttaa listan numerot samassa järjestyksessa kuin pythonin oma järjestysalgorimi. 

Kokeillaan testejä (jos projektin alustaminen tuntuu epäselvältä, katso esimerkki [yksikkötestauksen luvusta](/unittest)): 
```
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % coverage run --branch -m pytest src; coverage html
=========================================== test session starts ============================================
platform darwin -- Python 3.9.6, pytest-7.4.4, pluggy-1.3.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/sorttaus
plugins: hypothesis-6.92.6
collected 4 items                                                                                          

src/tests/sort_test.py ....                                                                          [100%]

============================================ 4 passed in 0.26s =============================================
Wrote HTML report to htmlcov/index.html
```
Ja tarkastetaan kattavuus
![]({{ "/images/performancetest-0.png" | absolute_url }})

Eli toisin sanoen, voimme testiemme perusteella todeta, että 15000 eri listalla oma implementaatiomme quicksortista palauttaa saman järjestyksen kuin pythonin oma kirjastojärjestys. Tämän lisäksi testien kattavuus on 100%. Nyt olisi houkuttelevaa todeta, että olemme implementoineet quicksortin oikein. 

## Suorituskykytestaus
Kuten osa jo varmaan on huomannut, tämä implementaatio quicksortista on (keinotekoisesti) muokattu olemaan erittäin huono. Koska pivotiksi valitaan aina listan pienin alkio, jokaisessa rekursiivisessa kutsussa osalista vasen on tyhjä, jolloin tämä algoritmin ajoaika on aina neliöllinen listan pituuden suhteen. Tarkastellaan seuraavaksi muutamaa tapaa, millä tämän bugin voisi huomata automatisoiduilla testeillä. 

**Huom** Seuraavassa on tärkeää huomata, että suorituskykytestien suunnitellu on huomattavan paljon haasteellisempaa, kuin [yksikkötestien](/unittest) ja [invarianttitestien](/invarianttest). Tämä johtuu yksinkertaisesti siitä, että koodin ajanotto ei ole determinististä. Saman metodin ajaminen moneen kertaan samalla syötteellä voi kestää eri määrän aikaa, riippuen esim processorin muusta käytöstä. Tämä tarkoittaa, että suorituskykytestien kirjoituksessa täytyy olla tarkkana sen kanssa, että testit todellakin testaavat sitä, mitä on tarkoitus. 

### Vertailu toiseen algoritmiin 

Tira kurssilta tiedetään, että insertionsort algoritmin aikavaativuus on (useimmilla taulukoilla)huonompi kuin quicksortin. Voisimme siis testata oman quicksortimme oikeellisuutta vertaamalla sen ajoaikaa bubblesorttiin. 

Implementoidaan ensin bubblesort sort.py luokkaan (käyttäen [geeksforgeeksin](https://www.geeksforgeeks.org/python-program-for-bubble-sort/) ohjeita inspiraationa)

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
    @given(taulukko=st.lists(st.integers()))
    @settings(max_examples=100)
    def test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis(self, taulukko):
        kopio = taulukko.copy()
        bubblesort_aika = timeit.timeit(lambda: bubblesort(kopio), number=1)
        quicksort_aika = timeit.timeit(lambda: quicksort_vaarin_implementoitu(taulukko), number=1)
        self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
```
Tässä ensin luodaan kokeiltavasta taulukosta kopio, ja sen jälkeen kutsutaan timeit metodia joka mittaa, kauanko molempien järjestysalgoritmien ajamiseen menee. Timeit metodi haluaa ensimmäiseksi parametrikseen kutsuttavan metodin, joten teemme ns. nimettömän lambda funktion joka kutsuu järjestysalgoritmia. Timeit funktion parametri ```number``` määrittelee kuinka monta kertaa funktiota kutsutaan ajan mittauksen aikana. Tässä siis kutsutaan kumpaakin järjestysalgoritmia kerran.  

Kokeillaan: 
``` 
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % pytest src
.
.
.
src/tests/sort_test.py:40: in test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis
    self.assertGreaterEqual(insertionSort_aika, quicksort_aika)
E   AssertionError: 1.1669999999686098e-06 not greater than or equal to 2.458000000038485e-06
E   Falsifying example: test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis(
E       self=<tests.sort_test.TestSort testMethod=test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis>,
E       taulukko=[0, 0],
E   )
E   Explanation:
E       These lines were always and only run by failing examples:
E           /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/unittest/case.py:1234
========================================================================================================== short test summary info ==========================================================================================================
FAILED src/tests/sort_test.py::TestSort::test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis - AssertionError: 1.1669999999686098e-06 not greater than or equal to 2.458000000038485e-06
======================================================================================================== 1 failed, 4 passed in 0.29s ========================================================================================================

```
Tässä siis hypothesis on todennut, että kun kokeillaan listalla [0,0] niin bubblesortilla meni 0.000001699... sekunttia järjestämiseen kun taas quicksortilla 0.0000024....

Tämän testin luotettavuutta kuitenkin heikentää se, että **ajanmittaus on epädeterminististä**. Timeit metodin ilmoittavat ajoajat ovat niin pieniä, että tulokset voivat hyvinkin riippua kohinasta.

Kokeillaan mitä tapahtuu, kun käsketään timeittia mittamaan useamman kuin yhden kerran. Muutetaan äskeisessä testissä timeit metodin numbers parametri olemaan 10.
```
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % pytest src
.
.
.
src/tests/sort_test.py:40: in test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis
    self.assertGreaterEqual(bubblesort_aika, quicksort_aika)
E   AssertionError: 4.8329999999818796e-06 not greater than or equal to 1.0084000000021298e-05
E   Falsifying example: test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis(
E       self=<tests.sort_test.TestSort testMethod=test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis>,
E       taulukko=[0, 0],
E   )
E   Explanation:
E       These lines were always and only run by failing examples:
E           /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/unittest/case.py:1234
E           /Users/jezberg/Documents/teaching/tiralabra/sorttaus/src/sort.py:12
E           /Users/jezberg/Documents/teaching/tiralabra/sorttaus/src/sort.py:41
========================================================================================================== short test summary info ==========================================================================================================
FAILED src/tests/sort_test.py::TestSort::test_quicksort_on_nopeampi_kuin_bubblesort_hypothesis - AssertionError: 4.8329999999818796e-06 not greater than or equal to 1.0084000000021298e-05
======================================================================================================== 1 failed, 4 passed in 0.47s ========================================================================================================
```
Edelleen testi ei mene läpi. Tässä testissä kuitenkin edelleen vastaesimerkkinä erittäin lyhyt lista. Täten ei ehkä kannata 
vielä uskoa, että koodisamme olisi jotain vialla. 
 

### Tarkempi testi
Vaihdetaan taktiikkaa ja testataan invarianttia: "suurimalla osalla listoista jotka ovat epäjärjestyksessä quicksort on insertionsorttia nopeampi". Nyt pitäisi kuitenkin päättää, miten mitataan taulukon epäjärjestystä. Aloitetaan testillä joka järjestää 
suuren määrän taulukoita ja testaa invarianttia: "suurimmalla osalla taulukoista quicksort on bubblesorttia nopeampi"
```python    
    taulukoita = st.lists(st.integers())     
    @given(taulukko_lista=st.lists( taulukoita, max_size=100 ) )
    def test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort(self, taulukko_lista):
        quicksort_win = 0
        bubblesort_win = 0
        for taulukko in taulukko_lista:
            kopio = taulukko.copy()
            bubblesort_aika = timeit.timeit(lambda: bubblesort(kopio), number=1)
            quicksort_aika = timeit.timeit(lambda: quicksort_vaarin_implementoitu(taulukko), number=1)
            if bubblesort_aika > quicksort_aika:
                quicksort_win += 1
            else:
                bubblesort_win += 1 
        self.assertGreaterEqual(quicksort_win -bubblesort_win, (len(taulukko_lista) / 2))
```
Tässä siis testi saa syötteenä listan monta eri taulukkoa. 
Jokainen listan taulukko järjestetään sekä bubblesortilla ja quicksortilla joidenka ajoaika mitataan. Lopuksi testataan, että quicksort on insertion sorttia nopeampi vähintään puolella listan taulukoista. Huomaa hypothesis strategioiden (aikaisempiin verrattuna) hieman monimutkaisempi käyttö. Ensin käytetään lists strategiaa muodostamaan lista numeroita ja tallennetaan strategia ´´´taulukoita´´´ muuttujaan. Tämän jälkeen lists strategiaa käytetään uudestamaan muodostamaan lista näistä listoista (@given statementissa). 

Kokeillaan:
```
FAILED src/tests/sort_test.py::TestSort::test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort - 
hypothesis.errors.Flaky: Hypothesis 
test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort(self=<tests.sort_test.TestSort 
testMethod=test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort>, 
taulukko_lista=[[], [], []]) produces unreliable results...
```
Hmm, ei vieläkään mitä haluttiin. Hypothesis ilmoittaa että testin tulokset heittävät. Kun hypothesis löytää esimerkin jolla testi ei mene läpi, se yrittää pienentää syötettä siten, että virhe pysyy. Tämä virheilmoitus sanoo, että kutsuttaessa testiä moneen kertaan tulokset vaihtelevat. Tämä johtuu siitä, että ajanmittaus on epädeterminististä. 

Pyritään korjaamaan tämä samalla lailla kuin aikaisemmin, lisätään timeitmetodin number parametri olemaan 10. 
```python
    taulukoita = st.lists(st.integers()) 
    @given(taulukko_lista=st.lists( taulukoita, max_size=100 ) )
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
ja kokeillaan:
```
E   AssertionError: -1 not greater than or equal to 0.5
E   Falsifying example: test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort(
E       self=<tests.sort_test.TestSort testMethod=test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort>,
E       taulukko_lista=[[0, 0]],
E   )
E   Explanation:
E       These lines were always and only run by failing examples:
E           /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/unittest/case.py:1234
E           /Users/jezberg/Documents/teaching/tiralabra/sorttaus/src/sort.py:12
E           /Users/jezberg/Documents/teaching/tiralabra/sorttaus/src/sort.py:41
E           /Users/jezberg/Documents/teaching/tiralabra/sorttaus/src/tests/sort_test.py:62
========================================================================================================== short test summary info ==========================================================================================================
FAILED src/tests/sort_test.py::TestSort::test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort - AssertionError: -1 not greater than or equal to 0.5
======================================================================================================== 1 failed, 4 passed in 0.64s ========================================================================================================
```
Testit ovat taas deteministisiä, mutta nyt epäonnistuu listalla jossa on täsmälleen yksi taulukko, jossa pelkkiä nollia. 
Nämä eivät mittaa järjestysalgoritmien tehokkuutta edustavasti.

Nyt pitäisi siis päättää, minkälaisilla listoilla oikeasti halutaan testata. Ideaalitilanteessa haluttaisiin siis testata suurella määrällä isoja listoja jotka kaikki ovat jollai ntavalla "epäjärjestyksessä". Teoriassa hypotheis taipuisi myös tälläisten listojen tuottamiseen, mutta käytännössä kannattaa myös miettiä, kuinka paljon aikaa testien tekemiseen halutaan käyttää. Kokeillaan siis hieman helpompaa ehtoa ja tehdään taulukoita joissa kaikissa om vähintään 50 lukua ja jotka kaikki ovat uniikkeja. TÄmä onnistuu erittäin pienillä muutoksilla aikaisempaan. Meidän tarvitsee vai nmuuttaa ```taulukoita``` muuttuja määritelmää.
```python
taulukoita = st.lists(st.integers(), min_size=50, unique=True) 
```
lisättiin siis van parametri min_size joka vaatii, että listassa on vähintään 50 lukua, ja parametri unique joka vaatii että listan kaikki alkiot ovat eri (unique parametrin toimiminen vaatii, että listan alkiot ovat [hashable](https://docs.python.org/2/glossary.html), onneksemme integereille tämä pätee). 

Kokeillaan taas:
```
E   AssertionError: -1 not greater than or equal to 0.5
E   Falsifying example: test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort(
E       self=<tests.sort_test.TestSort testMethod=test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort>,
E       taulukko_lista=[[2,
E         -11,
E         -20,
E         25,
E         -17,
E         -24,
E         24,
E         -23,
E         0,
E         23,
E         -22,
E         17,
E         22,
E         -16,
E         16,
E         -1,
E         3,
E         -21,
E         -15,
E         21,
E         15,
E         20,
E         -19,
E         -14,
E         14,
E         -13,
E         19,
E         -18,
E         13,
E         -12,
E         18,
E         12,
E         11,
E         -10,
E         10,
E         -9,
E         9,
E         -8,
E         8,
E         -7,
E         7,
E         -6,
E         6,
E         -5,
E         5,
E         -4,
E         4,
E         -3,
E         -2,
E         1]],
E   )
E   Explanation:
E       These lines were always and only run by failing examples:
E           /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/unittest/case.py:1234
E           /Users/jezberg/Documents/teaching/tiralabra/sorttaus/src/tests/sort_test.py:62
========================================================================================================== short test summary info ==========================================================================================================
FAILED src/tests/sort_test.py::TestSort::test_quicksort_on_useimmiten_nopeampi_kuin_bubblesort - AssertionError: -1 not greater than or equal to 0.5
================================================================================================== 1 failed, 4 passed in 89.89s (0:01:29) =================================================================================================
```
Näyttää paremmalta, testi ei mene läpi ja tällä kerralla hypothesis löytää esimerkin jolla olettaisimme, että quicksort on insertion sorttia nopeampi. Nyt pitäisi herätä huoli siitä, että koodissamme on tosiaan jotain väärin. 

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
taulukoita = st.lists(st.integers(), min_size=50, unique=True)     
    @given(taulukko_lista=st.lists( taulukoita, max_size=100 ) )
    def test_quicksort_oikein_on_useimmiten_nopeampi_kuin_bubblesort(self, taulukko_lista):
        quicksort_win = 0
        bubblesort_win = 0
        for taulukko in taulukko_lista:
            kopio = taulukko.copy()
            bubblesort_aika = timeit.timeit(lambda: bubblesort(kopio), number=10)
            quicksort_aika = timeit.timeit(lambda: quicksort_oikein_implementoitu(taulukko), number=10)
            if bubblesort_aika > quicksort_aika:
                quicksort_win += 1
            else:
                bubblesort_win += 1 
        self.assertGreaterEqual(quicksort_win -bubblesort_win, (len(taulukko_lista) / 2))
```
Ja kokeillaan: 
```
(sorttaus-py3.9) jezberg@LM2-500-27156 sorttaus % pytest src
=========================================================================================================== test session starts ===========================================================================================================
platform darwin -- Python 3.9.6, pytest-7.4.4, pluggy-1.3.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/sorttaus
plugins: hypothesis-6.92.6
collected 5 items                                                                                                                                                                                                                         

src/tests/sort_test.py .....                                                                                                                                                                                                        [100%]

============================================================================================================ 5 passed in 2.88s ============================================================================================================
```
Eli tuntuisi toimivan. Olipas kuitenkin haastavaa.... 


## Toinen tapa testata
Huomattiin siis, että ajoaikaa mittaavilla testeillä voidaan periaatteessa saada kiinni hienovaraisempia bugeija kuin invariantti ja yksikkötestauksella. Tämä vaatii kuitenkin tarkkuutta ja testien muuttamista hieman epädeterministisiksi. Tässä on omat haasteensa. 

Toinen (ja usein parempi) tapa on miettiä, voiko toivottuja asioita testata deterministisesti ilman ajoajan mittaamista. Järjestysalgoritmien tapauksessa voidaan miettiä, voisiko olla joku toinen (detemrinistinen) parametri joka erottaa bubblesortin ja quicksortin. Tälläinnen löytyy esim miettimällä _miksi_ quicksortin aikavaatimus on yleensä n log n kun bubblesortin on neliöllinen. Kuten tira kurssilta muistetaan, tämä johtuu siitä, että quicksortin ei yleensä tarvitse verrata kaikkia listan alkioita pareittan toisiinsa, sen sijaan jokaisella kierroksella verrataan kaikkia osalistan alkioita pivottiin. Muutetaan siis seuraavaksi 
sekä bubblesorttiamme ja quick sorttiamme niin, että ne palauttavat myös tehtyjen vertailujen määrän. Tämä arvo on deterministinen listoille, mutta tässäkin pitää olla tarkkana. Mille tahansa pivotin valintasäännölle on olemassa listoja joilla sekä quicksort, että bubblesort tekee neliöllisen määrän vertailuja. 

Jätetään tälläiset testit kotitehtäväksi. 

## Yhteeenveto 
Verrattuna muihin testityyppeihin, suorituskykytestien suunnittelussa pitää olla tietoinen siitä, että ajannittaus on epädeterminististä. Näimpä testit kannattaa suunnitella niin, että ne sallivat pienen heiton. Huomasimme myös, että hypothesiksen laajemmassa käytössä pitää alkaa olla tarkkana sen kanssa, minkälaista syötettä testataan ja mittaako se todella niitä asioita mitä halutaan. Oikein käytettynä tällä lailla voidaan kuitenkin saada kiinni bugeija joita muilla tekniikoilla ei saa. 

Tärkeä huomio on, että myös monimutkaisemmissa testeissä kannattaa keskittyä yhden asian testaamiseen.
Näimme, että järkevissä suorituskykytesteissä tarvitaan vähän isompia listoja joissa on "enemmän tekemistä" järjestysalgoritmien 
kannalta. Rajatapusten, kuten jo järjestetyjen ja tyhjien listojen testaus on kuitenkin oleellista, aikaisemmissa esimerkeissä tät hoitaa testimme ```test_quicksort_jarjestaa_listan_hypothesis``` jolloin tehokkuustestaukseen ei tarvita ihan kaikkia listoja. 


Vaikka quicksort ja listan järjestys algoritmit muutenkin ovat harjoitustyötä varten liian helppoja, samoja ideoita voi hyvin soveltaa myös harjoitustyöhön sopivissa aiheissa. Helppo esimerkikki on esimerkiksi reitinhaku algoritmit. Monet reitinhakualgoritmit voivat olla väärin implementoituja, mutta silti palauttaa lyhyimmän reitin. Mieti miten polunetsintäsi pitäis toimia, ja suunnitele testit testaamaan iniitä heuristiikkoja. Polunetsinnässäkään ei tarvitse luottaa ajoaikaan, sen sijaan voit laskea esimerkiksi vierailtujen solmujen määrän.


{% include typo_instructions.md %}
