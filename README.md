# deeBO

Este projeto tem a intenção de apontar pontos com maiores chances de crimes em São Paulo.

Dataset: https://www.kaggle.com/inquisitivecrow/crime-data-in-brazil

- Problema: O Brasil tem um alto índice de crimes e recursos insuficientes para lidar com isso.
- Solução: Com a identificação das áreas de maior risco, seria possível melhor planejamento estratégico para prevenir crimes.
- Beneficiados: O governo e a polícia que poderiam trabalhar de forma mais eficiente. A população que poderia evitar áreas com maiores índices de criminalidade.

O atual trabalho pode ser dividido em 3 principais partes:

- 1 - Análise Exploratória e preparação dos Dados
- 2 - Plotagem e visualização em mapa
- 3 - Construção de Redes Neurais Profundas para predição de crimes

O totoal do projeto pode ser verificado nos notebooks. Segue abaixo um resumo:

### Análise Exploratória

O Dataset possui uma seérie de arquivos. Dentre eles, temos arquivos com o prefixo "RDO", que são dados do Registro Geral de Ocorrências. Nele, temos dados sobre Boletins de Ocorrências de 2010 à 2017. Segue abaixo uma visão geral da quantidade de registros por mês:

![image](https://user-images.githubusercontent.com/15863005/60390510-b731ec00-9aae-11e9-8a16-909b74943326.png)

Note que, existe um certo desbalanceio em relação à quantidade de registros em alguns meses. Tendo em vista que alguns meses não há uma ocorrência sequer, nos leva a crer que o dataset não esteja completo e que essa discrepância não foi provocada pela simples redução de criminalidade.

Observando anualmente, podemos tirar as mesmas conclusões.

![image](https://user-images.githubusercontent.com/15863005/60390534-28719f00-9aaf-11e9-9902-2f528ef7d688.png)

O mesmo pode ser observado nos dados anuais que não estão presentes no RDO, como é possível ver no gráfico mensal abaixo:

![image](https://user-images.githubusercontent.com/15863005/60390543-548d2000-9aaf-11e9-8db1-6138a6a8364e.png)

Sobre os tipos de crimes cometidos, temos a coluna "RUBRICA" que apresenta um dado categórico. Sua distribuição no dataset RDO pode ser observada abaixo:

![image](https://user-images.githubusercontent.com/15863005/60390549-928a4400-9aaf-11e9-9d66-2a270e83bbdf.png)

A fim de reduzir o número de caegorias, no atual trabalho, realizamos uma série de generalizações deste campo. Assim, ficamos apenas com as categorias: "ROUBO", "FURTO", "HOMICÍDIO", "ESTUPRO", "LESÃO CORPORAL" E "TRÁFICO". Observe abaixo a distribuição desses crimes apenas no ano de 2016:

![image](https://user-images.githubusercontent.com/15863005/60390574-0a586e80-9ab0-11e9-8e56-35a307db37c1.png)

## Plotagem e Visualização no Mapa

Para visualizar a localização dos crimes, plotamos os dados em um mapa interativo. Assim é possível acompanhar onde ocorreu, sua categoria e detalhes adicionais. É possível navegar no mapa e pesquisar com detalhes as áreas de interesse. Cada cor representa uma das categorias criadas. Ao passar o mouse sobre o ponto, pode-se observar seus detalhes.

<img width="962" alt="mapa_crime2" src="https://user-images.githubusercontent.com/11601865/60390739-c4050e80-9ab3-11e9-8726-13b33177d50e.png">

## Construção de Redes Neurais Profundas para predição de crimes

### RNN para prever número de ocorrências

![image](https://user-images.githubusercontent.com/15863005/60390578-396ee000-9ab0-11e9-9657-e4b34cb00d8a.png)

Nesta rede, o desbalanceio do dataset influenciou negativamente no número de crimes previstos. Observe no exemplo acima, como a dado previsto é, em média, superior ao real.

- ANN para prever a localização das ocorrências

A fim de prever a localização dos crimes tendo no dataset a longitude e latitude. Construímos um geohash para essas coordenadas e, assim, podemos tratar essas duas colunas como sendo apenas uma. Cada geohash representa uma área no mapa, que engloba um conjunto de coordenadas. Dessa forma, utilizamos esse dado como dado categórico.
No total, o dataset possui 282 geohashes distintas espalhadas pela grande São Paulo. E o objetivo desta ANN é prever a geohash das observações.Observe no notbook "RDO_ANN_2.ipynb".
