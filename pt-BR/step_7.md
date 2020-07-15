## Adicionando alguma competição

Seu jogo funciona e agora você pode coletar pontos, obter poderes especiais dos power-ups e perder. Estamos chegando lá! Talvez seja divertido adicionar alguma competição — que tal incluir um personagem que se move um pouco, mas que você não deva tocar? Isso será parecido com os inimigos nos jogos de plataforma tradicionais, como Super Mario, que nós nos inspiramos aqui.

--- task ---

Primeiro, escolha um sprite para adicionar como seu inimigo. Como o nosso personagem é um gato, eu escolhi um cachorro. Existem muitos outros sprites que você pode adicionar. Eu também chamei o ator de **Inimigo**, só para tornar as coisas mais claras para mim.

Redimensione o ator para o tamanho certo e o coloque em algum lugar apropriado para começar. Aqui está a aparência do meu:

![O ator do inimigo cachorro](images/enemySprite.png)

--- /task ---

--- task ---

Escreva o código mais fácil primeiro: configure seu bloco para reagir à mensagem `fim de jogo`{:class="events"} para fazer o inimigo desaparecer quando o jogador perder o jogo.

```blocks3
+    when I receive [fim de jogo v]
+    hide
```

--- /task ---

--- task ---

Agora você precisa escrever o código para o que o inimigo faz. Use meu código aqui, mas considere adicionar algo a mais! (E se eles pudessem se teletransportar para as outras plataformas? E se um power-up fizesse eles se moverem mais rápido ou mais devagar?)

```blocks3
+    when green flag clicked
+    show
+    set [passos-de-movimento-do-inimigo v] to [5]
+    set rotation style [left-right v]
+    go to x: (-25) y: (-9)
+    forever
        move (passos-de-movimento-do-inimigo) steps
        if <not <touching [Plataformas v] ?>> then
            set [passos-de-movimento-do-inimigo v] to ((passos-de-movimento-do-inimigo) * (-1))
        end
     end
```

**Observação**: se você apenas arrastar o bloco `vá para x e y`{:class="block3motion"} para dentro do painel do ator e não mudar os valores de `x` e `y`, eles serão os valores para a localização atual do ator **Inimigo**!

O código dentro do bloco `se...então`{:class="block3control"} fará o ator girar quando eles chegarem ao final da plataforma!

--- /task ---

A próxima coisa que você vai precisar é que o jogador perca uma vida quando o seu ator **Personagem** encostar no ator **Inimigo**. Além disso, você precisa garantir que os atores **parem** de se encostar rapidamente, pois, caso contrário, o código que procura por toque continuará funcionando e o jogador continuará perdendo vidas.

--- task ---

Aqui está como eu fiz isso, mas você pode tentar melhorar esse código! Eu modifiquei o bloco principal do ator **Personagem**. Adicione o novo código antes do bloco `se`{:class="block3control"} que verifica se você está sem vidas.

```blocks3
    when green flag clicked
    reiniciar-jogo :: custom
    forever
        fisica-principal :: custom
        if <(y position) < [-179]> then
            hide
            reiniciar-personagem :: custom
            change [vidas v] by (-1)
            wait (0.05) secs
            show
        end
+        if <touching [Inimigo v] ?> then
            hide
            go to x: (-187) y: (42)
            change [vidas v] by (-1)
            wait (0.5) secs
            show
+        end
        if <(vidas) < [1]> then
            perder :: custom
        end
    end
```

--- /task ---

O novo código esconde o ator **Personagem**, move ele de volta à sua posição inicial, reduz a variável `vidas`{:class="block3variables"} por `1`, e depois de meio segundo faz o ator reaparecer.