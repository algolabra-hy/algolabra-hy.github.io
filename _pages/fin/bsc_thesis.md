---
layout: page
permalink: /bscthesis-fi
title: Algolabra ja kandidaatin tutkielma
title_long: Kandi
lang: fi # fi or en
ref: bsc_thesis # same as the markdown filename
---

## Tärkeää
Tällä sivulla on tietoa siitä, miten harjoitustyösi voi toimia kanditutkielman aiheen pohjana. **Haluamme kuitenkin painottaa**, että sivulla esitettyjä ajatuksia ei tule tulkita takuiksi hyväksyttävistä kandiaiheista. Kaikki tutkielmien aiheita ja rajauksia koskevat päätökset tekee tutkielmakurssin henkilökunta. Näiden sivujen näkemykset perustuvat harjoitustyökurssin henkilökunnan kokemukseen tutkielmien ohjaamisesta.
Toisin sanoen: jos valitset tällä sivulla mainitun aiheen ja toteutat siitä hyväksyttävän harjoitustyön, voit tutkielmavaiheessa melko todennäköisesti sopia ohjaajan kanssa siihen liittyvästä tutkielma-aiheesta. Toisaalta, aiheen valitseminen harjoitustyöhön ei sido sinua mihinkään tiettyyn kanditutkielman aiheeseen. Sinun pitää myös itsenäisesti kertoa tutkielmakurssin henkilökunnalle kiinnostuksesta jatkaa labraan liittyvän aiheen parissa. 

