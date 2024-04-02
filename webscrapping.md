---
title: "Tutorial de Web Scrapping simples em R"
---

Venho hoje com a tarefa, talvez ousada, de apresentar para vocês um código simples e adaptável para utilizar métodos de web scrapping no R, através do pacote **rvest**.

Gostaria de frisar que se trata do compartilhamento de uma ferramenta que eu mesma acabei de aprender para utilizar na minha pesquisa de doutorado, portanto, certamente não será a mais profissional e eficiente, mas deu certo! E muitas vezes é isso que importa! 
No decorrer desse post, deixarei linkados alguns materiais e vídeos que utilizei para desenvolver esse código e que foram extremamente úteis para me levar do ZERO a um resultado final de scrapping.

O primeiro material que utilizei para entender por onde começar foi a segunda edição do [R for Data Science](https://r4ds.hadley.nz/webscraping), que tem um capítulo específico apenas para web scrapping. Recomendo essa leitura para você começar a se familiarizar com o tema. Mas, como a ideia aqui é trazer um material mais direto ao ponto, vou sintetizar os aprendizados que foram mais importantes para mim. 

Os pacotes necessários para esse tutorial são os seguintes:

```{r}
library("tidyverse") # pois não sei fazer nada sem ele
library("rvest") # nosso pacote de scrape
library(data.table) # sempre bom ter
```

1. **Selector Gadget**

Para você, que como eu, nunca mexeu em html, essa ferramenta vai pegar na sua mão e te levar aonde você precisa ir sem solavancos. o [SelectorGadget](https://rvest.tidyverse.org/articles/selectorgadget.html) trata-se de uma espécie de aplicativo que você salva na sua barra de favoritos do chrome ou seu browser de escolha e te permite identificar exatamente o código que você precisará jogar no R para identificar o elemento da página que você deseja que seu programa busque. 

Após clicar no SelectorGadget você vai ver que uma caixinha laranja aparecerá ao redor de cada elemento da página da web em que você passar o mouse e no canto inferior esquerdo da tela surgirá uma barra branca. Com este programa ativado, você clicará o mouse sobre a caixinha laranja na qual está o elemento que você quer selecionar. Neste momento o elemento se tornará verde e, provavelmente outros elementos da página ficarão em amarelo. Isso significa que o programa entende que você tem interesse em todos esses elementos destacados. Caso você não tenha, basta clicar em um dos elementos que não te interessam e ele se tornará vermelho, indicando que não deve entrar na seleção, e os demais itens semelhantes a ele deixarão de estar em destaque. Quando você tiver conseguido destacar apenas os elementos que realmente quer extrair, você vai clicar no código que aparecer na barra do canto inferior e, com isso, copiar o código em html referente aos elementos de escolha. 

Esta é a chave que usaremos no nosso código do R para que nosso programa busque exatamente o que queremos na página da web. Agora, vamos ao R.

2. **Primeiros passos no rvest**

A maneira como eu contruí meu código para buscar elementos semelhantes em várias páginas da web foi pensando em um esquema "de dentro para fora". O que isso significa: primeiramente fiz testes buscando um único elemento em uma única página, depois que ele funcionou, busquei na página anterior a ele, que é como um índice e, por fim, criei o for loop para repetir essa atividade em todas as páginas linkadas nessa "página índice". Então vamos começar do começo:

**Como buscar um elemento em uma página da web?**

```

### Referenciando a página da web
  link = paste0("https://sarellas.github.io/dadosBR.html")    # link da página com o elemento final que você procura
  post <- read_html(link)

### Criando um objeto com o título do post
  elemento <- post %>% 
    html_node(".post-title") %>%   ### colar entre aspas o código fornecido pelo SelectorGadget
    html_text2() %>%               ### transforma em texto o elemento
    str_remove("\n")               ### remove do texto o elemento \n que pode aparecer
  
```

Ok. Assim você conseguiu extrair o título do meu primeiro post no meu site. Parabéns, você já fez um scrapping! 

Agora digamos que você não queira apenas o título, mas também o primeiro parágrafo do texto. Você vai voltar à página que quer ler, clicar novamente no SelectorGadget e selecionar o novo elemento de escolha. No nosso caso, o primeiro parágrafo de texto irá retornar o seguinte código de htmp: "p:nth-child(1)". Agora vamos colocar isso em um novo objeto do R:

```

```






