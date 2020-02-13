## Wettbewerb hinzufügen

Dein Spiel funktioniert und jetzt kannst du Punkte sammeln, besondere Kräfte von deinen Power-Ups erhalten und verlieren. Wir kommen weiter! Vielleicht wäre es Spaßig, ein wenig Konkurrenz hinzuzufügen - wie wäre es mit einer Figur, die sich ein wenig herum bewegt, die man aber nicht berühren sollte? Dies ist ähnlich zu Gegnern in traditionellen Plattformspielen wie Super Mario, die uns hier inspirieren.

--- task ---

Wähle zuerst eine Figur aus, die du als Feind hinzufügst. Da unsere Spielerfigur eine Katze ist, habe ich einen Hund ausgewählt. Es gibt viele andere Figuren, die du hinzufügen könntest. Ich habe auch die Figur in **Feind** umbenannt, nur um die Dinge für mich klarer zu machen.

Verändere die Größe der Figur auf die richtige Größe und platziere sie an einem geeigneten Ort, um zu beginnen. So sieht meins aus:

![Die Feindfigur Hund](images/enemySprite.png)

--- /task ---

--- task ---

Schreibe zuerst den einfachsten Code: Richte den Block ein, der auf die Meldung `Game Over`{:class="events"} reagiert, um den Feind verschwinden zu lassen, wenn der Spieler das Spiel verliert.

```blocks3
+ wenn ich [game over v] empfange
+ verstecke dich
```

--- /task ---

--- task ---

Nun musst du den Code für das, was der Feind tut, schreiben. Verwende meinen Code, erwäge jedoch, ein paar zusätzliche Dinge hinzuzufügen! (Was, wenn er sich auf verschiedene Plattformen teleportieren könnte? Was, wenn es ein Power-Up gibt, das ihn schneller oder langsamer bewegt?)

```blocks3
+ Wenn die grüne Flagge angeklickt
+ zeige dich
+ setze [Feindzugschritte v] auf [5]
+ setze Drehtyp auf [links-rechts v]
+ gehe zu x: (-25) y: (-9)
+ wiederhole fortlaufend 
  gehe (Feindzugschritte) er Schritt
  falls <nicht <wird [Platforms v] berührt?>> , dann
  setze [Feindzugschritte v] auf ((Feindzugschritte) * (-1))
end
```

**Hinweis**: Wenn du den `Gehe zu`{:class="block3motion"} - Block einfach in das Figur-Feld ziehst und die Werte für `x` und `y` nicht änderst, haben sie die Werte für den aktuellen Standort der **Feind** - Figur!

Der Code im `wenn... dann`{:class="block3control"} - Block bewirkt, dass die Figur umkehrt, wenn sie das Ende der Plattform erreicht!

--- /task ---

Als Nächstes musst du hinzufügen, dass der Spieler ein Leben verliert, wenn er mit seiner **Spielercharakter** -Figur einen **Feind** berührt. Außerdem musst du sicherstellen, dass die Figuren wirklich schnell **aufhören** sich zu berühren, da andernfalls der Code, der auf Berührungen überprüft, weiterhin ausgeführt wird und der Spieler weiterhin Leben verliert.

--- task ---

So habe ich es gemacht, aber du kannst versuchen, diesen Code zu verbessern! Ich habe den Hauptblock der **Spielercharakter**-Figur geändert. Füge den neuen Code vor dem `wenn`{:class="block3control"} - Block hinzu, der überprüft, ob du kein Leben mehr hast.

```blocks3
    Wenn die grüne Flagge angeklickt
    Spiel-zurücksetzen :: custom
    wiederhole fortlaufend 
      Hauptphysik :: custom
      falls <(y-Position) < [-179]> , dann 
        verstecke dich
        Spieler-zurücksetzen:: custom
        ändere [Leben v] um (-1)
        warte (0.05) Sekunden
        zeige dich
      ende
+      falls <wird [Feind v] berührt?> , dann 
        verstecke dich
        gehe zu x: (-187) y: (42)
        ändere [Leben v] um (-1)
        warte (0.5) Sekunden
        zeige dich
+      ende
      falls <(Leben) < [1]> , dann 
        verlieren :: custom
      ende
    end
```

--- /task ---

Mit dem neuen Code wird die **Spielercharakter**-Figur ausgeblendet, in die Ausgangsposition zurückbewegt, die `Leben`{:class="block3variables"}-Variable um `1` reduziert und nach einer halben Sekunde erscheint die Figur erneut.