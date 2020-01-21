## Super potenziamento!

Ora che hai un nuovo potenziamento funzionante da raccogliere, è il momento di fargli fare qualcosa di veramente interessante: facciamo in modo che piovano potenziamenti per alcuni secondi, invece di dare una vita extra.

Per questo, si andrà ad utilizzare un altro messaggio `invia a tutti`{:class="block3events"}.

\--- task \---

First, change the `react-to-player`{:class="block3myblocks"} block to broadcast a message when the player character touches a type `2` collectable. Call the message `collectable-rain`{:class="block3events"}.

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

Now you need to create a new piece of code inside the **Collectable** sprite scripts that will start whenever the `collectable-rain`{:class="block3events"} message is broadcast.

\--- task \---

Add this code for the **Collectable** sprite to make it listen out for the `collectable-rain`{:class="block3events"} broadcast.

```blocks3
+ quando ricevo [catturabili-pioggia v]
+ porta [catturabili-frequenza v] a [0.000001]
+ attendi (1) secondi
+ porta [catturabili-frequenza v] a [1]
```

\--- /task \---

## \--- collapse \---

## title: Cosa fa il nuovo codice?

This piece of code waits to receive a broadcast, and responds by setting the `collectable-frequency`{:class="block3variables"} variable to a very small number, then waiting for one second, and then changing the variable back to `1`.

Let's look at how the `collectable-frequency`{:class="block3variables"} variable is used to find out why this makes it rain collectables.

In the main game loop, the part of the code that makes **Collectable** sprite clones gets told by the `collectable-frequency`{:class="block3variables"} variable how long to wait between making one clone and the next:

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

You can see that the `wait`{:class="block3control"} block here pauses the code for the length of time set by `collectable-frequency`{:class="block3variables"}.

If the value of `collectable-frequency`{:class="block3variables"} is `0.000001`, the `wait`{:class="block3control"} block only pauses for **one millionth** of a second, meaning that the `repeat until`{:class="block3control"} loop will run many more times than normal. As a result, the code is going to create **a lot** more power-ups than it normally would, until `collectable-frequency`{:class="block3variables"} is changed back `1`.

Can you think of any problems that might cause? There’ll be a lot more power-ups…what if you kept catching them?

\--- /collapse \---