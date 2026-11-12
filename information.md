# information
> Categoria: Forensics

### Introdução
Este é um desafio de [análise forense digital](https://en.wikipedia.org/wiki/Digital_forensics) do **picoCTF 2021**, chamado **information**, no qual recebemos uma imagem no formato JPEG e precisamos encontrar uma flag escondida em informações que não aparecem diretamente ao visualizar a fotografia. O enunciado sugere que arquivos podem ser modificados de maneiras discretas, direcionando nossa investigação aos [metadados](https://en.wikipedia.org/wiki/Metadata) da imagem.

O enunciado do desafio é o seguinte:

> Files can always be changed in a secret way. Can you find the flag?
>
> Arquivo fornecido: `cat.jpg`

Print do enunciado da questão:

![Enunciado do desafio information](https://i.postimg.cc/SRtqX41H/f9b2db99-70df-49d9-8f04-dfeaeb196d87.png)

### Análise Inicial
Após baixar e abrir o arquivo `cat.jpg`, encontramos uma fotografia de um gato sobre o teclado de um notebook. À primeira vista, a imagem não apresenta nenhuma flag ou mensagem evidente, o que indica que a informação procurada pode estar armazenada fora do conteúdo visual da fotografia.

![Imagem original cat.jpg](https://i.postimg.cc/nVdnSKVh/4dd74a94-df46-4ad0-b269-44a6bf0fc118.png)

Arquivos JPEG podem conter metadados, como informações da câmera, software utilizado, data de criação e campos de descrição. Esses dados podem ser examinados sem alterar a imagem, sendo um ponto de partida importante para a análise forense.

### Interpretação
Como o desafio destaca que arquivos podem ser modificados de maneira secreta, nossa hipótese foi que a flag estivesse escondida em algum campo dos metadados do JPEG, e não nos pixels visíveis.

Para verificar essa possibilidade, utilizamos a ferramenta online [exif.tools](https://exif.tools/), que permite inspecionar os metadados de arquivos. O mesmo tipo de análise também pode ser realizado com o [ExifTool](https://exiftool.org/), ferramenta especializada na leitura e manipulação de metadados.

Ao examinar os campos disponíveis, identificamos no atributo **License / resource** uma sequência de caracteres aparentemente sem sentido. Pelo formato da string, consideramos a possibilidade de se tratar de uma mensagem codificada em **Base64**.

Para testar essa hipótese, utilizamos o [CyberChef](https://gchq.github.io/CyberChef/), que possui operações como **Magic**, para identificar possíveis codificações, e **From Base64**, para converter o conteúdo codificado em texto legível.

### Resolução
O primeiro passo foi acessar o site **exif.tools** e enviar o arquivo `cat.jpg` para análise. A ferramenta reconheceu o arquivo como uma imagem JPEG e apresentou sua prévia, além de informações sobre o arquivo e os metadados disponíveis.

![Arquivo cat.jpg carregado no exif.tools](https://i.postimg.cc/90NV42gv/4b2810cc-9735-467e-904b-b334e6300c42.png)

Em seguida, examinamos os metadados até encontrar o campo **License / resource**. O conteúdo desse campo era uma sequência de caracteres codificada, diferente de uma licença convencional e, portanto, relevante para a investigação.

![Campo License resource contendo a mensagem codificada](https://i.postimg.cc/FznmfvCq/739fc86f-2e39-4ed2-a8a3-8fee1d03e0ae.png)

Copiamos a sequência encontrada e a inserimos no campo **Input** do CyberChef. A operação **Magic** pode ser utilizada para identificar automaticamente padrões de codificação e sugerir uma conversão adequada. Nesse caso, a sequência correspondia a uma codificação **Base64**; a captura da resolução mostra a operação **From Base64** aplicada ao conteúdo.

Ao realizar a decodificação, o campo **Output** revelou a flag em texto claro:

```text
academy{the_m3tadata_1s_modified}
```

![Decodificação da mensagem Base64 no CyberChef](https://i.postimg.cc/GtSrBRgV/43b7bc5c-db9f-4793-83dc-32faae547a3c.png)

> **Flag:** academy{the_m3tadata_1s_modified}

### Conclusão
Este desafio demonstrou como informações podem ser escondidas nos **metadados de um arquivo de imagem**, sem modificar necessariamente sua aparência visual. Embora a fotografia parecesse comum, um de seus campos continha uma mensagem codificada em **Base64**, que pôde ser recuperada por meio da inspeção dos metadados e de uma operação de decodificação.

A utilização do **exif.tools** permitiu localizar rapidamente o campo que armazenava a mensagem, enquanto o **CyberChef** facilitou a identificação e a conversão do conteúdo para texto claro. É importante destacar que o Base64 não é um método de criptografia: trata-se de uma codificação reversível, utilizada aqui para ocultar a flag de uma leitura imediata.

O desafio reforça a importância de não limitar uma investigação forense ao que é visível na tela. Campos como descrição, autor, comentários e licença podem conter dados relevantes, tornando a análise de metadados uma etapa fundamental em desafios de **Forensics** e na investigação de arquivos digitais.
