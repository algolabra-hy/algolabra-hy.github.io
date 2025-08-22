---
layout: page
permalink: /bscthesis-en
title: AI Project and the BSc. Thesis
title_long: Kandi
lang: en # fi or en
ref: bsc_thesis # same as the markdown filename
---
## Note 
This is just a copy of the Finnish page for now. it will get translated when approved.


## Harjoitustyö kanditutkielman perustana
Monet harjoitustyön mahdollisista [aiheista]({% link _pages/fin/topics.md %}) soveltuvat mainiosti myös 
kanditutkielman aiheeksi. Toteuttamastasi algoritmista (tai sen laajennuksista) voi usein kirjoittaa kandintutkielman. Joissain tapauksissa harjoitustyössä tekemäsi ohjelman avulla voit sisällyttää tutkielmaasi myös kokeellisen osion, jossa kokeilet ohjelmasi tehokkuutta. Suosittelemme vahvasti harkitsemaan sellaisen harjoitustyön aiheen valitsemista, jonka sitten voi laajentaa tutkielmaksi. Alla vapaamuotoisia ajatuksia harjoitustyön aiheiden soveltuvuudesta tutkielman aiheiksi. **Haluamme kuitenkin painottaa**, että 
tällä sivulla olevia ajatuksia ei pidä nähdä takuina hyväksyttävistä kandiaiheista, Kandidaatintutkielmakurssin henkilökunnalla on lopullinen päätösvalta tutkielmien aiheista ja niiden rajauksista. Harjoitustyön henkilökunta on kuitenkin myös ohjannut tutkielmia ja tämän sivun näkemykset perustuvat siihen kokemukseen. Eli ts. jos valitsen tällä sivulla mainitun aiheen ja teet siitä hyväksyttävän harjoitustyön, niin melko todennäköisesti voit sitten tutkielmavaiheessa sopia tutkielman ohjaajan kanssa siihen liittyvästä tutkielma-aiheesta. Toisaalta, tälläisen aiheen valitseminen harjotustyösi aiheeksi ei sitouta mihinkään tutkielma-aiheeseen. 

Alla oleva olettaa, että olet tutustunut [aihe sivujen]({% link _pages/fin/topics.md %}) vastaaviin osioihin. Nyrkkisääntönä mainittakoon, että ollakseen sopiva tutkielman aihe, toteuttamastasi algoritmista (tai siihen liittyvistä asioista) täytyy löytyä myös tieteellisiä julkaisuja. 


