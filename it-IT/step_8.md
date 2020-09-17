## Livello 2

Seguendo questa scheda, aggiungerai un nuovo livello al gioco a cui il giocatore può accedere premendo semplicemente un pulsante. Più tardi, potrai cambiare il tuo codice per fare in modo che sia necessario ottenere un punteggio minimo, o qualcos'altro, per arrivarci.

### Passaggio al livello successivo

\--- task \---

Innanzitutto, crea un nuovo sprite che serva da pulsante aggiungendone uno dalla libreria o disegnando il tuo. Io ho fatto un po' di entrambi e mi sono inventato questo:

![Il pulsante sprite per cambiare i livelli](images/levelButton.png)

\--- /task \---

\--- task \---

Ora, il codice per questo pulsante è ingegnoso: è progettato in modo che ogni volta che lo premi ti porterà al livello successivo, indipendentemente da quanti livelli ci siano.

Aggiungi questi script allo sprite **Pulsante**. Dovrai creare alcune variabili mentre lo fai.

```blocks3
+ quando si clicca sulla bandiera verde
+ porta [max-livello v] a [2]
+ porta [min-livello v] a [1]
+ porta [livello-attuale v] a [1]
```

```blocks3
+ quando si clicca questo sprite
+ cambia [livello-attuale v] di (1)
+ se <(livello-attuale) > (max-livello :: variables)> allora 
  porta [livello-attuale v] a (min-livello :: variables)
end
+ invia a tutti [catturabili-ripulisci v]
+ invia a tutti (unione di [livello-] e (livello-attuale))
```

\--- /task \---

Riesci a capire come il programma userà le variabili che hai creato?

+ `max-livello`{:class="block3variables"} memorizza il livello più alto
+ `min-livello`{:class="block3variables"} memorizza il livello più basso
+ `livello-attuale`{:class="block3variables"} memorizza il livello al quale il giocatore si trova in questo momento

Questi devono essere tutti impostati dal programmatore \(tu! \), quindi se aggiungi un terzo livello, non dimenticare di cambiare il valore di `max-livello`{:class="block3variables"}! `min-livello`{:class="block3variables"} non avrà mai bisogno di cambiare, ovviamente.

Le trasmissioni dei messaggi broadcast sono utilizzate per indicare agli altri sprite quale livello visualizzare, e per azzerare gli oggetti da raccogliere all'avvio di un nuovo livello.

### Fai reagire gli sprite

#### Lo sprite **Catturabili**

Ora devi convincere gli altri sprite a rispondere a queste trasmissioni! Inizia con quello più semplice: azzerare tutti gli oggetti da raccogliere.

\--- task \---

Aggiungi il seguente codice agli script dello sprite **Catturabili** per dire a tutti i suoi cloni `nascondi`{:class="block3vlooks"} quando ricevono il messaggio broadcast di ripulitura:

```blocks3
+ quando ricevo [catturabili-ripulisci v]
+ nascondi
```

\--- /task \---

Dal momento che una delle prime cose che fa un nuovo clone è mostrarsi, non devi preoccuparti di mostrare gli oggetti da raccogliere!

#### Gli sprite **Piattaforme**

Ora vediamo come cambiare lo sprite **Piattaforme**. Puoi progettare il tuo nuovo livello più tardi se lo desideri, ma per ora utilizziamo quello che ho già incluso - vedrai il perché nella prossima scheda!

\--- task \---

Aggiungi questo codice allo sprite **giocatore**:

```blocks3
+ quando ricevo [livello-1 v]
+ passa al costume [Livello 1 v]
+ mostra
```

```blocks3
+ quando ricevo [livello-2 v]
+ passa al costume [Livello 2 v]
+ mostra
```

\--- /task \---

Riceve i messaggi `composti`{:class="block3operators"} da `livello-`{:class="block3variables"} e `livello-attuale`{:class="block3variables"} inviati dallo sprite **Pulsante**, e risponde cambiando il costume **Piattaforme**.

#### Lo sprite nemico **Nemico**

\--- task \---

