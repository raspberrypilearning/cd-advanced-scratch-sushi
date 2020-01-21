## Potenziamenti

Al momento hai solo un tipo di oggetto da raccogliere: una stella che ti fa guadagnare un punto quando la prendi. In questa scheda, creerai un nuovo tipo di oggetto da raccogliere, e lo farai in un modo che aggiungere ulteriori tipi di oggetti da raccogliere sarà più facile. E poi potrai inventare nuovi potenziamenti e bonus e rendere davvero questo gioco il tuo!

Ho già incluso alcuni pezzi per fare ciò grazie alla variabile `catturabili-tipo`{:class="block3variables"} ed il blocco `scegli-costume`{:class="block3myblocks"} ne **I Miei Blocchi**. Avrai bisogno di migliorarli però.

Diamo un'occhiata a come funzionano ora gli oggetti da raccogliere.

Negli script per lo sprite **Catturabili**, cerca il codice `quando vengo clonato`{:class="block3events"}. I blocchi in cui guardare sono quelli che ti danno i punti per la raccolta di una stella:

```blocks3
    se <touching [Player Character v]?> allora 
  cambia [punteggio v] di (catturabili-valore :: variables)
  elimina questo clone
end
```

e questo che seleziona un costume per il clone:

```blocks3
    scegli-costume (catturabili-tipo :: variables) :: custom
```

## \--- collapse \---

## title: Come funziona la scelta di un costume?

Il blocco `scegli-costume`{:class="block3myblocks"} funziona un po' come il blocco `perso`{:class="block3myblocks"}, ma ha qualcosa in più: richiede una variabile di **input** chiamata `tipo`{:class="block3myblocks"}.

```blocks3
    definisci scegli-costume (tipo :: custom-arg)
se <(tipo :: variables) = [1]> allora 
  passa al costume [star1 v]
end
```

Quando viene eseguito il blocco `scegli-costume`{:class="block3myblocks"}, ciò che fa è questo:

1. Cerca la variabile di input `tipo`{:class="block3myblocks"}
2. Se il valore di `tipo`{:class="block3myblocks"} è uguale a `1`, passa al costume `star1`

Dai un'occhiata alla parte dello script che usa il blocco:

```blocks3
    quando vengo clonato
scegli-costume (catturabili-tipo :: variables) :: custom
mostra
ripeti fino a quando <(posizione y) < [-170]> 
  cambia y di (catturabili-velocita :: variables)
  se <touching [Player Character v]?> allora 
    cambia [punteggio v] di (catturabili-valore :: variables)
    elimina questo clone
  end
end
```

Si può vedere che la variabile `catturabili-tipo`{class="block3variables"} viene **passata** al blocco `scegli-costume`{:class="block3myblocks"}. All'interno del codice `scegli-costume`{:class="block3myblocks"}, `catturabili-tipo`{:class="block3variables"} viene quindi utilizzata come variabile di input (`tipo`{:class="block3myblocks"}).

Ciò significa che il valore di `catturabili-tipo`{:class="block3variables"} decide quale costume riceve il clone dello sprite.

\--- /collapse \---

### Aggiungi un costume per il nuovo potenziamento

Certo, adesso lo sprite **Catturabili** ha solo un costume, dal momento che c'è solo un tipo di oggetto da raccogliere. Stai per cambiarlo.

\--- task \---

Add a new costume to the **Collectable** sprite for your new power-up. I like the lightning bolt, but pick whatever you like.

\--- /task \---

\--- task \---

Next, tell the `pick-costume`{:class="block3myblocks"} **My blocks** block to set the new costume whenever it gets the new value for `type`{:class="block3myblocks"}, like this \(using whatever costume name you picked\):

```blocks3
    definisci scegli-costume (type :: custom-arg)
se <(tipo) = [1]> allora 
  passa al costume [star1 v]
end
+ se <(tipo) = [2]> allora 
+  passa al costume [lightning v]
+ end
```

