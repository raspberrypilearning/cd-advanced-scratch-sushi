## Das Spiel verlieren

Das Wichtigste zuerst! Du brauchst eine Möglichkeit, das Spiel zu beenden, wenn der Spieler keine Leben mehr hat. Im Moment passiert das nicht.

Du hast vielleicht bemerkt, dass der `verlieren`{:class="block3myblocks"}-**Meine Blöcke**-Block im Skript für die Figur **Spieler-Character** leer ist. Du wirst diese ausfüllen und alle Teile zusammenstellen, die für einen schönen 'Game over'-Bildschirm benötigt werden.

--- task ---

Suche zunächst den Block `verlieren`{:class="block3myblocks"} und ergänze ihn mit folgendem Code:

```blocks3
    Definiere verlieren
+ stoppe [andere Skripte der Figur v] :: control stack
+ Sende [Game Over v] an alle
+ gehe zu x: (0) y: (0)
+ sage [Game over!] für (2) Sekunden
+ stoppe [alles v]
```

--- /task ---

--- collapse ---
---
title: Was macht dieser Code?
---

Wann immer der `verlieren`{:class="block3myblocks"}-Block jetzt läuft, wird Folgendes ausgeführt:

1. Stoppe die Physik und andere Spielskripte, die den **Spieler-Charakter** beeinflussen
2. Sage alle anderen Figuren, das das Spiel vorbei ist und **sende** eine `Game Over`{:class="block3events"}-Botschaft, auf die sie reagieren und ändern können, was sie tun
3. Bewege den **Spieler-Charakter** in die Mitte der Bühne und lasse ihn den Spieler darüber informieren, dass das Spiel beendet ist
4. Stoppe alle Skripte im Spiel

--- /collapse---

Jetzt musst du sicherstellen, dass alle Figuren wissen, was zu tun ist, wenn das Spiel vorbei ist, und wie sie sich zurücksetzen, wenn der Spieler ein neues Spiel startet. **Vergiss nicht, dass alle neuen Figuren, die du hinzufügst, möglicherweise Code dafür benötigen!**

### Plattformen und Kanten verstecken

--- task ---

Beginne mit den einfachsten Figuren. Die Figuren **Plattformen** und **Ecken** benötigen beide Code, um angezeigt zu werden, wenn das Spiel beginnt, und um zu verschwinden, wenn sie die Sendung `Game Over`{:class="block3events"} empfangen:

```blocks3
+ wenn ich [Game Over v] empfange
+ verstecke dich
```

```blocks3
+ Wenn grüne Flagge angeklickt wird
+ zeige dich
```

--- /task ---

### Die Sterne stoppen

Wenn du dir nun den Code für die **Sammelobjekt**-Figur ansiehst, wirst du feststellen, dass es funktioniert in dem es **Klone** von sich selbst erstellt. Das heißt, es macht Kopien von sich selbst, die der speziellen `Wenn ich als Klon entstehe`{:class="block3events"}-Anweisung folgen.

Wir werden mehr darüber sprechen, was Klone so besonders macht, wenn wir neue und andere Sammlerstücke erstellen. Was du jetzt wissen musst, ist, dass Klone **fast** alles tun können, was eine normale Figur kann, einschließlich `Sendung an alle`{:class="block3events"} - Nachrichten empfangen.

Schau dir an, wie die **Sammelobjekt**-Figur funktioniert. Schau ob du einen Teil des Codes verstehen kannst:

```blocks3
    wenn grüne Fahne angeklickt wird
    verstecke dich
    setze [sammelobjekt-wert v] zu [1]
    setze [sammelobjekt-geschwindigkeit v] zu [1]
    setze [sammelobjekt-häufigkeit v] zu [1]
    setze [erzeuge-sammelobjekt v] zu [wahr]
    setze [sammelobjekt-typ v] auf [1]
    wiederholen bis <nicht <(create-collectables) = [wahr]>> 
        warten (sammelobjekt-häufigkeit) Sekunden
        gehe zu x: (Wähle zufällig (-240) bis (240)) y: (179)
        erzeuge einen Klon von [mir selbst]
    Ende
```

1. Zuerst wird die ursprüngliche **Sammelobjekt**-Figur durch das Ausblenden unsichtbar
2. Dann werden die Steuervariablen festgelegt - wir kommen später darauf zurück
3. Die Variable `erzeuge-sammelobjekt`{:class="block3variables"} ist der Ein-/Ausschalter für das Klonen: Die Schleife erstellt Klone, wenn `erzeuge-sammelobjekt`{:class="block3variables"} `wahr` ist und nichts wenn sie nicht wahr ist

--- task ---

Richte jetzt einen Block für die **Sammelobjekt**-Figur ein, sodass es auf die `Game Over` Sendung an alle reagiert:

```blocks3
+ Wenn ich [Game Over v] empfange
+ verstecke dich
+ setze [erzeuge-sammelobjekt v] auf [falsch]
```

--- /task ---

Dieser Code ähnelt dem Code, der die **Plattform**- und **Ecken**-Figuren steuert. Der einzige Unterschied ist, dass du auch die `erzeuge-sammelobjekt`{:class="block3variables"} Variable auf `falsch` setzt, sodass keine neuen Klone erstellt werden, wenn ‚Game over‘ gesendet wurde.

Beachte, dass du die `erzeuge-sammelobjekt`{:class=„block3variables“}-Variable benutzen kannst, um Nachrichten von einem Teil des Codes zu einem anderen zu übergeben!