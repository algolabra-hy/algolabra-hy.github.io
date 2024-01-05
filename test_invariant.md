---
layout: page
permalink: /invarianttest
title: Invarianttitestaus
title_long: Invariant
inheader: no
---
_Nämä ohjeet on kirjoittanut Jeremias Berg_

Jatketaan siitä mihin [yksikkötestauksessa](/unittest) jäätiin. Jos unittest sovelluskehys, poetry ja pytest ovat tuttuja, voit lukea
tämän suoraan. Muuten kannattaa tustua ensin [tähän](/unittest).

Muistutuksena, tämänhetkinen `Maksukortti` luokka:

```python
# aterioiden hinnat ovat senteissä
EDULLINEN = 250
MAUKAS = 400

class Maksukortti:
    def __init__(self, saldo):
        # saldo on senteissä
        self.saldo = saldo

    def syo_edullisesti(self):
        if self.saldo >= EDULLINEN:
            self.saldo -= EDULLINEN

    def syo_maukkaasti(self):
        if self.saldo >= MAUKAS:
            self.saldo -= MAUKAS

    def lataa_rahaa(self, maara):
        if maara < 0:
            return

        self.saldo += maara

        if self.saldo > 15000:
            self.saldo = 15000

    def saldo_euroina(self):
        return self.saldo / 100

    def __str__(self):
        saldo_euroissa = round(self.saldo / 100, 2)

        return "Kortilla on rahaa {:0.2f} euroa".format(saldo_euroissa)
```
ja sen testit:
```python
import unittest
from maksukortti import Maksukortti

class TestMaksukortti(unittest.TestCase):
    def setUp(self):
        self.kortti = Maksukortti(1000)

    def test_konstruktori_asettaa_saldon_oikein(self):
        self.assertEqual(str(self.kortti), "Kortilla on rahaa 10.00 euroa")


    def test_syo_edullisesti_vahentaa_saldoa_oikein(self):
        self.kortti.syo_edullisesti()

        self.assertEqual(self.kortti.saldo_euroina(), 7.5)

    def test_syo_maukkaasti_vahentaa_saldoa_oikein(self):
        self.kortti.syo_maukkaasti()

        self.assertEqual(self.kortti.saldo_euroina(), 6.0)

    def test_syo_edullisesti_ei_vie_saldoa_negatiiviseksi(self):
        kortti = Maksukortti(200)
        kortti.syo_edullisesti()

        self.assertEqual(kortti.saldo_euroina(), 2.0)

    def test_kortille_voi_ladata_rahaa(self):
        self.kortti.lataa_rahaa(2500)

        self.assertEqual(self.kortti.saldo_euroina(), 35.0)

    def test_kortin_saldo_ei_ylita_maksimiarvoa(self):
        self.kortti.lataa_rahaa(20000)

        self.assertEqual(self.kortti.saldo_euroina(), 150.0)
```
jolla päästään kattavuuteen: 

```
Name                 Stmts   Miss Branch BrPart  Cover   Missing
----------------------------------------------------------------
src/maksukortti.py      22      1      8      2    90%   15->exit, 20
----------------------------------------------------------------
TOTAL                   22      1      8      2    90%
```

## Monimutkainen maksukortti

Simuloidaan seuraavaksi (hieman keinotekoisesti) monimutkaisemman algoritmin testausta. 
Kuvitellaan, että syödessä maukkaasti halutaan tarkastaa jokin monimutkainen ehto, joka varmistaa,
että syöjällä on tähän oikeudet. Kuvitellaan myös, että tämän ehdon implementoinissa tapahtuu virhe
jonka seurauksena oikeasti kortit jolla on 1337 senttiä eivät voi syödä maukkaasti. 

Lisätään nämä metodit Maksukortti luokkaan:
```python
def monimutkainen_ehto(self):
    return self.saldo != 1337
    
def syo_maukkaasti(self):
    if self.saldo >= MAUKAS and self.monimutkainen_ehto():
        self.saldo -= MAUKAS
```
Kokeillaan testejä: 

