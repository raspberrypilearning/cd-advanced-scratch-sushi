## Perdre la partie

Tout d'abord ! Tu dois trouver un moyen de mettre fin au jeu lorsque le joueur est à court de vies. Pour le moment, cela ne se produit pas.

Tu as peut-être remarqué que le bloc `perdre`{:class="block3myblocks"} de **Mes blocs** dans les scripts du sprite **Perso joueur** est vide. Tu vas remplir ceci et mettre en place toutes les pièces nécessaires pour un bel écran « Partie terminée ».

\--- task \---

Tout d'abord, trouve le bloc `perdu`{:class="block3myblocks"} et complète-le avec le code suivant :

```blocks3
    define lose
+    stop [other scripts in sprite v] :: control stack
+    broadcast [game over v]
+    go to x:(0) y:(0)
+    say [Game over!] for (2) secs
+    stop [all v]
```

\--- /task \---

## \--- collapse \---

## titre: Que fait ce code ?

À chaque fois que le bloc `perdu`{:class="block3myblocks"} s'exécute, ce qu'il fait est :

1. Arrêter la physique et les autres scripts de jeu agissant sur le **Perso joueur**
2. Dire à tous les autres sprites que le jeu est terminé par **diffusion ** du message `partie terminée`{:class="block3events"} auquel ils peuvent répondre et changer ce qu'ils font
3. Déplacer le **Perso joueur** au centre de la scène et leur faire dire au joueur que la partie est terminée
4. Arrêter tous les scripts du jeu

\--- /collapse \---

Maintenant tu dois t'assurer que tous les sprites savent quoi faire quand le jeu est terminé, et comment se réinitialiser quand le joueur démarre une nouvelle partie. **N'oublie pas que tous les nouveaux sprites que tu ajoutes peuvent aussi avoir besoin de code pour cela !**

### Cacher les plateformes et les bords

\--- task \---

Commence avec les sprites les plus simples. Les sprites **Plateformes** et **Bords** ont tous deux besoin de code pour apparaître quand le jeu commence et disparaître quand ils reçoivent le message `partie terminée`{:class="block3events"}, donc ajoute ces blocs à chacun d'eux :

```blocks3
+    when I receive [game over  v]
+    hide
```

```blocks3
+    when green flag clicked
+    show
```

\--- /task \---

### Arrêter les étoiles

Maintenant, si tu regardes le code du sprite **Collectable**, tu verras qu'il fonctionne par **clonage** de lui-même. C'est-à-dire qu'il fait des copies de lui-même qui suivent les instructions spéciales `quand je commence comme un clone`{:class="block3events"} .

Nous parlerons plus de ce qui rend les clones spéciaux lorsque nous arriverons à l'étape de la création de nouveaux objets de collection. Pour l'instant, ce que tu dois savoir, c'est que les clones peuvent faire **presque** tout ce qu'un sprite normal peut faire, y compris recevoir des messages `message`{:class="block3events"} .

Regarde comment le sprite **Collectable** fonctionne. Regarde si tu peux comprendre une partie de son code :

```blocks3
    when green flag clicked
    hide
    set [collectable-value v] to [1]
    set [collectable-speed v] to [1]
    set [collectable-frequency v] to [1]
    set [create-collectables v] to [true]
    set [collectable-type v] to [1]
    repeat until <not <(create-collectables) = [true]>>
        wait (collectable-frequency) secs
        go to x: (pick random (-240) to (240)) y: (179)
        create clone of [myself v]
    end
```

1. Tout d'abord, il rend invisible le sprite original **Collectable** en le cachant
2. Ensuite, il configure les variables de contrôle - nous y reviendrons plus tard
3. La variable `création-collectables`{:class="block3variables"} est l'interrupteur marche / arrêt pour le clonage : la boucle crée des clones si `création-collectables`{:class="block3variables"} est `true`, et ne fait rien si ce n'est pas le cas

\--- task \---

Maintenant, configure un bloc pour le sprite **Collectable** pour qu'il réagisse au message `partie terminée` :

```blocks3
+    when I receive [game over v]
+    hide
+    set [create-collectables v] to [false]
```

\--- /task \---

Ce code est similaire au code qui contrôle les sprites **Plateformes** et **Bords**. La seule différence est que tu définis également la variable `création-collectables`{:class="block3variables"} à `false` afin qu'aucun nouveau clone ne soit créé quand c'est « Partie terminée ».

Note que tu peux utiliser la variable `création-collectables`{:class="block3variables"} pour passer des messages d'une partie de ton code à une autre !