### Verkot ja polunetsintä
Voidaksesi käyttää [polunetsintä]({% link _pages/fin/topics.md %}#verkot-ja-polunetsintä) aiheista harjotustyötäsi kanditutkielmassa kannattaa varmistaa, että valitsemistasi algoritmeista löytyy myös tieteellisiä julkaisuja, eikä vaan esim. oppikirja tekstiä. Soveltuvia algoritmeja on ainakin Jump Point Search tai sitä haastavampi. Yksi mahdollisuus voi olla harjoitustyössä toteuttaa JPS, ja sitten tutkielmassa kirjoittaa siitä ja [Fringe Search](https://webdocs.cs.ualberta.ca/~holte/Publications/fringe.pdf) algoritmista vaikka et fringe searchia toteuttaisikaan. Toisaalta esimerkiksi A* ja Dijkstra ovat pääsääntöisesti liian yksinkertaisia kandiaiheiksi, ja niistä on vaikea löytää tieteellisiä viitteitä. 

### Tiedon tiivistys
[Esimerkkiaiheissa]({% link _pages/fin/topics.md %}#tiedon-tiivistys) mainitut Lempel-Ziv -algoritmit ovat hieman vanhoja, mutta periaatteessa mahdollisia tutkielman aiheita, varsinkin jos niiden lisäksi kirjoitat tutkielmassasi jostain moderneistakin metodeista.

Voidaksesi käyttää tiivistysaiheeseen liittyvää harjoitustyötäsi kanditutkielman kokeellisessa osiossa suosittelemme valitsemaan tekstin pakkauksen koska siitä on helpompi suunnitella empiirisiä kokeita tutkielmaan. 

### Pelit
Pelkkä Minimax-algoritmi alpha-beta-karsinnalla on pääsääntöisesti liian yksinkertainen kandiaiheeksi. Sitä voi kuitenkin mahdollisesti laajentaa tekniikoilla joita ei harjoitustyössä käsitellä, kuten esimerkiksi tehdään ns. [ProbCut](https://journals.sagepub.com/doi/abs/10.3233/ICG-1995-18202) algoritmilla. 
Pelitekoäly harjoitustyönä voi kuitenkin olla haastava laajentaa kandiksi. 


### DPLL
[DPLL]({% link _pages/fin/topics.md %}#dpll) algoritmista, tai nykyisin laajemmin käytetystä CDCL algoritmista saa helposti kandiaiheita. Jos haluat käyttää DPLL aiheista harjoitustyötä kandin kokeellisessa osuudessa kannattaa implementoida monia eri heuristiikkoja joiden tehokkuutta on helppo verrata. 


### Koneoppiminen 
[Koneoppiminen]({% link _pages/fin/topics.md %}#koneoppiminen) on erittäin laaja aihepiiri josta löytyy paljon kanditutkielmaan sopivia aiheita. Yleisenä ohjeena mainittakoon, että jos haluat laajentaa koneoppimisaiheisen harjoitustyön kanditutkielmaksi jossa on kokeellinen osio, sinun kannattaa valita sellainen aihe, jonka tehokkuutta on helppo mitata. Vaikka esim. "kivaa" musiikkia tuottava ohjelma on täysin sopiva harjoitustyön aiheeksi, kandin kokeelliseen osioon se ei oikein kelpaa koska "kivuutta" on vaikea mitata objektiivisesti. Parempi aihe on esim. itse toteutettu neuroverkko joka klassifioi käsin kirjoitettuja numeroita koska sen tarkkuuden voi ilmaista tarkasti. 

### Luolastojen generointi
[Luolastojen generointi]({% link _pages/fin/topics.md %}#luolastojen-generointi) ei ehkä ole 
paras mahdollinen aihe kanditutkielman pohjaksi. Jossain tapauksissa, luolastoja generoiva harjoitustyön käyttämät algoritmit voivat abstraktilla tasolla soveltua tutkielman aiheiksi, kunhan niistä löytyy tieteellisiä viitteitä. Muista myös, että mahdollisessa tutkielman kokeellisessa osuudessa et oikein voi mitata tuottamasi luolastojen "kauneutta", suunnittele harjoitustyösi niin, että saat työkalusta tarvittaessa ulos muutakin dataa. 


### Salaus ja tietoturva
[Salaukseen]({% link _pages/fin/topics.md %}#salaus-ja-tietoturva) ja esim. alkulukujen etsintään käytettävistä algoritmeista voi monissa tapauksissa hyvin kirjoittaa 
kandidaatin tutkielman. Harjoitustyöhön sopivat salauksen murtajat ovat pääsääntöisesti liian helppoja kanditutkielman aiheiksi. 

### Signaalinkäsittely (kuva, ääni)
[Signaalinkäsittelyn]({% link _pages/fin/topics.md %}#signaalinkäsittely-kuva-ääni) tekniikoista, tai esimerkiksi [nopeasta fourier-muunnoksesta](https://en.wikipedia.org/wiki/Fast_Fourier_transform) voi kirjoitta kandidaatin tutkielman. Jos kokeellinen osuus kiinnostaa, kannattaa tämä ottaa huomioon harjoitustyön suunnittelussa ja varmistaa, että työkalusta saa ulos myös kvantitatiivista dataa tuotettujen metodien tehokkuudesta. 

### Kontin pakkaus
[Kontin pakkaus]({% link _pages/fin/topics.md %}#kontin-pakkaus) harjotustyöaiheen perustana on ns. [knapsack](https://en.wikipedia.org/wiki/Knapsack_problem) ongelma, yksi klassista NP-vaikeista ongelmista. Tälläisistä ongelmista voi saada tutkielman aiheen, mutta tarkasta rajauksesta kannattaa keskustella tutkielman ohjaajan kanssa. Ts. tämä on mahdollinen, muttei kaikkein selkein aihe kanditutkielman näkökulman kannalta. 

### Säännöllisten lausekkeiden tulkki tai kääntäjä

[Säännölliset lausekkeet](({% link _pages/fin/topics.md %}#säännöllisten-lausekkeiden-tulkki-tai-kääntäjä))
kuuluvat kandikurssien aiheisiin, joten mahdollisia kanditutkielmia tästä aiheesta pitänee jonkin verran laajentaa.Ts. tämäkin on mahdollinen, muttei kaikkein selkein harjoitustyön aihe kanditutkielman laajennuksen kannalta. 


 
{% include typo_instructions_fin.md %}




