## Super potenziamento!

Ora che hai un nuovo potenziamento funzionante da raccogliere, è il momento di fargli fare qualcosa di veramente interessante: facciamo in modo che piovano potenziamenti per alcuni secondi, invece di dare una vita extra.

Per questo, si andrà ad utilizzare un altro messaggio `invia a tutti`{:class="block3events"}.

\--- task \--- Innanzitutto, modifica il blocco `reazione-al-giocatore`{:class="block3myblocks"} per trasmettere un messaggio quando il personaggio del giocatore tocca uno sprite catturabile di tipo `2`. Chiama il messaggio `catturabili-pioggia`{:class="block3events"}.

```blocks3
    definisci reazione-al-giocatore (tipo :: custom-arg)
se <(tipo :: custom-arg) = [1]> allora 
  cambia [punteggio v] di (catturabili-valore :: variables)
end
se <(tipo :: custom-arg) = [2]> allora 
- cambia [vite v] di [1]
+ invia a tutti [catturabili-pioggia v]
end
```

\--- /task \---

Ora devi creare una nuova porzione di codice all'interno dello script dello sprite **Catturabili** che verrà avviati ogni volta che viene trasmesso il messaggio `catturabili-pioggia` {:class="block3events"}.

\--- task \--- Aggiungi questo codice nello sprite **Catturabili** per fargli ascoltare il messaggio `catturabili-pioggia`{:class="block3events"}.

```blocks3
+ quando ricevo [catturabili-pioggia v]
+ porta [catturabili-frequenza v] a [0.000001]
+ attendi (1) secondi
+ porta [catturabili-frequenza v] a [1]
```

\--- /task \---

## \--- collapse \---

## title: Cosa fa il nuovo codice?

Questo pezzo di codice attende di ricevere un messaggio, e risponde impostando la variabile della frequenza di raccolta `catturabili-frequenza`{:class="block3variables"} ad un numero molto piccolo, attende un secondo, e poi riporta la variabile di nuovo a `1`.

Diamo un'occhiata a come la variabile `catturabili-frequenza`{:class="block3variables"} è usata per capire come riesce a far piovere oggetti da raccogliere.

Nel ciclo di gioco principale, la parte del codice che crea gli sprite cloni **Catturabili** viene istruita dalla variabile `catturabili-frequenza`{:class="block3variables"}per sapere quanto attendere tra un clone e il successivo:

```blocks3
    repeat until <not <(create-collectables ::variables) = [true]>>
se <[50] = (numero a caso tra (1) e (50))> allora 
  porta [catturabili-tipo v] a [2]
altrimenti 
  porta [catturabili-tipo v] a [1]
end
attendi (catturabili-frequenza :: variables) secondi
vai a x: (numero a caso tra (-240) e (240)) y: (179)
crea clone di [me stesso v]
end
```

Puoi vedere che il blocco `aspetta`{:class="block3control"} qui mette in pausa il codice per la durata del tempo impostata da `catturabili-frequenza`{:class="block3variables"}.

Se il valore di `catturabili-frequenza`{:class="block3variables"} è `0.000001`, il blocco `aspetta`{:class="block3control"} si interrompe soltanto per un **milionesimo** di secondo, il che significa che il ciclo `ripeti fino o quando`{:class="block3control"} verrà eseguito molte più volte del normale. Di conseguenza, il codice crea **tanti più** potenziamenti del normale, fino a che `catturabili-frequenza`{:class="block3variables"} torna di nuovo a `1`.

Riesci a pensare a eventuali problemi che ciò potrebbe causare? Ci saranno molti più potenziamenti…se continuassi a prenderli?

\--- /collapse \---