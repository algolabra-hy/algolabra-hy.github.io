---
layout: page
permalink: /aiplatformtest
title: Tekoälyalustan Testaus
title_long: AIPlatform
inheader: no
---


<div style="color:black; border-style: solid; border-width: thick; border-color: red; padding: 10px; margin-bottom: 15px; padding: 10px; background-color: #F1EFEF;">

<h4>Vasta Koekäytössä</h4>

<p>
Tekoälyalusta on tällä kurssilla (4 periodi lukukaudella 23-24) 
vasta koekäytössä. Kurssin henkilökuntakin vasta harjoittelee sen kanssa. Näinpä ohjeissa voi olla jonkin verran epäselvyyksiä ja käytännöt muuttua. Pyrimme minimoimaan muutoksista aiheutuvat häiriöt opiskelijoille. 

Tällä hetkellä alusta toimii vain (jollain) Linuxin distributioilla. 
 </p>

</div>

Tällä kurssilla on mahdollista koekäyttää harjoitustyölle kehitteillä olevaa tekoälyjen kehitysalustaa. Tällä hetkellä alusta tukee shakkipelin tekoälyn kehitystä **Linuxilla**. Jos siis aiot tehdä harjoitystyönäsi shakille tekoälyn, suosittelemme tämän käyttöliittymän kokeilemista ja siitä aktiivisen palautteen antoa. 

Lyhyesti sanottuna, alustalta saa käyttöönsä grafisen käyttöliittymän ja mahdollisuuden (melko) helposti pelata omaa tekoälyään vastaan. Tämän tarkoitus on helpottaa harjoitustyön ytimen (eli itse tekoälyn) kehittämiseen pääsemistä. 

**Mikäli aiot kokeilla käyttöliittymää**:
1. Kerro tästä määrittelydokumentissasi. 
1. Lisää jokaiseen viikkoraporttiin lyhyt palaute sen toimivuudesta ja siitä, mikä vaikutus sillä on harjoitustyön kehitykseen. 
1. Muista kirjoittaa käyttöohjeeseesi miten koko projektisi ajetaan. Tämä on tärkeää mm. vertaisarviointia varten. 


## Ohjeet Käyttöliittymän Lataamiseen
![]({{ "/images/ailocal0.png" | absolute_url }})