```
(maksukortti-py3.9) jezberg@dhcp-85-175 maksukortti % coverage run --branch -m pytest src ;   coverage report -m 
====================================================================== test session starts ======================================================================
platform darwin -- Python 3.9.6, pytest-7.4.4, pluggy-1.3.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/maksukortti
collected 6 items                                                                                                                                               

src/tests/maksukortti_test.py ......                                                                                                                      [100%]

======================================================================= 6 passed in 0.01s =======================================================================
Name                 Stmts   Miss Branch BrPart  Cover   Missing
----------------------------------------------------------------
src/maksukortti.py      24      1      8      2    91%   18->exit, 23
----------------------------------------------------------------
TOTAL                   24      1      8      2    91%
(maksukortti-py3.9) jezberg@dhcp-85-175 maksukortti % 
```
Huomaamme, että testien kattavuus on itse asiassa lisääntynyt. Syy tähän on, että lisäehtomme tuli haaraan jota [aikaisemmassa osassa](/unittest) ei testattu. Toisin sanoen kattavuudesta voisimme (virheellisesti) päätellä, että testaamme luokan toiminnallisuutta kunnollisesti, vaikka nyt millään kortilla jolla on 13.37€ rahaa ei voi ostaa maukkaita aterioita. 

**Huom.** Tässä keinotekoisessa esimerkissä on toki helppo huomata, että metodia ```monimutkainen_ehto()``` ei testata ja lisätä yksikkötesti joka alustaa kortin juuri 1337 sentillä. 
Tässä kuitenkin simuloidaan tilannetta, jossa funktion 
```monimutkainen_ehto()```totuusarvoa on mahdotonta todeta staattisesti etukäteen. Tämän seurauksena 
emme pysty määrittelemään syöteitä yksikkötestille joka varmasti saisi sen palauttamaan sekä true, että false. 
Jos tämä esimerkki tuntuu liian keinotekoiselta voit kuvitella esim. ohjelman joka tekee jotain erilailla jos jonkun neuroverkon 
virhe on enemmän kuin 15% tai tekoälyn, joka toimii erilailla mikäli se toteaa voittomahdollisuuksiensa olevan yli 83%. 

## Yksittäisistä Syötteistä Invariantteihin.
Nähtiin siis tapaus, jossa koodi toimii halutulla tavalla _melkein_ kaikilla syötteillä. Voidaksemme kirjoittaa testin joka huomaa bugin, meidän täytyisi osata arvata syötteet jolla koodi ei toimi. Harjoitustyössä toteutettaville algoritmeille tämä voi olla parhaimillaankin erittäin haastavaa, yleensä mahdotonta. Yksittäisten syötteiden sijasta tälläisissä tapauksissa kannattaakin testata invariantteja joita metodien tulisi toteuttaa, ja luoda mahdolliset syötteet automaattisesti. Englanniksi tätä tekniikka kutsutaan usein nimellä invariant tai property testing, ja se liittyy myös läheisesti ns. fuzzaukseen. 

Invarianttitestauksessa ideana on, että:
1. Kuvaillaan kaikki mahdolliset syötteet mitä halutaan testata. 
1. Tehdään niille jotakin. 
1. Tarkastetaan tulos.

Vertaa tätä "normaaliin" yksikkötestaukseen, jossa: 
1. Valitaan _yksi_ syöte. 
1. Tehdään sille jotakin.
1. Tarkastetaan tulos.

