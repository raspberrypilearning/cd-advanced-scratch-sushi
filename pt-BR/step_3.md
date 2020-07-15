## Perdendo o jogo

Começando pelo início! Você precisa fazer com que o jogo termine quando o jogador ficar sem vidas. No momento isso não acontece.

Você deve ter notado que o bloco `perder`{:class="block3myblocks"} em **Meus Blocos** nos scripts para o ator **Personagem** está vazio. Você vai preencher isso e configurar todas as peças necessárias para uma boa tela de 'Fim de Jogo'.

--- task ---

Primeiro ache o bloco `perder`{:class="block3myblocks"} e o complete com o seguinte código:

```blocks3
    define perder
+    stop [other scripts in sprite v] :: control stack
+    broadcast [fim de jogo v]
+    go to x:(0) y:(0)
+    say [Fim de Jogo!] for (2) secs
+    stop [all v]
```

--- /task ---

--- collapse ---
---
title: O que esse código faz?
---

Sempre que o bloco `perder`{:class="block3myblocks"} roda agora, o que ele faz é:

1. Parar a física e outros scripts de jogo agindo no **Personagem**
2. Dizer a todos os outros sprites que o jogo acabou fazendo o **transmissão** da mensagem `fim de jogo`{:class="block3events"} que eles podem responder e mudar o que estão fazendo
3. Moer o **Personagem** para o centro da tela e pedir que ele avise o jogador que o jogo acabou
4. Parar todos os scripts do jogo

--- /collapse ---

Agora você precisa ter certeza de que todos os atores sabem o que fazer quando o jogo terminar, e como se reiniciarem quando o jogador iniciar um novo jogo. **Não se esqueça de que qualquer novo ator que você adicionar pode também precisar de código para isso!**

### Ocultando plataformas e bordas

--- task ---

Comece com os atores mais fáceis. Ambos os atores de **Plataformas** e **Lados** precisam de código para aparecerem quando o jogo iniciar, e de desaparecer quando receberem a mensagem de `fim de jogo`{:class="block3events"}, então adicione esse blocos a cada um deles:

```blocks3
+    when I receive [fim de jogo  v]
+    hide
```

```blocks3
+    when green flag clicked
+    show
```

--- /task ---

### Parando as estrelas

Agora, se você olhar o código para o ator **Colecionavel**, você verá que ele funciona **clonando** a si mesmo. Ou seja, ele faz cópias de si mesmo que seguem as instruções em `quando eu começar como um clone`{:class="block3events"}.

Falaremos mais sobre o que torna os clones especiais quando chegarmos no passo de criar novos colecionáveis. Por enquanto, o que você precisa saber é que os clones podem fazer **quase** tudo o que um ator normal pode, inclusive receber mensagens `transmitidas`{:class="block3events"}.

Veja como o ator **Colecionavel** funciona. Veja se você pode entender algo do seu código:

```blocks3
    when green flag clicked
    hide
    set [colecionavel-valor v] to [1]
    set [colecionavel-aceleracao v] to [1]
    set [colecionavel-frequencia v] to [1]
    set [criar-colecionaveis v] to [true]
    set [colecionavel-tipo v] to [1]
    repeat until <not <(criar-colecionaveis) = [true]>>
        wait (colecionavel-frequencia) secs
        go to x: (pick random (-240) to (240)) y: (179)
        create clone of [myself v]
    end
```

1. Primeiramente ele faz com que o ator **Colecionavel** original fique invisível ao escondê-lo
2. Então ele cria as variáveis de controle — nós voltaremos para elas mais tarde
3. A variável `criar-colecionaveis`{:class="block3variables"} é uma chave liga/desliga para clonagem: o loop cria clones somente se `criar-colecionaveis`{:class="block3variables"} for `true`

--- task ---

Agora configure um bloco para o ator **Colecionavel** para que ele reaja a mensagem de `fim de jogo`:

```blocks3
+    when I receive [fim de jogo v]
+    hide
+    set [criar-colecionaveis v] to [false]
```

--- /task ---

Esse código é parecido com o código que controla os atores **Plataformas** e **Bordas**. A única diferença é que você também está configurando a variável `criar-colecionaveis`{:class="block3variables"} para `false` para que nenhum novo clone seja criado quando o jogo estiver terminado.

Note que você pode usar a variável `criar-colecionaveis`{:class="block3variáveis"} para passar mensagens de uma parte do seu código para outra!