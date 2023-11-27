---
title: Dados em painel para modelo diff-in-diff
---

*Uma breve introdução ao modelo de diferenças em diferenças*

Seguindo o post recentemente publicado com uma análise visual de dados em painel, achei que seria interessante fazer o mesmo para a aplicação de modelos específicos que exigem o uso de bases de dados formatadas em painel. 

Vamos começar com o modelo diff-in-diff, ou diferenças em diferenças. 

Este modelo é muito utilizado em avaliações de impacto de políticas públicas, pois ele considera duas variações, a variação temporal e a variação entre tratados e controle. 

Ou seja, considerando o exemplo visual abaixo, digamos que uma política seja adotada em 2018 e que ela atinja apenas indivíduos que se caracterizam por um fator intrínseco a eles, como região de moradia, cor, sexo, renda. Neste caso, vamos ter duas características que definem se o indivíduo será ou não afetado pela política:

1) **Período**: o período em questão figurando no painel é antes ou depois da política ter sido adotada?

2) **Tratamento**: o indivíduo em questão é alvo da política ou não?

|  | Antes | Depois |
| Tratamento | | |
| Controle | | |

Essas categorias figuram no painel utilizado para DID como dummies. Observe que, para todos os indivíduos, a dummy de período apresentará os mesmos valores, assumindo valor zero antes de 2018 e valor 1 após 2018, já que a política foi adotada de maneira homogênea nesta amostra a partir de 2018. Já a dummy de tratamento aponta apenas as unidades que foram tratadas ou não, dessa forma, ela assume 1 para os indivíduos tratados em todos os períodos e 0 para os indivíduos não tratados (ou de controle).

Ao final, a variável que utilizamos para aplicar o método é dada pela interação entre essas duas dummies, e forma uma nova variável dummy, que assume valor 1 apenas para os indivíduos tratados após o período de tratamento.


![print-did](/assets/painel-did.png)

Vale fazer algumas ressalvas. Uma política cujo tratamento se basea em características passíveis de mudança pelos indivíduos pode estar desenhada de maneira ineficiente, permitindo que os indivíduos busquem ativamente formas de se encaixar nessa classificação para serem abarcados pela política.

Além disso, note que, para o uso do diff-in-diff tradicional como apresentado aqui, consideramos que uma vez tratadas, as unidades continuam tratadas para sempre, além de que a política atinge todos os indivíduos no mesmo período. Hoje já existem variações deste modelo para políticas cuja adoção ocorre gradualmente, sendo expandida no decorrer de vários períodos. Se quiser consultar alguns desses modelos mais recentes, busque por diferenças em diferenças em múltiplos estágios do Callaway e Sant'Anna (2021). Outras referências que introduziram esses novos métodos foram os artigos de Goodman-Bacon (2021) e Sun e Abraham (2021).

Esse post foi publicado de maneira simplificada no meu [LinkedIn](https://www.linkedin.com/in/natalia-sarellas/), caso queira, confira minhas publicações por lá.

### Referências

* Callaway, B. and P. H. Sant’Anna (2021). Difference-in-differences with multiple time periods. Journal of Econometrics 225 (2), 200–230.
* Goodman-Bacon, A. (2021). Difference-in-differences with variation in treatment timing. Journal of Econometrics 225 (2), 254–277.
* Sun, L. and S. Abraham (2021). Estimating dynamic treatment effects in event studies with heterogeneous treatment effects. Journal of Econometrics 225 (2), 175–199.
