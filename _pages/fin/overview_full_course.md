---
layout: page
permalink: /overview-fi
title: Yleiskatsaus harjoitustyöstä
title_long: Yleiskatsaus harjoitustyön kulusta
lang: fi # fi or en
ref: overview_full_course # same as the markdown filename
inheader: no
---

Alla yleiskatsaus kurssin kulusta. Kaikista tällä sivuilla käsitellyistä aiheista löytyy 
tarkempaa tietoa materiaalin muista osista. 

Kurssilla opiskelija toteuttaa ohjelman, joka ratkaisee jonkin ohjelmointiongelman. Ongelmanratkaisuun käytetään sopivia tehokkaita algoritmeja ja tietorakenteita. Aihe on vapaa, kunhan ratkaisussa on tarpeeksi algoritmista vaativuutta. Käytännössä tämä tarkoittaa kirjallisuuteen perustuvien algoritmien käyttämistä, jotta tiedetään algoritmin olevan tarkoitukseen soveltuva ja tuottavan halutun tuloksen.
Relevantin kirjallisuuden etsiminen ja siihen tutustuminen---tarvittaessa kurssin henkilökunnan avustuksella---on oleellinen (ja aikaa vievä) osa harjoitustyötä. 

### Aiheen valinnasta 
[Aihe ehdotuksista]({% link _pages/fin/topics.md %}) löytyy ehdotuksia harjoitustyön sopivista aiheista. Näiden lisäksi,
opiskelijat voivat---periaatteessa---valita harjoitustyönsä aiheen itse. 
Algoritmit, jotka on opittu kurssilla “Tietorakenteet ja Algoritmit” tai sitä edeltävillä ohjelmointikursseilla, ovat tämän kurssin esitietoa, eivätkä siten voi olla projektin oleellista sisältöä. Tämän lisäksi harjoitustyön toteutuksen tulee 
olla käytettävissä jonkin algoritmin soveltamiseen käytännön tilanteessa. Tämä toteutuu kaikissa kurssimateriaalin aihe-ehdotuksissa.

Jos valitset täysin oman aiheen, tai aihe-ehdotuksesi ei ole yksityiskohtainen, sovi tapaaminen ohaajan kanssa jo ensimmäisellä viikolla, ennen määrittelydokumentin palautusta, jotta voitte sopia, miten aihe kannattaa rajata, ja mitkä osat aiheesta sinun tulee toteuttaa itse, jotta harjoitustyölle saavutetaan vaadittu laajuus.

### Ohjelmointikielen valinnasta
Harjoitustyössä käytettävä ohjelmointikieli on---periaatteessa---vapaasti valittavissa.
Useimissa aiheissa voidaan käyttää mitä tahansa ohjelmointikieltä. 
Kuitenkin esimerkiksi tietorakennevertailu on aihe, joka ei ole mielekäs muuten kuin laiteläheisellä (C, C++) kielellä  toteutettuna. Muuten voidaan päätyä mittaamaan tietorakenteiden erojen sijasta enemmänkin käytetyn ohjelmointikielen välineiden valintaa tai tehokkuutta. 

Lähtökohtaisesti sinun kannattaa käyttää kieltä, jonka osaat parhaiten. *Uutta kieltä* ei ole hyvä alkaa projektin yhteydessä opettelemaan, koska harjoitustyön aiheen omaksumisessa on opittavaa tarpeeksi.

Python on monessa mielessä paras valinta ohjelmointikieleksi, mikäli osaat sitä riittävästi. 
Useimmat kurssilaiset tekevät projektin Pythonilla, ja moni ei tunne muita kieliä. Siksi kurssin ohjeet painottuvat Pythoniin. 
Jos käytät Pythonia, saat luultavasti vertaisarvioinneissa tutkittavaksi projekteja, joissa on sama tai vastaava aihe kuin itselläsi. Saat yleensä myös itse vertaispalautetta joltain, joka tuntee aiheesi ja ohjelmointikielesi. 
Vertaisarvioita jaettaessa hyödynnetään opiskelijoiden antamia tietoja osaamistaan kielistä, mutta perusjako on, että Pythonia käyttävät arvioivat toisiaan, ja kaikki muut taas toisiaan kielestä riippumatta.

Huomaa, että automaattinen [testaus]({% link _pages/fin/testing_frontpage.md %}) ja testikattavuuden laskenta ovat pakollista kaikissa projekteissa, kielestä riippumatta. Tästä ei ole [kurssimateriaalissa]({% link _pages/fin/unit_testing.md %}) ohjeita muille kielille kuin Pythonille, eikä ohjaajakaan välttämättä  osaa neuvoa. Täten, mikäli valitsen jonkun muun kielen, joudut ottamaan enemmän vastuuta näiden asioiden omaksumisesta. 
Kunhan hallitset ohjelmistokehitykseen tarvittavat välineet omassa kielessäsi, saat kuitenkin ohjaajalta tuen toteutettavien algoritmien ymmärtämisessä ja toteutuksen virheiden jäljityksessä. Virheiden etsintä tapahtuu joka tapauksessa enimmäkseen yhdessä ohjaajan kanssa esim. Zoomissa, ei niin että ohjaaja tutkii oma-aloitteisesti koodiasi.