## Harjoitustyö kanditutkielman tukena
Monet mahdolliset [harjoitustyöaiheet]({% link _pages/fin/topics.md %}) soveltuvat myös kanditutkielman aiheiksi. Koska harjoitustyössäsi joudut joka tapauksessa syventymään valitsemasi [ydinalgoritmin]({% link _pages/fin/documentation.md %}#määrittelydokumentti) toimintaan, voit myöhemmin hyödyntää tätä ymmärrystä ja kirjoittaa tutkielmasi samasta aihepiiristä. Suosittelemme vahvasti harkitsemaan sellaista harjoitustyön aihetta, jonka voi laajentaa tutkielmaksi.

Hyvin toteutettu harjoitustyö voi myös tarjota mahdollisuuden sisällyttää kanditutkielmaan kokeellisen osion. Kokeellisessa osiossa voit esimerkiksi käyttää harjoitustyötäsi algoritmin toiminnan mittaamiseen kandityössä asettamasi tutkimustavoitteen mukaisesti. Sovi kuitenkin kokeellisen osion tarkasta sisällöstä tutkielman ohjaajan kanssa. Huomaa myös, että kandiseminaarin laajuus ei yleensä riitä algoritmien toteuttamiseen ja kokeilemiseen osana itse tutkielmaa. Jos haluat sisällyttää tutkielmaasi kokeellisen osuuden, kannattaa käyttää hyväksesi harjoitustyön tarjoamaa pohjaa.

## Harjoitustyön aiheet kanditutkielmina
Alla on vapaamuotoisia ajatuksia siitä, miten harjoitustyön aiheet voivat soveltua kanditutkielman aiheiksi. Oletamme, että olet perehtynyt myös [aihesivujen]({% link _pages/fin/topics.md %}) vastaaviin osioihin. Yleisenä nyrkkisääntönä: jotta aihe olisi sopiva kanditutkielmaan, toteuttamastasi algoritmista (tai siihen liittyvistä menetelmistä) tulee löytyä tieteellisiä julkaisuja, jotka voivat toimia tutkielmasi lähteinä. Kokeellisen osuuden motivointi, suunnittelu ja analysointi sidotaan tutkimuskirjallisuuteen ja osaksi aiheen tutkimusta. Mahdollisen kokeellisen osuuden tehtävä on tuottaa tietoa algoritmista tai vastaavasta osana tutkielmaa, ei olla sen pääsisältö.

### Verkot ja polunetsintä
Jos haluat kirjoittaa [polunetsinnästä]({% link _pages/fin/topics.md %}#verkot-ja-polunetsintä) kanditutkielmassasi, varmista että toteuttamistasi algoritmeista löytyy tieteellisiä julkaisuja, ei pelkästään oppikirjoja. Soveltuvia algoritmeja ovat esimerkiksi Jump Point Search (JPS) tai sitä haastavammat menetelmät. Mahdollinen etenemistapa on toteuttaa harjoitustyössä JPS ja käsitellä kanditutkielmassa sekä JPS:ää että esimerkiksi [Fringe Search](https://webdocs.cs.ualberta.ca/~holte/Publications/fringe.pdf) algoritmia, vaikka et toteuttaisi jälkimmäistä harjoitustyössäsi. Sen sijaan perusmenetelmät kuten A* ja Dijkstran algoritmi ovat yleensä liian yksinkertaisia kandiaiheiksi, ja niistä on vaikea löytää tieteellisiä viitteitä.

### Tiedon tiivistys
[Esimerkkiaiheissa]({% link _pages/fin/topics.md %}#tiedon-tiivistys) mainitut Lempel–Ziv-algoritmit ovat mahdollisia kandiaiheita. Koska ne ovat hieman vanhempia, niistä kertoviin viitteisiin tutustuminen voi vaatia hieman enemmän aikaa. 

Jos haluat sisällyttää kanditutkielmaasi tiedon tiivistykseen liittyvän kokeellisen osion, suosittelemme toteuttamaan harjoitustyön tekstin pakkauksesta. Tekstiaineistolla kokeiden suunnittelu ja mittaaminen on yleensä helpompaa kuin kuva- tai äänipakkauksessa.

### Pelit
Pelkkä minimax-algoritmi alpha-beta-karsinnalla on pääsääntöisesti liian yksinkertainen kandiaiheeksi. Sen laajennuksista, kuten esimerkiksi [ProbCut](https://journals.sagepub.com/doi/abs/10.3233/ICG-1995-18202) algoritmista, voi sen sijaan olla mahdollista kirjoittaa tutkielma. Pelitekoäly harjoitustyön aiheena voi kuitenkin olla haastava laajentaa selkeästi rajatuksi kanditutkielmaksi.

### DPLL
[DPLL]({% link _pages/fin/topics.md %}#dpll)-algoritmista tai nykyisin laajemmin käytetystä CDCL:stä saa varsin helposti kandiaiheita. Jos haluat sisällyttää DPLL-aiheiseen kanditutkielmaan kokeellisen osion, kannattaa harjoitustyössä toteuttaa esimerkiksi useita erilaisia heuristiikkoja, joiden tehokkuutta voi vertailla kokeissa.

### Koneoppiminen
[Koneoppiminen]({% link _pages/fin/topics.md %}#koneoppiminen) on erittäin laaja aihealue josta löytyy sekä kanditutkielman aiheeksi sopivia, että liian vaikeita aiheita. Mikäli tälläinen aihe kiinnostaa myös tutkielmassa, kannattaa harjoitustyössä miettiä selkeitä, ja melko suoraviivaisia aiheita. Esimerkiksi "hyvän kuuloista musiikkia" tuottava ohjelma ei oikeen sovi aiheeksi koska musiikin "hyvyyttä" on vaikea mitata oobjektiivisesti ja musiikkia tuottavat algoritmit voivat joissain tapauksissa olla liian monimutkaisia tutkielman aiheeksi. Parempi aihe on itse toteutettu neuroverkko, joka luokittelee käsin kirjoitettuja numeroita – sen tarkkuutta voidaan mitata ja raportoida täsmällisesti. Yhteenvetona siis mainittakoon, että koneoppiminen on mahdollinen tutkielman aihe, mutta sen tarkasta rajuksesta pitää jutella sitten tutkielman ohjaajan kanssa. 

### Luolastojen generointi
[Luolastojen generointi]({% link _pages/fin/topics.md %}#luolastojen-generointi) ei ole paras mahdollinen pohja kanditutkielmalle. Joissain tapauksissa harjoitustyössä käytetyt algoritmit voivat kuitenkin abstraktilla tasolla soveltua tutkielman aiheiksi, kunhan niistä löytyy tieteellisiä julkaisuja. Muista, että mahdollisessa kokeellisessa osiossa et voi mitata tuottamiesi luolastojen ”kauneutta”; suunnittele harjoitustyösi niin, että saat työkalusta tarvittaessa ulos myös muuta numeerista dataa.

### Salaus ja tietoturva
[Salaukseen]({% link _pages/fin/topics.md %}#salaus-ja-tietoturva) ja esimerkiksi alkulukujen etsintään käytettävistä algoritmeista voi monissa tapauksissa kirjoittaa kanditutkielman. Harjoitustyöhön sopivat ”salauksen murtajat” ovat sen sijaan yleensä liian yksinkertaisia kandiaiheiksi.

### Signaalinkäsittely 
[Signaalinkäsittelyn]({% link _pages/fin/topics.md %}#signaalinkäsittely-kuva-ääni) tekniikoista pystyy muodostamaan tutkielman aiheita. Tässä pitää kuitenkin olla tarkkana, että aiheestasi löytyy myös tieteellisiä julkaisuja. Vaikka voit harjoitustyössäsi toteuttaa esim. [nopean fourier-muunnoksen](https://en.wikipedia.org/wiki/Fast_Fourier_transform) jotain sopivaa oppikirjaa seuraten, tutkielmassasi täytyy olla myös lähteitä jotka eivät ole oppikirjoja. 


### Kontin pakkaus
[Kontin pakkaus]({% link _pages/fin/topics.md %}#kontin-pakkaus)-aiheen taustalla on niin sanottu [knapsack](https://en.wikipedia.org/wiki/Knapsack_problem)-ongelma, yksi klassisista NP-vaikeista ongelmista. Tällaisista ongelmista voi muodostaa kandiaiheen, mutta tarkasta rajauksesta kannattaa keskustella tutkielman ohjaajan kanssa. Toisin sanoen: aihe on mahdollinen, muttei välttämättä kaikkein selkein valinta kanditutkielmaksi.

### Säännöllisten lausekkeiden tulkki tai kääntäjä
[Säännölliset lausekkeet]({% link _pages/fin/topics.md %}#säännöllisten-lausekkeiden-tulkki-tai-kääntäjä) kuuluvat kandikurssien perussisältöön, joten mahdollisia kanditutkielmia tästä aiheesta on hyvä laajentaa riittävästi. Myös tämä on mahdollinen, vaikkei välttämättä kaikkein selkein kandiaihe ilman huolellista rajausta.

 
{% include typo_instructions_fin.md %}




