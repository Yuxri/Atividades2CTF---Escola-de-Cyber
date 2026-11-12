# Crackme-py (picoCTF)

> Categoria: Reverse Engineering

### Introdução

Este CTF é um desafio introdutório de **engenharia reversa**. O objetivo é analisar um
programa escrito em Python, compreender sua lógica e identificar como
recuperar uma informação que foi ocultada por meio de uma transformação
ROT47.

Diferentemente de desafios nos quais precisamos explorar um serviço ou
sistema externo, aqui a análise é feita diretamente sobre o código-fonte
fornecido. O principal exercício é entender o comportamento das funções
e perceber que uma rotina de decodificação já está implementada no
próprio programa.

### Análise Inicial

O código apresenta o seguinte comentário:

> Hiding this really important number in an obscure piece of code is
> brilliant! AND it's encrypted! We want our biggest client to know his
> information is safe with us.

(Esconder esse número realmente importante em um trecho obscuro de
código é brilhante! E ELE ESTÁ CRIPTOGRAFADO! Queremos que nosso maior
cliente saiba que suas informações estão seguras conosco.)

Logo abaixo, encontramos uma variável chamada `bezos_cc_secret`, que
armazena uma sequência de caracteres aparentemente sem sentido:

``` python
bezos_cc_secret = "24256>JL`>0c0Abc?FE02a_53e7fe7af5gN"
```

O programa também possui duas funções principais:

-   `decode_secret(secret)`: recebe uma string e aplica uma
    transformação para recuperar seu conteúdo.
-   `choose_greatest()`: solicita dois valores ao usuário e imprime
    aquele que considera maior.

Ao observar o final do código, percebemos que apenas `choose_greatest()`
é executada. A função responsável por decodificar a variável secreta
está pronta, mas não é chamada.

Esse comportamento é um dos pontos centrais da resolução.

### Interpretação

Dentro da função `decode_secret(secret)`, encontramos um comentário que
identifica o método utilizado:

``` python
"""ROT47 decode"""
```

Portanto, a informação foi transformada utilizando a cifra **ROT47**.

ROT47 é uma cifra de substituição que trabalha com os 94 caracteres
ASCII imprimíveis, correspondentes aos códigos de 33 a 126. Cada
caractere é deslocado em 47 posições dentro desse conjunto.

Como 47 corresponde à metade de 94, aplicar a mesma rotação novamente
recupera o caractere original. Por isso, a operação pode ser utilizada
tanto para codificar quanto para decodificar.

O próprio programa também fornece o alfabeto de referência e a constante
de rotação:

``` python
rotate_const = 47
```

``` python
alphabet = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ" + \
           "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~"
```

Com essas informações, podemos concluir que não é necessário descobrir
uma chave ou testar diversos algoritmos. Basta compreender a função
existente e executá-la com o conteúdo de `bezos_cc_secret`.

### Resolução

Primeiramente, analisamos o funcionamento da função
`decode_secret(secret)`:

``` python
for c in secret:
    index = alphabet.find(c)
    original_index = (index + rotate_const) % len(alphabet)
    decoded = decoded + alphabet[original_index]
```

O processo acontece da seguinte maneira:

1.  **Localização:** `alphabet.find(c)` encontra a posição do caractere
    atual no alfabeto de referência.
2.  **Rotação:** são adicionadas 47 posições ao índice encontrado.
3.  **Módulo:** o operador `%` mantém o resultado dentro dos limites do
    alfabeto, que possui 94 caracteres.
4.  **Reconstrução:** o caractere correspondente à nova posição é
    adicionado à variável `decoded`.

O problema é que a função não é executada em nenhum momento no código
original. Para utilizá-la, basta adicionar uma chamada ao final do
programa:

``` python
decode_secret(bezos_cc_secret)
```

Assim, a string armazenada na variável `bezos_cc_secret` é enviada para
a função, que realiza a decodificação e imprime o resultado.

Também podemos executar o processo separadamente, utilizando um pequeno
script em Python:

``` python
secret = "24256>JL`>0c0Abc?FE02a_53e7fe7af5gN"

alphabet = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ" + \
           "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~"

decoded = ""

for c in secret:
    index = alphabet.find(c)
    original_index = (index + 47) % len(alphabet)
    decoded += alphabet[original_index]

print(decoded)
```

Ao executar o script, obtemos a seguinte saída:

``` text
academy{1m_4_p34nut_a20db6f76f27d8}
```

> **Flag:** `academy{1m_4_p34nut_a20db6f76f27d8}`

### Observação adicional

Durante a análise, também encontramos a função `choose_greatest()`,
responsável por comparar dois valores fornecidos pelo usuário.

Entretanto, existe um detalhe na implementação: as entradas são
recebidas por meio de `input()`, que retorna valores do tipo string.

Consequentemente, os operadores `>` e `<` realizam uma comparação
lexicográfica, comparando os caracteres das strings em vez de seus
valores numéricos.

Por exemplo, ao comparar `"9"` e `"10"`, a string `"9"` é considerada
maior, pois o primeiro caractere tem valor lexicográfico superior ao
primeiro caractere de `"10"`.

Uma maneira de corrigir esse comportamento seria converter as entradas
para números utilizando `int()` ou `float()` antes de realizar a
comparação.

Esse detalhe não interfere na recuperação da informação criptografada,
mas demonstra a importância de observar o comportamento de todo o
programa, inclusive de funções que não são necessárias para a solução
principal.

### Conclusão

O desafio Crackme-py aborda conceitos introdutórios de engenharia
reversa e criptografia, exigindo a leitura e interpretação de um código
Python para descobrir como recuperar uma informação oculta.

Durante a resolução, identificamos a cifra ROT47, compreendemos o
funcionamento da rotina de decodificação e percebemos que a função
necessária já estava implementada, mas não era chamada pelo programa.

O principal aprendizado é a importância de analisar o fluxo de execução
de um programa, e não apenas suas variáveis ou comentários. Em desafios
de engenharia reversa, compreender o que cada função faz e quando ela é
executada pode ser suficiente para encontrar a solução, sem a
necessidade de desenvolver ferramentas complexas.
