## Aggiungiamo un po' di difficoltà

Il tuo gioco funziona e ora puoi raccogliere punti, ottenere poteri speciali dai potenziamenti e anche perdere. Stiamo arrivando da qualche parte! Forse sarebbe divertente aggiungere un po' di concorrenza - che dici di includere un personaggio che si muove un po', ma che non dovresti toccare? Sarà simile ai nemici nei tradizionali giochi come Super Mario da cui ci siamo ispirati.

\--- task \---

Prima cosa, scegli uno sprite da aggiungere come tuo nemico. Poiché il nostro personaggio è un gatto, ho scelto un cane. Ci sono molti altri sprite che potresti aggiungere. Ho anche ribattezzato lo sprite nemico **Nemico**, giusto per rendere le cose più chiare per me.

Ridimensiona lo sprite alla giusta dimensione e posizionalo in un punto appropriato per iniziare. Ecco come appare il mio:

![Lo sprite del cane nemico](images/enemySprite.png)

\--- /task \---

\--- task \---

Scrivi prima il codice più semplice: imposta il blocco per reagire al messaggio `game over`{:class="events"} che fa sparire il nemico quando il giocatore perde la partita.

```blocks3
+ quando ricevo [game over v]
+ nascondi
```

\--- /task \---

\--- task \---

Ora devi scrivere il codice per ciò che deve fare il nemico. Usa il mio codice, ma valuta l'aggiunta di qualcosa extra! (E se potessero teletrasportarsi su piattaforme diverse? Cosa succede se c'è un potenziamento che li fa muovere più velocemente, o più lentamente?)

```blocks3
+ quando si clicca sulla bandiera verde
+ mostra
+ porta [nemico-moto-passi v] a [5]
+ usa stile rotazione [sinistra-destra v]
+ vai a x: (-25) y: (-9)
+ per sempre 
fai (nemico-moto-passi) passi
  if <not <touching [Platforms v] ?>> then
  porta [nemico-moto-passi v] a ((nemico-moto-passi) * (-1))
end
end
```

**Nota**: se trascini il blocco `vai a`{:class="block3motion"} nel pannello sprite e non cambi i valori `x` e `y`, questi saranno anche i valori per la posizione corrente dello sprite del **Nemico**!

Il codice nel blocco `se... allora`{:class="block3control"} farà tornare lo sprite indietro quando arriva alla fine della piattaforma!

\--- /task \---

La prossima cosa di cui hai bisogno è far perdere una vita al giocatore quando il loro sprite **Personaggio-giocatore** tocca lo sprite **Nemico**. Inoltre, è necessario assicurarsi che gli sprite si **fermino** molto velocemente dopo il tocco, poiché altrimenti il codice che controlla il tocco continuerà a funzionare e il giocatore continuerà a perdere vite.

\--- task \---

Ecco come l'ho fatto, ma puoi provare a migliorare questo codice! Ho modificato il blocco principale dello sprite **Personaggio-giocatore**. Aggiungi il nuovo codice prima del blocco `se`{:class="block3control"} che controlla se hai terminato le vite.

```blocks3
    quando si clicca sulla bandiera verde
reset-partita :: custom
per sempre 
  mondo-reale :: custom
  se <(posizione y) <[-179]> allora 
    nascondi
    reset-personaggio :: custom
    cambia [vite v] di (-1)
    attendi (0.05) secondi
    mostra
  end
  + se <touching [Enemy v] ?> allora 
  +   nascondi
  +   vai a x: (-187) y: (42)
  +   cambia [vite v] di (-1)
  +   attendi (0.5) secondi
  +   mostra
  + end
  se <(vite) <[1]> allora 
    perso :: custom
  end
end
```

\--- /task \---

Il nuovo codice nasconde lo sprite **Personaggio-giocatore**, lo riporta alla sua posizione di partenza, riduce la variabile `vite`{:class="block3variables"} di `1`, e dopo mezzo secondo fa riapparire lo sprite.