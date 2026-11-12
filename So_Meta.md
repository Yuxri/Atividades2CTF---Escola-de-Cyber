# So Meta
> Categoria: Forensics

### Introdução
Este é um desafio de [análise forense digital](https://en.wikipedia.org/wiki/Digital_forensics) do picoCTF 2019, no qual recebemos uma imagem PNG e precisamos encontrar uma flag que não está visível à primeira vista. O título, **"So Meta"**, sugere que a solução pode estar relacionada aos **metadados** do arquivo: informações armazenadas junto à imagem, como autoria, software utilizado e propriedades técnicas.

O enunciado do desafio é o seguinte:

> Find the flag in this picture.
>
> Tradução: Encontre a flag nesta imagem.

Print do enunciado da questão:

![Enunciado do desafio So Meta](https://i.postimg.cc/brF8GPV0/download-(9).png)

### Análise Inicial
Ao abrir o arquivo `pico_img.png`, fornecido pelo desafio, encontramos uma imagem formada por círculos e arcos pretos sobre um fundo branco. Não há nenhuma flag aparente no desenho, nem uma mensagem textual que indique diretamente a resposta.

![Imagem PNG fornecida pelo desafio](https://i.postimg.cc/QCnsBDYk/download-(10).png)

Por se tratar de um desafio da categoria **Forensics**, consideramos a possibilidade de a informação estar armazenada fora da parte visual da imagem. Um arquivo PNG pode conter campos de metadados com informações adicionais, mesmo que elas não apareçam quando visualizamos a imagem normalmente.

### Interpretação
O nome **"So Meta"** foi a principal pista para direcionar nossa investigação. Em vez de tentar interpretar o desenho ou procurar padrões entre os círculos, decidimos examinar os **metadados** associados ao arquivo.

Para isso, utilizamos o site [ExifTools](https://exiftools.com/pt), que permite consultar informações embutidas em arquivos de imagem. Entre os campos que podem aparecer nesse tipo de análise estão dimensões, formato, software de edição e identificação do autor ou artista.

Nossa hipótese era que algum desses campos conteria um texto fora do padrão, possivelmente a própria flag.

### Resolução
O primeiro passo foi acessar o [ExifTools](https://exiftools.com/pt) e enviar o arquivo `pico_img.png` disponibilizado no desafio. A ferramenta processou a imagem e exibiu suas informações técnicas e seus metadados.

![Arquivo pico_img.png carregado no ExifTools](https://i.postimg.cc/90NV42gY/download-(11).png)

Em seguida, examinamos os campos retornados. Na seção referente ao formato **PNG**, encontramos uma propriedade chamada **Artist**, normalmente utilizada para identificar o artista ou criador da imagem.

Entretanto, em vez de apresentar um nome, esse campo continha uma sequência que seguia diretamente o formato esperado de uma flag:

```text
Artist: academy{s0_m3ta_d4aa0408}
```

![Campo Artist contendo a flag nos metadados](https://i.postimg.cc/sx0yBzHY/download-(12).png)

A presença dessa informação no campo de autoria confirmou que a flag estava escondida nos metadados do arquivo, e não no desenho mostrado pela imagem. Portanto, não foi necessário aplicar filtros visuais, decodificações ou outras técnicas de extração.

> **Flag:** academy{s0_m3ta_d4aa0408}

### Conclusão
Este desafio demonstrou a importância da **análise de metadados** na investigação de arquivos digitais. Embora a imagem `pico_img.png` não apresentasse nenhuma informação relevante visualmente, seu campo **Artist** continha a flag completa.

A pista fornecida pelo nome *"So Meta"* foi fundamental para escolher uma abordagem direta: consultar os metadados usando o ExifTools e identificar um valor incomum no campo associado ao criador da imagem.

O exercício reforça que arquivos de imagem não armazenam apenas pixels. Eles também podem conter informações textuais e técnicas que, em desafios de CTF, servem como esconderijos para pistas e flags. Reconhecer essa possibilidade é uma habilidade importante em **Forensics**, especialmente durante a análise inicial de arquivos aparentemente simples.
