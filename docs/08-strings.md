# Capítulo 8: Strings

Strings não são como números inteiros, de ponto flutuante ou booleanos. Uma string é uma sequência, ou seja, uma coleção ordenada de outros valores. Neste capítulo você verá como acessar os caracteres que compõem uma string e aprenderá alguns métodos que as strings oferecem.

## 8.1 - Uma string é uma sequência

Uma string é uma sequência de caracteres. Você pode acessar um caractere de cada vez com o operador de colchete:

```python
>>> fruit = 'banana'
>>> letter = fruit[1]
```

A segunda instrução seleciona o caractere número 1 de fruit e o atribui a letter.

A expressão entre colchetes chama-se índice. O índice aponta qual caractere da sequência você quer (daí o nome).


```python
Mas pode ser que você não obtenha o que espera:
>>> letter
'a'
```

Para a maior parte das pessoas, a primeira letra de 'banana' é b, não a. Mas para os cientistas da computação, o índice é uma referência do começo da string, e a referência da primeira letra é zero.


```python
>>> letter = fruit[0]
>>> letter
'b'
```

Então b é a 0ª (“zerésima”) letra de 'banana', a é a 1ª (primeira) letra e n é a 2ª (segunda) letra.

Você pode usar uma expressão que contenha variáveis e operadores como índice:



```python
>>> i = 1
>>> fruit[i]
'a'
>>> fruit[i+1]
'n'
```

Porém, o valor do índice tem que ser um número inteiro. Se não for, é isso que aparece:

```python
>>> letter = fruit[1.5]
TypeError: string indices must be integers
```

## 8.2 - len

len é uma função integrada que devolve o número de caracteres em uma string:


```python
>>> fruit = 'banana'
>>> len(fruit)
6
```

Para obter a última letra de uma string, pode parecer uma boa ideia tentar algo assim:


```python
>>> length = len(fruit)
>>> last = fruit[length]
IndexError: string index out of range
```

A razão de haver um IndexError aqui é que não há nenhuma letra em 'banana' com o índice 6. Como a contagem inicia no zero, as seis letras são numeradas de 0 a 5. Para obter o último caractere, você deve subtrair 1 de length:


```python
>>> last = fruit[length-1]
>>> last
'a'
```

Ou você pode usar índices negativos, que contam de trás para a frente a partir do fim da string. A expressão fruit[-1] apresenta a última letra, fruit[-2] apresenta a segunda letra de trás para a frente, e assim por diante.

## 8.3 - Travessia com loop for

Muitos cálculos implicam o processamento de um caractere por vez em uma string. Muitas vezes começam no início, selecionam um caractere por vez, fazem algo e continuam até o fim. Este modelo do processamento chama-se travessia. Um modo de escrever uma travessia é com o loop while:



```python
index = 0
while index < len(fruit):
    letter = fruit[index]
    print(letter)
    index = index + 1
```

Este loop atravessa a string e exibe cada letra sozinha em uma linha. A condição do loop é index &lt;len (fruit), então quando index é igual ao comprimento da string, a condição é falsa e o corpo do loop não é mais executado. O último caractere acessado é aquele com o índice len (fruit)-1, que é o último caractere na string.

Como exercício, escreva uma função que receba uma string como argumento e exiba as letras de trás para a frente, uma por linha.

Outra forma de escrever uma travessia é com um loop for:

```python
for letter in fruit:
    print(letter)
```

Cada vez que o programa passar pelo loop, o caractere seguinte na string é atribuído à variável letter. O loop continua até que não sobre nenhum caractere.

O próximo exemplo mostra como usar a concatenação (adição de strings) e um loop for para gerar uma série abecedária (isto é, em ordem alfabética). No livro de Robert McCloskey, Make Way for Ducklings (Abram caminho para os patinhos), os nomes dos patinhos são Jack, Kack, Lack, Mack, Nack, Ouack, Pack e Quack. Este loop produz estes nomes em ordem:






```python
prefixes = 'JKLMNOPQ'
suffix = 'ack'
for letter in prefixes:
    print(letter + suffix)
A saída é:
Jack
Kack
Lack
Mack
Nack
Oack
Pack
Qack
```

