+++
title = 'Selfhosting E Outras Aventuras'
date = 2026-04-06T22:03:31-03:00
draft = true
+++


## Prévia
Eu ja imaginava que eu iria demorar para fazer outro post, mas eu consegui superar minhas expectativas e demorar mais de quatro meses para começar a escrever o segundo post desse blog.


Não foi por falta de ideias nem de conteúdo, eu tenho feito algumas coisas bem legais nos últimos tempos. A primeira e talvez mais óbvia é que eu comprei um domínio (`kgmats.cc`) e configurei um servidor (o meu Raspberry PI, que eu havia comentado no post anterior), com isso abri um leque de possibilidades, já que agora eu posso hospedar qualquer tipo de conteúdo ou serviço sem depender mais do servidor do IC da Unicamp, que era limitado a hospedar conteúdo estático e majoritariamente académico. 

---- 

## Dando um pouco de contexto
 Desde que eu comecei a programar alí pelos meus 12 anos, me lembro de que achava muito legal a ideia de ter um site próprio, tanto que eu até cheguei a fazer alguns protótipos meio tosquinhos usando HTML e CSS, mas como eu ainda era uma criança eu obviamente não tinha conta em banco muito menos cartão de crédito para poder pagar por uma hospedagem numa AWS da vida.

Eu lembro que cheguei a tentar usar meu computador pessoal como servidor fazendo Port-Forwarding e usando No-IP para obter um domínio gratuito, mas toda a burocracia de configuração juntamente com o firewall do provedor de internet ipediram que ele se concretizasse, então esse sonho de ter meu site ficou ¨guardado na gaveta¨ por quase 10 anos até que eu entrei na Unicamp, onde tive um lugar para hospedar meu primeiro site que era realmente meu.

Para quem não sabe: os alunos do IC (Instituto de Computação) da Unicamp podem hospedar um site estático utilizando sua conta institucional. Para isso, basta criar uma pasta chamada `public_html` dentro da sua `HOME` e colocar suas páginas HTML lá. Fazendo isso seu conteúdo passa a ser acessível utilizando a url:

`https://students.ic.unicamp.br/~{seu_usuario}/`

Daí todo o conteúdo passa a ser acessado usando o caminho relativo à pasta `public_html`. Foi assim que eu hospedei meu primeiro portifólio (que, inclusive, nunca terminei).


Mas isso é bem limitado. Como eu disse antes, não é possível executar código no Backend, não tem banco de dados e você (ao menos em tese) não pode hospedar conteúdo que não seja académico.

---

## Montando meu próprio servidor

Recentemente, durante as férias, eu vi meu bom e velho Raspberry PI parado em casa e pensei que poderia ser legal utilizar ele como servidor.

Reservei uma tarde para instalar e configurar:

- Debian 13 (Trixie)
- Nginx
- PHP
- PostgreSQL
- Docker

Além das ferramentas que sempre instalo em todas as minhas máquina, como Neovim e ZSH.

Depois de configurado, fui pesquisar se hoje em dia tinha alguma ferramenta que me permitisse expor meu servidor sem precisar pedir para o provedor de internet por um IP fixo e acabei de deparando com o Cloudflare Tunnel. É uma ferramenta incrível. Funciona super bem, é gratuito e cumpre exatamente o propósito de tornar meu servidor acessível sem muita configuração. O princípio que o Cloudflare Tunnel utiliza para tornar seu servidor acessível é bem simples: Se você é uma pessoa comum, muito provavelmente seu roteador está configurado atras de um NAT, o que significa na pratica que o seu endereço de IP público não é seu de fato, na verdade ele é compartilhado por vários outros clientes do seu provedor e vocês näo säo acessíveis para computadores fora da rede do seu provedor, portanto mesmo se você fizesse algo como port-forwarding e não houvessem restrições do firewall, não há uma forma simples de alguém conseguir acessar seu servidor simplesmente porque ele não tem um IP válido. 

