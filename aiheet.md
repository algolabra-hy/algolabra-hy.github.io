---
layout: page
permalink: /aiheet
title: Harjoitustyön mahdolliset aiheet
title_long: Aiheideoita
inheader: no
---

## Aiheen valinnasta
Harjoitustyön keskeisenä tavoitteena on toteuttaa ja testata monimutkaisempia algoritmeja jota ei ole käsitelty aiemmilla kursseilla. Aiheen voi keksiä itse[^1], tai valita alla olevasta listasta. Huomaa kuitenkin että alla olevat ehdotukset on tarkoitettu vain auttamaan alkuun pääsemisessä. Harjoitustyöhon kuuluu oleellisena osana (ohjaajan tukema) itsenäinen tiedon haku, oman aiheen opiskelu ja algoritmin ymmärtäminen. **Varaudu käyttämään tähän aikaa.** Sellaisen algoritmin toteuttaminen, jonka toimintaa ei itse ymmärrä, on erittäin vaikeaa ja turhauttavaa[^2]. 

## Lista aiheista
- [Verkot ja Ppolunetsintä](/aiheet#verkot-ja-polunetsintä)
- [Tiedon tiivistys](/aiheet#tiedon-tiivistys) 
- [Pelit](/aiheet#pelit)
  - Gomoku
  - Miinaharava 
  - Shakki
  - Reversi 
  - Battle Sheep 
  - 2048
  - Kivi-sakset-paperi
  - 15-peli
- [DPLL](/aiheet#dpll)
- [Koneoppiminen](/aiheet#koneoppiminen)
  - Laskennallinen Luovuus, tekstin tai musiikin generointi.
  - Hahmontunnistus 
  - Luolastojen Generointi
- [Salaus ja tietoturva](/aiheet#salaus-ja-tietoturva)
- [Signaalin käsittely](/aiheet#signaalinkäsittely-kuva-ääni)
- [Kontin pakkaus](/aiheet#kontin-pakkaus)
- [Sännölliset lausekkeet](/aiheet#säännöllisten-lausekkeiden-tulkki-tai-kääntäjä)
- [Kirjoitusvirheiden korjaaja](/aiheet#kirjoitusvirheiden-korjaaja)
- [Tieteellinen laskin](/aiheet#tieteellinen-laskin)

---

## Verkot ja polunetsintä
Miten löydetään tehokkaasti nopein/lyhin reitti verkossa kahden pisteen välillä? Verkon pisteet voivat olla esimerkiksi katuosoitteita, joukkoliikenteen pysäkkejä, tai koordinaatteja.

### Tarkempi määrittely 
Toteuta **vähintään kahden** eri reitinhakualgoritmin vertailu. Näistä **korkeintaan toinen** saa olla [Dijkstra](https://fi.wikipedia.org/wiki/Dijkstran_algoritmi) tai [A](https://fi.wikipedia.org/wiki/A*-algoritmi)\* koska Dijkstra opitaan harjoitustyön esitetoihin kuuluvalla Tira-kurssilla ja A* on toteutukseltaan erittäin lähellä Dijkstraa. 

Harjoitustyöhön sopivia reitinhakualgoritmeja ovat:
- [JPS, eli Jump Point Search](https://www.youtube.com/watch?v=afoQvbXvaiQ), josta löytyy tietoa myös [täältä](https://www.youtube.com/watch?v=NmM4pv8uQwI).
  - Soveltuu vain pikselikartoille. Pikselikartalla on kahdeksan etenemissuuntaa ja kaksi mahdollista painoa, kaaren paino riippuu siitä kuljetaanko seuraavaan solmuun suoraan vai viistottain. 
  - Pikselikarttoja löytyy esim. [Moving AI Lab](http://www.movingai.com/benchmarks/) sivuilta.
- [IDA](https://en.wikipedia.org/wiki/Iterative_deepening_A*)\*.
- [Fringe Search](https://webdocs.cs.ualberta.ca/~holte/Publications/fringe.pdf) joka on astetta haastavampi. 

Muutama **lisävaatimus**:
- Jos aiheena on JPS vs Dijkstra / A*, voit käyttää ohjelmointikielen valmiita tietorakenteita. 
- Mikäli aiheena on IDA\* vs Dijkstra / A\*, tulee toteuttaa itse minimikeko, jonka avulla järjestetään IDA\*:ssa naapurisolmut ja Dijkstrassa tutkittavat solmut. IDA\*:n pinoa ei tarvitse toteuttaa itse.


### Hyödyllisiä neuvoja 
Reitinhakualgoritmien vertailussa on syytä heti alkuun toteuttaa löydetyn reitin ja läpikäytyjen solmujen / hyppypisteiden visualisointi. Ilman sitä on vaikea nähdä toimiiko algoritmi oikein. 
Visualisointi auttaa hakualgoritmin oikeellisuuden toteamisessa, ja se nopeuttaa myös virheiden löytämistä ohjelman kehityksen aikana. 
Visualisoinnin laatimiseen ei saisi mennä paljon työaikaa, sillä varsinainen ydin on reitinhakualgoritmien toteutus ja huolellinen testaus. Graafinen käyttöliittymä on kätevä, mutta selkeä ASCII-grafiikka riittää, jos käytät pikselikarttoja. **Huomaa** että oikeellisuuden ja tehokkuuden testaamiseen tarvitaan monimutkaisia ja tarpeeksi laajoja karttoja, jotka ovat vertailemiesi algoritmien kannalta mielekkäitä. Niiden tuottaminen käsin olisi kohtuuttoman työlästä, joten tarvitset myös valmiita karttoja jostain lähteestä.

Valmiita karttoja löytyy esimerkiksi [Moving AI Lab](http://www.movingai.com/benchmarks/) sivuilta tai [maanmittauslaitoksen kartoista](http://kartat.kapsi.fi/). Huomaa, että Moving AI:n pikselikartoissa ilmoitetut etäisyydet on laskettu niin, että reitti kiertää esteen kulmapikselin, sen sijaan että kulkisi viistosti tavallaan puoliksi estepikselin yli. Myös joukkoliikenteen [reitti / aikataulut](https://developers.google.com/transit/gtfs/) tai [digitransitin kartat](https://digitransit.fi/en/developers/) ja [avoin karttadata](https://www.openstreetmap.org) ovat olleet suosittuja valmiiden karttojen lähteitä.

Joidenkin karttojen mukana tulee etäisyystietoja erilaisille reiteille, ja niitä voi hyödyntää testeissä. Muista kuitenkin, että se että algoritmisi palauttaa oikean pituden ei vielä takaa, että se toimii oikein. 

---

## Tiedon tiivistys
Miten erityyppisiä tiedostoja voidaan *pakata* ja *purkaa* tehokkaasti? Eri pakkausalgoritmit voidaan jakaa 
häviöllisiin tai häviöttömiin menetelmiin. Häviölliset menetelmät pystyvät usein suurempaan *pakkaustehoon*, eli pienentämään tiedostoa enemmän. Toisaalta, purettu tiedosto ei häviöllisellä menetelmällä välttämättä ole sama kuin alkuperäinen. Häviöllisiä menetelmiä käytetään usein kuvan tai äänen pakkaamiseen kun taas tekstin pakkauksessa käytetään häviöttömiä menetelmiä.

Lisää tietoa tiedonpakkauksesta [Wikipediasta](https://fi.wikipedia.org/wiki/Tiedonpakkaus).

### Tarkempi määrittely
Toteuta algoritmeja tiedoston pakkaamiseen ja pakatun tiedoston purkamiseen. Sopiva määrä toteutettavia pakkausalgoritmeja riippuu niiden monimutkaisuudesta. Ohjaaja antaa tästä tarkempaa tietoa. Yleensä harjoitustyön vaatimuksiin pääsemiseksi tarvitaan kahden eri algoritmin toteutus ja vertailu. Jotkut menetelmät ovat kuitenkin niin monimutkaisia, että niiden toteutus yksinään riittää. **Keskustele ohjaajan kanssa** sopivasta rajauksesta, varsinkin jos toteutat kuvan tai äänen pakkausta. 

Harjoitustyöhön sopivia pakkausemenetelmiä ovat esim:
- [Lempel-Ziv -algoritmit](https://en.wikipedia.org/wiki/LZ77_and_LZ78) kuten LZ77, LZ78, LZSS tai LZW.
- [Huffman koodaus](https://en.wikipedia.org/wiki/Huffman_coding) johonka liittyy oleellisesti [Huffman-puun tallettaminen](https://stackoverflow.com/questions/759707/efficient-way-of-storing-huffman-tree)

Sopiva aihe harjoitustyölle on esimerkiksi yhden LZ algoritmin vertaaminen Huffman koodaukseen tekstin pakkauksessa. 
Ohjelman tulee tuottaa kiintolevylle tiedosto, joka sisältää kaiken sen purkamiseen tarvittavan datan, ja jonka koko on käytetylle pakkausmenetelmälle tyypillinen.

### Hyödyllisiä neuvoja 
Kun pakataan luonnollista kieltä (tai ohjelmistokoodia) pakatun tiedoston koon tulisi olla noin 40-60% alkuperäisestä koosta, kunhan pakattava tiedosto on riittävän suuri. 
Tekstin pakkaamiseen käytetään vain häviöttömiä menetelmiä, joten pakatut tekstitiedostot täytyy pystyä palauttamaan alkuperäiseen muotoon.
Kuvaa ja ääntä pakattaessa pyritään paljon suurempaan pakkaustehoon, mutta käyttäen häviöllisiä menetelmiä jolloin pakattua tiedostoa ei voi enää palauttaa alkuperäiseksi.

Aiheen vaatimusten saavuttaminen vaatii datan lukemista ja kirjoittamista tiedostoon bittitasolla, 
mikä ei onnistu samoilla välineillä kuin tekstitiedoston käsittely. 
Voit käyttää ohjelmointikielen valmiita tietorakenteita kaikissa pakkausalgoritmeissa.
**Huomaa** että pakkausalgoritmejasi täytyy testata [edustavilla](/respresentativeinputs) syötteillä, jotka ovat tarpeeksi isoja. 

---

## Pelit
Miten toteutetaan tekoäly erityyppisille peleille? Tässä projektissa valitaan yksi peli, ja toteutetaan sille tekoäly. 
Useimille alla olevista peleistä tekoälyn voi toteuttaa [minimax-algoritmilla, jota on tehostettu alpha-beta-karsinnalla](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning).

Minmax-algoritmi laskee jokaisesta pelitilateesta eteenpäin ja valitsee siirron, joka johtaa omaan voittoon. Täten algoritmi olettaa, että sekä tekoäly että vastapelaaja tekevät joka tilanteessa itsensä kannalta parhaan mahdollisen siirron. Koska harvasta pelitilanteesta 
voidaan laskea voittoon, häviöön, tai tasapeliin asti, lasketaan sen sijaan tietty määrä siirtoja eteenpäin ja 
arvioidaan jollain heuristiikalla, kuinka hyvään pelitilanteeseen päästään. Heuristiikan perusteella valitaan se siirto, joka johtaa parhaimpaan pelitilanteeseen. 

**Jos haluat tehdä shakille tai connect fourille tekoälyn** suosittelemme vahvasti harjoitustyön [tekoäly alustan](/aiplatform) käyttöä. 
Alusta tarjoaa graafisen käyttöliittymän ja mahdollisuuden pelata omaa tekoälyäsi vastaan minimaalisella overheadilla. 


### Tarkempi määrittely
Toteuta jonkin pelin tekoäly. Tekoälysi pitää pystyä pelaamaan ihmistä vastaan käyttöliittymäsi kautta. 
Voidaksesi käyttää tekoälyäsi, sinun täytyy myös toteuttaa sovelluslogiikka ja käyttöliittymä pelillesi. Sovelluslogiikan ja käyttöliittymän toteuttamiseen ei 
kuitenkaan saisi käyttää liikaa aikaa, harjoitustyön ydin on itse tekoäly. 
Valmiita kirjastoja tms. ei saa käyttää pelin sovelluslogiikassa, vaan esim. sallittujen siirtojen generointi, 
voiton tunnistus ja siirtojen suorittaminen toteutetaan itse. Käyttöliittymään voi käyttää valmiita välineitä, mutta monissa peleissä tekstipohjainen 
käyttöliittymä on täysin käyttökelpoinen. Käyttöliittymää ei tarvitse testata. 

Alla lista mahdollisista peleistä sekä hyödyllisiä neuvoja kullekin pelille. Peleissä joiden solvelluslogiikka ja 
käyttöliittymä ovat helpompia toteuttaa, itse tekoälyltä vaaditaan hieman lisää ominaisuuksia. Nämä vaatimukset 
mainitaan erikseen pelin kohdalta. Mikäli pelin kohdalla ei mainita muuta, tekoälyn sille pelille voi toteuttaa minimax algoritmilla. 

#### Ristinolla / Gomoku
20 x 20 ruudukolla pelattava ristinolla, jossa voittaa kun saa vähintään 5 merkin pituisen rivin. 

**Lisävaatimukset.** Hyväksyttyyn suoritukseen vaaditaan tehokas toteutus, johon kuuluu:
- Tutkitaan vain vapaat ruudut, jotka ovat korkeintaan kahden ruudun päässä aiemmin tehdyistä siirroista, tai muu tätä tehokkaampi mielekäs kokeiltavien siirtojen karsinta. Tutkittavia siirtoja ei selvitetä erikseen joka pelitilanteessa, vaan pidetään yllä listaa tällaisista ruuduista, ja päivitetään sitä tehtyjen / minimaxissa kokeiltujen siirtojen myötä. Siirtojen mukaan päivitetty lista annetaan parametrina eteenpäin minimaxissa.
- Ristinollassa on usein pakko reagoida vastustajan edelliseen siirtoon, tai se on jatkoa ajatellen kannattavaa. Usein paras reaktio on jokin edellisen siirron viereinen siirto. Noudata tätä heuristiikkaa lisäämällä / nostamalla viimeisimmän siirron lähinaapurit ensimmäisiksi tutkittaviksi.
- Voiton tarkistus tehdään tutkimalla vain rivit, jotka sisältävät edellisen siirron. Jos viiden rivi on syntynyt, voittaja on edellisen siirron tehnyt pelaaja, ja edellinen siirto on osa voittoriviä.

**Hyödylliset Neuvot.**
**Älä** toteuttaa ensin 3 x 3 pelin toimintalogiikaa ja tekoälyä. Kaikki pitää kuitenkin tehdä täysin eri tavalla, kun lauta on laaja.

#### Shakki

Normaaleilla säännöillä 8 x 8 laudalla pelattava shakkipeli jossa voit jättää toteuttamatta osan tai kaikki näistä toiminnoista: 
  - tornitus, 
  - ohestalyönti, 
  - sotilaan korotus ja 
  - toistuvaan asemaan perustuva tasapeli.

Projektisi heuristiikkafunktion tulee arvioida materiaalin määrän lisäksi jollain tavalla nappuloiden sijoittumista laudalla.
Shakin tekoälyn toteuttamiseen voit käyttää harjoitustyön [tekoälyalustaa](/aiplatform).

#### Connect4
6 x 7 -kokoisella laudalla pelattava peli, jossa voittaa kun saa neljä omaa pelimerkkiä riviin. 
Jos peli ei ole tuttu, katso [Connect Four Wikipediasta](https://en.wikipedia.org/wiki/Connect_Four). 
**Tämä on hyvä aihe**, jos haluat käyttää suurimman osan työajastasi juuri minimax-algoritmin tehostamiseen. Tutkittavien siirtojen generointi ja 
siirtojen toteuttaminen on Connect4:ssä yksinkertaisempaa kuin monessa muussa pelissä, ja sen sijaan panostetaan laskennan nopeuttamiseen 
käyttäen peliohjelmointiin yleisesti soveltuvia menetelmiä.

**Lisävaatimukset**
Minimax-pohjaisissa Connect4 harjoitustöissä vaaditaan seuraavat optimoinnit:
- *Siirtojen järjestäminen.* Kokeillaan kaikissa laskennan vaiheissa ensin keskimmäiseen sarakkeeseen tehtävä siirto ja edetään siitä reunoja kohti. Tämä tehostaa alfa-beta -karsintaa, koska paras siirto löytyy useammin keskeltä.

- [*Iteratiivinen syveneminen.*](https://domwil.co.uk/minimaxer/part2/) Suoritetaan ensin minimax pienellä syvyydellä, sitten yhä suuremmalla, kunnes aikaraja on saavutettu. Näin saadaan ensinnäkin hyödynnettyä käytettävissä oleva aika paremmin, koska eri pelitilanteissa samalle syvyydelle tapahtuvaan laskentaan tarvittava aika vaihtelee paljon. Jokaisessa tutkitussa pelitilanteessa talletetaan tieto siitä, mikä oli paras siirto vuorossa olevan pelaajan kannalta. Kun tullaan uudestaan samaan pelitilanteeseen samalla tai myöhemmällä iteraatiolla, kokeillaan ensin edellisellä kerralla parhaaksi arvioitua siirtoa. Se on usein paras tai ainakin hyvä siirto myös sitten, kun lasketaan siirtoja syvemmälle, joten alfa-beta -karsinta tehostuu, kun saadaan nopeasti nostettua / laskettua alfa / beta -arvoa. Uusi hajautustaulu luodaan aina, kun käyttäjä on tehnyt oman siirtonsa, ja aletaan laskea tekoälyn siirtoa. Tällöin talletus onnistuu tavallisella hajautustaululla (dictionary, HashMap), koska muistin käyttö on maltillista. Hajautustaulussa avain kuvaa pelitilanteen, ja arvona on siirto. Huomaa, että et voi tallettaa hajautustauluun siirtojen arvoja ja palauttaa niitä, koska alfa-beta -karsinnan takia suurin osa minimaxin palauttamista arvoista ei ole aitoja vaan vain ylä- tai alarajoja todellisille arvoille. Kaikkia siirtoja täytyy kokeilla normaalisti, tietoa viimeksi parhaaksi arvioidusta siirrosta voi käyttää vain siirtojen järjestämiseen. 

#### Othello / Reversi
[Othelloa](https://en.wikipedia.org/wiki/Reversi) pelataan 8 x 8 pelilaudalla. Pelin voittaa se, jolla on eniten nappuloita laudalla, kun kaikki ruudut on täytetty. 

**Hyödylliset Neuvot.**
Esim. shakkiin verrattuna Othellossa on vaikea arvioida pelitilanteen arvoa merkityksellisesti, mutta ihmistä vastaan pelatessa auttaa, että tehtävä on vaikea myös ihmiselle. 
Neuvoja heuristisen evaluaatiofunktion laatimiseen löytyy, esim.
- [Kartik Kukrejan blogista](https://kartikkukreja.wordpress.com/2013/03/30/heuristic-function-for-reversiothello/)
- [Vaishnavi Sannidhanamin and Muthukaruppan Annamalain kurssiprojektista](https://courses.cs.washington.edu/courses/cse573/04au/Project/mini1/RUSSIA/Final_Paper.pdf)

Othellon tekoälyn voi minimaxin lisäksi toteuttaa esim. [Monte Carlo Tree Searchilla](https://en.wikipedia.org/wiki/Monte_Carlo_tree_search). Silloin ei tarvita evaluaatiofunktiota.

#### 2048
[2048](https://en.wikipedia.org/wiki/2048_(video_game)) poikkeaa aikaisemmista siinä mielessä, että pelissä on vain yksi pelaaja ja
satunnaiselementti. Näimpä sen tekoälyn pohjaksi sopii [expectiminimax-algoritmi](https://en.wikipedia.org/wiki/Expectiminimax), 
muunnettuna niin että siinä on kahden sijasta vain yksi pelaaja + satunnainen tapahtuma. Myös minimaxilla jossa satunnainen tapahtuma on vastapelaaja 
on kuitenkin saavutettu hyviä tuloksia, vaikka silloin oletetaan aina uuden luvun ilmaantuvan pahimpaan mahdolliseen kohtaan pahimmalla arvolla.

Jos otat jostain mallia heuristiseen arviointifunktioon, huomaa että ihan sama funktio ei ehkä ole ihanteellinen minimaxille ja 
expectiminimaxille. Minimaxilla saavutetaan alfa-beta -karsinnan avulla suurempi laskentasyvyys, jolloin esim. vapaiden ruutujen 
määrä ennustaa paremmin menestystä. Hyvä heuristinen funktio huomioi joka tapauksessa sekä vapaan tilan määrän että arvojen sijoittumisen.
Yun Nie, Wenqi Hou ja Yicheng An ovat kirjoittaneet [lyhyen artikkelin lähestymistavoista ja heuristiikoista](https://cs229.stanford.edu/proj2016/report/NieHouAn-AIPlays2048-report.pdf).

#### Battle sheep
[Battle Sheep](https://www.lautapelit.fi/product/20852/battle-sheep) on hauska vaihtoehto klassikkopeleille. 
Pelilaudan ei tarvitse olla muokattava, kuten lautapelissä, vaan voit käyttää sopivaa kiinteää pelilautaa. Tähän peliin tarvitaan 
graafinen käyttöliittymä, jotta pelaaminen on sujuvaa.

#### Kivi-sakset-paperi
Kivi-sakset-paperi on kaikille tuttu peli, jota ei yleisesti voi pelata hyvin tai huonosti. Näimpä (tehokasta) tekoälyä pelille **ei** voi toteuttaa
minimax algoritmilla. Sen sijaan tässä projektissa tehdään oppiva tekoäly joka pyrkii oppimaan vastustajansa pelityylin ja 
pelaamaan hyvin sitä vastaan. Yksi tapa oppia toisen pelityyli on käyttää useamman eri asteen [Markovin ketjuja](https://arxiv.org/pdf/2003.06769) (katso myös kohta 
[laskennallisesta luovuudesta](/aiheet/#koneoppiminen)). 
Siihen voi yhdistää muitakin malleja vastustajan toimminnalle. *Kannattaa jutella ohjaajan kanssa, jos tämä aihe kiinnostaa.*

#### 15-peli
[15-peli](https://en.m.wikipedia.org/wiki/15_Puzzle) on haastava ratkaistava, pelin ratkaisu vie pahimmassa tapauksessa paljon aikaa ainakin heikolla heuristiikalla. 
Ratkaisussa tulee lähtökohtaisesti käyttää [IDA* -algoritmia](https://en.wikipedia.org/wiki/Iterative_deepening_A*). 
Keskustele ohjaajan kanssa jos haluat käyttää jotain muuta. Tähän peliin soveltuvista heuristisista 
etäisyysfunktioista kerrotaan esim. [Michael Kimin blogissa](https://michael.kim/blog/puzzle).

#### Miinaharava
Tälle kurssille sopivista miinaharavan ratkaisijoista löytyy tietoa [David Becerran kandidaatin tutkielmasta](https://dash.harvard.edu/handle/1/14398552).  
Jos käytät projektissa Javaa, voit toteuttaa ratkaisijan / auttajan käyttöliittymän valmiilla [Miinaharavan projektipohjalla](https://github.com/TiraLabra/minesweeper). 
Jos käytät valmista Java-pohjaa, kerro koodin kommenteissa selvästi mikä on omaa koodiasi, ja mikä on pohjaa. Älä muokkaa pohjaa, vaan kirjoita oma koodisi omaan luokkaansa / metodiinsa.

---

## DPLL
[Propositiologiikan päätösongelma](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem) (SAT) on 
keskeinen sekä teoreettisessa, että soveltavassa tietojenkäsittelytieteessä. 
Nykyaikaiset ns. CDCL algoritmien toteutukset (SAT-solverit) pystyvät päättämään miljoonia muutujia sisältävien 
kaavojen toteutuvuuden. Tälläisiä algoritmeja käytetään monissa [käytännön sovelluksissa](https://en.wikipedia.org/wiki/SAT_solver#Applications),
tehokkaat SAT solverit ovat esimerkiksi oleellisia erilaisten piirien oikeellisuden varmistamisessa. 

Tehokkaan CDCL algoritmin toteuttaminen on harjoitustyölle liian vaativaa. Sen sijaan tässä
aiheessa tutkimme sen edeltäjää, [DPLL](https://en.wikipedia.org/wiki/DPLL_algorithm) algoritmia. 

### Tarkempi määrittely
Toteuta ohjelma, joka lukee propositioloogisen kaavan konjunktiivisessa 
normaalimuodossa [DIMACS](https://www.cs.utexas.edu/users/moore/acl2/manuals/current/manual/index-seo.php/SATLINK____DIMACS) tiedostomuodossa 
ja palauttaa joko sen toteuttavan totuusjakelun, tai tiedon siitä, ettei tälläistä jakelua ole. Ohjelman pitää käyttää DPLL algoritmia. 

Ollakseen hyväksyttävä ohjelman täytyy toteuttaa [yksikköpropagaatio](https://en.wikipedia.org/wiki/Unit_propagation) ja [
puhtaan literaalin poisto](https://users.aalto.fi/~tjunttil/2020-DP-AUT/notes-sat/preprocessing.html#pure-literal-elimination). 
Katso tarkempi selitys algoritmista [täältä](https://users.aalto.fi/~tjunttil/2020-DP-AUT/notes-sat/dpll.html). Kaavan käsittelyyn vaadittavat 
tietorakenteet täytyy toteuttaa itse. Aihe on parasta toteuttaa **C++** kielellä. 

### Hyödyllisiä neuvoja 
Oman algoritmin oikeellisuutta voi testata vertaamalla sen tuloksia johonkin CDCL SAT solverin tulostukseen. Esim [CaDiCal](https://github.com/arminbiere/cadical/tree/master) tai [Kissat](https://github.com/arminbiere/kissat) ovat tähän oikeen soveltavia. Molemissa näiden repositoorioissa löytyy myös testilauseita: ([Cadicalin testit](https://github.com/arminbiere/cadical/tree/master/test/cnf), 
[Kissatin testit](https://github.com/arminbiere/kissat/tree/master/test/cnf.)). Muista vaan, että sekä CaDiCal, että Kissat ovat erittäin optimpoituja 
CDCL algoritmin toteutuksia, tämän kurssin aikana oma ratkojasi ei pääse lähellekkään samanlaista tehokkuutta. 

Lisää testilauseita voi luoda esim: [CNFGen](https://massimolauria.net/cnfgen/) työkalulla. 

**Lisähaastetta**
Jos haluat lisähaastetta voit tutustua ns. [2-watched literal](https://www.youtube.com/watch?v=n3e-f0vMHz8) tapaan toteuttaa yksikköpropagaatio tehokkaasti. 
Huomaa, että ilman 2-watched literaalia ohjelmasi luutavimmin pystyy vain ~100 muuttujan kokoisten kaavojen ratkaisuun. Tämä riittää harjoitustyöhön, mutta 
testisyötteitesi koko kannattaa säätää tämän mukaan. 
Lisää mahdollisia tehostuksia algoritmillesi löytyy esim [Aalto Yliopiston](https://users.aalto.fi/~tjunttil/2020-DP-AUT/notes-sat/cdcl.html) kurssimateriaalista. 
Oleellisena (mutta haasteellisena) tehostuksena mainittakoon konfliktiklausuulien oppiminen ja epäkronolooginen taaksepäinhyppy. 

Huomaa, että SAT solvereilla voi ratkoa monta erilaista ongelmaa mallintamalla ne ensiksi propositiologiikaan. Saatko omasta DPLL algoritmistasi tarpeeksi tehokkaan,
jotta se pystyy ratkomaan [Sudokuja](https://sat.inesc-id.pt/~ines/publications/aimath06.pdf)?

---
## Koneoppiminen
Koneoppiminen on erittäin laaja alue josta löytyy paljon harjoitustyöhön sopivia 
aiheita. Monissa koneoppimiseen liittyvissä aiheissa kannattaa muistaa, että algoritmit ovat stokastisia, 
niiden tuottama tulos riippuu osaksi myös siitä harjoitusdatasta, jota niille syötetään. Täten niiden oikeellisuuden 
varmistamiseen tarvitaan hyvin suunniteltuja [testejä](/testing) edustavilla syötteillä.

# Laskennallinen luovuus.
Sekä sanojen, lauseiden, musiikin, että kuvien[^3] tuottaminen algoritmisesti onnistuu periaatteessa samalla tavalla. 
Ohjelma lukee ensin harjoitusdatan ja opettelee siitä erilaisia sanojen / lauseiden / sävel- / sointusekvenssejä. 
Uutta materiaalia tuotetaan sitten tarkastelemalla tämänhetkistä tekstiä tai musiikkia, ja lisäämällä siihen jatkoa harjoitusdatasta opittujen 
sekvenssien perusteella. 

#### Tarkempi määrittely 
Toteuta ohjelma, joka lukee harjoitusdataa, oppii siitä sekvenssejä ja generoi niiden perusteella  
uusia sekvenssejä käyttäjän kehotteiden perusteella. Tällä kurssilla suosittelemme käyttämään 
[markovin ketjuja](https://en.wikipedia.org/wiki/Markov_chain) jonka avulla voidaan onnistuneesti tuottaa esimerkiksi musiikkia tai 
luonnollisen kielen kaltaisia sanoja tai [lauseita](https://algoritmaonline.com/text-generating-with-markov-chains/). Ketju tallettaa 
harjoitusdatansa [trie](https://www.geeksforgeeks.org/trie-insert-and-search/#:~:text=Definition%3A%20A%20trie%20(derived%20from,%2C%20are%2C%20bat%2C%20bad.)) 
tietorakenteeseen josta voidaan tehokkaasti etsiä mahdollisia jatkoja annetulle syöttelle. 

Toteuta itse trie-tietorakenne sanojen / lauseiden / sävel- / sointusekvenssien tallettamiseen. 
Voit käyttää sekä valmiita kirjastoja että ulkoisia ohjelmia opetusdatan esikäsittelyyn, melodian soittamiseen / nuotintamiseen jne.

### Hyödyllisiä ohjeita

Markovin ketju on prosessi, jonka jokainen tila määrittelee todennäköisyyden sitä seuraaville tiloille. 
Tässä tapauksessa jokainen tila on tämänhetkisen syötteen (sanan, lauseen, musiikin etc.) viimeinen kirjain/sana/nuotti, tai sointu. 
Siirtyminen seuraavaan tilaan määrittelee mitä lisätään syötteeseen. Niin sanotun *ensimmäisen asteen* markovin ketjun
kunkin tila riippuu vain edellisestä tilasta, tässä tapauksessa tämähetkisen syötteen viimeisimmästä osasta. Vastaavasti, toisen asteen ketjun tila 
riippuu kahdesta viimeisimmästä tilasta, eli toisin sanoen tämänhetkisen syötteen kahdesta viimeisimmästä osasta.  
Huomaa, että esimerkiksi toisen asteen Markovin ketjun toteuttaminen vaatii kaikkien opetusdatassa peräkkäin esiintyvien kolmikoiden tallettamista, 
jotta tiedetään kullekin viimeisimmälle kaksikolle mahdolliset seuraajat ja niiden todennäköisyydet. 

Kokeile generointia alkaen 1. asteesta ja vertaa tuloksia eri asteilla. Seuraava kirjain, sana tai sävel arvotaan opetusdatasta opittujen 
todennäköisyyksien mukaan. Järkevien - tai hauskojen - lauseiden tuottamiseen tarvitaan minimissään toisen asteen Markovin ketju. 
Musiikkikin on 1-asteella tuotettuna aika satunnaista, vaikka noudattaa toki jotain sävellajia, kunhan opetusdata on ollut siinä suhteessa konsistenttia. 

**Musiikin tuottaminen.** Aiemmissa projekteissa on musiikkidataa syötetty ohjelmalle MIDI-tiedostoina, [Lilypond](http://lilypond.org/)-nuotteina tai [abc](https://abcnotation.com/)-notaationa. Python-kirjastossa [music21](https://web.mit.edu/music21/) on monia hyödyllisiä välineitä. Markov ketjuja musiikin generaatioon voi tehostaa muillakin tekniikoilla, katso esim. (Musikalisches Würfelspiel)[https://en.wikipedia.org/wiki/Musikalisches_W%C3%BCrfelspiel]. Myös [geneettisillä algoritmeilla](https://en.wikipedia.org/wiki/Genetic_algorithm) voi tuottaa taidetta.

**Harjoitusdatan määrä**. Jotta ei päädytä toistamaan opetusdataa sellaisenaan, pitää esim. 2-asteella generoitaessa olla niin paljon opittuja mahdollisia 
kolmen sanan / sävelen jonoja, että kahden edellisen perusteella voi kolmannen riittävän usein valita useammalla tavalla.
Varsinkin tekstiä tuotettaessa tarvitaan paljon harjoitusdataa (kokonaisia kirjoja tms.). Jos tuotetaan musiikkia tai vaikka nimiä, 
riittää pienempi määrä opetusdataa, mutta silti niin paljon, että datan syöttäminen käsin olisi kohtuuttoman työlästä. 
Tarvitaan sopivaa dataa, joka muunnetaan automaattisesti ohjelman käyttämään muotoon.

Jos tämä aihe kiinnostaa, kannattaa jutella ohjaajan kanssa jo ennen työn aloittamista. 

# Hahmontunnistus
#### Tarkempi määrittely 
Toteuta ohjelma, joka harjoitusdatan perusteella oppii tunnistamaan jotakin kuvia. Lopullinen ohjelma 
lukee ensin harjoitusdatan, oppii sen perusteella tunnistamaan uusia, entuudestaan tuntemattomia kuvia. 
Alla muutama tarkempi aiheidea. Muutkin ovat mahdollisia (juttele ohjaajan kanssa). 

**Kasvojentunnistuksen** voi toteuttaa esimerkiksi [Eigenface](https://en.wikipedia.org/wiki/Eigenface):n avulla. 
Tähän aiheeseen vaaditaan vähintään kurssi lineaarialgebra ja matriisilaskenta 1+2 käytynä. Jos käsitteet kovarianssimatriisi ja pääkomponenttianalyysi ovat 
tuttuja, ymmärrät varmaan tähän aiheeseen liittyvän matemaattisen teorian. Toteuta vaativia matriisilaskennan operaatioita itse.

**Käsin kirjoitettujen numeroiden tunnistus.** [MNIST](http://yann.lecun.com/exdb/mnist/) on tietokanta, jota käytetään paljon hahmontunnistusmenetelmien 
testaamiseen. Tällä kurssilla on numeroita luokiteltu esimerkiksi neuroverkoilla. Sovi ohjaajan kanssa mitä valmiita välineitä voit käyttää, 
jotta työmäärä on kohtuullinen. Joka tapauksessa neuroverkko vastavirta-algoritmeineen ym. toteutetaan itse. 

Neuroverkkoja ennestään tuntemattomalle helpompi ratkaisu on muuntaa MNIST:in harmaasävykuvat mustavalkoisiksi ja käyttää 
[k:n lähimmän naapurin](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm) menetelmää pistejoukkojen etäisyysmitoilla. 
Tällöin tuntematon kuva luokitellaan samaksi, kuin k sitä lähimmät naapurit. Näin voi myös saavuttaa niin hyvän luokittelutuloksen, 
että neuroverkoilla ei ole helppo päästä samaan. Artikkeli [A Modified Hausdorff Distance for Object Matching](https://ieeexplore.ieee.org/document/576361) 
kertoo muutamasta mahdollisesta etäisyysmitasta. Artikkelissa parhaaksi mainitun mitan D22 lisäksi kannattaa kokeilla ainakin mittaa D23 sellaisenaan ja ilman kerrointa 1/N osakaavassa d6.

Lisää materiaalia neuroverkoista:  
- [The Neural Blogin](https://theneuralblog.com/forward-pass-backpropagation-example/) Rabindra Lamsalin kirjoittama artikkeli ns. feed forward verkosta ja sen treenaamisesta. 
- [Neuroverkkojen testauksesta](https://www.sebastianbjorkqvist.com/blog/writing-automated-tests-for-neural-networks/) kertona Sebastian Björkqvistin artikkeli. 
- [Michael Nielsenin](http://neuralnetworksanddeeplearning.com/chap1.html) kirjoittama arikkeli MNISTin numeroiden tunnistuksesta neuroverkoilla. 
- [Heli Tuomisen](https://tim.jyu.fi/view/143092#lis%C3%A4tietoa-aktivointifunktioista) kirjoittama kurssimateriaali neuroverkkojen matematiikasta suomeksi. 
- [3Blue1Brown](https://www.youtube.com/watch?v=aircAruvnKk&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)in erittäin hyvin tehdyt videot neuroverkoista. 
- [Deep Learning](https://www.deeplearningbook.org/) oppikirja ns. syväoppimisesta. **Huom** vaikka syväoppiminen on "aidoissa" sovelluksissa useimmin käytetty tekniikka, on syväoppivan verkon toteuttaminen huomattavasti haastavampaa kuin tältä harjoitustyöltä vaaditaan. 


# Luolastojen generointi
#### Tarkempi määrittely
Toteuta ohjelma, joka luo jonkinlaisen luolaston, tai kartan dynaamisesti. 
Luolaston generointi voi olla joko etukäteen tapahtuva tai dynaamisesti pelin aikana pelaajan liikkumisen mukaan kehittyvä. 
Luolastoja tuotetaan useampivaiheisen prosessin kautta. Tällöin esim. yksi algoritmi voi tuottaa huoneita, toinen niiden väliset 
käytävät ja kolmas halutun kaltaisen ulkoasun. Ohjelmassa tulee olla vähintään yksi riittävän laaja algoritmi, 
joka ei kuulu kurssin esitietoihin, esimerkiksi jokin [delaunay triangulaation](https://en.wikipedia.org/wiki/Delaunay_triangulation) suorittava algoritmi.

**Hyödyllisiä Lähteitä**:
- [Tom Stephensonin](https://www.tomstephensondeveloper.co.uk/post/creating-simple-procedural-dungeon-generation) blogikirjoitus
- [Bowyer–Watson](https://en.wikipedia.org/wiki/Bowyer%E2%80%93Watson_algorithm) algoritmi delaunay triangulaatioiden laskemiseen. 

---
## Salaus ja Tietoturva
Tietoturva on tänä päivänä tärkeämpää kuin koskaan. Salausta voi tehdä useilla eri tavoilla ja moniin käyttötarkoituksiin. 
Esim. [RSA-salaus](https://fi.wikipedia.org/wiki/RSA) on harjoitustyöhön sopiva aihe. 

### Tarkempi Määrittely
Toteuta ohjelma joka salaa ja purkaa tekstiä. Ohjelman tulee salaamisen ja salauksen purkamisen lisäksi tuottaa avaimia, joiden pituus on oikean 
RSA-salauksen tavoin vähintään 1024 bittiä. Käyttäjä voi antaa salattavaksi sen pituisen tekstin kuin avaimen pituus sallii. 
[Paddingia](https://en.wikipedia.org/wiki/Padding_(cryptography)) ei tarvitse toteuttaa. Isojen alkulukujen etsimiseen ja avaimen muodostamiseen 
tarvittavat metodit, kuten [Miller-Rabin](https://en.wikipedia.org/wiki/Miller%E2%80%93Rabin_primality_test) algoritmi, tulee toteuttaa itse, 
mutta ohjelmointikielen valmista modulaarista potenssiin korotusta saa käyttää laskennassa.

Tämän kurssin vaatimustasoa **eivät** vastaa sellaiset salausmenetelmät, jotka perustuvat yksittäisten sanojen tai koko tekstin merkkien paikan 
vaihtamiseen tai yksittäisten merkkien korvaamiseen aina jollain tietyllä merkillä.

**Vaihtoehtoisesti** voit toteuttaa ohjelman joka **murtaa** (eli purkaa tietämättä siihen tarvittavaa avainta) salauksia. Vaihtosalaukseen perustuvan 
salakirjoituksen saa murrettua sanaston avulla merkkien frekvenssejä analysoimalla, jos teksti on riittävän pitkä ja tiedetään mitä kieltä se on. 
Ratkaisuksi käy peruuttava haku, joka kokeilee korvata salattuja merkkejä siinä järjestyksessä, mitkä frekvenssien perusteella ovat luultavimpia. 
Sanaston talletukseen sopii [trie](https://www.geeksforgeeks.org/introduction-to-trie-data-structure-and-algorithm-tutorials/#:~:text=Trie%20data%20structure%20is%20defined,finding%20something%20or%20obtaining%20it.)-tietorakenne. Koska mikään sanasto ei ole täydellinen, pitää peruuttava haku toteuttaa niin, että hyväksytään tietty määrä virheellisiltä vaikuttavia sanoja.

---
## Muita aiheita
### Signaalinkäsittely (kuva, ääni)
Toteuta algoritmien vaativuudesta riippuen yksi tai useampi signaalinkäsittelyalgoritmi. Useat signaalinkäsittelyn algoritmit hyödyntävät 
matriisilaskentaa ja lineaarialgebraa, joten niiden tunteminen on hyödyksi. Ohjelman tulee tuottaa tuloste (visualisointi tai ääni), josta algoritmia 
tuntematonkin voi havaita ohjelman toimivan suunnilleen tarkoitetusti. Aiheena on aiemmin ollut esimerkiksi signaalin voimakkaimman taajuuden 
tunnistaminen ja / tai kohinansuodatus käyttäen [nopeaa fourier-muunnosta](https://en.wikipedia.org/wiki/Fast_Fourier_transform).

### Kontin pakkaus
Rahtifirma NopsaToimitus haluaa optimoida konttikuljetuksissa käytettävän tilan. Suunnittele miten voidaan täyttää yksi tai useampi 
kontti mahdollisimman tehokkaasti, jos tiedetään pakettien määrä ja koot. Tämä aihe vaatii kolmiulotteista konttien kuvaamista näytöllä, jotta lopputulosta voi arvioida.

### Säännöllisten lausekkeiden tulkki tai kääntäjä

Toteuta ns. tulkki, eli ohjelma joka sovittaa [säännöllistä lauseketta](https://blog.stevenlevithan.com/archives/10-reasons-to-learn-and-use-regular-expressions) 
merkkijonoon ja kertoo, kuuluuko se lausekkeen määräämään kieleen. Toteuta myös [kääntäjä](https://www.geeksforgeeks.org/regular-expression-to-dfa/) 
joka annetun säännölisen lausekkeen perusteella tuottaa [DFA](https://en.wikipedia.org/wiki/Deterministic_finite_automaton):n joka hyväksyy samat merkkijonot, kuin lauseke. 


### Kirjoitusvirheiden korjaaja

Toteuta ohjelma, joka annettuna käyttäjän väärinkirjoitetun sanan ehdottaa sille oikeinkirjoitusta. 
Tälläinen ohjelma voidaan toteuttaa tallettamalla mahdollisia sanoja itse toteutettuun [trie-tietorakenteeseen](https://en.wikipedia.org/wiki/Trie) ja 
vertaamalla käyttäjän väärinkirjoitetun merkkijonon etäisyyttä oikein kirjoitettuihin sanoihin. 
Yksi tähän soveltuva etäisyysmitta on [Damerau–Levenshtein -etäisyys](https://en.wikipedia.org/wiki/Damerau%E2%80%93Levenshtein_distance). 

### Tieteellinen laskin
Toteuta laskin joka laskee annetun matemaattisen lausekkeen arvon, ja mahdollisesti sijoittaa sen muuttujaan, joita on käytettävissä riittävä määrä. Lauseke voi sisältää lukuarvoja, muuttujia, peruslaskutoimituksia ja sekä yhden (sqrt, sin) että kaksi parametria (min, max) saavia funktioita. Ohjelman tulisi antaa yksilöity virheilmoitus, jos käyttäjä syöttää virheellisen lausekkeen, ja erityisesti se ei saa ilmoittaa mitään arvoa lausekkeelle, jolle ei oikeasti voi laskea arvoa.  Tälläinen ohjelma toteutetaan [shunting-yard](https://en.wikipedia.org/wiki/Shunting-yard_algorithm) algoritmilla.

{% include typo_instructions.md %}

[^1]: **Huomaa**, että lopullinen päätösvalta kunkin aiheen hyväksyttävyydellä on kurssin henkilökunnalla. Omaa aihe ehdotustasi joudutaan ehkä muokkaamaan jotta päästään kurssin vaatimaan vaativuuteen. 
[^2]: Muista kuitenkin, että ohjaaja auttaa tiedonhaussa tarvittaessa, yritä ensin itse ja ota sitten yhteyttä matalalla kynnyksellä. 
[^3]: Kuvien tuottaminen on tälle kursille liian haastava aihe. 



