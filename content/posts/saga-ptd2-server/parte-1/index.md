+++
title = 'Por que decidi fazer reverse engineering de um jogo Flash morto'
date = 2026-04-21T12:59:12-03:00
draft = false
tags = ["Reverse Engineering", "Pokémon Tower Defense", "Flash Games", "PHP"]
categories = ["Projetos", "Saga PTD2 Server"]
+++

Se você nasceu no final dos anos 90 ou no início dos anos 2000 e teve acesso à internet durante a infância, com certeza em algum momento você pesquisou por algo como "jogos online grátis" e acabou parando em sites como o ClickJogos, Kongregate, Newgrounds ou Friv.

Neles, você conheceu jogos clássicos que marcaram a minha e a sua infância, como o "*Dad'n me*", "*Super Smash Flash*", "*Age of War*", "*Fire Boy and Water Girl*" e "*Club Penguin*".

![Mosaico de logos de sites de jogos Flash antigos](/assets/flash-games.webp)


Eu sempre gostei muito de Pokémon, então joguei praticamente todos os jogos online relacionados à franquia. A maioria não era muito boa, mas alguns eram incríveis e se destacavam muito. Entre eles, posso citar a trilogia de **Pokémon Tower Defense** (ou PTD para os mais íntimos), criada pela *SnD Games*. O primeiro PTD já contava com todos os Pokémon da primeira geração e um modo história que seguia a linha dos jogos da região de Kanto (Red e Blue). Você podia escolher qual versão do jogo queria jogar e isso determinava quais Pokémon poderiam aparecer na natureza para você capturar.


{{< figure
src=assets/ptd1-menu.webp
alt="Menu do primeiro Pokémon Tower Defense"
caption="Menu do primeiro Pokémon Tower Defense"
>}}

O jogo funcionava com um sistema de seleção de fases, na qual você ia avançando na história e desbloqueando os próximos capítulos conforme ia avançando nas fases. Ao entrar nas fases, o jogo era bem parecido com outros *tower defense*. Sua tarefa era posicionar bem suas torres (Pokémon) e selecionar a melhor combinação de ataques para impedir que os inimigos avançassem e roubassem seus **Rare Candies** (um item raro da franquia Pokémon). Quando seus Pokémon derrotavam inimigos em batalha, eles ganhavam XP e com isso passavam de nível e ficavam mais fortes, podendo até mesmo evoluir. Para uma criança que nunca tinha tido um console da Nintendo, tudo aquilo era incrível.

{{< figure
src=assets/ptd1-gameplay.webp
alt="Imagem de gameplay do PTD1"
caption="Imagem de gameplay do PTD1"
>}}

Ele estava longe de ser um jogo fácil. Mesmo com Pokémon no nível máximo (lvl 100), ainda sim é preciso montar estratégias para passar de algumas fases e ginásios. Mas sem dúvidas foi um dos jogos que eu mais joguei. Mesmo com dificuldade eu eventualmente acabei zerando o jogo depois de alguns anos (sim, eu demorei anos para zerar).

Foi aí que eu descobri que tinha uma continuação, que contava com todas as gerações (que existiam na época) e também com um mapa de **mundo aberto**! O jogo em si é baseado na versão Gold e Silver de Pokémon, mas conta uma história um pouco diferente da original que também é bem interessante.

{{< figure
src=assets/ptd2-gameplay.webp
alt="Mapa do mundo aberto no Pokémon Tower Defense 2"
caption="Mapa do mundo aberto no Pokémon Tower Defense 2"
>}}

### O Fim de uma Era

Mas como vocês devem saber, no final de 2020 aconteceu o inevitável: o [Adobe Flash Player](https://www.adobe.com/br/products/flashplayer/end-of-life.html) foi oficialmente descontinuado. Os navegadores cortaram o suporte e, pouco a pouco, os servidores de dezenas de estúdios independentes começaram a ser desligados. Com a SnD Games não foi diferente.

> O servidor oficial dos jogos da série PTD saiu do ar permanentemente no dia 13 de abril de 2021, levando com ele os saves da comunidade e qualquer chance de jogar de forma oficial.

Diferente de muitos jogos em Flash clássicos, onde bastava baixar o arquivo `.swf` e rodar em um emulador offline como o [Ruffle](https://ruffle.rs/) ou o [Flashpoint](https://flashpointarchive.org/), o PTD2 era um caso mais complexo. **Ele tinha uma dependência do backend para poder iniciar o jogo.** Ter apenas o cliente do jogo era como ter um carro sem motor: a tela inicial abria, mas não tinha como ir muito além disso.

Eu não queria deixar esse pedaço da minha infância desaparecer. Eu tinha os arquivos do jogo (o cliente em Flash), mas ele era inútil sem o servidor para autenticar, salvar o progresso e processar os eventos do jogo. Foi aí que percebi que se eu quisesse jogar PTD2 de novo, eu teria que decifrar como o jogo se comunicava com um servidor que não existia mais. Eu precisaria abrir o código ActionScript, entender seus pacotes de rede e construir um backend inteiro do zero.

E é exatamente sobre essa insanidade que vamos falar no próximo post.
