# Cookies
> Categoria: Web Exploitation

### Introdução
Este é um desafio de [exploração web](https://en.wikipedia.org/wiki/Web_security) do picoCTF 2021 no qual precisamos descobrir qual é o *cookie* favorito de uma aplicação. O próprio nome do desafio, **Cookies**, já sugere o principal elemento que devemos investigar: os [cookies HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Guides/Cookies), pequenos dados que um site pode armazenar no navegador e enviar em requisições posteriores.

O enunciado do desafio é o seguinte:

> Who doesn't love cookies? Try to figure out the best one.

Em tradução livre: "Quem não ama cookies? Tente descobrir o melhor deles."

Print do enunciado da questão:

![Enunciado do desafio Cookies](https://i.postimg.cc/sx0yBzHK/download-(4).png)

### Análise Inicial
Após iniciar a instância fornecida pelo desafio, acessamos uma página intitulada **Cookies**, com um campo de pesquisa para procurar diferentes tipos de biscoitos. O campo já apresentava o termo `snickerdoodle` como exemplo.

![Página inicial da aplicação Cookies](https://i.postimg.cc/ZnDZ9mss/download-(5).png)

Como o nome da atividade faz referência direta a *cookies*, interpretamos que o desafio poderia envolver não apenas os biscoitos mencionados na página, mas também os **cookies armazenados pelo navegador**. Por isso, decidimos inspecionar a aplicação usando as ferramentas de desenvolvedor do navegador (*DevTools*).

Na aba **Application**, na seção **Storage > Cookies**, encontramos um cookie chamado `name`, inicialmente com o valor `-1`.

![Cookie name com valor inicial -1 nas ferramentas de desenvolvedor](https://i.postimg.cc/Rhb93mpR/download-(6).png)

Esse detalhe chamou nossa atenção: o valor do cookie era numérico, sugerindo que a aplicação poderia utilizar números para identificar diferentes tipos de biscoitos.

### Interpretação
A partir dessa observação, formulamos a hipótese de que o cookie `name` funcionava como um **identificador** utilizado pelo site para selecionar a resposta exibida ao usuário. Se esse valor fosse alterado, a aplicação poderia apresentar mensagens referentes a outros biscoitos.

Assim, em vez de buscar apenas pelo campo de texto da página, optamos por investigar o comportamento da aplicação ao modificar o valor do cookie diretamente pelo DevTools. O objetivo era localizar o número correspondente ao "melhor cookie" mencionado no enunciado.

Essa abordagem também permite observar um conceito importante em segurança web: **dados controlados pelo cliente não devem ser considerados confiáveis pelo servidor**, mesmo quando são armazenados em cookies.

### Resolução
Primeiramente, abrimos as ferramentas de desenvolvedor do navegador e acessamos **Application > Storage > Cookies**, selecionando o domínio da instância. Identificamos o cookie `name`, cujo valor inicial era `-1`.

Em seguida, começamos a alterar manualmente o campo **Value** desse cookie, testando valores numéricos progressivamente e atualizando a página para observar a resposta da aplicação.

Durante os testes, ao definir o valor como `6`, a página exibiu a mensagem:

```text
I love whoopie pie cookies!
```

Além disso, foi apresentada a informação de que aquele era um cookie, mas não era especialmente importante. Isso confirmou que a mudança no valor numérico de `name` alterava o conteúdo retornado pela aplicação.

![Página exibindo o resultado para name igual a 6](https://i.postimg.cc/x8FYkQp5/download-(7).png)

Com essa hipótese confirmada, continuamos testando os valores em sequência até chegar ao número **18**. Nesse momento, a aplicação deixou de exibir uma mensagem comum sobre biscoitos e apresentou diretamente a **flag** do desafio.

![Flag encontrada com o cookie name definido como 18](https://i.postimg.cc/C56YZ0r4/download-(8).png)

> **Flag:** `academy{3v3ry1_l0v3s_c00k13s_90a3a7cb}`

### Conclusão
O desafio **Cookies** demonstrou como informações armazenadas no navegador podem influenciar o comportamento de uma aplicação web. O nome da atividade foi a principal pista para investigar os cookies HTTP, e a inspeção pelo DevTools revelou um campo numérico chamado `name`.

Ao modificarmos esse valor e observarmos as respostas do site, identificamos que diferentes números correspondiam a diferentes resultados. Após uma sequência de testes manuais, o valor `18` revelou a flag.

A resolução reforçou a importância de compreender o funcionamento dos cookies e de analisar como aplicações utilizam dados provenientes do cliente. Também destacou o valor de uma investigação simples e sistemática, na qual uma pista do enunciado pode indicar diretamente o componente relevante da aplicação.
