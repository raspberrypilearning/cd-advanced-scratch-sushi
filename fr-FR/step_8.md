## Niveau 2

Avec cette étape, tu vas ajouter un nouveau niveau au jeu auquel le joueur peut accéder en appuyant simplement sur un bouton. Plus tard, tu pourras modifier ton code pour qu’ils aient besoin d’un certain nombre de points ou de quelque chose d’autre pour y parvenir.

### Passer au niveau suivant

--- task ---

Tout d'abord, crée un nouveau sprite en tant que bouton soit en ajoutant un à partir de la bibliothèque ou en le dessinant toi-même. J'ai fait un peu des deux et je suis arrivé à ceci :

![Le sprite bouton pour changer de niveau](images/levelButton.png)

--- /task ---

--- task ---

Maintenant, le code de ce bouton est intelligent : il est conçu de sorte que chaque fois que tu cliques il te mènera au niveau suivant, peu importe le nombre de niveaux.

Ajoute ces scripts à ton sprite **Bouton**. Tu devras créer quelques variables comme tu le fais.

```blocks3
+    when green flag clicked
+    set [niveau-max v] to [2]
+    set [niveau-min v] to [1]
+    set [niveau-actuel v] to [1]
```

```blocks3
+    when this sprite clicked
+    change [niveau-actuel v] by (1)
+    if <(niveau-actuel) > (niveau-max ::variables)> then
        set [niveau-actuel v] to (niveau-min ::variables)
    end
+    broadcast [collectable-nettoyage v]
+    broadcast (join [level-](niveau-actuel))
```

--- /task ---

Peux-tu voir comment le programme utilisera les variables que tu as créées ?

+ `niveau-max`{:class="block3variables"} enregistre le niveau le plus élevé
+ `niveau-min`{:class="block3variables"} enregistre le niveau le plus bas
+ `niveau-actuel`{:class="block3variables"} enregistre le niveau actuel du joueur

Tous ces éléments doivent être définis par le programmeur \(toi !\), donc si tu ajoutes un troisième niveau, n'oublie pas de changer la valeur de `niveau-max`{:class="block3variables"} ! `niveau-min`{:class="block3variables"} n'aura jamais besoin de changer, bien sûr.

Les diffusions sont utilisées pour indiquer aux autres sprites le niveau à afficher et pour nettoyer les objets de collection lorsqu'un nouveau niveau commence.

### Fais réagir les sprites

#### Le sprite **Collectionable**

Maintenant tu dois amener les autres sprites à répondre à ces diffusions ! Commence par le plus simple: effacer tous les objets de collection.

--- task ---

Ajoute le code suivant aux scripts de sprite **Collectable** pour dire à tous ses clones de `cacher`{:class="block3vlooks"} quand ils reçoivent le message de nettoyage :

```blocks3
+    when I receive [collectable-nettoyage v]
+    hide
```

--- /task ---

Puisque l'une des premières choses que fait n'importe quel nouveau clone est de se montrer, tu n'as pas à te soucier de dévoiler des objets de collection !

#### Le sprite **Plateforme**

Maintenant, pour basculer le sprite **Plateformes**. Tu pourras concevoir ton propre nouveau niveau plus tard si tu le souhaites, mais pour l’instant, nous allons utiliser celui que j’ai déjà inclus — tu verras pourquoi à la prochaine étape !

--- task ---

Ajoute ce code au sprite **Plateformes** :

```blocks3
+    when I receive [niveau-1 v]
+    switch costume to [Niveau 1 v]
+    show
```

```blocks3
+    when I receive [niveau-2 v]
+    switch costume to [Niveau 2 v]
+    show
```

--- /task ---

Il reçoit les messages `joints`{:class="block3operators"} de `niveau-`{:class="block3variables"} et `niveau-actuel`{:class="block3variables"} que le sprite **Bouton** envoie et répond en changeant le costume **Plateformes**.

#### Le sprite **Ennemi**

--- task ---

