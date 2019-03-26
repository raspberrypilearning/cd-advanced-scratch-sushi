## Power-ups

Op dit moment heb je slechts één type prijs: een ster die je één punt oplevert als je hem grijpt. Op deze kaart ga je een nieuw type prijs maken en zul je het doen op een manier die het toevoegen van andere soorten prijzen makkelijk maakt. Dan kun je je eigen power-ups en bonussen verzinnen en echt je eigen spel maken!

Ik heb hier al enkele stukjes voor toegevoegd met de `prijs-type`{:class="block3variables"} variabele en het `kies-uiterlijk`{:class="block3myblocks"} **Mijn blokken** blok. Je zult ze echter moeten verbeteren.

Laten we eens kijken hoe de prijs nu werkt.

Zoek in de scripts voor de **Prijs** sprite de `wanneer ik als kloon start`{:class="block3events"} code. De blokken waar je naar moet kijken zijn degenen die je punten geven voor het verzamelen van een ster:

```blocks3
    als <touching [Player Character v]?> dan
        verander [punten v] met (prijs-waarde ::variables)
        verwijder deze kloon
```

en deze die een uiterlijk voor de kloon selecteert:

```blocks3
    kies-uiterlijk (prijs-type ::variables) :: aangepast
```

## \--- collapse \---

## title: Hoe werkt het kiezen van een uiterlijk?

Het blok `kies-uiterlijk`{:class="block3myblocks"} werkt een beetje zoals het blok `verlies`{:class="block3myblocks"}, maar er is iets extra's: er is een variabele met **invoer**, genaamd `type`{:class="block3myblocks"}.

```blocks3
    definieer kies-uiterlijk (type)
    als <(type ::variabelen) = [1]> dan
        verander uiterlijk naar  [star1 v]
    end
```

Wanneer het blok `kies-uiterlijk`{:class="block3myblocks"} wordt uitgevoerd, doet het hier het volgende:

1. Het kijkt naar de invoervariabele `type`{:class="block3myblocks"}
2. Als de waarde van `type`{:class="block3myblocks"} gelijk is aan `1`, schakelt het over naar het `star1` kostuum

Bekijk het deel van het script dat het blok gebruikt:

```blocks3
    wanneer ik als kloon start
    kies-uiterlijk (prijs-type :: variables) :: custom
    verschijn
    herhaal tot <(y positie) < [-170]>
        verander y met (prijs-snelheid ::variables)
        als <touching [Player Character v]?> dan
            verandering [punten v] met (prijs-waarde ::variables)
            verwijder deze kloon
```

Je kunt zien dat de `prijs-type`{:class="block3variables"} variabele **doorgezet wordt** naar het blok `kies-uiterlijk`{:class="block3myblocks"}. Binnen de code voor `kies-uiterlijk`{:class="block3myblocks"}, wordt `prijs-type`{:class="block3variables"} vervolgens gebruikt als de invoervariabele (`type`{:class="block3myblocks"}).

Dit betekent dat de waarde van `prijs-type`{:class="block3variables"} bepaalt welk uiterlijk de sprite-kloon krijgt.

\--- /collapse \---

### Voeg een uiterlijk toe voor de nieuwe power-up

Natuurlijk heeft de sprite van **Prijs** maar één uiterlijk, omdat er maar één type prijs is. Je staat op het punt om dat te veranderen.

\--- task \--- Voeg een nieuw uiterlijk toe aan de **Prijs** sprite voor je nieuwe power-up. Ik hou van de bliksemschicht, maar kies wat je maar wilt. \--- /task \---

\--- task \--- Vertel vervolgens het `kies-uiterlijk`{:class="block3myblocks"} **Mijn blokken** blok om het nieuwe uiterlijk in te stellen wanneer het de nieuwe waarde krijgt voor `type`{:class=" block3myblocks "}, zoals dit \(gebruik de uiterlijknaam die je hebt gekozen\):

```blocks3
    definieer kies-uiterlijk (type)
    als <(type ::variable) = [1]> dan
        verander uiterlijk naar [star1 v]
    end
+ als <(type ::variable) = [2]> dan
+       verander uiterlijk naar [Lightning v]
+ end
```

\--- /task \---

### Maak de code voor de power-up

Nu moet je beslissen wat de nieuwe prijs zal doen! We beginnen met iets eenvoudigs: de speler een nieuw leven geven. In de volgende stap zorg je ervoor dat het iets gavers doet.