Claro que não está exatamente certo porque “Ouack” e “Quack” foram mal soletrados. Como exercício, altere o programa para corrigir este erro.

## 8.4 - Fatiamento de strings

Um segmento de uma string é chamado de fatia. Selecionar uma fatia é como selecionar um caractere:

```python
>>> s = 'Monty Python'
>>> s[0:5]
'Monty'
>>> s[6:12]
'Python'
```

O operador `[n:m]` retorna a parte da string do “enésimo” caractere ao “emésimo” caractere, incluindo o primeiro, mas excluindo o último. Este comportamento é contraintuitivo, porém pode ajudar a imaginar os índices que indicam a parte entre os caracteres, como na Figura 8.1.

![Figura 8.1 – Índices de fatias.](https://github.com/PenseAllen/PensePython2e/raw/master/fig/tnkp_0801.png)
<br>_Figura 8.1 – Índices de fatias._

Se você omitir o primeiro índice (antes dos dois pontos), a fatia começa no início da string. Se omitir o segundo índice, a fatia vai ao fim da string:

```python
>>> fruit = 'banana'
>>> fruit[:3]
'ban'
>>> fruit[3:]
'ana'
```

Se o primeiro índice for maior ou igual ao segundo, o resultado é uma string vazia, representada por duas aspas:

```python
>>> fruit = 'banana'
>>> fruit[3:3]
''
```

Uma string vazia não contém nenhum caractere e tem o comprimento 0, fora isso, é igual a qualquer outra string.

Continuando este exemplo, o que você acha que `fruit[:]` significa? Teste e veja.

## 8.5 - Strings são imutáveis

É tentador usar o operador `[]` no lado esquerdo de uma atribuição, com a intenção de alterar um caractere em uma string. Por exemplo:

```python
>>> greeting = 'Hello, world!'
>>> greeting[0] = 'J'
TypeError: 'str' object does not support item assignment
```

O “objeto” neste caso é a string e o “item” é o caractere que você tentou atribuir. Por enquanto, um objeto é a mesma coisa que um valor, mas refinaremos esta definição mais adiante ([Objetos e valores](<a href="10-listas.md#sec:10.10"), no capítulo 10).

A razão do erro é que as strings são imutáveis, o que significa que você não pode alterar uma string existente. O melhor que você pode fazer é criar uma string que seja uma variação da original:

```python
>>> greeting = 'Hello, world!'
>>> new_greeting = 'J' + greeting[1:]
>>> new_greeting
'Jello, world!'
```

Esse exemplo concatena uma nova primeira letra a uma fatia de `greeting`. Não tem efeito sobre a string original.

## 8.6 - Buscando

```python
O que faz a seguinte função?
def find(word, letter):
    index = 0
    while index < len(word):
        if word[index] == letter:
            return index
        index = index + 1
    return-1
```

De certo modo, `find` é o inverso do operador `[]`. Em vez de tomar um índice e extrair o caractere correspondente, ele toma um caractere e encontra o índice onde aquele caractere aparece. Se o caractere não for encontrado, a função retorna -1.

Esse é o primeiro exemplo que vimos de uma instrução `return` dentro de um loop. Se `word[index] == letter`, a função sai do loop e retorna imediatamente.

Se o caractere não aparecer na string, o programa sai do loop normalmente e devolve -1.

Este modelo de cálculo – atravessar uma sequência e retornar quando encontramos o que estamos procurando – chama-se busca.

Como exercício, altere `find` para que tenha um terceiro parâmetro: o índice em `word` onde deve começar a busca.

## 8.7 - Loop e contagem

O seguinte programa conta o número de vezes que a letra a aparece em uma string:

```python
word = 'banana'
count = 0
for letter in word:
    if letter == 'a':
        count = count + 1
print(count)
```

Este programa demonstra outro padrão de computação chamado contador. A variável `count` é inicializada com 0 e então incrementada cada vez que um a é encontrado. Ao sair do loop, `count` contém o resultado – o número total de letras `'a'`.

Como exercício, encapsule este código em uma função denominada `count` e generalize-o para que aceite a string e a letra como argumentos.

Então reescreva a função para que, em vez de atravessar a string, ela use a versão de três parâmetros do find da seção anterior.

## 8.8 - Métodos de strings

As strings oferecem métodos que executam várias operações úteis. Um método é semelhante a uma função – toma argumentos e devolve um valor –, mas a sintaxe é diferente. Por exemplo, o método upper recebe uma string e devolve uma nova string com todas as letras maiúsculas.

Em vez da sintaxe de função `upper(word)`, ela usa a sintaxe de método `word.upper()`:

```python
>>> word = 'banana'
>>> new_word = word.upper()
>>> new_word
'BANANA'
```

Esta forma de notação de ponto especifica o nome do método, `upper` e o nome da string, `word`, à qual o método será aplicado. Os parênteses vazios indicam que este método não toma nenhum argumento.

Uma chamada de método denomina-se invocação; neste caso, diríamos que estamos invocando `upper` em `word`.

E, na verdade, há um método de string denominado `find`, que é notavelmente semelhante à função que escrevemos:

```python
>>> word = 'banana'
>>> index = word.find('a')
>>> index
1
```

Neste exemplo, invocamos `find` em `word` e passamos a letra que estamos procurando como um parâmetro.

Na verdade, o método `find` é mais geral que a nossa função; ele pode encontrar substrings, não apenas caracteres:

```python
>>> word.find('na')
2
```

Por padrão, `find` inicia no começo da string, mas pode receber um segundo argumento, o índice onde deve começar:

```python
>>> word.find('na', 3)
4
```

Este é um exemplo de um argumento opcional. `find` também pode receber um terceiro argumento, o índice para onde deve parar:

```python
>>> name = 'bob'
>>> name.find('b', 1, 2)
-1
```

Esta busca falha porque `'b'` não aparece no intervalo do índice de 1 a 2, não incluindo 2. Fazer buscas até (mas não incluindo) o segundo índice torna `find` similar ao operador de fatiamento.

## 8.9 - Operador in

A palavra `in` é um operador booleano que recebe duas strings e retorna `True` se a primeira aparecer como uma substring da segunda:

```python
>>> 'a' in 'banana'
True
>>> 'seed' in 'banana'
False
```

Por exemplo, a seguinte função imprime todas as letras de `word1` que também aparecem em `word2`:

```python
def in_both(word1, word2):
    for letter in word1:
        if letter in word2:
            print(letter)
```

Com nomes de variáveis bem escolhidos, o Python às vezes pode ser lido como um texto em inglês. Você pode ler este loop, “para (cada) letra em (a primeira) palavra, se (a) letra (aparecer) em (a segunda) palavra, exiba (a) letra”.

Veja o que é apresentado ao se comparar maçãs e laranjas:

```python
>>> in_both('apples', 'oranges')
a
e
s
```

## 8.10 - Comparação de strings

Os operadores relacionais funcionam em strings. Para ver se duas strings são iguais:

```python
if word == 'banana':
    print('All right, bananas.')
```

Outras operações relacionais são úteis para colocar palavras em ordem alfabética:

```python
if word < 'banana':
    print('Your word, ' + word + ', comes before banana.')
elif word > 'banana':
    print('Your word, ' + word + ', comes after banana.')
else:
    print('All right, bananas.')
```

O Python não lida com letras maiúsculas e minúsculas do mesmo jeito que as pessoas. Todas as letras maiúsculas vêm antes de todas as letras minúsculas, portanto:

```python
Your word, Pineapple, comes before banana.
```

Uma forma comum de lidar com este problema é converter strings em um formato padrão, como letras minúsculas, antes de executar a comparação. Lembre-se disso caso tenha que se defender de um homem armado com um abacaxi.

## 8.11 - Depuração

Ao usar índices para atravessar os valores em uma sequência, é complicado acertar o começo e o fim da travessia. Aqui está uma função que supostamente compara duas palavras e retorna True se uma das palavras for o reverso da outra, mas contém dois erros:

```python
def is_reverse(word1, word2):
    if len(word1) != len(word2):
        return False
    i = 0
    j = len(word2)
    while j > 0:
        if word1[i] != word2[j]:
            return False
        i = i+1
        j = j-1
    return True
```

A primeira instrução if verifica se as palavras têm o mesmo comprimento. Se não for o caso, podemos retornar False imediatamente. Do contrário, para o resto da função, podemos supor que as palavras tenham o mesmo comprimento. Este é um exemplo do modelo de guardião em “Verificação de tipos”, na página 101.

i e j são índices: i atravessa word1 para a frente, enquanto j atravessa word2 para trás. Se encontrarmos duas letras que não combinam, podemos retornar False imediatamente. Se terminarmos o loop inteiro e todas as letras corresponderem, retornamos True.

Se testarmos esta função com as palavras “pots” e “stop”, esperamos o valor de retorno True, mas recebemos um IndexError:

```python
>>> is_reverse('pots', 'stop')
...
  File "reverse.py", line 15, in is_reverse
    if word1[i] != word2[j]:
IndexError: string index out of range
```

Para depurar este tipo de erro, minha primeira ação é exibir os valores dos índices imediatamente antes da linha onde o erro aparece.

```python
while j > 0:
    print(i, j)        # exibir aqui
    if word1[i] != word2[j]:
        return False
    i = i+1
    j = j-1
```

Agora quando executo o programa novamente, recebo mais informação:

```python
>>> is_reverse('pots', 'stop')
0 4
...
IndexError: string index out of range
```

Na primeira vez que o programa passar pelo loop, o valor de j é 4, que está fora do intervalo da string 'pots'. O índice do último caractere é 3, então o valor inicial de j deve ser len(word2)-1.

Se corrigir esse erro e executar o programa novamente, recebo:

```python
>>> is_reverse('pots', 'stop')
0 3
1 2
2 1
True
```

Desta vez, recebemos a resposta certa, mas parece que o loop só foi executado três vezes, o que é suspeito. Para ter uma ideia melhor do que está acontecendo, é útil desenhar um diagrama de estado. Durante a primeira iteração, o frame de `is_reverse` é mostrado na Figura 8.2.

![Figura 8.2 – Diagrama de estado de is_reverse.](https://github.com/PenseAllen/PensePython2e/raw/master/fig/tnkp_0802.png)
<br>_8.2 – Diagrama de estado de is_reverse._

Tomei a liberdade de arrumar as variáveis no frame e acrescentei linhas pontilhadas para mostrar que os valores de i e j indicam caracteres em word1 e word2.

Começando com este diagrama, execute o programa em papel, alterando os valores de i e j durante cada iteração. Encontre e corrija o segundo erro desta função.

## 8.12 - Glossário

<dl>
<dt><a id="glos:objeto" href="#termo:objeto">objeto</a></dt>
<dd>Algo a que uma variável pode se referir. Por enquanto, você pode usar “objeto” e “valor” de forma intercambiável.</dd>

<dt><a id="glos:sequência" href="#termo:sequência">sequência</a></dt>
<dd>Uma coleção ordenada de valores onde cada valor é identificado por um índice de número inteiro.</dd>

<dt><a id="glos:item" href="#termo:item">item</a></dt>
<dd>Um dos valores em uma sequência.</dd>

<dt><a id="glos:índice" href="#termo:índice">índice</a></dt>
<dd>Um valor inteiro usado para selecionar um item em uma sequência, como um caractere em uma string. No Python, os índices começam em 0.</dd>

<dt><a id="glos:fatia" href="#termo:fatia">fatia</a></dt>
<dd>Parte de uma string especificada por um intervalo de índices.</dd>

<dt><a id="glos:string vazia" href="#termo:string vazia">string vazia</a></dt>
<dd>Uma string sem caracteres e de comprimento 0, representada por duas aspas.</dd>

<dt><a id="glos:imutável" href="#termo:imutável">imutável</a></dt>
<dd>A propriedade de uma sequência cujos itens não podem ser alterados.</dd>

<dt><a id="glos:atravessar" href="#termo:atravessar">atravessar</a></dt>
<dd>Repetir os itens em uma sequência, executando uma operação semelhante em cada um.</dd>

<dt><a id="glos:busca" href="#termo:busca">busca</a></dt>
<dd>Um modelo de travessia que é interrompido quando encontra o que está procurando.</dd>

<dt><a id="glos:contador" href="#termo:contador">contador</a></dt>
<dd>Uma variável usada para contar algo, normalmente inicializada com zero e então incrementada.</dd>

<dt><a id="glos:invocação" href="#termo:invocação">invocação</a></dt>
<dd>Uma instrução que chama um método.</dd>

<dt><a id="glos:argumento opcional" href="#termo:argumento opcional">argumento opcional</a></dt>
<dd>Um argumento de função ou método que não é necessário.</dd>

</dl>

## 8.13 - Exercícios

### Exercício 8.1

Leia a documentação dos métodos de strings em http://docs.python.org/3/library/stdtypes.html#string-methods. Pode ser uma boa ideia experimentar alguns deles para entender como funcionam. `strip` e `replace` são especialmente úteis.

A documentação usa uma sintaxe que pode ser confusa. Por exemplo, em `find(sub[, start[, end]])`, os colchetes indicam argumentos opcionais. Então `sub` é exigido, mas `start` é opcional, e se você incluir `start`, então `end` é opcional.

### Exercício 8.2

Há um método de string chamado `count`, que é semelhante à função em “Loop e contagem”, na página 123. Leia a documentação deste método e escreva uma invocação que conte o número de letras `'a'` em 'banana'.

### Exercício 8.3

Uma fatia de string pode receber um terceiro índice que especifique o “tamanho do passo”; isto é, o número de espaços entre caracteres sucessivos. Um tamanho de passo 2 significa tomar um caractere e outro não; 3 significa tomar um e dois não etc.

```python
>>> fruit = 'banana'
>>> fruit[0:5:2]
'bnn'
```

Um tamanho de passo -1 atravessa a palavra de trás para a frente, então a fatia `[::-1]` gera uma string invertida.

Use isso para escrever uma versão de uma linha de `is_palindrome` do Exercício 6.3.

### Exercício 8.4

As seguintes funções pretendem verificar se uma string contém alguma letra minúscula, mas algumas delas estão erradas. Para cada função, descreva o que ela faz (assumindo que o parâmetro seja uma string).

```python
def any_lowercase1(s):
    for c in s:
        if c.islower():
            return True
        else:
            return False

def any_lowercase2(s):
    for c in s:
        if 'c'.islower():
            return 'True'
        else:
            return 'False'

def any_lowercase3(s):
    for c in s:
        flag = c.islower()
    return flag

def any_lowercase4(s):
    flag = False
    for c in s:
        flag = flag or c.islower()
    return flag

def any_lowercase5(s):
    for c in s:
        if not c.islower():
            return False
    return True
```

### Exercício 8.5

Uma cifra de César é uma forma fraca de criptografia que implica “rotacionar” cada letra por um número fixo de lugares. Rotacionar uma letra significa deslocá-lo pelo alfabeto, voltando ao início se for necessário, portanto ‘A’ rotacionado por 3 é ‘D’ e ‘Z’ rotacionado por 1 é ‘A’.

Para rotacionar uma palavra, faça cada letra se mover pela mesma quantidade de posições. Por exemplo, “cheer” rotacionado por 7 é “jolly” e “melon” rotacionado por -10 é “cubed”. No filme 2001: Uma odisseia no espaço, o computador da nave chama-se HAL, que é IBM rotacionado por -1.

Escreva uma função chamada `rotate_word` que receba uma string e um número inteiro como parâmetros, e retorne uma nova string que contém as letras da string original rotacionadas pelo número dado.

Você pode usar a função integrada ord, que converte um caractere em um código numérico e chr, que converte códigos numéricos em caracteres. As letras do alfabeto são codificadas em ordem alfabética, então, por exemplo:

```python
>>> ord('c') - ord('a')
2
```

Porque `'c'` é a “segunda” letra do alfabeto. Mas tenha cuidado: os códigos numéricos de letras maiúsculas são diferentes.

Piadas potencialmente ofensivas na internet às vezes são codificadas em ROT13, que é uma cifra de César com rotação 13. Se não se ofender facilmente, encontre e decifre algumas delas.
