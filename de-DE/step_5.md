## Super Power-Ups!

Nun, da das neue sammelbare Power-Up funktioniert, ist es an der Zeit, etwas wirklich Cooles zu machen: Lass es einige Sekunden lang Power-Ups "regnen", anstatt nur ein zusätzliches Leben auszugeben.

Dazu verwendest du eine weitere `Sendung an alle`{:class="block3events"}-Nachricht.

--- task ---

Ändere zunächst den Block `reagiere-auf-Spieler`{:class="block3myblocks"}, um eine Nachricht an alle zu senden, wenn der Spielercharacter ein Typ-`2`-Sammelobjekt berührt. Rufe die Nachricht `Sammelobjekt-Regen`{:class="block3events"} auf.

```blocks3
Definiere react-to-player (typ :: custom-arg)
falls <(typ :: custom-arg) = [1]> , dann 
  ändere [Punkte v] um (Sammelobjekt-Wert :: variables)
end
falls <(typ :: custom-arg) = [2]> , dann 
  - ändere [Leben v] um [1]
  + sende [Sammelobjekt-Regen v] an alle
end
```

--- /task ---

Jetzt musst du einen neuen Code im **Sammelobjekt**-Figur-Skript erstellen, der jedes Mal gestartet wird, wenn die Meldung `Sammelobjekt-Regen`{:class="block3events"} gesendet wird.

--- task ---

Füge diesen Code für die **Sammelobjekt**-Figur hinzu, damit sie auf die `Sammelobjekt-Regen`{:class="block3events"}-Sendung lauscht.

```blocks3
+ Wenn ich [Sammelobjekt-Regen v] empfange
+ setze [Sammelobjekt-Häufigkeit v] auf [0.000001]
+ warte (1) Sekunden
+ setze [Sammelobjekt-Häufigkeit v] auf [1]
```

--- /task ---

--- collapse ---
---
title: Was macht der neue Code?
---

Dieses Stück Code wartet darauf, eine Nachricht zu empfangen und setzt `Sammelobjekt-Häufigkeit`{:class="block3variables"} auf eine sehr kleine Zahl, wartet dann eine Sekunde lang, und setzt dann die Variable zurück auf `1`.

Lass uns einen Blick darauf werfen, wie die Variable `Sammelobjekt-Häufigkeit`{:class="block3variables"} verwendet wird, um herauszufinden, warum diese Sammelobjekte regnen lassen kann.

In der Hauptspielschleife erhält der Teil des Codes, der die **Sammelobjekt**-Figur-Klone erzeugt, von der Variablen `Sammelobjekt-Häufigkeit`{:class="block3variables"} die Information, wie lange bis zum Erzeugen eines Klons gewartet werden soll:

```blocks3
    wiederhole bis <nicht <(erzeuge-Sammeobjekte ::variables) = [wahr]>>
        falls < [50] = (Zufallszahl von (1) bis (50))>, dann
            setze [Sammelobjekt-Typ v] auf [2]
        sonst
            setze [Sammelobjekt-Typ v] auf [1]
        Ende
        warte (Sammelobjekt-Häufigkeit ::variables) Sekunden
        gehe zu x: (Zufallszahl von (-240) bis (240)) y: (179)
        erzeuge  Klon von [mir selbst v]
 Ende
```

Du kannst sehen, dass der `warte`{:class="block3control"}-Block den Code für die Dauer der Zeit pausiert, die von `Sammelobjekt-Häufigkeit`{:class="block3variables"} gegeben wird.

Wenn der Wert von `Sammelobjekt-Häufigkeit`{:class="block3variables"} `0,000001` ist, pausiert der `warte`{:class="block3control"} - Block nur für **Millionstel** Sekunden, was bedeutet, dass die `Wiederholen bis`{:class="block3control"}-Schleife viel öfter ausgeführt wird als normal. Als Ergebnis wird der Code **eine Menge** mehr Power-Ups erstellen, als er es normalerweise tun würde, bis `Sammelobjekt-Häufigkeit`{:class="block3variables"} wieder auf `1` geändert wird.

Fällt dir ein Problem ein was möglicherweise auftreten könnte? Es wird viel mehr Power-Ups geben..., was wenn du sie weiter fängst?

--- /collapse ---