---
title: "Tutorial de Web Scrapping simples em R"
---

Venho hoje com a tarefa, talvez ousada, se apresentar para vocês um código simples e adaptável para utilizar métodos de web scrapping no R, através do pacote **rvest**.

Gostaria de frisar que se trata do compartilhamento de uma ferramenta que eu mesma acabei de aprender para utilizar na minha pesquisa de doutorado, portanto, certamente não será a mais profissional e eficiente, mas deu certo! E muitas vezes é isso que importa! 
No decorrer desse post, deixarei linkados alguns materiais e vídeos que utilizei para desenvolver esse código e que foram extremamente úteis para me levar do ZERO a um resultado final de scrapping.

O primeiro material que utilizei para entender por onde começar foi a segunda edição do [R for Data Science](https://r4ds.hadley.nz/webscraping), que tem um capítulo específico apenas para web scrapping. Recomendo essa leitura para você começar a se familiarizar com o tema. Mas como a ideia aqui é trazer um material mais direto ao ponto, vou sintetizar os aprendizados que foram mais importantes para mim. 

Os pacotes necessários para esse tutorial são os seguintes:

```{r}
library("tidyverse") # pois não sei fazer nada sem ele
library("rvest") # nosso pacote de scrape
```

1. **Selector Gadget**

Para você, que como eu, nunca mexeu em html, essa ferramenta vai pegar na sua mão e te levar aonde você precisa ir sem solavancos. o [SelectorGadget](https://rvest.tidyverse.org/articles/selectorgadget.html) trata-se de uma espécie de aplicativo que você salva na sua barra de favoritos do chrome ou seu browser de escolha e te permite identificar exatamente o código que você precisará jogar no R para identificar o elemento da página que você deseja que seu programa busque. 

Após clicar no SelectorGadget você vai ver que uma caixinha laranja aparecerá ao redor de cada elemento da página da web em que você passar o mouse e no canto inferior esquerdo da tela surgirá uma barra. Com este programa ativado, você clicará o mouse sobre a caixinha laranja na qual está o elemento que você quer selecionar. Neste momento o elemento se tornará amarelo e, provavelmente outros elementos da página também. Isso significa que o programa entende que você tem interesse em todos esses elementos destacados. Caso você não tenha, basta clicar em um dos elementos que não te interessam e ele se fornará vermelho, assim como apagará o destaque de outros parecidos com ele. Quando você tiver conseguido destacar apenas os elementos que realmente quer extrair, você vai clicar no código que aparecer na barra do canto inferior e, com isso, copiar esse código. 

Esta é a chave que usaremos no nosso código do R para que nosso programa busque exatamente o que queremos na página da web. 
