## Perdere al gioco

Cominciando dall'inizio! Hai bisogno di un metodo per far finire il gioco quando il giocatore ha esaurito le vite. Al momento ciò non succede.

Potresti aver notato che il blocco `perso`{:class="block3myblocks"} de **I Miei Blocchi** negli script per lo sprite di **Personaggio-giocatore** è vuoto. La riempirai e imposterai tutti i pezzi necessari per una bella schermata 'Game over'.

\--- task \--- Per prima cosa, trova il blocco `perso`{:class="block3myblocks"} e completalo con il seguente codice:

```blocks3
    definisci perso
+ ferma [other scripts in sprite v]
+ invia a tutti [game over v]
+ vai a x: (0) y: (0)
+ dire [Game over!] per (2) secondi
+ ferma [all v]
```

\--- /task \---

## \--- collapse \---

## title: Cosa fa questo codice?

Ogni volta che il blocco `perso`{:class="block3myblocks"} viene eseguito, ciò che fa è:

1. Fermare le leggi fisiche e altri script di gioco che agiscono sul personaggio **Personaggio-giocatore**
2. Dice a tutti gli altri sprite che il gioco è finito trasmettendo con il **broadcasting** a `game over`{:class="block3events"} un messaggio a cui tutti gli sprite possono reagire, cambiando il loro comportamento
3. Muove il personaggio **Personaggio-giocatore** al centro dello schermo e gli fa dire al giocatore che il gioco è finito
4. Interrompe tutti gli script nel gioco

\--- /collapse \---

Ora devi assicurarti che tutti gli sprite sappiano cosa fare quando il gioco è finito e come resettarsi quando il giocatore inizia una nuova partita. **Non dimenticare che eventuali nuovi sprite che aggiungi potrebbero richiedere del codice a questo proposito!**

### Nascondere le piattaforme e i bordi

\--- task \--- Inizia con gli sprite più facili. Gli sprite **Piattaforme** e **Bordi** hanno entrambi bisogno di codice per apparire quando il gioco inizia e sparire quando ricevono il `game over`{:class="block3events"}, quindi aggiungi questi blocchi a ciascuno di essi:

```blocks3
+ quando ricevo [game over v]
+ nascondi
```

```blocks3
+ quando si clicca sulla bandiera verde
+ mostra
```

\--- /task \---

### Fermare le stelle

Ora, se guardi il codice per lo sprite **Catturabili**, vedrai che funziona **clonando** se stesso. Cioè, fa copie di se stesso che seguono le istruzioni del blocco `quando vengo clonato`{:class="block3events"}.

Parleremo nuovamente di cosa rende speciali i cloni quando arriveremo al punto di creare nuovi e diversi oggetti da raccogliere. Per ora, quello che devi sapere è che i cloni possono fare **quasi** tutto ciò che può fare un normale sprite, incluso ricevere i messaggi `broadcast`{:class="block3events"}.

Guarda come funziona lo sprite **Catturabili**. Vedi se riesci a capire un po' del suo codice:

```blocks3
    quando si clicca sulla bandiera verde
nascondi
porta [catturabili-valore v] a [1]
porta [catturabili-velocita v] a [1]
porta [catturabili-frequenza v] a [1]
porta [crea-catturabili v] a [true]
porta [catturabili-tipo v] a [1]
repeat until <not <(create-collectables) = [true]>>
attendi (collectable-frequenza) secondi
vai a x: (numero a caso tra (-240) e (240)) y: (179)
crea clone di [myself v]
end
```

1. Per prima cosa rende invisibile l'originale **Catturabili** nascondendolo
2. Quindi imposta le variabili di controllo - torneremo su queste più tardi
3. La variabile `crea-catturabili`{: class = "block3variables"} è l'interruttore on/off per la clonazione: il ciclo crea cloni se `crea-catturabili`{:class="block3variables"} è `true` e non fa nulla se non lo è

\--- task \--- Ora imposta un blocco per lo sprite **Catturabili** in modo che reagisca al messaggio broadcast `game over`:

```blocks3
+ quando ricevo [game over v]
+ nascondi
+ porta [crea-catturabili v] a [false]
```

\--- /task \---

Questo codice è simile al codice controllo degli sprite **Piattaforme** e **Bordi**. L'unica differenza è che stai anche impostando la variabile `crea-catturabili`{:class="block3variables"} su `false` in modo che nessun nuovo clone venga creato quando è "Game over".

Nota che puoi usare la variabile `crea-catturabili`{:class="block3variables"} per passare messaggi da una parte del tuo codice a un'altra!