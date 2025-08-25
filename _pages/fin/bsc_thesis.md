---
layout: page
permalink: /bscthesis-fi
title: Algolabra ja Kandidaatin Tutkielma
title_long: Kandi
lang: fi # fi or en
ref: bsc_thesis # same as the markdown filename
---

## Harjoitustyö kanditutkielman perustana
Monet harjoitustyön mahdollisista [aiheista]({% link _pages/fin/topics.md %}) soveltuvat mainiosti myös 
kanditutkielman aiheeksi. Toteuttamastasi algoritmista (tai sen laajennuksista) voi usein kirjoittaa kandintutkielman. Suosittelemmekin vahvasti harkitsemaan sellaisen harjoitustyön aiheen valitsemista, jonka voi laajentaa tutkielmaksi. 

## Sivuhuomio: Kokeellinen osio kandidaatintutkielmassa
Useimmissa tapauksissa kandiseminaarin laajuus ei riitä implementoimaan ja kokeilemaan algoritmeja käytännössä osana kandiasi. Kuitenkin, mikäli kirjoitat tutkielman harjoitustyösi aiheesta, voit mahdollisesti sisällyttää siihen kokeellisen osion jossa kokeilet harjoitustyösi tehokkuutta ja raportoit kokeiden tuloksista.
Muista kuitenkin, että kandityön pitää edelleen kytkeytyä vahvasti tutkimuskirjallisuuteen myös kokeiden osalta, mm. kuvata ja perustella testattava asia kirjallisuuden perusteella, samoin suunnitella testit sen perusteella, ja tulosten raportoinnissa verrata tuloksia kirjallisuuten sekä pohtia ja tehdä johtopäätöksiä kirjallisuudesta saatavaa tietoa hyväksi käyttäen, esim. mistä tulokset johtuvat ja mitä ne kertovat.

Mikäli sinua kiinnostaa sisällyttää jonkinlainen kokeellinen osio, suosittelemme jonkin verran miettimään näitä asioista jo suunnitellessasi harjoitustyötäsi. Mieti minkälaista dataa harjotustyönäsi toteuttamasi ohjelmastasi pitää saada jotta voit myöhemmin ajaa systemaattisia, tieteellisiä, kokeita. 

## Harjoitustyön aiheet kanditutkielman aiheina

Alla vapaamuotoisia ajatuksia harjoitustyön aiheiden soveltuvuudesta tutkielman aiheiksi. **Haluamme kuitenkin painottaa**, että tällä sivulla olevia ajatuksia ei pidä nähdä takuina hyväksyttävistä kandiaiheista, Kandidaatintutkielmakurssin henkilökunnalla on lopullinen päätösvalta tutkielmien aiheista ja niiden rajauksista. Harjoitustyön henkilökunta on kuitenkin myös ohjannut tutkielmia ja tämän sivun näkemykset perustuvat siihen kokemukseen. Eli ts. jos valitset tällä sivulla mainitun aiheen ja teet siitä hyväksyttävän harjoitustyön, niin melko todennäköisesti voit tutkielmavaiheessa sopia tutkielman ohjaajan kanssa siihen liittyvästä tutkielma-aiheesta. Toisaalta, tälläisen aiheen valitseminen harjotustyösi aiheeksi ei sitouta mihinkään tutkielma-aiheeseen. 

Alla oleva olettaa, että olet tutustunut [aihe sivujen]({% link _pages/fin/topics.md %}) vastaaviin osioihin. Nyrkkisääntönä mainittakoon, että ollakseen sopiva tutkielman aihe, toteuttamastasi algoritmista (tai siihen liittyvistä asioista) täytyy löytyä myös tieteellisiä julkaisuja joihin mahdollinen tutkielmasi voi kytkeytyä. 


