## Power-Up

Im Moment hast du nur eine Art Sammelobjekt: einen Stern, der dir einen Punkt bringt, wenn du ihn auffängst. Auf dieser Karte erstellst du eine neue Art von Sammelobjekt, und tust dies auf eine Weise, die das Hinzufügen anderer Arten von Sammelobjekten vereinfacht. Danach kannst du deine eigenen Power-Ups und Boni erfinden und das Spiel wirklich zu deinem eigenen machen!

Ich habe bereits einige Teile dazu mit der Variable `sammelobjekt-typ`{:class="block3variables"} und dem `wähle-Kostüm`{:class="block3myblocks"} **Meine Blöcke**-Block hinzugefügt. Du musst sie jedoch verbessern.

Schauen wir uns an, wie das Sammelobjekt jetzt funktioniert.

Suche in den Skripten für die Figur **Sammelobjekt** den `wenn ich als Klon entstehe`{:class="block3events"}-Code. Die Blöcke, die du betrachten solltest, sind diejenigen die dir Punkte geben, wenn du einen Stern sammelst:

```blocks3
    falls <wird [Spieler Character v]berührt?>, dann
    ändere [Punkte v] um (Sammelobjekt-wert::variables)
    lösche diesen Klon
```

und diesen hier, der ein Kostüm für den Klon auswählt:

```blocks3
    wähle-Kostüm (Sammelobjekt-typ ::variables) :: custom
```

--- collapse ---
---
title: Wie funktioniert das Auswählen eines Kostüms?
---

Der `wähle-Kostüm`{:class="block3myblocks"}-Block funktioniert ein bisschen wie der `verlieren`{:class="block3myblocks"}-Block, aber er kann etwas Besonderes: Er benötigt eine **Eingabe-**Variable mit der Bezeichnung `Typ`{:class="block3myblocks"}.

```blocks3
Definiere wähle-Kostüm (typ :: custom-arg)
falls <(typ :: variables) = [1]> , dann 
  wechsle zu Kostüm [Stern1 v]
end
```

Wenn der Block `wähle-Kostüm`{:class="block3myblocks"} ausgeführt wird, macht er Folgendes:

1. Es betrachtet die Eingangsvariable `Typ`{:class="block3myblocks"}
2. Wenn der Wert von `Typ`{:class="block3myblocks"} gleich `1`ist, wechselt er zum `Stern1` - Kostüm

Schau dir den Teil des Skripts an, der den Block verwendet:

```blocks3
    Wenn ich als Klon entstehe
  wähle-Kostüm (Sammelobjekt-Typ ::variables) :: custom
  zeige dich
  wiederhole bis <(y-Position) <[-170]> 
     ändere y um (Sammelobjekt-Geschwindigkeit ::variables)
     falls <wird [Spieler Character v] berührt?> , dann 
          ändere [Punkte v] um (Sammelobjekt-Wert ::variables)
          lösche diesen Klon
  Ende
Ende
```

Du siehst, dass die `Sammelobjekt-Typ`{:class="block3variables"} - Variable an den `wähle-Kostüm`{:class="block3myblocks"}-Block **weitergereicht** wird. Im Code für `wähle-Kostüm`{:class="block3myblocks"}, wird `Sammelobjekt-Typ`{:class="block3variables"} dann als Eingabevariable (`Typ`{:class="block3myblocks"}) verwendet.

Das bedeutet, dass der Wert von `Sammelobjekt-Typ`{:class="block3variables"} entscheidet, welches Kostüm der Klon der Figur erhält.

--- /collapse ---

### Füge ein Kostüm für das neue Power-Up hinzu

Natürlich hat die **Sammelobjekt** - Figur momentan nur ein Kostüm, da es nur eine Art von Sammelobjekten gibt. Du wirst das jetzt ändern.

--- task ---

Füge ein neues Kostüm zur **Sammelobjekt** - Figur für das neue Power-Up hinzu. Ich mag den Blitz, aber wähle, was du willst.

--- /task ---

--- task ---

Als nächstes sage dem `wähle-Kostüm`{:class="block3myblocks"} **Meine Blöcke** - Block, dass er das neue Kostüm nutzen soll, wenn er einen neuen Wert für `typ`{:class="block3myblocks"} erhält, wie folgt \(nutze den Kostümnamen, den du gewählt hast\):

```blocks3
    Definiere wähle-Kostüm (typ)
    falls <(typ ::variable) = [1]>, dann
        wechsle zu Kostüm [Stern v] 
    Ende
+    falls <(typ ::variable) = [2]>, dann
+         wechsle zu Kostüm [Blitz v]
+    Ende
```

--- /task ---

### Erstelle den Power-Up-Code

Jetzt musst du entscheiden, was das neue Sammelobjekt tun wird! Wir beginnen mit etwas Einfachem: Dem Spieler ein neues Leben geben. Im nächsten Schritt musst du dafür sorgen, dass es etwas Cooleres macht.

--- task ---

Wechsle in den Bereich **Meine Blöcke** und klicke auf **Neuer Block**. Benenne den neuen Block `reagiere-auf-Spieler`{:class="block3myblocks"} und füge ein **Zahl-Eingabefeld** mit dem Namen `Typ`{:class="block3myblocks"} hinzu.