Para contornar isso, a cloudflare utiliza o que eles chamam de Tunel que resumidamente funciona do seguinte modo: As pessoas de fora da rede são incapazes de acessar seu computador, e vice-versa, mas tanto seu computador quanto o do seu cliente é capaz de acessar os servidores da Cloudflare, então o que acontece é que a Cloudflare atua como intermediária, passando adiante os pacotes de rede que vocês enviam um para o outro utilizando uma conexão criptografada que é passada pela rede da Cloudflare do seu servidor até chegar no outro lado do tunel, que nesse caso é computador do seu cliente.


---

## Comprando um domínio

Com meu servidor acessível à internet, agora tudo que eu precisava era comprar um domínio. Eu pesquisei um pouco e acabei escolhendo `kgmats.cc`. KGMats é a abreviação do meu nome e `.cc` é a abreviação de Ciência da Computação (`.cc` Também é o código de país das Ilhas Cocos, um território australiano, mas isso aí deve ser só coincidência). Essa brincadeira de comprar o domínio saiu bem mais barato do que eu imaginei, custando a bagatela de 80 reais por ano. 
 
----

 ## Mas manter um site não é caro?
Surpreendentemente, não.

Manter a infraestrutura de um site pequeno como o meu de pé hoje em dia é surpreendentemente barato. O custo mensal do meu domínio é de pouco mais de R$6.60 e Meu Raspberry PI utiliza uma pequena fonte de alimentação USB de 5V e 3A para funcionar, o que equivale a uns 15W. Considerando que ele fica ligado 24/7, o consumo mensal é da faixa de uns 10.8kW/h. O preço do kW/h em São Paulo hoje é por volta de uns R$0.70, o que faz com que meu Raspberry tenha um custo teórico de R$7.56/mês, o que resulta num custo total de aproximadamente R$14.22/mês para manter meu site no ar. Mas obviamente o custo real é bem menor, já que ele utilizaria os 15W em uso máximo, mas na maior parte do tempo ele fica em IDLE com uso de CPU praticamente 0. É basicamente o orçamendo de uma coxinha e uma Coca-Cola.


## Mas o que você hospeda afinal?
Bom, atualmente eu tenho 10 aplicações Web rodando no meu servidor, que são:


- `hugo`: Um blog (Esse mesmo que você está lendo agora)
- Meu portifólio (acessível pela url `kgmats.cc`)
- `librespeed`: Um teste de velocidade similar ao `speedtest.net`
- `grafana`: Uma plataforma onde eu consigo criar dashboards para monitorar consumo de recursos e acessos meu servidor (juntamente com cADvisor, prometheus e Loki)
- `portainer`: Ferramenta que utilizo para gerenciar meus containers Docker
- `PTD2`: Backend de um jogo chamado Pokemon Tower Defense 2, o qual eu construí do zero em PHP fazendo engenharia reversa do bytecode decompilado do client do jogo
- `privatebin`: Versão Open-Source do Privatebin, usada para compartilhar textos e arquivos temporários via link (muito útil para compartilhar código ou outros arquivos rápidos)
- `traefik`: proxy reverso que gerencia roteamento e HTTPS dos serviços
- `streak-stats` e `github-stats`: Micro serviços que geram cards de estatísticas de contribuições para minha página do github

Além claro do bom e velho SSH que é sempre útil. Nunca se sabe quando você vai precisar de um servidor linux para executar algum comando rápido quando estiver sem seu notebook na rua.

Todos os meus serviços estão configurados em sandbox utilizando containers docker e docker-compose


## Conclusão
Acredito que me estendi bastante, este post já está um pouco maior do que eu gostaria.

Posso fazer mais posts explicando em mais detalhes cada um dos meus serviços no futuro e Também os outros projetos que eu ainda estou desenvolvendo e pretendo publicar em breve.

No mais, recomendo fortemente a qualquer estudante da área de técnologia que pretende trabalhar como desenvolvedor web experimente configurar seu próprio servidor do zero. Mesmo montando um setup simples como o meu, já ensina muito sobre redes, infraestrutura e DevOps.
