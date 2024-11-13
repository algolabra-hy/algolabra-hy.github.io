---
layout: page
permalink: /aiplatform
title: Tekoälyalusta
title_long: AI Platform
inheader: no
---

#### Tällä hetkellä tuetut toiminnot

Tällä hetkellä tekoälyalusta tukee **shakkia** ja **connect-fouria**. Tekoälyalustan lokaali (omalla koneella pyöritettävä) versio toimii **linux koneilla** (ainakin fuksiläppärillä). Mikäli saat käyttäessäsi virheilmoituksen "no module called pex" voit kokeilla pex kirjaston asentamista [näiden ohjeiden](https://pypi.org/project/pex/) mukaan. **Huom** tekoälyalusta ei toimii virtuaalikoneilla. Sen serveripohjainen (remote) versio toimii muillakin, mutta sitä kannattaa käyttää  vasta oman tekoälyn perustoimintojen ollessa kunnossa .

## Briefly in English
This page describes how to use an AI-platform to support the devleopment of game AI:s in the project. The platform offers an GUI and 
the ability to play against your AI with minimal overhead. 
The platform can be found on [Github](https://github.com/game-ai-platform-team/tira-ai-local)
The [readme](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#tira-ai-local) provides a comprehensive 
description of its usage. Notice however that the example chess AI project mentioned in the readme makes use of pythons chess library, which
your own project is not allowed to use! 

Currently the platform works on Linux and supports the games chess and connect 4. 

## AI-platform - tekoälyjen kehitystä tukeva alusta. 
AI-platform on harjoitustyölle ohjelmistoprojektina tuotettu alusta, joka tarjoaa tämän kurssin opiskelijoille alustan jolla kehittää 
pelitekoälyjään. Tarkemmin sanottuna alusta tarjoaa--minimaalisella setupilla--graafisen käyttöliittymän ja mahdollisuuden ihmiselle pelata kehitteillä olevaa 
tekoälybottia vastaan. 

Alustan käyttöönotto on huomattavan paljon helpompaa, kuin oman GUI:n koodaaminen joten suosittelemme sitä vahvasti kaikille, jotka haluavat tehdä shakki tai connect 4 tekoälyn harjoitustyössä. 
Tekoälyalusta löytyy [Githubista](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file). Sen readme on hyvä ja kattaa samat asiat kuin mitä tässä käydään (lyhennettynä)
läpi. **Huomaa** kuitenkin, että readmen mainitsema [esimerkkiharjoitustyön](https://github.com/game-ai-platform-team/stupid-chess-ai) [tekoäly](https://github.com/game-ai-platform-team/stupid-chess-ai/blob/main/src/stupid_ai.py) käyttää pythonin chess kirjastoa jonka käyttö **ei ole sallittua** harjotustyössä. 
*Mikäli käytät harjoitustyössäsi tekoälyalustaa* muista mainita tästä dokumentaatiossasi ja ohjelmasi käyttöohjeissa jotta vertaisarvioijat osaavat ajaa ohjelmaasi oikein. 


## Minimaaliset ohjeet käyttöönottoon

Alla minimaaliset ohjeet python-pohjaisen shakki tai connect-four kehityksen aloittamiseen ai platformin kanssa linux koneella. 
Tämän osion jälkeen sinun pitäisi pystyä aloittamaan oman harjoitustyösi kehitys pythonilla. 
Alusta tukee myös muita 
ohjelmointikieliä. Kohdassa [oman harjoitustyön konfigurointi](aiplatform#oman-harjoitustyön-konfigurointi) selitetään tarkemmin, miten oma harjotustyösi 
pitää konfiguroida. 

1. Lataa alustan uusimman [releasen zip tiedosto](https://github.com/game-ai-platform-team/tira-ai-local/releases) (kuvassa tira-ai-local-linux-x64-1.0.4.zip)
![]({{ "/images/tira-ai1.png" | absolute_url }})
1. Kloonaa esimerkkitekoälyn projekti: [shakki](https://github.com/game-ai-platform-team/stupid-chess-ai), [connect 4](https://github.com/game-ai-platform-team/stupid-connect-four-ai)
    - kopioi sen sisältö oman harjoitustyösi repositorioon. 
1. Asenna [poetry](/poetry).
1. Pura alustan zip tiedosto, navigoi purettuun kansioon terminaalissa ja käynnistä se komennolla ```./tira-ai-local```
![]({{ "/images/tira-ai2.png" | absolute_url }})
1. Valitse ylhäältä oikea peli. 
![]({{ "/images/tira-ai4.png" | absolute_url }})
1. Drag-and-droppaa oma harjoitustyösi juurikansio submit folderin alla olevaan ruutuun ja paina submit. 
    - kunhan olet asentanut poetryn (kokeile ajamalla esim ```poetry -v``` terminaalissa ja varmista, ettei tule erroreita) voit jättää "run setup.sh" ruudun valitsematta.
1. Pelisi pitäisi alkaa. 
    - Mahdolliset virheilmoitukset printaantuvat terminaaliin ruudun alarunassa. Jos ilmenee ongelmia, varmista että oman projektisi rakenne vastaa täsmälleen esimerkkitekoälyjä. 
    - Kohdassa  [oman harjoitustyön konfigurointi](aiplatform#oman-harjoitustyön-konfigurointi) selitetään tarkemmin, mitä ehtoja oman projektisi täytyisi toteuttaa toimiakseen platformin kanssa. 
![]({{ "/images/tira-ai5.png" | absolute_url }})
![]({{ "/images/tira-ai6.png" | absolute_url }})

Jos pääsit näin pitkälle voit nyt aloittaa oman tekoälysi kehityksen muokkaamalla tiedostoa ``main.py`` (connect 4) tai ``src/stupid_ai.py``(shakki). 
Tässä vaiheessa kannattaa tustua esimerkkitekoälyjen rakenteeseen ja [tekoälyalustan kanssa kommunikoinnin](aiplatform#tekoälyalustan-kanssa-kommunikointi) ohjeisiin. 
Muista, että molemmat esimerkkitekoälyt tekevät vain sattumanvaraisia siirtoja, eli aika pian kannattaa poistaa kaikki niiden sisältö ja rakentaa oma. 
Muista että stupid_ai.py_n käyttämää pythonin chess kirjastoa **ei saa** käyttää omassa lopullisessa harjoitustyössä, toteuta laillisten siirtojen tarkistus ja laudan tilan hallinta itse! 

Voit myös muokata (ja sinun kannattaakin näin tehdä) tiedostojen nimiä ja projektin rakennetta. Muista kuitenkin aina muutosten jälkeen muokata tiraconfig kansioiden scriptejä. "runcommand" scriptissä pitäisi olla täsmälleen se komento, jota tekoälyalustan pitäisi kutsua käynnistäkseen oma tekoälysi, ja "setup.sh":ssa pitäisi olla kaikkien niiden kirjastojen asennus, joita oma tekoälysi käyttää. Huomaa, että seup.sh:ta ei tarvitse ajaa jos koneellasi on jo tekoälyn tarvitsemat kirjastot. Lisää niiden asennuskomennot kuitenkin sinne jotta esim. vertaisarvioijasi vpovat ajaa projektiasi.  

## Oman harjoitustyön konfigurointi 
Tekoälyalusta tukee pythonin ja poetryn lisäksi monia muitakin ohjelmointikieliä. Tässä selitetään miten oma harjoitustyösi pitäisi konfiguroida, jotta se toimisi 
alustan kanssa. Samat ohjeet löytyvät [alustan readmesta](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#ai-configuration). 

Lyhyesti sanottuna, tekoälyalusta olettaa, että projektisi juurikansiossa on ``tiraconfig`` kansio jossa on (ainakin) kaksi 
tiedostoa: ``runcommand`` ja ``setup.sh``.

**setup.sh** tiedoston pitäisi sisältää ne komennot jotka vaaditaan tekoälysi käyttämien kirjastojen ja riippuvuuksien asentamiseen. 
Lyhyesti sanottuna, setup.sh scriptin ajamisen jälkeen, koneellasi pitäisi pysytä ajamaan runcommandissa oleva komento ilman muita erroreita. 
Poetrya käyttäville python projekteille 
setup.sh voisi olla esim: 
```
#! /bin/bash

poetry install
```
Tässä ensimmäisellä rivillä kerrotaan terminaalille, että kyseessä on scripti jota ajetaan. Toinen rivi asentaa poetryn. 

**runcommand** tiedostossa pitäisi olla täsmälleen se komento, jolla tekoälysi voi käynnistää terminaalista. Huomaa että tämän ei tarvitse olla 
python komento, jopa käännettyjä kieliä voi käyttää (tällöin setup.sh:n pitäisi kääntää ohjelmasi).

Ajettaessa runcommandissa oleva komento, tekoälysi pitäisi käynnistyä ja mennä ikuiseen looppiin jonka aikana se lukee komentoja stdinistä, ja tulostaa 
omia komentojaan stdouttiin. Pythonille tämä voisi näyttää esimerkiksi seuraavalta:
```python 
def main():
    while True:
        # Lue komento alustalta
        command = input().strip()
        
        # Käsittele komento ja tulosta vastaukset
        # Tekoälysi logiikka tulee tänne
        
if __name__ == "__main__":
    main()
```
Looppi katkaistaan tekoälyalustan "kill process" napista joka lähettää ohjelmallesi "sigtermin" ja sen jälkeen "sigkillin". Hajroitustyötäsi varten sinun ei tarvitse osata käsitellä näitä signaaleja. Kunhan et aktiivisesti lisää koodia joka estää tämän, nämä signaalit johtavat ohjelmasi lopettamiseen jonka jälkeen se pitää submitata uudelleen.  

## Tekoälyalustan kanssa kommunikointi 
Katso myös [alustan readmesta](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#ai-communication-protocol-input).
Oma tekoälysi keskustelee alustan kanssa standard outputin ja inputin kautta. 

**Input**. Jokaisen tekoäly looppisi pitäisi siis alkaa lukemalla inputtia standard inputista. Pythonissa tämä onnistuu metodilla 
``ìnput()``. Kaikki alustan lähettämät merkkijonot ovat muotoa ``KOMENTO:DATA`` jossa ``KOMENTO`` on yksi seuraavista:
-  ``PLAY``. Tämä tarkoittaa, että alusta haluaa tekoälysi pelaavan siirron ja tulostavan sen standard outtiin. 
    - **Huomaa** että tekoälysi voi saada monta play komentoa peräkkäin ja sen pitäisi siis pystyä laskemaan seuraava siirto pelin molemmille osapuolille. Pidä siis huoli siitä, että tekoälysi tietää kumman vuoro on ja osaa tehdä siirron vuorossa olevalle pelaajalle aina lukiessaan ``PLAY`` komennon. 
- ``MOVE``. Tämä tarkoittaa, että tekoälyalusta suoritti jonkun siirron jonka oma tekoälysi pitäisi tallettaa pelilogiikkaansa. Yleensä tämä komento lähetetään sen jälkeen, kun ihminen on pelannut siirron alustan kautta. Suoritettu siirto on ``DATA``:ssa. Sen tarkka muoto riippuu mitä peliä pelataan. Katso pelikohtaiset formaatit [alta](). 
- ``BOARD``. Tämä tarkoittaa, että tekoälysi sovelluslogiikan pitäisi asettaa lauta johonkin tiettyyn konfiguraatioon. Nyt ```DATA``` osassa on jokin merkkijono esitys pelilaudan nykyisestä tilasta.  Katso pelikohtaiset formaatit [alta](/aiplatform#pelikohtainen-info).
- ``RESET``. Tämä tarkoittaa, että alusta haluaa, että tekoälysi resetoi pelin alkuasetelmaan. 

**Voidaksesi käyttää alustaa** sinun täytyy toteuttaa vähintään ``PLAY``ja ``MOVE`` komentojen kästtely tekoälyssäsi. ``BOARD`` ja ``RESET`` komennot lähetään vaan, jos tekoälyalustan käyttäjä (eli yleensä sinä itse) joko:
1. painaa reset nappia tai
1. yrittää selata siirtoja taaksepäin tehdäkseen jonkun muun siirron. 

Eli kunhan et koskaan käytä näitä toimintoja, tekoälyä joka tukee vain PLAY ja MOVE komentoja voi käyttää. Suosittelemme kuitenkin, että toteutat myös ``BOARD``ja ``RESET`` komennot niin pian kuin mahdollista. 

**Output.** Oma tekoälysi voi kirjoittaa standard outtiin (esim. Pythonissa print() metodilla) mitä vaan. Tekoälyalusta etsii tulostuksia jotka ovat muotoa ``MOVE:siirto`` joista se lukee siirron [pelikohtaisessa formaatissa](/aiplatform#pelikohtainen-info) ja suorittaa sen. Mikäli ``siirto`` ei vastaa siinä pelitilanteessa laillista siirtoa, tekoälyalusta kaatuu. 

Kaikki muut tekoälyn tulostamat merkkijonot tallennetaan alustan terminaaliin ja näytetään käyttäjälle. Näin voit kirjoittaa omaa kehitystäsi helpottavia logeja. 


#### Esimerkki shakkitekoälystä 
Katsotaan vielä tarkemmin esimerkkiprojektin tekoälyn (stupid_ai.py) rakennetta. 
```python
import random
# chess kirjaston käyttö EI OLE sallitua harjoitustyössä. 
import chess
import time

def set_board(board: chess.Board, board_position:str):
    print(f"Set board to {board_position}!")
    board.set_fen(board_position)

def make_move(board: chess.Board):
    legal_moves = [move.uci() for move in list(board.legal_moves)]
    print(f"I found {len(legal_moves)} legal moves: {', '.join(legal_moves)}")
    choice = random.choice(legal_moves)
    board.push_uci(choice)

    return choice

def main():

    board = chess.Board()

     while True:
        opponent_move = input()
        time.sleep(random.randrange(1,10)/100)
        if opponent_move.startswith("BOARD:"):
            set_board(board, opponent_move.removeprefix("BOARD:"))
        elif opponent_move.startswith("RESET:"):
            board.reset()
            print("Board reset!")
        elif opponent_move.startswith("PLAY:"):
            choice = make_move(board)
            # example about logs
            print(f"I chose {choice}!")
            # example about posting a move
            print(f"MOVE:{choice}")
        elif opponent_move.startswith("MOVE:"):
            move = opponent_move.removeprefix("MOVE:")
            board.push_uci(move)
            print(f"Received move: {move}")
        else:
            print(f"Unknown tag: {opponent_move}")
            break

if __name__ == "__main__":
    main()
```
**Huom** tämä esimerkki käyttää pythonin valmista chess kirjastoa jonka käyttö *ei* ole sallittua harjoitustyössä. Toteuta siis itse laudan hallinta ja siirtojen kirjoitus.

Esimerkissä main metodi alustaa shakkilaudan ja aloittaa sitten ikuisen loopin. 
Jokainen looppi alkaa metodilla ``input()`` joka lukee alustan lähettämän komennon. Tämän jälkeen kaikki 
mahdolliset komennot (PLAY, MOVE, BOARD, ja RESET) käydään läpi ja käsitellään. Esimerkiksi, saadessaan komennon, joka alkaa
merkkijonolla "MOVE:" tekoäly ensin poistaa siitä alkuosan, jonka jälkeen sen loppuosa vastaa jotain siirtoa [shakkinotaatiossa](/aiplatform#shakki-siirrot). 
Tämän jälkeen se suorittaa saadun siirron. 
Esimerkki lähettää alustalle tiedon tehdystä siirrosta komennolla ``print(f"MOVE:{choice}")``. Kaikki muut print statementit tulevat näkyviin alustan terminaalissa. 

## Pelikohtainen info
Katsotaan vielä pelikohtaiset merkkijonoesitykset laudan tiloista ja siirroista. 

### Shakki
Katso myös [readmeta](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#chess)
#### Shakki siirrot
Käyttöliitymä tukee ns uci standardia shakin siirtojen merkitsemiseen merkkijonoina. 
Jokaisessa siirtoa kuvaavassa merkkijonossa on neljä tai viisi merkkiä.  
Merkkijonon kaksi ensimmäistä merkkiä ovat siirrettävän nappulan lähtöruutu. Seuraavat kaksi 
ovat ruutu jonne se siirretään (katso alla oleva kuva). Valkoiset nappulat aloittavat riveiltä 1 ja 2, mustat riveiltä 7 ja 8. Valkoinen kuningas aloittaa ruudusta e1 ja valkoinen kuningatar ruudusta d1. 

Viidettä merkkiä käytetään vain sotilaiden korotuksessa. 
Viides merkki kuvaa nappulaa johon sotilas korotetaan:
**q**->kuningatar (queen), **r**->torni (rook), **b**->lähetti (bishop), **k**->ratsu (knight)

![]({{ "https://ucichessengine.files.wordpress.com/2011/03/square_numbers.gif" | absolute_url }})
 
Esimerkiksi merkkijono "e2e4" kuvastaa nappulan, joka tällä hetkellä on ruudussa e2 siirtoa ruutuun e4.
Merkkijono "e7e8q" kuvastaa sotilaan joka tällä hetkellä on ruudussa e7 korotusta kuningattareksi.  

Tornitus merkataan kuninkaan kahden tai kolmen askeleen siirtona. Mikäli yrität siirtää tornia, tämä tulkitaan tornin siirtona.

#### Shakkilauta
Shakkilaudan tilaa kuvaava merkkijono selitetään [täällä](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#boards-fen).
Harjoitustyötä varten sinun ei tarvitse välttämättä pitää kirjaa tornituksista tai oheestälyönnistä (en-passant). Tekoälyalusta sallii kutenkin näiden siirtojen tekemisen, eli jos teet ihmisenä sen kautta näitä siirtoja, joudut ottamaan tämän huomioon oikeellisuuden tarkistuksessa. 

### Connect four
Katso myös [readmeta](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#connect-four).
#### Connect four siirrot
Connect fourin siirrot merkataan yksinkertaisesti sarakkeena, jonne siirto tehdään. Vasemmanpuoleisin sarake on numero 0, oikeanpuoleisin numero 6. Huomaa, että tekoälysi täytyy itse pitää kirjaa siitä, kumman vuoro on. "Punainen" pelaaja tekee ensimmäisen siirronon 

#### Connect four lauta
Conenct four laudat merkataan sekvenssinä siirtoja. Eli "BOARD:" komennon jälkeen tulee joukko numeroita, joiden välillä on ",". 
ensimmäinen näistä numeroista vastaa siirtoa, jonka punainen tekee ensin, seuraava keltaisen siirtoa etc. etc. 

## Kiitos
Kiitokset tekoälyplatformin kehittämisestä kuuluu ohjelmistotuoantoprojektin ryhmälle. 
Keväällä 2024 sitä kehittivät: Jiahao Li, Max Leikas, Rasmus Marttila, Elijas Veijalainen, Miika Piiparinen sekä Emilia Kupsanen Marianna Ojasen ohjauksessa. 
Koko projekti löytyy [Githubista](https://github.com/game-ai-platform-team).



{% include typo_instructions.md %}
