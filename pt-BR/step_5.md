## Super power-ups!

Agora que você tem um novo colecionável power-up funcionando, é hora de fazer algo realmente legal: vamos fazer 'chover' power-ups por alguns segundos ao invés de apenas dar uma vida extra.

Para isso, você `transmitirá`{:class="block3events"} outra mensagem.

--- task ---

Primeiro, mude o bloco `reagir-ao-jogador`{:class="block3myblocks"} para transmitir uma mensagem quando o jogador tocar num colecionável tipo `2`. Chame a mensagem `chuva-de-colecionaveis`{:class="block3events"}.

```blocks3
    define reagir-ao-jogador (tipo)
    if <(tipo ::variable) = [1]> then
        change [pontos v] by (colecionavel-valor ::variables)
    end
    if <(tipo ::variable) = [2]> then
-        change [vidas v] by [1]    
+        broadcast [chuva-de-colecionaveis v]
    end
```

--- /task ---

Agora você precisa criar um pedaço de código novo dentro dos scripts do ator **Colecionavel** que será iniciado sempre que a mensagem `chuva-de-colecionaveis`{:class="block3events"} for transmitida.

--- task ---

Adicione esse código no ator **Colecionavel** para fazer com que ele aguarde a transmissão da mensagem `chuva-de-colecionaveis`{:class="block3events"}.

```blocks3
+    when I receive [chuva-de-colecionaveis v]
+    set [colecionavel-frequencia v] to [0.000001]
+    wait (1) secs
+    set [colecionavel-frequencia v] to [1]
```

--- /task ---

--- collapse ---
---
title: O que o novo código faz?
---

Esse trecho de código aguarda a transmissão, e ao receber, define o valor da variável `colecionavel-frequencia`{:class="block3variables"} para um número muito pequeno, então espera por um segundo e em seguida muda o valor da variável novamente para `1`.

Vamos ver como a variável `colecionavel-frequencia`{:class="block3variables"} é usada para descobrir porque isso faz chover colecionáveis.

No loop principal do jogo, a parte do código que faz clones do ator **Colecionavel** é informada pela variável `colecionavel-frequencia`{:class="block3variables"} quanto tempo esperar novos clones:

```blocks3
    repeat until <not <(criar-colecionaveis ::variables) = [true]>>
        if < [50] = (pick random (1) to (50))> then
            set [colecionavel-tipo v] to [2]
        else
            set [colecionavel-tipo v] to [1]
        end
        wait (colecionavel-frequencia ::variables) secs
        go to x: (pick random (-240) to (240)) y:(179)
        create clone of [myself v]
    end
```

Você pode ver que o bloco `espere`{:class="block3control"} pausa o código pelo período de tempo definido por `colecionavel-frequencia`{:class="block3variables"}.

Se o valor de `colecionavel-frequencia`{:class="block3variables"} é `0.000001`, o bloco `espere`{:class="block3control"} só pausa por **um milionésimio** de segundo, o que significa que o loop `repita até que`{:class="block3control"} vai ser executado muito mais vezes que o normal. Como resultado, o código criará **muito** mais power-ups do que normalmente faria, até que `colecionavel-frequencia`{:class="block3variables"} seja alterado novamente para `1`.

Você consegue pensar em algum problema que isso possa causar? Haverá muito mais power-ups…e se você continuasse pegando eles?

--- /collapse ---