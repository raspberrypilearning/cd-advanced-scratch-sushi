## Het spel verliezen

Ten eerste! Je hebt een manier nodig om het spel te laten eindigen als de speler geen levens meer heeft. Op dit moment gebeurt dat niet.

Je hebt misschien gemerkt dat het `verlies`{:class="block3myblocks"} **Mijn blokken** blok in het script voor de **Speler** sprite leeg is. Je gaat dit invullen en alle stukken instellen die nodig zijn voor een leuk 'Game over' scherm.

--- task --- 
Zoek eerst het blok `verlies`{:class="block3myblocks"} en vul het aan met de volgende code:

```blocks3
    definieer verlies
+ stop [andere scripts in sprite v] :: control stack
+ zend signaal [game over v]
+ ga naar x: (0) y: (0)
+ zeg [Game over!] (2) sec
+ stop [alle v]
```

--- /task ---

--- collapse ---
---
title: Wat doet deze code?
---

Telkens wanneer het blok `verlies`{:class="block3myblocks"} wordt uitgevoerd, doet het het volgende:

1. Stop de natuurkunde en andere spelscripts die de **Speler** aansturen
2. Vertel alle andere sprites dat de game afgelopen is door een `game over`{:class="block3events"} bericht **uit te zenden**, waar ze op kunnen reageren en aanpassen wat ze doen
3. Verplaats de **Speler** naar het midden van het werkgebied en vertel de speler dat het spel voorbij is
4. Stop alle scripts in het spel

--- /collapse ---

Nu moet je ervoor zorgen dat alle sprites weten wat ze moeten doen als het spel is afgelopen en hoe ze zichzelf kunnen resetten als de speler een nieuw spel start. **Vergeet niet dat als je nieuwe sprites toevoegt, hier misschien ook code voor nodig is!**

### De platforms en randen verbergen

--- task --- 
Begin met de makkelijkste sprites. De **Platform** en **Randen** sprites hebben beide code nodig om te verschijnen wanneer het spel start en om te verdwijnen wanneer ze het `game over`{:class= "block3events"} bericht ontvangen, dus voeg deze blokken toe aan beide sprites:

```blocks3
+ wanneer ik signaal [game over v] ontvang
+ verdwijn
```

```blocks3
+ wanneer op de groene vlag wordt geklikt
+ verschijn
```

--- /task ---

### Stop de sterren

Als je nu naar de code voor de sprite **Prijs** kijkt, zie je dat deze werkt door zichzelf te **klonen**. Dat wil zeggen dat het kopieën van zichzelf maakt die de speciale `wanneer ik als kloon start`{:class="block3events"} instructies volgen.

We zullen meer vertellen over wat klonen speciaal maakt wanneer we de stap zetten over het maken van nieuwe en verschillende prijzen die je kunt verzamelen. Voor nu, wat je moet weten is dat klonen **bijna** alles kunnen doen wat een normale sprite kan, met inbegrip van het ontvangen van `signalen`{:class="block3events"}.

Kijk hoe de **Prijs** sprite werkt. Kijk of je een deel van de code kunt begrijpen:

```blocks3
    wanneer op de groene vlag wordt geklikt
    verdwijn
    maak [prijs-waarde v] [1]
    maak [prijs-snelheid v] [1]
    maak [prijs-frequentie v] [1]
    maak [maak-prijzen v] [true]
    maak [prijs-type v] [1]
    herhaal <not <(create-collectables) = [true]>>
        wacht (prijs-frequentie) sec
        ga naar x: (willekeurig getal tussen (-240) tot (240)) y: (179)
        maak een kloon van [mijzelf v]
    end
```

1. Eerst maakt de originele **Prijs** sprite onzichtbaar door deze te verbergen
2. Vervolgens worden de besturingsvariabelen ingesteld - we komen hier later op terug
3. De variabele `maak-prijzen`{:class="block3variables"} is de aan/uit schakelaar voor klonen: de lus maakt klonen als `maak-prijzen`{:class="block3variables"} `waar` is en doet niets als het niet waar is

--- task --- 
Stel nu een blok in voor de **Prijs** sprite, zodat deze reageert op het `game over` signaal:

```blocks3
+ wanneer ik signaal [game over v] ontvang
+ verdwijn
+ maak [maak-prijzen v] [false]
```

--- /task ---

Deze code is gelijk aan de code die de **Platforms** en **Randen** sprites controleert. Het enige verschil is dat je ook de variabele `maak-prijzen`{:class="block3variables"} instelt op `false` zodat er geen nieuwe klonen worden aangemaakt als het 'Game over' is.

Merk op dat je de variabele `maak-prijzen`{:class="block3variables"} kunt gebruiken om berichten van het ene deel van je code door te geven aan een ander deel!