# Mod 26
> Categoria: Cryptography

### Introdução
Este é um desafio de [criptografia](https://en.wikipedia.org/wiki/Cryptography) do **picoCTF 2021**, criado por *Pandu*, em que recebemos um arquivo de texto contendo uma mensagem aparentemente sem sentido. A proposta é reconhecer uma cifra de substituição simples e recuperar a flag original.

O enunciado do desafio é o seguinte:

> Cryptography can be easy, do you know what ROT13 is?
>
> Arquivo fornecido: `values.txt`

**A própria pergunta do enunciado menciona ROT13. Essa foi a pista decisiva que nos levou diretamente ao site [rot13.com](https://rot13.com/), usado para realizar a decodificação.** Não foi necessário descobrir o método por tentativa e erro.

Print do enunciado da questão:

![Enunciado do desafio Mod 26](https://i.postimg.cc/hv3gJnZ5/download.png)

### Análise Inicial
Ao abrir o arquivo `values.txt`, disponibilizado junto da questão, encontramos uma única mensagem com a estrutura de uma flag, mas com as letras substituídas:

```text
npnqrzl{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_5p5s5o36}
```

Embora o conteúdo esteja ilegível, os caracteres especiais, números, chaves e sublinhados permanecem nas posições esperadas. Isso sugere uma transformação aplicada principalmente às letras do alfabeto, como acontece com a cifra ROT13.

![Conteúdo criptografado do arquivo values.txt](https://i.postimg.cc/gjBdwptS/download-(2).png)

### Interpretação
O [ROT13](https://en.wikipedia.org/wiki/ROT13) é uma variação da [cifra de César](https://en.wikipedia.org/wiki/Caesar_cipher) que desloca cada letra em **13 posições** no alfabeto de 26 letras. Por exemplo, `A` se transforma em `N`, enquanto `N` se transforma em `A`. Como 13 é metade de 26, aplicar ROT13 duas vezes devolve o texto original.

O método preserva números, espaços e símbolos, o que explica por que a mensagem do arquivo ainda mantém o formato característico de uma flag. Trata-se de uma cifra muito simples e não de um mecanismo adequado para proteger informações sensíveis.

Como **o enunciado já perguntava explicitamente sobre ROT13**, acessamos o [rot13.com](https://rot13.com/), uma ferramenta online que permite aplicar essa transformação diretamente no navegador.

![Acesso à ferramenta rot13.com](https://i.postimg.cc/2yXmqY9t/download-(1).png)

### Resolução
Primeiro, copiamos o conteúdo completo do arquivo `values.txt`. Em seguida, acessamos o [rot13.com](https://rot13.com/) e colamos a mensagem no campo superior da página, mantendo a opção **ROT13** selecionada.

A ferramenta aplica a substituição automaticamente e apresenta o texto decodificado no campo inferior. O resultado foi:

```text
academy{next_time_I'll_try_2_rounds_of_rot13_5c5f5b36}
```

![Aplicação do ROT13 e obtenção da flag](https://i.postimg.cc/2yXmqY9H/download-(3).png)

O prefixo `npnqrzl` foi convertido em `academy`, e o restante da mensagem passou a formar um texto legível, confirmando que o método indicado pelo enunciado era o correto.

> **Flag:** `academy{next_time_I'll_try_2_rounds_of_rot13_5c5f5b36}`

### Conclusão
Este desafio apresentou uma aplicação direta do ROT13, uma cifra de substituição que troca cada letra pela correspondente 13 posições adiante no alfabeto. A resolução foi simples porque o próprio enunciado forneceu a indicação essencial: **conhecer ROT13**.

A partir dessa dica, utilizamos o site rot13.com para decodificar a mensagem presente no arquivo `values.txt`, sem precisar recorrer a scripts ou técnicas mais complexas. O desafio reforça a importância de interpretar atentamente as pistas do enunciado e reconhecer cifras clássicas, que aparecem com frequência em desafios introdutórios de CTF.
