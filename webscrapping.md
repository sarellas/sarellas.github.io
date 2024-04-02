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

## 1. Selector Gadget

Para você, que como eu, nunca mexeu em html, essa ferramenta vai pegar na sua mão e te levar aonde você precisa ir sem solavancos. o [SelectorGadget](https://rvest.tidyverse.org/articles/selectorgadget.html) trata-se de uma espécie de aplicativo que você salva na sua barra de favoritos do chrome ou seu browser de escolha e te permite identificar exatamente o código que você precisará jogar no R para identificar o elemento da página que você deseja que seu programa busque. 

Após clicar no SelectorGadget você vai ver que uma caixinha laranja aparecerá ao redor de cada elemento da página da web em que você passar o mouse e no canto inferior esquerdo da tela surgirá uma barra branca. Com este programa ativado, você clicará o mouse sobre a caixinha laranja na qual está o elemento que você quer selecionar. Neste momento o elemento se tornará verde e, provavelmente outros elementos da página ficarão em amarelo. Isso significa que o programa entende que você tem interesse em todos esses elementos destacados. Caso você não tenha, basta clicar em um dos elementos que não te interessam e ele se tornará vermelho, indicando que não deve entrar na seleção, e os demais itens semelhantes a ele deixarão de estar em destaque. Quando você tiver conseguido destacar apenas os elementos que realmente quer extrair, você vai clicar no código que aparecer na barra do canto inferior e, com isso, copiar o código em html referente aos elementos de escolha. 

Esta é a chave que usaremos no nosso código do R para que nosso programa busque exatamente o que queremos na página da web. Agora, vamos ao R.

## 2. Primeiros passos no rvest

A maneira como eu contruí meu código para buscar elementos semelhantes em várias páginas da web foi pensando em um esquema "de dentro para fora". O que isso significa: primeiramente fiz testes buscando um único elemento em uma única página, depois que ele funcionou, busquei na página anterior a ele, que é como um índice e, por fim, criei o for loop para repetir essa atividade em todas as páginas linkadas nessa "página índice". Então vamos começar do começo:

**Como buscar um elemento em uma página da web?**

```

### Referenciando a página da web
  link = paste0("https://sarellas.github.io/dadosBR.html")    # link da página com o elemento final que você procura
  post <- read_html(link)

### Criando um objeto com o título do post
  titulo <- post %>% 
    html_node(".post-title") %>%   ### colar entre aspas o código fornecido pelo SelectorGadget
    html_text2() %>%               ### transforma em texto o elemento
    str_remove("\n")               ### remove do texto o elemento \n que pode aparecer
  
```

Ok. Assim você conseguiu extrair o título do meu primeiro post no meu site. Parabéns, você já fez um scrapping! 

Agora digamos que você não queira apenas o título, mas também o primeiro parágrafo do texto. Você vai voltar à página que quer ler, clicar novamente no SelectorGadget e selecionar o novo elemento de escolha. No nosso caso, o primeiro parágrafo de texto irá retornar o seguinte código de htmp: "p:nth-child(1)". Agora vamos colocar isso em um novo objeto do R:

```
### Criando um objeto com o primeiro parágrafo 
  primeiro_paragrafo <- post %>% 
    html_node("p:nth-child(1)") %>%   ### colar entre aspas o código fornecido pelo SelectorGadget
    html_text2() %>%               
    str_remove("\n")               
```

Prontinho! Conseguimos buscar através do R dois elementos de uma página da web, mas você deve ter notado que eles foram salvos como lista, o que não é tão conveniente para checarmos o que estamos fazendo. Então, vamos colocar todos os dados que resolvemos extrair em um tibble, para ver se deu tudo certo:

```
dados_post1 <-
  tibble(
    titulo = titulo,
    primeiro_paragrafo = primeiro_paragrafo
  )
```

Agora, temos um tibble com duas colunas, a primeira com o título do post e a segunda com o primeiro parágrafo do post. 

![print_tibble](/assets/post_webscrapping1.png)

Podemos acrescentar aqui vários outros elementos que quisermos do site da web e seguir o mesmo processo, de maneira que cada um se tornará uma nova coluna do nosso tibble. Mas como isso é um tutorial simplificado, vamos para o próximo passo:

## 3. Identificando links de uma página raíz

Bom, dificilmente você vai querer usar um código para buscar elementos em apenas uma página da web, para isso você poderia simplesmente copiar e colar os elementos de interesse no Excel. Se você está apelando para o R, é porque você precisa automatizar uma tarefa repetitiva e desgastante, como clicar em vários links e buscar em cada um deles as informações do seu interesse. Então agora, vamos para a segunda camada da cebola e vamos olhar para o nosso repositório de links, que no caso do meu site, se chama a página "posts".

Vamos repedir o mesmo processo que fizemos dentro do primeiro post nessa nova página: linkar a página que queremos scrapear, buscar no SelectorGadget o elemento dos htmls que queremos e usar a função **html_attr()** para encontrar como os urls linkados variam.

```
### Referenciando a página da web
  link2 = paste0("https://sarellas.github.io/posts.html")    # link da página com o elemento final que você procura
  repositorio_posts <- read_html(link2)

### Identificando os urls das páginas que queremos
repositorio_posts %>% 
    html_nodes(".post-content a") %>%   ### código em html referente (apenas) aos posts linkados na página 
    html_attr("href")      # função que busca atributo na página, no caso, queremos o atributo "href" que significa hyperlink reference        
```




## 4. Criando uma função para automatizar o processo

Bom, agora que entendemos como ler e buscar informações de uma página da web, ou melhor, se duas páginas interligadas, queremos criar um programa que clique em cada link da página "Posts" e busque dentro de cada página à qual é direcionado as duas informações de interesse: o título e o primeiro parágrafo do post. Para tanto, vamos precisar criar uma função. Nesta etapa, eu me baseei consideravelmente [nesse](https://www.youtube.com/watch?v=6KWlPhPMluE) e [nesse](https://www.youtube.com/watch?v=x3UMny1fQhc&list=PLNUVZZ6hfXX1tyUykCWShOKZdIB0TIhtM&index=43) vídeos do YouTube que achei incrivelmente didático, fica a indicação do canal e da playlist, que tem conteúdos muito bons.

O fato de termos a mesma estrutura em todas as páginas das quais queremos obter os dados permite que nossa função seja composta de elementos que vão se repetir em cada link aberto, assim, a única variável que vai se alterar na nossa função é o link ou url de acesso já que, uma vez abertos, queremos a mesma informação de todos eles.

```

scrape_posts <- function(url){
  
  company_page <- read_html(url)
  
  name <- company_page %>% 
    html_node("tr:nth-child(1) .half") %>% 
    html_text2() %>%
    str_remove("\n")
  
  trade_name <- company_page %>% 
    html_node("tr:nth-child(1) td:nth-child(2)") %>% 
    html_text2() %>%
    str_remove("\n")
  

  corteva <-
    tibble(
      name = name,
      trade_name = trade_name,
      naics1 = naics1,
      naics2=naics2,
      sales = sales,
      url = url
    )
}

### testando
scrape_company(url = "https://www.naics.com/company-profile-page/?co=2") %>%
glimpse()

```