Invariantteja testattaessa käytetään usein olemassa olevia kirjastoja, joille voidaan kuvata miten mahdollisia syötteitä luodaan, ja minkä testin jokaisen syötteen pitäisi läpäistä. Kirjasto luo sitten syötteitä sattumanvaraisesti ja ajaa niillä testejä läpi kunnes joko jokin raja saavutetaan, tai jokin syötteistä ei läpäise testiä. Jälkimmäisessä tapauksessa invariantti testaukseen tarkoitettu kirjasto usein myös pyrkii heuristisesti pienentämään syötettä joka ei läpäissyt testiä löytääkseen pienimmän mahdollisen jolla testi ei mene läpi. Tämän tarkoituksena on auttaa ihmiskoodaajaa ymmärtämään, miten korjata koodia.

Katsotaan seuraavaksi konkreettisesti invarianttitestien toteuttamista pythonin [hypothesis](https://hypothesis.readthedocs.io/en/latest/#) kirjaston avulla. 
Lisätään se ensin maksukortti projektiin kehityksen aikaisesksi riippuvuudeksi:
```
jezberg@dhcp-85-175 maksukortti % poetry add hypothesis --group dev 
```
Lisätään testi luokan (maksukortti_test) alkuun.
```python
import hypothesis.strategies as st
from hypothesis import given
```
ja kirjoitetaan testi
```python 
@given(arvo=st.integers(min_value=0, max_value=15000))
def test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis(self, arvo):
    kortti = Maksukortti(arvo)
    kortti.syo_maukkaasti()
    self.assertTrue(kortti.saldo_euroina() == ((arvo - 400) / 100) or arvo < 400)
```
Tässä @given kertoo, mitä parametrin "arvo" mahdollisia arvoja halutaan testata. Tässä tapauksessa käytetään hypothesis kirjaston omia valmiita [strategioita](https://hypothesis.readthedocs.io/en/latest/data.html) kokonaislukujen (ingetereiden) luomiseen. Tässä normaali strategiaan lisätään, että halutaan testata kaikkia arvoja 0an ja 15000 (kortin maksimiarvon) välillä. Ts. @given määrittelee, että seuraavassa testissä parametri "arvo" on jokin kokonaisluku välillä 0 ja 15000. 
Tätä seuraava testi oleellisesti testaa invarianttia "jos kortilla on arvoa yli 400 senttiä, niin tällöin metodin ```syo_maukkaasti``` kutsuminen vähentää arvoa 400:lla. 

Kokeillaan testejä (muista käynnistää virtuaaliympäristö):
```
(maksukortti-py3.9) jezberg@dhcp-85-175 maksukortti % pytest src                                                 
======================================================================================== test session starts =========================================================================================
platform darwin -- Python 3.9.6, pytest-7.4.4, pluggy-1.3.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/maksukortti
plugins: hypothesis-6.92.2
collected 7 items                                                                                                                                                                                    

src/tests/maksukortti_test.py .......                                                                                                                                                          [100%]

========================================================================================= 7 passed in 0.13s ==========================================================================================
(maksukortti-py3.9) jezberg@dhcp-85-175 maksukortti % 
               24      1      8      1    94%
```
Vaikuttaa siltä, että jokin olisi väärin. Pytest löytää uuden testin, mutta ne kaikki menevät läpi, vaikka tässsä (keinotekoisessa) tapauksessa tiedetäään, että kun arvo on 1337 testin pitäisi hylätä.
Tutkitaan vielä coveragen raporttia samalla lailla kun aiemmin:
```bash
coverage run --branch -m pytest src; coverage html
```
![]({{ "/images/invarianttest0.png" | absolute_url }})
Kun verrataan [aiempaan reporttiin](http://localhost:4000/unittest#visuaalisempi-testikattavuusraportti)
huomataan, että haarakattavuutemme on parempi. Eritysesti, nykyisen rivin 18 (aiemman rivin 15) haarasta testataan nyt molemmat tapaukset. 
Tämä johtuu siitä, että juuri kirjoittamamme testi kokeilee myös arvoja jotka ovat alle 4 euroa, kun aiemmat testit kutsuvat ```syo_maukkaasti``` metodia vain kun kortilla on 10 euroa. 

Haarakattavuuden mielessä nämä testit ovat siis parempia ja testaavat suurempaa osaa koodista. Tämän lisäki toivottu invariantti tuntuu pitävän. Vielä tämäkään ei kuitenkaan riitä. Ongelmana on, että testimme hylkää täsmälleen yhden yhteensä 150000 mahdollisesta arvosta ja normaaleilla asetuksilla hypotheis kirjasto ajaa jokaisen testin vain [100 kertaa](https://hypothesis.readthedocs.io/en/latest/settings.html#hypothesis.settings.max_examples) eri, sattumanvaraisesti valituilla, arvoilla. Jos ajaisimme testejä tarpeeksi monta kertaa, lopulta hypothesis voisi sattumalta valita arvon 1337 jolloin testit hylkäisivät. Meillä ei kuitenkaan ole mitään takuita siitä monta kertaa täytyy ajaa. Toisin sanoen invarianttitestit eivät vielä itsessään täysin takaa koodin toimivuutta. Moninmutkaisten algoritmien testaaminen vaatii siis edelleenkin hyvää ymmärrystä algoritmista ja sen toivotusta toiminnasta 

## Miten Parannetaan? 

Katsotaan vielä, miten tätä yhtä testiä voisi parantaa saamaan kiinni tunnetun bugin. Yleisesti tähän on kolme tapaa:
1. Testataan enemmän arvoja.
1. Lisätään yksittäisiä arvoja pakollisiksi testeiksi.  
1. Testataan arvoja jotka oletamme vaikeiksi

# Testataan Enemmän
Tämä on ehkä kaikkein luonnollisin ajatus parantaa testejä. Käsketään yksinkertaisesti hypothesisiä kokeilemaan enemmän arvoja. 
Tämä onnistuu lisäämällä importteihin "settings" käskyn ja lisäämällä sen testin eteen:
```python
import hypothesis.strategies as st
from hypothesis import given, settings
```
ja lisätään testiin
```python 
@given(arvo=st.integers(min_value=0, max_value=15000))
@settings(max_examples=15000)
def test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis(self, arvo):
    kortti = Maksukortti(arvo)
    kortti.syo_maukkaasti()
    self.assertTrue(kortti.saldo_euroina() == ((arvo - 400) / 100) or arvo < 400)
```
Tässä siis @settings käsky käskee ajamaan seuraavan testin vähintään 15000 eri arvolla ennen kuin testi määritellän hyväksytyksi. Tässä keinotekoisessa esimerkissä tästä seuraa, että itse asiassa kokeillaan kaikki mahdolliset arvot. 

Kokeillaan:
```
(maksukortti-py3.9) jezberg@dhcp-85-175 maksukortti % pytest src 
============================================== test session starts ==============================================
platform darwin -- Python 3.9.6, pytest-7.4.4, pluggy-1.3.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/maksukortti
plugins: hypothesis-6.92.2
collected 7 items                                                                                               

src/tests/maksukortti_test.py ......F                                                                     [100%]

=================================================== FAILURES ====================================================
_____________________ TestMaksukortti.test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis _____________________

self = <tests.maksukortti_test.TestMaksukortti testMethod=test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis>

    @given(arvo=st.integers(min_value=0, max_value=15000))
>   @settings(max_examples=15000)

src/tests/maksukortti_test.py:44: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
src/tests/maksukortti_test.py:48: in test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis
    self.assertTrue(kortti.saldo_euroina() == ((arvo - 400) / 100) or arvo < 400)
E   AssertionError: False is not true
E   Falsifying example: test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis(
E       self=<tests.maksukortti_test.TestMaksukortti testMethod=test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis>,
E       arvo=1337,
E   )
E   Explanation:
E       These lines were always and only run by failing examples:
E           /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/unittest/case.py:681
============================================ short test summary info ============================================
FAILED src/tests/maksukortti_test.py::TestMaksukortti::test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis - AssertionError: False is not true
========================================== 1 failed, 6 passed in 3.22s ==========================================
```
Nyt saatiin mitä haluttiin, hypotheis kertoo, että yksi testi epäonnistui, ja myös että se epäonnistui silloin kun muuttuja arvo on 1337, eli aivan kuten odotimmekin. 

# Lisätään Yksikkötestejä
Jos ajoit edellisen testin itse, huomasit että siihen meni (verattaessa aiempaan) melko paljon aikaa. Tämä johtuu yksinkertaisesti siitä, että viimeinen testi ajettiin yhteensä 15000 kertaa. Tämä oin useamman arvon testaamisen heikkous, vaikeita metodeja voi olla aivan liian hidasta testata näin perusteellisesti aina kun ajetaan testejä. Tilanne pahenee edelleen jos halutaan testata ei vakioaikaisia metodeja. 

Kuitenkin jos satuttaisiin jollain lailla tietämään, että arvo 1337 on hankala metodille (esim. ajamalla kerran perusteelliset testit), niin voimme pakottaa hypotheis kirjaston aina kokeilemaan ainakin sen arvon. Tämä onnistuu @example lisäyksellä:
```python
import hypothesis.strategies as st
from hypothesis import given, settings, example
```
ja muokataan testiin
```python 
@given(arvo=st.integers(min_value=0, max_value=15000))
@example(1337)
def test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis(self, arvo):
    kortti = Maksukortti(arvo)
    kortti.syo_maukkaasti()
    self.assertTrue(kortti.saldo_euroina() == ((arvo - 400) / 100) or arvo < 400)
```
Huomaa, että poistimme aikaisemmin lisätyn setting käskyn. Täten hypothesis kokeilee vain 100 eri arvoa, jonkas ei pitäisi kestää niin kauaa. Kuitenkin @example lisäyksen takia, yksi näistä arvoista on varmasti 1337.
Kokeillaan:
``` 
(maksukortti-py3.9) jezberg@dhcp-85-175 maksukortti % pytest src
============================================== test session starts ==============================================
platform darwin -- Python 3.9.6, pytest-7.4.4, pluggy-1.3.0
rootdir: /Users/jezberg/Documents/teaching/tiralabra/maksukortti
plugins: hypothesis-6.92.2
collected 7 items                                                                                               

src/tests/maksukortti_test.py ......F                                                                     [100%]

=================================================== FAILURES ====================================================
_____________________ TestMaksukortti.test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis _____________________

self = <tests.maksukortti_test.TestMaksukortti testMethod=test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis>

    @given(arvo=st.integers(min_value=0, max_value=15000))
>   @example(1337)

src/tests/maksukortti_test.py:44: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
../../../../Library/Caches/pypoetry/virtualenvs/maksukortti-15_6LZF8-py3.9/lib/python3.9/site-packages/hypothesis/core.py:1230: in _raise_to_user
    raise the_error_hypothesis_found
src/tests/maksukortti_test.py:48: in test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis
    self.assertTrue(kortti.saldo_euroina() == ((arvo - 400) / 100) or arvo < 400)
E   AssertionError: False is not true
E   Falsifying explicit example: test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis(
E       self=<tests.maksukortti_test.TestMaksukortti testMethod=test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis>,
E       arvo=1337,
E   )
============================================ short test summary info ============================================
FAILED src/tests/maksukortti_test.py::TestMaksukortti::test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis - AssertionError: False is not true
========================================== 1 failed, 6 passed in 0.13s ==========================================
```
Eli testi ei mene läpi, eikä kestäkään niin kauaa enää,.

*Huom* Yleisessä tapauksessa invariantti testejä ei siis kannata ajaa kaikille mahdollisille syötteille, tämä veisi aivan liian kauan. Sen sijaan niitä kannattaa ajaa _tarpeeksi monelle_ arvolle vähän harvemmin kuin perus yksikkkötestejä. Nämä, vähän hitaammat, testit voi sitten ajaa aina isompien muutosten jälkeen, ja tarpeen mukaan nostaa niistä löydettyjä hankalia syötteitä yksikkötesteihin jotka ajetaan useammin, esimerkiksi @example komennon kautta.

# Testataan Tarkemmin
Lopuksi voimme myös todeta, että jos sattuisimme tietäämään, että kortin arvot 1300-1400 ovat haassteellisia niin voimme toki käskeä hypothesista testaamaan vain niitä:
```python 
@given(arvo=st.integers(min_value=1300, max_value=1400))
def test_syo_maukkaasti_vahentaa_saldoa_oikein_hypothesis(self, arvo):
    kortti = Maksukortti(arvo)
    kortti.syo_maukkaasti()
    self.assertTrue(kortti.saldo_euroina() == ((arvo - 400) / 100) or arvo < 400)
```
joka failaa ilman parametrien säätöä. Tälläinen tapaus voisi sattua jos vaikka tietäisimme että ```monimutkainen_ehto``` metodimme Maksukortti luokassa tekee jotain (vaikka emme tietäisi mitä) vain jos arvo on tietyllä välillä. 

# Syötteiden generoinnista
Lopuksi mainittakoon vielä, että hypothesiksen syötteen generointi ulottuu huomattavasti kokonaislukuja pidemmälle. Hypothetiksen [valmiit strategiat](https://hypothesis.readthedocs.io/en/latest/data.html) määrittelevät kuinka perus tyyppejä voidaan luoda, mutta myös miten voit määritellä oman datatyyppisi luojan tai yhdistellä eri tyyppien generoijia toisinsa. Täten voit käytännössä käyttää hypothesista minkälaisten metodien testaamiseen tahansa. Palataakseni aikaisempiin esimerkkeihin, voisimme esim testata metodeja jotka otavat koko neuroverkon syötteeksi muista [riippuvuuden injektointi](/riippuvuuksien_injektointi_python) ja kertoa hypothesikselle, miten neuroverkkoja muodostetaan. Tällöin kirjasto voisi (teoriassa) testata sattumanvaraisesti muodostetuilla (ja treenatuilla) neuroverkoilla kunnes löytyy joku, jonka virhe on yli 15%, ilman että meidän täytyy itse osata määritellä, miten sellainen muodostetaan. 


## Yhteenveto 
Invarianttitestaus automatisoi joitain osia testauksesta ja helpottaa bugien löytämistä monimutkaisista algoritmeista. Teoriassa voimme vain kuvailla minkälaisia syötteitä haluamme testata, ja mitä näiden syötteiden täytyy toteuttaa. Kuitenkin, kuten tässä huomasimme, myös invarianttitestien toteuttaminen vaatii hyvää algoritmin tuntemusta ja tarkkuutta testien toteuttamisessa. Suositelemme vahvasti käyttämään niitä yksikkötestien lisänä harjoitustyön kehityksessä.


## Lisää materiaalia
- [Hypothesis](https://hypothesis.readthedocs.io/en/latest/#) kirjaston oma dokumentaatio.
- [Jqwik](https://jqwik.net/) on javalle tehty samanlainen kirjasto. 
- [Junit-quickcheck](https://github.com/pholser/junit-quickcheck) on otinen Junit testikirjastoa muistuttava java kirjasto jolla tälläinen testaaminen onnistuu.
- [Haskelin Quickcheck](https://hackage.haskell.org/package/QuickCheck) kirjasto on inspiroinut paljon olemassa olevista kirjastoista.
- [Tutoriaali](https://www.inspiredpython.com/course/testing-with-hypothesis/testing-your-python-code-with-hypothesis) hypothesiksen käytöstä Mickey Petersenin kirjoittmana. 

{% include typo_instructions.md %}