\--- task \--- Ga naar het gedeelte **Mijn blokken** en klik op **Maak een blok**. Noem het nieuwe blok `reageer-op-speler`{:class="block3myblocks"} en voeg een **nummerinvoer** genaamd `type`{:class="block3myblocks"} toe.

![Typ de naam voor het blok](images/powerupMakeName.png)

Klik **OK**. \--- /task \---

\--- task \--- Laat de `reageer-op-speler`{:class="block3myblocks"} **Mijn blokken** blok de punten of de levensduur van de speler verhogen, afhankelijk van de waarde van `type`{:class="block3myblocks"}.

```blocks3
+ definieer reageer-op-speler (type)
+ als <(type ::variable) = [1]> dan
+ verander [punten v] met (prijs-waarde ::variables)
+ end
+ als <(type ::variable) = [2]> dan
+ verander [levens v] met [1]
+ end
```

\--- /task \---

\--- task \--- Werk de `wanneer ik als kloon start`{:class="block3events"} code bij om het blok te vervangen dat een punt toevoegt met een **aanroep** naar `reageer-op-speler`{:class="block3myblocks"}, waarmee `prijs-type`{: class = "block3variables"} **doorgegeven** wordt.

```blocks3
+ als <touching [Player Character v] ?> dan
+ reageer-op-speler (prijs-type ::variables) :: custom
+ verwijder deze kloon
+ end
```

\--- /task \---

Door dit nieuwe `reageer-op-speler`{:class="block3myblocks"} **Mijn blokken** blok te gebruiken, voegen sterren nog steeds een punt toe, maar de nieuwe power-up die je hebt gemaakt voegt een leven toe.

### Gebruik `prijs-type`{:class="block3variables"} om verschillende prijzen willekeurig weer te geven

Op dit moment vraag je je wellicht af hoe je elke prijs dat het spel maakt, kunt vertellen welk type het zou moeten zijn.

Je doet dit door de waarde van `prijs-type`{:class="block3variables"} in te stellen. Deze variabele is slechts een getal. Zoals je hebt gezien, wordt het gebruikt om het `kies-uiterlijk`{:class="block3myblocks"} en `reageer-op-speler`{:class="block3myblocks"} te vertellen welk uiterlijk, regels etc. te gebruiken voor de prijs.

## \--- collapse \---

## title: Werken met variabelen in een kloon

Voor elke kloon van de **Prijs** sprite kun je een andere waarde instellen voor `prijs-type`{:class="block3variables"}.

Zie het als het creëren van een nieuw exemplaar van de **Prijs** sprite met behulp van de waarde die is opgeslagen in `prijs-type`{:class="block3variables"} op het moment dat de **Prijs** kloon wordt gemaakt.

Je vraagt je misschien af of het veranderen van de waarde van `prijs-type`{:class="block3variables"} alle prijzen in het werkgebied in hetzelfde type verandert. Dat gebeurt niet, want een van de dingen die klonen speciaal maken, is dat ze de waarden van de variabelen waarmee ze beginnen niet kunnen veranderen. Sprite-klonen hebben eigenlijk **constante** waarden. Dat betekent dat wanneer je de waarde van `prijs-type`{:class="block3variables"} wijzigt, dit niet van invloed is op de **Prijs** sprite-klonen die al in het spel aanwezig zijn. \--- /collapse \---

Je gaat het `prijs-type`{:class="block3variables"} instellen op `1` of `2` voor elke nieuwe kloon die je maakt. Om het spel interessant te houden, kun je willekeurig tussen de nummers kiezen om telkens een willekeurige prijs te maken.

\--- task \--- Zoek de `herhaal tot`{:class="block3control"} lus in de groene vlag code voor de **Prijs** sprite, en voeg de `als... anders`{:class="block3control"} code toe zoals hieronder weergegeven.

```blocks3
    herhaal tot <not <(create-collectables ::variables) = [true]>>
+ als <[50] = (willekeurig getal tussen (1) en (50))> dan
+ maak [prijs-type v] [2]
+ anders
+ maak [prijs-type v] [1]
+ end
        wacht (prijs-frequentie ::variables) sec
        ga naar x: (willekeurig getal tussen (-240) en (240)) y: (179)
        maak een kloon van [mijzelf v]
```

\--- /task \---

Deze code geeft een kans van 1 op 50 om het `prijs-type`{:class="block3variables"} in te stellen op `2`. Je wilt de speler immers niet de kans geven om een extra leven te vaak te verzamelen, anders zou het spel te gemakkelijk zijn.

Nu heb je een nieuw type prijs dat soms wordt weergegeven in plaats van de ster, en dat geeft je een extra leven in plaats van een punt wanneer je het verzamelt.