![Gebe den Namen für den Block ein](images/powerupMakeName.png)

Klicke auf **OK**.

--- /task ---

--- task ---

Lasse den `reagiere-auf-spieler`{:class="block3myblocks"} **Meine Blöcke**-Block entweder die Punkte oder die Leben des Spielers erhöhen, abhängig vom Wert von `typ`{:class="block3myblocks"}.

```blocks3
+ Definiere reagiere-auf-Spieler (typ)
+ falls <(typ ::variable) = [1]>, dann
+    ändere [Punkte v] um (Sammelobjekt-Wert ::variables)
+ Ende
+ falls <(typ ::variable) = [2]>, dann
+     ändere [Leben v] um [1]
+ Ende
```

--- /task ---

--- task ---

Aktualisiere den `Wenn ich als Klon entstehe`{:class="block3events"} Code, um den Block, der einen Punkt addiert, durch einen **Aufruf** von `reagiere-auf-Spieler`{:class="block3myblocks"}, dem du `Sammelobjekt-Typ`{:class="block3variables"} **übergibst**, zu ersetzten.

```blocks3
+ falls <wird [Spieler Character v] berührt?>, dann
+       reagiere-auf-Spieler (Sammelobjekt-Typ ::variables) :: custom
+       lösche diesen Klon
+    Ende
```

--- /task ---

Mit diesem neuen `reagiere-auf-Spieler`{:class="block3myblocks"} **Meine Blöcke**-Block fügen Sterne immer noch einen Punkt hinzu, aber das neu erstellte Power-Up fügt ein Leben hinzu.

### Verwende `Sammelobjekt-Typ`{:class="block3variables"}, um verschiedene Sammelobjekte zufällig erscheinen zu lassen

Im Moment fragst du dich vielleicht, wie du jedem Sammelobjekt, das das Spiel erzeugt, sagst welchen Typ es haben sollte.

Das tust du, indem du den Wert von `Sammelobjekt-Typ`{:class="block3variables"} festlegst. Diese Variable ist nur eine Zahl. Wie du gesehen hast, wird es verwendet, um `wähle-Kostüm`{:class="block3myblocks"}- und `reagiere-auf-Spieler`{:class="block3myblocks"}-Blöcken zu sagen, welche Kostüme, Regeln usw. für das Sammelobjekt verwendet werden.

--- collapse ---
---
title: Mit Variablen in einem Klon arbeiten
---

Für jeden Klon der Figur **Sammelobjekt** kannst du einen anderen Wert für `Sammelobjekt-Typ`{:class="block3variables"} festlegen.

Stell dir vor, du erstellst eine neue Kopie der **Sammelobjekt**-Figur mit Hilfe des Werts, der in `Sammelobjekt-Typ`{:class="block3variables"} gespeichert ist, wenn der **Sammelobjekt**-Klon erstellt wird.

Du fragst dich vielleicht, ob durch das Ändern des Werts von `Sammelobjekt-Typ`{:class="block3variables"} alle Sammelobjekte auf der Bühne in denselben Typ umgewandelt werden. Das passiert nicht, weil ein Ding das Klone speziell macht ist, dass sie Werte von Variablen, mit denen sie beginnen, nicht ändern können. Figur-Klone haben tatsächlich **konstante** Werte. Das heißt, wenn du den Wert von `Sammelobjekt-Typ`{:class="block3variables"} änderst, hat dies keinen Einfluss auf die **Sammelobjekt**-Figur-Klone, die bereits im Spiel sind.

--- /collapse ---

Du wirst den `Sammelobjekt-Typ`{:class="block3variables"} für jeden neuen Klon, den du erstellst, entweder auf `1` oder `2` setzen. Um das Spiel interessant zu halten, wähle zufällig eine Zahl aus, um jedes Mal ein zufälliges Sammelobjekt zu erstellen.

--- task ---

Finde die `Wiederhole bis`{:class="block3control"} -Schleife im grünen Flagge-Code für die **Sammelobjekt**-Figur und füge den `wenn... dann `{:class="block3control"} Code, der unten angezeigt wird, ein.

```blocks3
    wiederhole bis <nicht <(erzeuge-Sammelobjekte :: variables) = [wahr]>> 
+    falls <[50] = (Zufallszahl von (1) bis (50))> , dann 
+    setze [Sammelobjekt-Typ v] auf [2]
+    sonst 
+    setze [Sammelobjekt-Typ v] auf [1]
+    end
    warte (Sammelobjekt-Häufigkeit :: variables) Sekunden
    gehe zu x: (Zufallszahl von (-240) bis (240)) y: (179)
    erzeuge Klon von [mir selbst v]
```

--- /task ---

Dieser Code sorgt mit einer 1 zu 50-Chance dafür, das `Sammelobjekt-Typ`{:class="block3variables"} auf `2` gesetzt wird. Schließlich möchtest du dem Spieler nicht zu oft die Chance geben, ein zusätzliches Leben zu sammeln, sonst wäre das Spiel zu einfach.

Jetzt hast du eine neue Art von Sammelobjekt, das manchmal anstelle des Sterns auftaucht und dem Spieler beim Sammeln ein zusätzliches Leben anstelle eines Punktes gibt.