Kurssin tavoite on oppia toteuttamaan itse tietorakenteita ja algoritmeja, jotka eivät sisälly kurssin esitietoihin. Lähinnä toteutetaan algoritmeja, mutta osassa suppeammista aiheista vaaditaan myös tietorakenteiden 
omaa toteuttamista. Tälläisissä aiheissa suosittelemme, että laitat ensin kuntoon oman harjoitustyön [ytimen]({% link _pages/fin/documentation.md %}#määrittelydokumentti)
käyttäen kielen standardikirjastojen valmiita tietorakenteita ja algoritmeja. Kun ohjelma toimii oikein, voit sitten korvata valmiit tietorakenteet omilla toteutuksilla.

Jokaisessa harjoitustyössä saa käyttää kielen alkeistyyppien matemaattisia funktioita ja merkkijonojen funktioita,

### Harjoitustyön testaamisesta 
Ohjelman toiminnan oikeellisuuden testaaminen on olennaisen tärkeää, kun käytetään vaativia algoritmeja. Täytyy tutkia tuottaako algoritmi oikean tuloksen, ja toimiiko algoritmi myös niin tehokkaasti kuin sen tulisi. Oikeellisuustestaus tehdään automaattisin yksikkötestein, joita laaditaan projektin alusta asti sitä mukaa, kun testattavaa koodia syntyy. Yleisohje testaamiseen (m.m sen vaatimuksista) löytyy [testaus]({% link _pages/fin/testing_requirements.md %}) sivulta. 

### Käyttöliittymästä
Käyttöliittymä ei ole keskeisin asia kurssilla, mutta toimiva käyttöliittymä on tärkeä olla alusta asti.
Sovelluksen tulee tuottaa tuloste (teksti, kuva, ääni, muu tiedosto), josta on helppo havaita ohjelman toimivan oikein.
Mitä tämä tarkalleen tarkoittaa, riippuu työn aiheesta. Joissakin tapauksessa pelkät komentorivin käynnistysparametrit ovat riittävä tapa kommunikoida ohjelman kanssa. Yleensä kuitenkin tarvitaan ainakin valikko-ohjaus komentoriviltä ja ASCII grafiikka. Usein myös selkeä visualisointi on välttämätön jo ohjelman kehitysvaiheessa, jotta näkee toimiiko ohjelma oikein. Graafisenkin käyttöliittymän koodaamiseen kuluva aika voi säästyä harjoitustyön kehitys- / testausvaiheessa, jos siitä on ennestään kokemusta, tai jos joutuu paljon kokeilemaan ohjelmaa erilaisilla parametrien arvoilla yms., vaikkapa valitsemaan pisteitä kartalta. 

Käyttöliittymän kehityksessä saa käyttää mitä tahansa valmiita välineitä. Käyttöliittymää ei tarvitse testata, eikä sen testaamisesta saa harjoitustyön arvostelussa lisäpisteitä.

### Aikataulusta
Kurssin [aikataulu]({% link _pages/fin/suggested_schedule.md %}) on tiukka. Suunnittele ajankäyttösi niin, että voit käyttää suurimman osan ajastasi harjoitustyösi [*ytimen*]({% link _pages/fin/documentation.md %}#määrittelydokumentti) kehitykseen. 
- Älä käytä esimerkiksi käyttöliittymän kehitykseen enempää aikaa, kuin mitä tarvitset ymmärtääksesi ohjelman kulkua. 
- **Esim.** jos teet shakkibottia, shakkipelin siirtojen generoinnin pitäisi olla valmis toisen viikon aikana.   

Kurssilla ei juurikaan ole aikaa tehdä asioita, jotka eivät edistä harjoitustyötä. Varmista siis, että 
et käytä aikaa sellaisten asioiden kehitykseen, jotka eivät kuulu omaan aiheeseesi. 

  - 3 kertaa 3 ristionollan kehitys ei edistä isomman pelin kehitystä koska
      useimmat haasteet ilmaantuvat vasta kun siirryt isompiin lautoihin. 
  - Polunetsinnän graaffisen käyttöliittymän hienosäätö ei edistä harjoitustyötä koska sen ydin on polunetsintä algoritmit,
  - Kehitä testejä samaan aikaan ohjelman kanssa, niistä on silloin eniten hyötyä. Muista kuitenkin, että 
      tarvittavien testien tyypit riippuu omasta aiheestasi. Kaikki aiheet eivät vaadi esim. suorituskykytestausta.
  - Kysy henkilökunnalta jos olet epävarma jostain asiasta. Varaudu kuitenkin miettimään asiaa ensin. Kysy mielummin "onko asian X kehittäminen minulle hyödyllistä" kuin "mitä minun pitäisi nyt tehdä"? 

  {% include typo_instructions_fin.md %}
    