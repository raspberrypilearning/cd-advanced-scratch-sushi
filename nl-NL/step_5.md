## Super power-ups!

Nu je een nieuwe power-up prijs hebt, is het tijd om het iets heel cools te maken: laten we het een paar seconden power-ups 'regenen' in plaats van alleen maar een extra leven te geven.

Hiervoor gebruik je een ander `signaal`{:class="block3events"} bericht.

--- task --- Wijzig eerst het blok `reageer-op-speler`{:class="block3myblocks"} om een bericht uit te zenden wanneer het personage van de speler een type `2` prijs raakt. Roep het bericht `prijzen-regen`{:class="block3events"} op.

```blocks3
    definieer reageer-op-speler (type)
    als <(type ::variable) = [1]> dan
        verander [punten v] met (prijs-waarde ::variables)
    end
    als <(type ::variable) = [2]> dan
- verander [levens v] met [1]    
+ zend signaal [prijzen-regen v]
    end
```

--- /task ---

Nu moet je een nieuw stuk code maken in de **Prijs** sprite-scripts die worden gestart wanneer het bericht `prijzen-regen`{:class="block3events"} wordt uitgezonden.

--- task --- Voeg deze code toe voor de **Prijs** sprite om hem te laten luisteren naar het `prijzen-regen`{:class="block3events"} signaal.

```blocks3
+ wanneer ik signaal [prijzen-regen v] ontvang
+ maak [prijs-frequentie v] [0.000001]
+ wacht (1) sec
+ maak [prijs-frequentie v] [1]
```

--- /task ---

--- collapse ---
---
title: Wat doet de nieuwe code?
---

Dit stukje code wacht tot het een signaal ontvangt, en reageert door de `prijs-frequentie`{:class="block3variables"} variabele zeer klein te maken, wacht dan een seconde, en verandert de variabele daarna naar `1`.

Laten we eens kijken naar hoe de `prijs-frequentie`{:class="block3variables"} variabele wordt gebruikt om erachter te komen waarom het dan prijzen regent.

In de hoofdgame-lus wordt het deel van de code dat **Prijs** sprite-klonen maakt, verteld door de variabele `prijs-frequentie`{:class="block3variables"} hoe lang te wachten tussen het maken van een kloon en de volgende:

```blocks3
    herhaal tot <not <(create-collectables ::variables) = [true]>>
        als < [50] = (willekeurig getal tussen (1) en (50))> dan
            maak [prijs-type v] [2]
        anders
            maak [prijs-type v] [1]
        end
        wacht (prijs-frequentie ::variables) sec
        ga naar x: (willekeurig getal tussen (-240) en (240)) y: (179)
        maak een kloon van [mijzelf v]
    end
```

Je kunt zien dat het blok `wacht`{:class="block3control"} hier de code pauzeert gedurende de tijdsduur ingesteld door `prijs-frequentie`{:class="block3variables"}.

Indien de waarde van `prijs-frequentie`{:class="block3variables"} `0,000001` is, dan pauzeert het`wacht`{:class="block3control"} blok slechts **miljoenste** van een seconde, wat betekent dat de `herhaal tot`{:class="block3control"} lus veel vaker dan normaal uitgevoerd zal worden. Daarom zal de code **veel** meer power-ups creëren dan normaal, tot `prijs-frequentie`{:class="block3variables"} terug veranderd wordt naar `1`.

Kun je mogelijke problemen bedenken? Er zullen veel meer power-ups zijn…wat als je ze blijft vangen?

--- /collapse ---