### Verkot ja polunetsintä
Voidaksesi kirjoittaa [polunetsinnästä]({% link _pages/fin/topics.md %}#verkot-ja-polunetsintä) 
kanditutkielmassasi, kannattaa varmistaa, että toteuttamistasi algoritmeista löytyy myös tieteellisiä julkaisuja, eikä vaan esim. oppikirjoja. Soveltuvia algoritmeja on ainakin Jump Point Search tai sitä haastavampi. Yksi mahdollisuus voi olla harjoitustyössä toteuttaa JPS, ja sitten kanditutkielmassa kirjoittaa siitä ja [Fringe Search](https://webdocs.cs.ualberta.ca/~holte/Publications/fringe.pdf) algoritmista vaikka et fringe searchia harjoitustyössäsi toteuttaisikaan. Toisaalta esimerkiksi A* ja Dijkstra ovat pääsääntöisesti liian yksinkertaisia kandiaiheiksi, ja niistä on vaikea löytää tieteellisiä viitteitä. 

### Tiedon tiivistys
[Esimerkkiaiheissa]({% link _pages/fin/topics.md %}#tiedon-tiivistys) mainitut Lempel-Ziv -algoritmit ovat hieman vanhoja, mutta periaatteessa mahdollisia tutkielman aiheita, varsinkin jos niiden lisäksi kirjoitat tutkielmassasi jostain uusistakin metodeista.

Voidaksesi sisällyttää tiedon tiivistykseen liittyvään kanditutkielmaasi kokeellisen osion, suosittelemme toteuttamaan harjoitustyön tekstin pakkauksesta, koska siitä on helpompi suunnitella kokeita kuin kuvan tai äänen pakkauksesta. 

### Pelit
Pelkkä Minimax-algoritmi alpha-beta-karsinnalla on pääsääntöisesti liian yksinkertainen kandiaiheeksi. 
Sen laajennuksista, kuten esimerkiksi [ProbCut](https://journals.sagepub.com/doi/abs/10.3233/ICG-1995-18202) algoritmista voi olla mahdollista kirjoittaa tutkielman. 
Pelitekoäly harjoitustyön aiheena on kuitenkin haastava laajentaa kanditutkielmaksi. 


### DPLL
[DPLL]({% link _pages/fin/topics.md %}#dpll) algoritmista, tai nykyisin laajemmin käytetystä CDCL algoritmista saa helposti kandiaiheita. Jos haluat sisällyttää DPLL aiheiseen kandidaatintutkielmaan kokeellisen osion, kannattaa harjoitustyöshösi toteuttaa esimerkiks imonia eri heuristiikkoja joiden tehokkuutta voi sitten verrata. 


### Koneoppiminen 
[Koneoppiminen]({% link _pages/fin/topics.md %}#koneoppiminen) on erittäin laaja aihepiiri josta löytyy paljon kanditutkielmaan sopivia aiheita. Yleisenä ohjeena mainittakoon, että jos haluat laajentaa koneoppimisaiheisen harjoitustyön kanditutkielmaksi jossa on kokeellinen osio, sinun kannattaa valita sellainen aihe, jonka tehokkuutta on helppo mitata. Vaikka esim. "kivaa" musiikkia tuottava ohjelma on täysin sopiva harjoitustyön aiheeksi, kandin kokeelliseen osioon se ei oikein kelpaa koska musiikin "kivuutta" on vaikea mitata objektiivisesti. Parempi aihe on esim. itse toteutettu neuroverkko joka klassifioi käsin kirjoitettuja numeroita koska sen tarkkuutta voi mitata ja sen raportoida tarkasti. 

### Luolastojen generointi
[Luolastojen generointi]({% link _pages/fin/topics.md %}#luolastojen-generointi) harjoitustyönä ei ole 
paras mahdollinen aihe kanditutkielman pohjaksi. Jossain tapauksissa, luolastoja generoivan harjoitustyön käyttämät algoritmit voivat abstraktilla tasolla soveltua tutkielman aiheiksi, kunhan niistä löytyy tieteellisiä julkaisuja. Muista myös, että mahdollisessa tutkielman kokeellisessa osuudessa et oikein voi mitata tuottamasi luolastojen "kauneutta", suunnittele harjoitustyösi niin, että saat työkalusta tarvittaessa ulos muutakin dataa. 


### Salaus ja tietoturva
[Salaukseen]({% link _pages/fin/topics.md %}#salaus-ja-tietoturva) ja esim. alkulukujen etsintään käytettävistä algoritmeista voi monissa tapauksissa hyvin kirjoittaa 
kandidaatin tutkielman. Harjoitustyöhön sopivat salauksen murtajat ovat pääsääntöisesti liian helppoja kanditutkielman aiheiksi. 

### Signaalinkäsittely (kuva, ääni)
[Signaalinkäsittelyn]({% link _pages/fin/topics.md %}#signaalinkäsittely-kuva-ääni) tekniikoista, tai esimerkiksi [nopeasta fourier-muunnoksesta](https://en.wikipedia.org/wiki/Fast_Fourier_transform) voi kirjoitta kandidaatin tutkielman. Jos kokeellisen osuuden sisällyttäminen kiinnostaa, kannattaa tämä ottaa huomioon harjoitustyön suunnittelussa ja varmistaa, että työkalusta saa ulos myös kvantitatiivista dataa tuotettujen metodien tehokkuudesta. 

### Kontin pakkaus
[Kontin pakkaus]({% link _pages/fin/topics.md %}#kontin-pakkaus) harjotustyöaiheen perustana on ns. [knapsack](https://en.wikipedia.org/wiki/Knapsack_problem) ongelma, yksi klassista NP-vaikeista ongelmista. Tälläisistä ongelmista voi saada tutkielman aiheen, mutta tarkasta rajauksesta kannattaa keskustella tutkielman ohjaajan kanssa. Ts. tämä on mahdollinen, muttei kaikkein selkein aihe kanditutkielmaksi. 

### Säännöllisten lausekkeiden tulkki tai kääntäjä

[Säännölliset lausekkeet](({% link _pages/fin/topics.md %}#säännöllisten-lausekkeiden-tulkki-tai-kääntäjä))
kuuluvat kandikurssien aiheisiin, joten mahdollisia kanditutkielmia tästä aiheesta pitänee jonkin verran laajentaa. Ts. tämäkin on mahdollinen, muttei kaikkein selkein kanditutkielman aihe. 


 
{% include typo_instructions_fin.md %}