Dans les scripts de sprite **Ennemi**, assure-toi juste que le sprite disparaisse quand le joueur entre dans le niveau 2, comme ceci :

```blocks3
+    when I receive [niveau-1 v]
+    show
```

```blocks3
+    when I receive [niveau-2 v]
+    hide
```

--- /task ---

Si tu préfères, tu peux plutôt faire bouger l'ennemi vers une autre plateforme. Dans ce cas, tu utiliserais un bloc `aller à`{:class="block3motion"} au lieu des blocs `montrer`{:class="block3looks"} et `cacher`{:class="block3looks"}.

### Fais en sorte que le **Perso joueur** apparaisse au bon endroit

À chaque fois qu'un nouveau niveau commence, le sprite **Perso joueur** doit aller au bon endroit pour ce niveau. Pour que cela se produise, tu dois changer d'où le sprite obtient ses coordonnées lorsqu'il apparaît pour la première fois sur la scène. A ce moment, il y a des valeurs `x` et `y` définies dans son code.

--- task ---

Commence par créer des variables pour les coordonnées de départ : `x-début`{:class="block3variables"} et `y-début`{:class="block3variables"}. Puis mets-les dans le bloc `aller à`{:class="block3motion"} dans le bloc `reset-personnage`{:class="block3myblocks"} **Mes blocs** au lieu des valeurs `x` et `y` définies :

```blocks3
    define reset-personnage
    set [peut-sauter v] to [true]
    set [x-velocity v] to [0]
    set [y-velocity v] to [-0]
+    go to x: (x-début) y: (y-début)
```

--- /task ---

--- task ---

Ensuite, pour chaque message annonçant le début d'un niveau, définis les coordonnées `x-début`{:class="block3variables"} et `y-début`{:class="block3variables"} dans la réponse, et ajoute un **appel** à `reset-personnage`{:class="block3myblocks"} :

```blocks3
+    when I receive [niveau-1 v]
+    set [x-début v] to [-183]
+    set [y-début v] to [42]
+    reset-personnage :: custom
```

```blocks3
+    when I receive [niveau-2 v]
+    set [x-début v] to [-218]
+    set [y-début v] to [-143]
+    reset-personnage :: custom
```

--- /task ---

### Démarrer au Niveau 1

Tu dois également t'assurer que chaque fois que quelqu'un commence le jeu, le premier niveau qu'il joue est le niveau 1.

--- task ---

Va au script `reset-jeu`{:class="block3myblocks"} et retire l'appel à `reset-personnage`{:class="block3myblocks"} de celui-ci. À sa place, mettre le message `niveau-min`{:class="block3variables"}. Le code que tu as déjà ajouté avec cette carte va alors configurer les coordonnées de départ correctes pour le sprite **Perso joueur** et appeler `reset-personnage`{:class="block3myblocks"}.

```blocks3
    define reset-jeu
    set rotation style [left-right v]
    set [saut-hauteur v] to [15]
    set [gravité v] to [2]
    set [x-speed v] to [1]
    set [y-speed v] to [1]
    set [vies v] to [3]
    set [points v] to [0]
+    broadcast (join [niveau-](niveau-min ::variables))
```

--- /task ---

--- collapse ---
---
title: Réinitialisation du perso joueur par rapport à la réinitialisation du jeu
---

Note que le premier bloc dans le principal script de drapeau vert du sprite **Perso joueur** est un appel au bloc `reset-jeu`{:class="block3myblocks"} **Mes blocs**.

Ce bloc configure toutes les variables pour un nouveau jeu, et appelle le bloc `reset-personnage`{:class="block3myblocks"} **Mes blocs**, qui replace le personnage dans sa position de départ correcte.

Avoir le code `reset-personnage`{:class="block3myblocks"} dans son propre bloc, séparé de `reset-jeu`{:class="block3myblocks"} te permet de réinitialiser le personnage à différentes positions **sans** réinitialiser l'ensemble du jeu.

--- /collapse ---