Negli script dello sprite **Nemico**, assicurati che lo sprite scompaia quando il giocatore entra nel livello 2, in questo modo:

```blocks3
+ quando ricevo [livello-1 v]
+ mostra
```

```blocks3
+ quando ricevo [livello-2 v]
+ nascondi
```

\--- /task \---

Se preferisci, puoi far spostare il nemico su un'altra piattaforma. In questo caso, useresti un blocco `vai a`{:class="block3motion"} invece dei blocchi `mostra`{:class="block3looks"} e `nascondi`{:class="block3looks"}.

### Fai apparire il personaggio **Personaggio-giocatore** nel posto giusto

Ogni volta che inizia un nuovo livello, lo sprite di **Personaggio-giocatore** deve andare nel posto giusto per quel livello. Per fare in modo che ciò accada, è necessario cambiare il punto in cui lo sprite ottiene le sue coordinate dalla prima volta che appare sullo schermo. Al momento, ci sono valori fissi `x` e `y` nel suo codice.

\--- task \---

Inizia creando variabili per le coordinate di partenza: `partenza-x`{:class="block3variables"} e `partenza-y`{:class="block3variables"}. Quindi inseriscili nel blocco `vai a`{:class="block3motion"} nel blocco `reset-personaggio`{:class="block3myblocks"} de **I Miei Blocchi** invece dei valori fissi di `x` e `y`:

```blocks3
    definisci reset-character
porta [puo-saltare v] a [true]
porta [x-velocita v] a [0]
porta [y-velocita v] a [-0]
+ vai a x: (partenza-x) y: (partenza-y)
```

\--- /task \---

\--- task \---

Quindi per ogni trasmissione che annuncia l'inizio di un livello, imposta le coordinate `partenza-x`{:class= "block3variables"} e `partenza-y`{:class="block3variables"} in risposta, e aggiungi una **chiamata** a `reset-personaggio`{:class="block3myblocks"}:

```blocks3
+ quando ricevo [livello-1 v]
+ porta [partenza-x v] a [-183]
+ porta [partenza-y v] a [42]
+ reset-personaggio :: custom
```

```blocks3
+ quando ricevo [livello-2 v]
+ porta [partenza-x v] a [-218]
+ porta [partenza-y v] a [-143]
+ reset-personaggio :: custom
```

\--- /task \---

### Partenza dal livello 1

Devi anche assicurarti che ogni volta che qualcuno inizia il gioco, il primo livello che giocano sia il livello 1.

\--- task \---

Vai allo script `reset-partita`{:class="block3myblocks"} e rimuovi la chiamata a `reset-personaggio`{:class="block3myblocks"}. Al suo posto, trasmetti il `min-livello`{:class="block3variables"}. Il codice che hai già aggiunto con questa scheda imposterà quindi le coordinate iniziali corrette per lo sprite **Personaggio-giocatore**, e chiamerà anche `reset-personaggio`{:class="block3myblocks"}.

```blocks3
    definisci reset-partita
usa stile rotazione [sinistra-destra v]
porta [salto-altezza v] a [15]
porta [gravita v] a [2]
porta [x-velocita v] a [1]
porta [y-velocita v] a [1]
porta [vite v] a [3]
porta [punteggio v] a [0]
+ invia a tutti (unione di [livello-] e (min-livello :: variables))
```

\--- /task \---

## \--- collapse \---

## title: Reset del personaggio del giocatore rispetto al reset della partita

Si noti che il primo blocco nello script principale della bandiera verde dello sprite **Personaggio-giocatore** è una chiamata al `reset-partita`{:class="block3myblocks"} de **I Miei Blocchi**.

Questo blocco imposta tutte le variabili per un nuovo gioco e quindi chiama il blocco `reset-personaggio`{:class="block3myblocks"} de **I Miei Blocchi**, che riporta il personaggio nella sua posizione iniziale corretta.

Essendo il codice `reset-personaggio`{:class="block3myblocks"} separato da `reset-partita`{:class="block3myblocks"} ciò ti permette di reimpostare il personaggio in diverse posizioni **senza che** si debba reimpostare l'intero gioco.

\--- /collapse \---