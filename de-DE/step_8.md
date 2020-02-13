## Level 2

Mit diesem Schritt fügst du dem Spiel ein neues Level hinzu, das der Spieler durch Drücken einer Taste erreichen kann. Später kannst du deinen Code so ändern, dass er eine bestimmte Anzahl von Punkten oder etwas anderes benötigt, um dorthin zu gelangen.

### Auf das nächste Level gelangen

--- task ---

Erstelle zunächst eine neue Figur als Schaltfläche, indem du entweder eine Figur aus der Bibliothek hinzufügst oder eine eigene zeichnest. Ich habe ein bisschen von beidem gemacht und das kam dabei heraus:

![Die Tasten-Figur zum Umschalten der Level](images/levelButton.png)

--- /task ---

--- task ---

Der Code für diese Schaltfläche ist clever: er ist so konzipiert, dass du jedes Mal, wenn du darauf klickst, ins nächste Level gelangst, egal wie viele Level es gibt.

Füge diese Skripte deiner **Taste** - Figur hinzu. Du musst dabei einige Variablen erstellen.

```blocks3
+ Wenn die grüne Flagge angeklickt
+ setze [max-Level v] auf [2]
+ setze [min-Level v] auf [1]
+ setze [aktuelles-Level v] auf [1]
```

```blocks3
+ Wenn diese Figur angeklickt wird
+ ändere [aktuelles-Level v] um (1)
+ falls <(aktuelles-Level) > (max-Level :: variables)>  dann 
  setze [aktuelles-Level v] auf (min-Level :: variables)
ende
+ sende [Sammelobjekte-aufräumen v] an alle
+ sende (betrete [Level-] (aktuelles-Level)) an alle
```

--- /task ---

Kannst du sehen, wie das Programm die von dir erstellten Variablen verwendet?

+ `max-Level`{:class="block3variables"} speichert den höchsten Level
+ `min-Level`{:class="block3variables"} speichert den untersten Level
+ `aktuelles-Level`{:class = "block3variables"} speichert das Level, auf dem sich der Spieler gerade befindet

Dies alles muss vom Programmierer \(dir!\) festgelegt werden. Wenn du ein drittes Level hinzufügst, vergiss nicht, den Wert von `max-Level`{:class="block3variables"} zu ändern! `min-Level`{:class="block3variables"} muss natürlich niemals geändert werden.

Die Nachrichten werden verwendet, um den anderen Figuren mitzuteilen, welches Level angezeigt werden soll, und um die Sammelobjekte zu löschen, wenn ein neues Level beginnt.

### Lass die Figuren reagieren

#### Die **Sammelobjekt** - Figur

Jetzt musst du die anderen Figuren dazu bringen, auf diese Nachrichten zu antworten! Beginnen Sie mit dem einfachsten: Alle Sammelobjekte löschen.

--- task ---

Füge den **Sammelobjekt**-Figur-Skripts den folgenden Code hinzu, um allen Klonen zu sagen, dass sie sich `verstecken`{:class="block3looks"} sollen, wenn sie die aufräumen Nachricht empfangen:

```blocks3
+    wenn ich [Sammelobjekte-aufräumen v] empfange   
+    verstecke dich
```

--- /task ---

Das erste was ein neuer Klon macht, ist sich selbst zu zeigen. Daher musst du dir keine Sorgen um das wieder anzeigen von Sammelobjekten machen!

#### Die **Plattormen** - Figur

Jetzt wechselst du die Figur **Plattformen**. Du kannst später dein eigenes neues Level entwerfen, wenn du möchtest, aber jetzt verwenden wir das bereits enthaltene - du wirst den Grund dafür im nächsten Schritt sehen!

--- task ---

Füge diesen Code zur Figur **Plattformen** hinzu:

```blocks3
+ Wenn ich [Level-1 v] empfange
+ wechsle zu Kostüm [Level 1 v]
+ zeige dich
```

```blocks3
+ Wenn ich [Level-2 v] empfange
+ wechsle zu Kostüm [Level 2 v]
+ zeige dich
```

--- /task ---

Die Figur empfängt die `betrete`{:class="block3operators"}-Nachricht von `Level-`{:class="block3variables"} und `aktuelles-Level`{:class="block3variables"}, die die **Taste**-Figur sendet und antwortet durch wechseln des **Plattformen**-Kostüms.

#### Die **Feind** - Figur

--- task ---

Stelle in den Figurskripten des **Feinds** sicher, dass die Figur verschwindet, wenn der Spieler Level 2 betritt:

```blocks3
+ wenn ich [Level-1 v] empfange
+ zeige dich
```

```blocks3
+ wenn ich [Level-2 v] empfange
+ verstecke dich
```

--- /task ---

Wenn du möchtest, kannst du den Feind stattdessen zu einer anderen Plattform bewegen. In diesem Fall würdest du anstelle des `Zeige dich`{:class="block3looks"}- und `Verstecke dich`{:class="block3looks"}-Blocks einen `Gehe zu`{:class="block3motion"}-Block verwenden.

### Lass den **Spielercharakter** an der richtigen Stelle erscheinen

Immer wenn ein neues Level beginnt, muss die Figur des **Spielercharakters** an den richtigen Ort für diesen Level gelangen. Damit dies geschieht, musst du ändern, von wo die Figur ihre Koordinaten erhält, wenn sie das erste Mal auf der Bühne erscheint. Im Moment gibt es im Code feste Werte von `x` und `y`.

--- task ---

Beginne mit dem Erstellen von Variablen für die Startkoordinaten: `start-x`{:class="block3variables"} und `start-y`{:class="block3variables"}. Ziehe sie dann in den `Gehe zu`{:class="block3motion"} - Block im `Spieler-zurücksetzen`{:class="block3myblocks"} **Meine Blöcke** - Block um die festen `x`- und `y`-Werte zu ersetzen:

```blocks3
    Definiere Spieler-zurücksetzen
    setze [kann-springen v] auf [wahr]
    setze [x-Beschleunigung v] auf [0]
    setze [y-Beschleunigung v] auf [-0]
+    gehe zu  x: (start-x) y: (start-y)
```

--- /task ---

--- task ---

Setze als Antwort auf jede Nachricht an alle, die den Beginn eines Levels ankündigt, die richtigen Koordinaten `start-x`{:class="block3variables"} und `start-y`{:class="block3variables"} und füge einen **Aufruf** zu `Spieler-zurücksetzen`{:class="block3myblocks"} hinzu:

```blocks3
+ wenn ich [Level-1 v] empfange
+ setze [start-x v] auf [-183]
+ setze [start-y v] auf [42]
+ Spieler-zurücksetzen :: custom
```

```blocks3
+ wenn ich [Level-2 v] empfange
+ setze [start-x v] auf [-218]
+ setze [start-y v] auf [-143]
+ Spieler-zurücksetzen :: custom
```

--- /task ---

### Beginne mit Level 1

Du musst auch sicherstellen, dass jedes Mal, wenn jemand das Spiel startet, der erste Level den er spielt, Level 1 ist.

--- task ---

Gehe zum Skript `Spiel-zurücksetzen`{:class="block3myblocks"} und entferne den Aufruf von `Spieler-zurücksetzen`{:class="block3myblocks"}. Sende stattdessen `min-Level`{:class="block3variables"} an alle. Der mit dieser Karte bereits hinzugefügte Code setzt dann die korrekten Startkoordinaten für die Figur **Spielercharakter** und ruft auch `Spieler-zurücksetzen`{:class="block3myblocks"} auf.

```blocks3
    Definiere Spiel-zurücksetzen
    setze Drehtyp auf [links-rechts v]
    setze [Sprunghöhe v] auf [15]
    setze [Schwerkraft v] auf [2]
    setze [x-Geschwindigkeit v] auf [1]
    setze [Y-Geschwindigkeit v] auf [1]
    setze [Leben v] auf [3]
    setze [Punkte v] auf [0]
+ Sende (betrete [Level-](min-Level ::variables)) an alle
```

--- /task ---

--- collapse ---
---
title: Zurücksetzen des Spielercharakters im Vergleich zum Zurücksetzen des Spiels
---

Beachte, dass der erste Block im Grüne Flagge Skript der **Spielercharakter** - Figur ein Aufruf an den `Spiel-zurücksetzen`{:class="block3myblocks"} **Meine Blöcke** - Block ist.

Dieser Block legt alle Variablen für ein neues Spiel fest und ruft dann den `Spieler-zurücksetzen`{:class="block3myblocks"} **Meine Blöcke** - Block auf, wodurch der Charakter wieder in die richtige Startposition versetzt wird.

Mit dem `Spieler-zurücksetzen`{:class="block3myblocks"} - Code in einem eigenen Block getrennt von `Spiel-zurücksetzen`{:class="block3myblocks"} kannst du den Charakter in verschiedene Positionen zurücksetzen, **ohne** dass das ganze Spiel zurückgesetzt werden muss.

--- /collapse ---