\--- /task \---

### Crea il codice di potenziamento

Now you need to decide what the new collectable will do! We’ll start with something simple: giving the player a new life. In the next step, you’ll make it do something cooler.

\--- task \---

Go into the **My blocks** section and click **Make a Block**. Name the new block `react-to-player`{:class="block3myblocks"} and add a **number input** named `type`{:class="block3myblocks"}.

![Type in the name for the block](images/powerupMakeName.png)

Click **OK**.

\--- /task \---

\--- task \---

Make the `react-to-player`{:class="block3myblocks"} **My blocks** block either increase the points or increase the player’s lives, depending on the value of `type`{:class="block3myblocks"}.

```blocks3
+ definisci reazione-al-giocatore (tipo :: custom-arg)
+ se <(tipo :: custom-arg) = [1]> allora 
+  cambia [punteggio v] di (catturabili-valore :: variables)
+ end
+ se <(tipo :: custom-arg) = [2]> allora 
+  cambia [vite v] di [1]
+ end
```

\--- /task \---

\--- task \---

Update the `when I start as a clone`{:class="block3events"} code to replace the block that adds a point with a **call** to `react-to-player`{:class="block3myblocks"}, **passing** `collectable-type`{:class="block3variables"} to it.

```blocks3
+ se <touching [Player Character v] ?> allora 
+  reazione-al-giocatore (catturabili-tipo :: variables) :: custom
+  elimina questo clone
+ end
```

\--- /task \---

By using this new `react-to-player`{:class="block3myblocks"} **My blocks** block, stars still add a point, but the new power-up you've created adds a life.

### Usare `catturabili-tipo`{:class="block3variables"} per far apparire oggetti da raccogliere a caso

Right now, you might be wondering how you'll tell each collectable the game makes what type it should be.

You do this by setting the value of `collectable-type`{:class="block3variables"}. This variable is just a number. As you've seen, it's used to tell the `pick-costume`{:class="block3myblocks"} and `react-to-player`{:class="block3myblocks"} blocks what costume, rules, etc. to use for the collectable.

## \--- collapse \---

## title: Lavorare con le variabili in un clone

For each clone of the **Collectable** sprite, you can set a different value for `collectable-type`{:class="block3variables"}.

Think of it like creating a new copy of the **Collectable** sprite with the help of the value that is stored in `collectable-type`{:class="block3variables"} at the time the **Collectable** clone gets created.

You might be wondering whether changing the value of `collectable-type`{:class="block3variables"} will turn all the collectables on the Stage into the same type. That doesn't happen, because one of the things that makes clones special is that they cannot change the values of any variables they start with. Sprite clones effectively have **constant** values. That means that when you change the value of `collectable-type`{:class="block3variables"}, this doesn't affect the **Collectable** sprite clones that are already in the game.

\--- /collapse \---

You're going to set the `collectable-type`{:class="block3variables"} to either `1` or `2` for each new clone that you make. To keep the game interesting, pick between the numbers at random to make a random collectable every time.

\--- task \---

Find the `repeat until`{:class="block3control"} loop inside the green flag code for the **Collectable** sprite, and add the `if...else`{:class="block3control"} code shown below.

```blocks3
    repeat until <not <(create-collectables ::variables) = [true]>>
+ se <[50] = (numero a caso tra (1) e (50))> allora 
+  porta [catturabili-tipo v] a [2]
+ altrimenti 
+  porta [catturabili-tipo v] a [1]
+ end
attendi (catturabili-frequenza :: variables) secondi
vai a x: (numero a caso tra (-240) e (240)) y: (179)
crea clone di [me stesso v]
```

\--- /task \---

This code gives a 1-in-50 chance of setting the `collectable-type`{:class="block3variables"} to `2`. After all, you don't want to give the player the chance to collect an extra life too often, otherwise the game would be too easy.

Now you have a new type of collectable that sometimes shows up instead of the star, and that gives you an extra life instead of a point when you collect it.