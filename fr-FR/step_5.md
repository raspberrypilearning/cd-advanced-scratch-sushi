## Super power-ups !

Maintenant que tu as une nouvelle collection de power-ups qui fonctionnent, il est temps de faire quelque chose de vraiment cool : faisons en sorte que les power-ups « pleuvent » pendant quelques secondes, au lieu de simplement donner une vie supplémentaire.

Pour cela, tu vas utiliser un autre message `diffuser`{:class="block3events"}.

\--- task \---

Tout d'abord, change le bloc `réagir-au joueur`{:class="block3myblocks"} pour diffuser un message lorsque le personnage du joueur touche un collectable-type `2` . Appelle le message `collectable-pluie `{:class="block3events"}.

```blocks3
    define react-to-player (type)
    if <(type ::variable) = [1]> then
        change [points v] by (collectable-value ::variables)
    end
    if <(type ::variable) = [2]> then
-        change [lives v] by [1]    
+        broadcast [collectable-rain v]
    end
```

\--- /task \---

Maintenant tu dois créer un nouveau morceau de code à l'intérieur du script du sprite **Collectable** qui commencera chaque fois que le message `collectable-pluie`{:class="block3events"} est diffusé.

\--- task \---

Ajoute ce code pour le sprite **Collectable** pour le faire écouter pour la diffusion de `collectable-pluie`{:class="block3events"} .

```blocks3
+    when I receive [collectable-rain v]
+    set [collectable-frequency v] to [0.000001]
+    wait (1) secs
+    set [collectable-frequency v] to [1]
```

\--- /task \---

## \--- collapse \---

## title: Que fait le nouveau code ?

Ce morceau de code attend pour recevoir un message, et répond en mettant la variable `collectable-fréquence`{:class="block3variables"} à un très petit nombre, puis attend une seconde, et puis change la variable en `1`.

Regardons comment la variable `collectable-fréquence`{:class="block3variables"} est utilisée pour découvrir pourquoi cela fait qu'il pleut des objets de collection.

Dans la boucle du jeu principal, la partie du code qui fait que les clones de sprites **Collectable** se voient dire par la `collectable-fréquence`{:class="block3variables"} combien de temps attendre entre faire un clone et le suivant :

```blocks3
    repeat until <not <(create-collectables ::variables) = [true]>>
        if < [50] = (pick random (1) to (50))> then
            set [collectable-type v] to [2]
        else
            set [collectable-type v] to [1]
        end
        wait (collectable-frequency ::variables) secs
        go to x: (pick random (-240) to (240)) y:(179)
        create clone of [myself v]
    end
```

Tu peux voir que le bloc `attendre`{:class="block3control"} met ici en pause le code pour la durée définie par `collectable-fréquence`{:class="block3variables"}.

Si la valeur de `collectable-fréquence`{:class="block3variables"} est `0.00001`, le bloc `attendre`{:class="block3control"} ne met en pause que pour **un millionième de** seconde, ce qui signifie que la boucle `répéter jusqu'à`{:class="block3control"} s'exécutera plus de fois que d'habitude. Par conséquent, le code va créer **beaucoup** plus de power-ups qu'il ne le ferait normalement jusqu'à ce que `collectable-fréquence`{:class="block3variables"} soit remise à `1`.

Peux-tu penser aux problèmes que cela pourraient causer ? Il y aura beaucoup plus de power ups … Et qu'est-ce qui se passerait si tu continues à les attraper ?

\--- /collapse \---