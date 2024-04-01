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

Para você, que como eu, nunca mexeu em html, essa ferramenta vai pegar na sua mão e te levar aonde você precisa ir sem solavancos. Trata-se de uma espécie de aplicativo que você salova na sua barra de favoritos do chrome ou seu browser de escolha e te permite identificar exatamente o código que você precisará jogar no R para identificar o elemento da página que você deseja que seu programa busque.
