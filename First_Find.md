# First Find
> Categoria: General Skills

### Introdução
Este é um desafio da categoria **General Skills** que trabalha a navegação por diretórios e a localização de arquivos. Recebemos um arquivo compactado contendo diversas pastas e arquivos, e nosso objetivo é encontrar um documento específico chamado `uber-secret.txt`.

O enunciado do desafio é o seguinte:

> Unzip this archive and find the file named 'uber-secret.txt'

Em tradução livre, devemos descompactar o arquivo fornecido e encontrar o documento chamado `uber-secret.txt`.

Print do enunciado da questão:

![Enunciado do desafio First Find](https://postimg.cc/yWZqkZZH)

### Análise Inicial
Após baixar o arquivo ZIP disponibilizado pelo desafio, encontramos um arquivo compactado chamado `files`, que reúne os diretórios e documentos que precisamos examinar.

![Arquivo compactado fornecido pelo desafio](https://postimg.cc/pyFNpFFt)

Ao extrair seu conteúdo e abrir a pasta principal, identificamos vários arquivos de texto e três diretórios: `acceptable_books`, `adequate_books` e `satisfactory_books`. Como o enunciado solicita apenas a localização de um arquivo, podemos prosseguir examinando a organização das pastas, sem necessidade de decodificação ou ferramentas adicionais.

![Conteúdo inicial do arquivo descompactado](https://postimg.cc/NLHh5HHv)

### Interpretação
A principal pista do desafio é o próprio nome do arquivo procurado: `uber-secret.txt`. Dessa forma, nossa tarefa consiste em explorar a estrutura de diretórios até encontrá-lo.

Embora o arquivo compactado contenha vários documentos, não precisamos analisar o conteúdo de todos eles. Basta acompanhar as pastas disponíveis e verificar seus nomes e arquivos. Neste caso, utilizamos o **Explorador de Arquivos do Windows** para realizar a busca manualmente.

### Resolução
Começamos acessando o diretório `acceptable_books`, no qual encontramos outros arquivos e uma subpasta chamada `more_books`. Essa organização indica que existem níveis adicionais a serem explorados.

![Arquivos e pasta more_books encontrados durante a navegação](https://postimg.cc/9z73r773)

Em seguida, abrimos a pasta `more_books`. Nela, encontramos outro arquivo de texto e um diretório chamado `.secret`, cujo nome sugere que possa conter o arquivo solicitado no enunciado.

![Pasta .secret localizada dentro de more_books](https://postimg.cc/s1hFvhZb)

Ao acessar o diretório `.secret`, encontramos um documento de texto chamado `uber-secret`. Como o Windows pode ocultar extensões de tipos de arquivos conhecidos, esse nome corresponde ao arquivo `uber-secret.txt` solicitado pelo desafio.

![Arquivo uber-secret encontrado na pasta .secret](https://postimg.cc/CnD9t3gJ)

Por fim, abrimos o documento em um editor de texto e encontramos a flag, confirmando que havíamos localizado o arquivo correto.

![Conteúdo do arquivo uber-secret contendo a flag](https://postimg.cc/yWZqkZSG)

> **Flag:** `academy{f1nd_15_f457_ab443fd1}`

### Conclusão
O desafio **First Find** explorou uma habilidade básica, mas importante, em CTFs: localizar arquivos dentro de estruturas de diretórios. A resolução exigiu apenas descompactar o arquivo recebido, navegar pelas pastas e abrir o documento indicado no enunciado.

Durante o processo, também observamos que diretórios iniciados por ponto, como `.secret`, podem ser utilizados para organizar ou disfarçar conteúdos. Essa convenção é especialmente comum em sistemas Unix-like, nos quais nomes iniciados por ponto normalmente são tratados como ocultos.

Esse exercício reforça a importância de compreender a organização de arquivos e diretórios, uma competência útil tanto em desafios de CTF quanto na análise inicial de sistemas e conjuntos de dados.
