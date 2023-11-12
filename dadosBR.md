# Pacotes de dados brasileiros no R

Na hora de encontrar os dados necessários para uma pesquisa, o trabalho pode ser muito árduo, envolvendo abrir sites do governo e investigar os seus confins para encontrar o que se precisa. Às vezes, você se depara com tabelas desorganizadas ou com informações mais resumidas do que gostaria.

Felizmente, descobri ao longo de 4 anos de doutorado, pacotes disponíveis no R para download automático de dados, nos quais muitas vezes uma única linha de código já é capaz de revolver o seu problema.

Creio que muitos deles já sejam bastante conhecidos, mas como alguns foram novidade para mim e outros estavam por aí perdidos em projetos nos quais já trabalhei, achei interessante listar aqui todos os que me lembro, já que podem ser também novidade para outras pessoas.
- **BETS**: o nome já diz tudo “Brazilian Economic Time Series”. Para encontrar os códigos das séries que você quer utilizar, consulte no SGS do Banco Central.
- **Rbcb**: permite acesso aos dados do SGS do BCB, é muito prático e também funciona com os códigos do SGS. Muito rica em dados macroeconômicos.
- **Ipeadatar**: permite acesso aos dados da plataforma IpeaData.
- **Sidrar**: permite o download das bases disponíveis no portal SIDRA do IBGE, como dados do censo e da Pnad (não achei a usabilidade tão boa quanto de outros nesta lista)
- **Siconfir**: pacote para acessar dados de impostos dos estados e municípios brasileiros.
- **cepR**: pacote R para buscar informações sobre CEPs, endereços, bairros e cidades.
- **Microdatasus**: trabalho incrível do Rafael Saldanha para download de dados do DataSUS e pré-processamento no R, inclui microdados de nascimento e mortes por municípios.
- **Geobr**: permite acesso à conjuntos de dados espaciais oficiais do Brasil, extremamente útil para o desenvolvimento de mapas.
- **PNADcIBGE**: para baixar dados da Pnad. 

Provavelmente esqueci ou não conheço muitos outros, então fiquem à vontade para contribuir nos comentários com os pacotes que vocês conhecem. Todos os pacotes comentados acima contam com página no GitHub, na qual é possível consultar a melhor forma de uso.