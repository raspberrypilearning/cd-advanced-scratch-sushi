## Ajoute de la concurrence

Ton jeu fonctionne et tu peux maintenant accumuler des points, obtenir des pouvoirs spéciaux grâce à des power-ups, et perdre. Voilà qui est mieux ! Peut-être serait-il amusant d'ajouter un peu de compétition — qu'en est-il de l'ajout d'un personnage qui se déplace un peu, mais que tu n'es pas censé toucher ? Cela ressemblera aux ennemis des jeux de plateforme traditionnels comme Super Mario, qui nous inspirent ici.

--- task ---

Tout d'abord, choisis un sprite à ajouter comme ennemi. Parce que notre personnage joueur est un chat, j'ai choisi un chien. Il y a beaucoup d'autres sprites que tu pourrais ajouter. J'ai également renommé le sprite **Ennemi** , juste pour que les choses soient plus claires pour moi.

Redimensionne le sprite à la bonne taille et place-le à un endroit approprié pour commencer. Voici à quoi ressemble le mien :

![Le sprite ennemi chien](images/EnnemiSprite.png)

--- /task ---

--- task ---

Écris d'abord le code le plus simple : configure son bloc pour réagir au message `partie terminée`{:class="events"} pour faire disparaître l'ennemi quand le joueur perd la partie.

```blocks3
+    when I receive [partie terminée v]
+    hide
```

--- /task ---

--- task ---

Maintenant, tu dois écrire le code pour ce que fait l'ennemi. Utilise mon code ici, mais envisage d'ajouter des morceaux supplémentaires ! (Et s'ils peuvent se téléporter sur différentes plateformes ? Et s'il y a un power-up qui les rend plus rapides ou plus lents ?)

```blocks3
+    when green flag clicked
+    show
+    set [ennemi-pas-déplacement v] to [5]
+    set rotation style [left-right v]
+    go to x: (-25) y: (-9)
+    forever
        move (ennemi-pas-déplacement) steps
        if <not <touching [Plateformes v] ?>> then
            set [ennemi-pas-déplacement v] to ((ennemi-pas-déplacement) * (-1))
        end
     end
```

**Note** : si tu fais juste glisser le bloc `aller à`{:class="block3motion"} dans le panneau des sprites et ne change pas les valeurs `x` et `y` ce seront les valeurs pour l'emplacement actuel du sprite **Ennemi** !

Le code dans le bloc `si...alors`{:class="block3control"} fera tourner les sprites quand ils arriveront à la fin de la plateforme !

--- /task ---

La prochaine chose dont tu auras besoin est que le joueur perde une vie quand son sprite **Joueur** touche le sprite **Ennemi**. En outre, tu dois t'assurer que les sprites **arrêtent** de toucher très rapidement, car autrement, le code qui vérifie le toucher continuera à fonctionner et le joueur continuera à perdre des vies.

--- task ---

Voici comment je l'ai fait, mais tu peux essayer d'améliorer ce code ! J’ai modifié le bloc principal du sprite **Perso joueur**. Ajoute le nouveau code avant le bloc `si`{:class="block3control"} qui vérifie si tu n'as plus de vie.

```blocks3
    when green flag clicked
    reset-jeu :: custom
    forever
        physique-principal :: custom
        if <(y position) < [-179]> then
            hide
            reset-personnage :: custom
            change [vies v] by (-1)
            wait (0.05) secs
            show
        end
+        if <touching [Ennemi v] ?> then
            hide
            go to x: (-187) y: (42)
            change [vies v] by (-1)
            wait (0.5) secs
            show
+        end
        if <(vies) < [1]> then
            perdu :: custom
        end
    end
```

--- /task ---

Le nouveau code cache le sprite **Perso joueur**, le déplace à sa position de départ. réduit la variable `vies`{:class="block3variables"} de `1`, et après une demi-seconde le sprite réapparaît.