1. Aloita lataamalla **uusin** github release [AI-localin](https://github.com/game-ai-platform-team/tira-ai-local/tags) repositoriosta (kuvan .zip tiedosto).
1. Pura zip tiedosto (kuva otettu 1.0.0 releasesta joka ei enää ole uusin) ja käynnistä sieltä löytyvä tira-ai-local ohjelma (joko terminaalista tai kansiosta klikkaamalla)

![]({{ "/images/ailocal1.png" | absolute_url }})

Käynnistyvään ohjelmaan voit linkata oman tekoälyprojektisi root kansion (file-path ruutuun jonka jälkeen paina submit). 

![]({{ "/images/ailocal2w.png" | absolute_url }})

**Jos ohjelma ei käynnisty**: voi olla että Linux distributiostasi puuttuu jokin kirjastoista 
joista se riippuu. Näihin kuuluu ainakin libatk, libatk-bridge2.0-0, libcups2, libgtk-3-0 ja libgbm1. Näitä voi asentaa [täällä](https://www.masmasit.com/2021/08/how-to-install-package-libatk-10so0-on_01058658241.html) olevien ohjeiden mukaisesti. 

## Oman Tekoälyn Konfiguroiminen 

Mallia oman tekoälyn konfiguroimiseen voi ottaa [stupid chess AI](https://github.com/game-ai-platform-team/stupid-chess-ai) projektista. Tiraconfig kansioon laitetaan 
shell scriptit jolla projekti setupataan ja ajetaan. 

Oma tekoäly kirjoitetaan python tiedostoon jota "runcommand" scripti kutsuu (esimerkissä /src/stupid_ai.py)

### Käyttöliittymän Kanssa Keskustelu
Katsotaan vielä esimerkkiprojektin tekoälyn (stupid_ai.py) rakennetta. 
```python
import random
# chess kirjaston käyttö EI OLE sallitua harjoitustyössä. 
import chess
import time
import random

def set_board(board: chess.Board, board_position:str):
    board.set_fen(board_position)

def make_move(board: chess.Board):
    legal_moves = [move.uci() for move in list(board.legal_moves)]
    choice = random.choice(legal_moves)
    board.push_uci(choice)

    return choice

def main():

    board = chess.Board()

    while True:
        opponent_move = input()
        time.sleep(random.randrange(1,10)/100)
        if opponent_move.startswith("BOARD: "):
            set_board(board, opponent_move.removeprefix("BOARD: "))
        elif opponent_move.startswith("START: "):
            board.reset()
            print("Started a new game!")
            choice = make_move(board)
            print(f"MOVE: {choice}")
        elif opponent_move.startswith("MOVE: "):
            board.push_uci(opponent_move.removeprefix("MOVE: "))
            choice = make_move(board)

            # example about logs
            print(f"I moved {choice}")
            # example about posting a move
            print(f"MOVE: {choice}")
        else:
            print("Unknown tag!")
            break

if __name__ == "__main__":
    main()
```
**Huom** tämä esimerkki käyttää pythonin valmista chess kirjastoa jonka käyttö *ei* ole sallittua harjoitustyössä. Toteuta siis itse laudan hallinta ja siirtojen kirjoitus.

Esimerkissä tekoäly keskustelee käyttöliittymän kanssa input() ja print komentojen kautta. 
Input komenolla luetaan käyttöliitymästä tuleva komento. 
Käyttöliitymästä voi tulla kolme eri tyypin komentoa:
1. Uuden pelin aloitus merkkijonona joka alkaa sanoilla "START:" tämän komennon seurauksena 
laudan tila nollataan, jonka jälkeen on oman tekoälyn siirron vuoro.
1. Mukautettu laudan tila joka alkaa tekstillä "BOARD:" sanan jälkeen seuraa laudan tila ns. [Forthsyn-Edwards](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation) muodossa. 
**Laudan tiloja ei välttämättä tarvitse tukea omassa tekoälyssäsi**, mutta se voi auttaa kehityksessä koska käyttäöliittymään voi syöttää eri laudan tiloja. Laudan tilan asetuksen seuraavaa siirtoa odotetaan käyttöliittymältä. 
1. Ihmisen tekemä siirto joka alkaa merkkijonolla "MOVE:" 

Aina kun saadaan tai tehdään uusi siirto, se tallennetaan tekoälyn omaan laudan hallintaan (esimerkissä komennolla "board.push()) jonka jälkeen oman tekoäly laskee seuraavan siirron. Esimerkkitekoälymme yksinkertaisesti arpoo sattumanvaraisesti jonkun laillisista siirroista, make_move() metodissa. Muista ettei oma harjoitustyösi saa käyttää chess kirjaston metodeja. 

Käyttöliittymä tukee myös muun syötteen loggaamista. Kaikki print lauseet paitsi ne, jotka alkavat "MOVE:" syötetään käyttöliittymän outputtiin josta ne voi lukea ohjelman avaamassa terminaalissa.
Jos yrität omasta tekoälystäsi lähettää laittoman siirron, käyttöliittymä kaattuu.  

### Siirtojen Käsittely Merkkijonoina
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

## Kiitos
Kiitokset tekoälyplatformin kehittämisestä kuuluu Ohjelmistotuoantoprojektin Ryhmälle. 
Koko projekti löytyy [Githubista](https://github.com/game-ai-platform-team), tänne sivulle tulee ehkä heidän nimiä kunhan kysyn siihen luvan.



{% include typo_instructions.md %}