---
title: "Como organizar uma base de dados em painel?"
---

*Uma apresentação visual para melhor entendimento desse formato de base de dados*


Estava recentemente fazendo um trabalho freelancer em pesquisa que envolvia, antes de tudo, transformar a base de dados exportada no formato em painel, durante este trabalho me dei conta como, uma vez que colocamos a mão na massa, as coisas fazem muito mais sentido e achei que poderia fazer um esforço em traduzir esse formato de base de dados por aqui.

Para aqueles da economia, seja graduação ou pós, é muito comum nos depararmos nas disciplinas de econometria com as especificações do modelo, ou seja, aquela expressão y = beta_0 + beta_1X + erro. Aprendemos as derivações dos modelos, minimizando erros quadrados, as propriedades necessárias para o resultado ser o mais próximo possível da realidade, mas comumente não temos muita compreensão de como o trabalho é feito na prática. Por isso, resolvi trazer um esquema visual de dados em painel, para tentar deixar o mais intuitivo possível como a base é construída.

Dados em painel são muito usados para avaliação de políticas públicas e estão entre uma análise de **série temporal** e **cross-section** (imagem abaixo), já que apresentam uma mesma unidade (no exemplo, indivíduo) e valores para vários períodos (no exemplo, 2016 a 2019). 

![print](/assets/print-st-cs.png)

Note que, no painel (imagem abaixo), o indivíduo se repete exatamente a quantidade de períodos que temos na amostra e temos resultados de todas as variáveis para cada indiv.-período (caso não tivéssemos, seria um painel desbalanceado).

As primeiras colunas até F já seriam o suficiente caso quiséssemos utilizar um modelo como o pooled OLS, no entanto, quando incluímos dummies para **efeitos fixos** de indivíduos e período, isso nos ajuda a “filtrar” características específicas dessas variáveis e ter uma análise mais precisa, usando o modelo de Efeitos Fixos. Podemos entender essas variáveis dummies como uma forma de se considerar as especificidades de um indivíduo no efeito que a variável explicativa terá sobre ele, ou então as especificidades de um ano, no qual podem ter ocorrido eventos muito particulares, neste efeito. 

![print](/assets/print-painel.png)

Esse post está longe de buscar se aproximar de uma aula, trata-se apenas de uma aluna compartilhando uma forma de visualização que a ajudou a compreender o assunto. Por isso não entrei em detalhes técnicos de econometria, nem nada assim. Fiquem à vontade para desenvolver a discussão e incrementar pontos que possam ter faltado.

Confira a [versão completa](https://docs.google.com/document/d/1r-Njf6lgkScfKHMmYQI2xvpI_AC3xj-_-7g10ADDE88/edit?usp=sharing) deste material em formato de texto. Esse post foi inicialmente criado para o [LinkedIn](https://www.linkedin.com/in/natalia-sarellas/), caso queira confira minhas publicações por lá.
