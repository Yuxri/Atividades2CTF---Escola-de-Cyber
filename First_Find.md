# First Find
> Categoria: General Skills

### Introdução
Este é um desafio da categoria **General Skills** que trabalha a navegação por diretórios e a localização de arquivos. Recebemos um arquivo compactado contendo diversas pastas e arquivos, e nosso objetivo é encontrar um documento específico chamado `uber-secret.txt`.

O enunciado do desafio é o seguinte:

> Unzip this archive and find the file named 'uber-secret.txt'

Em tradução livre, devemos descompactar o arquivo fornecido e encontrar o documento chamado `uber-secret.txt`.

Print do enunciado da questão:

![Enunciado do desafio First Find](https://i.postimg.cc/HWSTv0WV/9209c35c-d9a2-4ef7-9dad-e6e421ed9ea6.png)

### Análise Inicial
Após baixar o arquivo ZIP disponibilizado pelo desafio, encontramos um arquivo compactado chamado `files`, que reúne os diretórios e documentos que precisamos examinar.

![Arquivo compactado fornecido pelo desafio](https://i.postimg.cc/7PBqt1Pb/9b87abc7-979e-4523-a2af-554058bb8d35.png)

Ao extrair seu conteúdo e abrir a pasta principal, identificamos vários arquivos de texto e três diretórios: `acceptable_books`, `adequate_books` e `satisfactory_books`. Como o enunciado solicita apenas a localização de um arquivo, podemos prosseguir examinando a organização das pastas, sem necessidade de decodificação ou ferramentas adicionais.

![Conteúdo inicial do arquivo descompactado](https://i.postimg.cc/jq8R36q2/94118963-787a-4f8d-a39c-0a3f4a47efed.png)

### Interpretação
A principal pista do desafio é o próprio nome do arquivo procurado: `uber-secret.txt`. Dessa forma, nossa tarefa consiste em explorar a estrutura de diretórios até encontrá-lo.

Embora o arquivo compactado contenha vários documentos, não precisamos analisar o conteúdo de todos eles. Basta acompanhar as pastas disponíveis e verificar seus nomes e arquivos. Neste caso, utilizamos o **Explorador de Arquivos do Windows** para realizar a busca manualmente.

### Resolução
Começamos acessando o diretório `acceptable_books`, no qual encontramos outros arquivos e uma subpasta chamada `more_books`. Essa organização indica que existem níveis adicionais a serem explorados.

![Arquivos e pasta more_books encontrados durante a navegação](https://i.postimg.cc/Kc9mp7cY/0a9193c7-3752-4722-950e-f980ddede55e.png)

Em seguida, abrimos a pasta `more_books`. Nela, encontramos outro arquivo de texto e um diretório chamado `.secret`, cujo nome sugere que possa conter o arquivo solicitado no enunciado.

![Pasta .secret localizada dentro de more_books](https://i.postimg.cc/qBmpDcBB/95549274-49fe-4c9f-9031-eec7c4fc0b4e.png)

Ao acessar o diretório `.secret`, encontramos um documento de texto chamado `uber-secret`. Como o Windows pode ocultar extensões de tipos de arquivos conhecidos, esse nome corresponde ao arquivo `uber-secret.txt` solicitado pelo desafio.

![Arquivo uber-secret encontrado na pasta .secret](https://i.postimg.cc/PJFhLHFG/b0023f82-a92e-4b42-80a1-9d825dcc68da.png)

Por fim, abrimos o documento em um editor de texto e encontramos a flag, confirmando que havíamos localizado o arquivo correto.

![Conteúdo do arquivo uber-secret contendo a flag](https://i.postimg.cc/fWHMq7WM/c6ce2871-df1d-496c-9eb4-6dbd4d782ef4.png)

> **Flag:** `academy{f1nd_15_f457_ab443fd1}`

### Conclusão
O desafio **First Find** explorou uma habilidade básica, mas importante, em CTFs: localizar arquivos dentro de estruturas de diretórios. A resolução exigiu apenas descompactar o arquivo recebido, navegar pelas pastas e abrir o documento indicado no enunciado.

Durante o processo, também observamos que diretórios iniciados por ponto, como `.secret`, podem ser utilizados para organizar ou disfarçar conteúdos. Essa convenção é especialmente comum em sistemas Unix-like, nos quais nomes iniciados por ponto normalmente são tratados como ocultos.

Esse exercício reforça a importância de compreender a organização de arquivos e diretórios, uma competência útil tanto em desafios de CTF quanto na análise inicial de sistemas e conjuntos de dados.
