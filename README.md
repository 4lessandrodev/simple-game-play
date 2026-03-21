# Fuja da Tempestade

![Banner do jogo](source/og-image.png)

<p align="center">
  <strong>Jogo de tabuleiro digital local desenvolvido com Phaser 3, HTML, CSS e JavaScript.</strong><br />
  Um projeto focado em tensão, leitura de risco, feedback visual forte e regras simples de aprender.
</p>

<p align="center">
  <img alt="Status" src="https://img.shields.io/badge/status-jog%C3%A1vel-22c55e" />
  <img alt="Engine" src="https://img.shields.io/badge/engine-Phaser%203-3b82f6" />
  <img alt="Modo" src="https://img.shields.io/badge/modo-local%202--4%20jogadores-f59e0b" />
  <img alt="Plataforma" src="https://img.shields.io/badge/plataforma-web-111827" />
</p>

---

## Visão geral

**Fuja da Tempestade** é um jogo de tabuleiro competitivo para **2 a 4 jogadores** em que cada participante tenta alcançar o final do percurso antes de ser destruído pela tempestade. A partida mistura:

- avanço por dado
- casas especiais de bomba e pergunta
- perguntas de múltipla escolha por categoria
- eventos de suspense
- efeitos sonoros e feedback visual
- uma tempestade progressiva que elimina jogadores e pressiona o ritmo da partida

O objetivo é simples: **chegar primeiro à casa final ou sobreviver até ser o último jogador em pé**.

<p align="center">
  <a href="https://4lessandrodev.github.io/simple-game-play/index.html" target="_blank">
    <img alt="Jogar agora" src="https://img.shields.io/badge/⚡%20JOGAR%20AGORA-FUJA%20DA%20TEMPESTADE-ef4444?style=for-the-badge&logo=google-chrome&logoColor=white" />
  </a>
</p>

---

## Destaques do projeto

- tabuleiro com **54 casas**
- suporte a **2, 3 ou 4 jogadores locais**
- configuração inicial com nomes dos jogadores e categoria de perguntas
- sistema de dado com **carregamento por barra de espaço**
- rolagem com **probabilidade influenciada pela força**
- casas especiais de **bomba** e **pergunta**
- tempestade progressiva com destruição de casas e eliminação
- modais de suspense para reforço de feedback
- efeitos sonoros para ações relevantes
- fluxo completo de início, partida, eliminação, vitória e reinício

---

## Mecânica principal do dado

Um dos diferenciais atuais do projeto é a substituição da rolagem simples por uma mecânica com mais tensão e participação do jogador.

### Como funciona

1. o jogador abre o modal de rolagem
2. segura a **barra de espaço**
3. a barra de força começa a carregar
4. ao soltar, a força é travada
5. essa força altera a **probabilidade** do resultado do dado
6. o peão então se move com base no valor sorteado

### Intenção de design

A proposta não foi transformar o jogo em simulação física, e sim criar uma sensação de:

- risco
- timing
- controle parcial
- tensão psicológica

O centro da barra favorece mais controle. Os extremos aumentam o risco. Isso torna a rolagem mais interessante do que um clique puro e ajuda a dar identidade própria ao jogo.

---

## Regras da partida

### Objetivo

- alcançar a **casa 54**
- ou sobreviver até restar apenas um jogador vivo

### Fluxo do turno

1. o jogador da vez inicia sua jogada
2. abre o modal de rolagem
3. segura a barra de espaço para carregar a força
4. solta para rolar o dado
5. o peão avança conforme o resultado
6. se cair em uma casa especial, o efeito é aplicado
7. ao fim do ciclo de rodadas, a tempestade pode avançar

### Casas especiais

- **Bomba (`💣`)**: o jogador volta **3 casas**
- **Pergunta (`?`)**:
  - acerto: avança **1 casa**
  - erro: volta **1 casa**

### Tempestade

- começa a pressionar a partida a partir das rodadas seguintes
- possui rolagem própria
- destrói casas a partir do início do tabuleiro
- elimina jogadores que entrem ou permaneçam em casas já consumidas

---

## Categorias de perguntas

O jogo atualmente trabalha com categorias temáticas para aumentar a variedade entre partidas.

Categorias disponíveis:

- Tecnologia
- Sobre o Brasil
- Filmes
- Músicas
- Inglês
- K-pop

---

## Áudio e feedback

O projeto usa áudio como parte funcional da experiência, não apenas como decoração. Cada som ajuda o jogador a entender o estado da partida.

### Principais eventos sonoros

- `loading.mp3`: carregamento da barra de força
- `dice_roll.wav`: rolagem do dado após soltar a barra de espaço
- `token_move.wav`: movimentação do peão
- `bomb_explosion.wav`: queda em bomba
- `correct_answer.wav`: resposta correta
- `wrong_answer.wav`: resposta incorreta
- `storm_advance.wav`: avanço da tempestade
- `storm_hit.wav`: impacto da tempestade
- `win_fanfare.wav`: vitória
- `player_eliminated.wav`: eliminação
- `modal_open.wav`: abertura do modal inicial
- `modal_action.wav`: abertura de modal de suspense
- `button_click.wav`: ações de botão

---

## Detalhes do desenvolvimento

Este projeto foi construído como um jogo web completo, com foco claro em **game feel**, legibilidade e progressão da tensão.

### Decisões de desenvolvimento relevantes

#### 1. Phaser 3 como núcleo da experiência
O Phaser foi escolhido por permitir um controle direto sobre:

- cena principal
- desenho do tabuleiro
- movimentação dos peões
- tweens e animações
- modais desenhados no próprio canvas
- sincronização entre lógica e feedback visual

#### 2. Estrutura de jogo orientada ao loop de turno
A partida foi pensada em cima de um fluxo claro:

- preparar turno
- rolar dado
- mover jogador
- aplicar efeito da casa
- verificar eliminação
- avançar tempestade
- passar o turno

Esse encadeamento deixa a experiência previsível do ponto de vista técnico, mas tensa do ponto de vista do jogador.

#### 3. Feedback visual como parte da regra
Os modais, as reações, as cores das casas, a barra de força, os avisos de tempestade e os estados do botão lateral não existem só para “embelezar”. Eles ajudam o jogador a interpretar risco, contexto e consequência.

#### 4. Mecânica de suspense intencional
O jogo foi sendo refinado para sair do padrão “clique e descubra” e entrar em uma lógica mais dramática:

- rolagem com timing
- modais de reação
- ameaça constante da tempestade
- casas especiais com leitura imediata
- ritmo de eliminação progressiva

#### 5. Protótipo evoluído de forma iterativa
O projeto não nasceu como arquitetura refinada. Ele foi amadurecendo por camadas:

- primeiro a base do tabuleiro
- depois o fluxo de turnos
- depois casas especiais
- depois perguntas
- depois tempestade
- depois áudio
- depois UX dos modais
- depois a mecânica de força no dado

Essa evolução é importante porque mostra um processo real de desenvolvimento: **primeiro validar o jogo, depois refinar a estrutura**.

---

## Sobre o desenvolvedor

**Alessandro** conduz o projeto com uma abordagem que combina produto, engenharia e senso de experiência do usuário.

Este jogo evidencia algumas competências fortes do desenvolvimento:

- capacidade de transformar uma ideia simples em um loop jogável completo
- refinamento incremental com foco em experiência real
- atenção a feedback visual e sonoro
- leitura de mecânica, ritmo e tensão
- autonomia para prototipar, testar e evoluir
- senso de produto ao pensar não só no código, mas no comportamento do jogador

Não é apenas um experimento técnico. É um projeto que mostra iniciativa de construção, domínio prático e intenção clara de evolução.

---

## Configurações atuais

- tamanho base do jogo: `1500 x 1000`
- jogadores: mínimo `2`, máximo `4`
- total de casas: `54`
- bombas: `10, 19, 28, 36, 46, 50`
- perguntas: `4, 8, 14, 17, 24, 26, 31, 34, 39, 44, 48, 52`

---

## Estrutura atual do projeto

```bash
.
├── README.md
├── index.html
├── css/
│   └── style.css
├── source/
│   ├── questions.js
│   └── og-image.png
└── audio/
```

### Situação atual da arquitetura

Hoje o projeto já entrega valor jogável, mas ainda está concentrado demais em poucos arquivos, especialmente na lógica principal.

Atualmente, o núcleo reúne no mesmo fluxo:

- cena principal do Phaser
- regras do jogo
- criação de modais
- desenho do tabuleiro
- movimentação
- controle de turnos
- tempestade
- áudio
- interface lateral

Isso é aceitável para protótipo validado, mas é fraco para escalar.

---

## Como executar

### Opção 1 — Abrir diretamente
Abra o arquivo `index.html` no navegador.

### Opção 2 — Servidor local
Use um servidor local, como o **Live Server** do VS Code:

1. abra a pasta do projeto no VS Code
2. instale a extensão **Live Server**
3. clique com o botão direito em `index.html`
4. selecione **Open with Live Server**

---

## Estado atual da implementação

### Pontos fortes

- jogo local completo e jogável
- loop principal consistente
- identidade visual já definida
- boa base de feedback visual e sonoro
- mecânica de dado mais interessante que o padrão simples
- suporte a múltiplos jogadores locais
- base forte para evolução em produto maior

### Limitações atuais

- parte relevante da lógica ainda está centralizada demais
- ausência de testes automatizados
- ausência de persistência de partida
- sem multiplayer online
- regras e interface ainda muito acopladas
- escalabilidade estrutural limitada se o projeto crescer sem refatoração

---

## Roadmap de evolução

## Fase 1 — Organizar a arquitetura sem quebrar o jogo

Objetivo: separar responsabilidades e reduzir o acoplamento.

### Próximos passos

- extrair a cena principal para `src/scenes/GameScene.js`
- mover configuração do tabuleiro para `src/config/boardConfig.js`
- mover configuração de casas especiais para `src/config/specialHouses.js`
- isolar regras de movimento em `src/core/movement.js`
- isolar regras de turno em `src/core/turnManager.js`
- isolar regras da tempestade em `src/core/stormEngine.js`
- isolar perguntas em `src/data/questions.js`
- criar utilitário de áudio em `src/services/audioService.js`
- separar modais em componentes/fábricas dedicadas
- criar constantes para cores, tamanhos, tempos e textos

### Estrutura alvo sugerida

```bash
.
├── index.html
├── README.md
├── css/
│   └── style.css
├── audio/
├── source/
│   └── og-image.png
└── src/
    ├── main.js
    ├── scenes/
    │   ├── BootScene.js
    │   └── GameScene.js
    ├── config/
    │   ├── boardConfig.js
    │   ├── gameConfig.js
    │   └── specialHouses.js
    ├── core/
    │   ├── movement.js
    │   ├── turnManager.js
    │   ├── diceEngine.js
    │   └── stormEngine.js
    ├── data/
    │   └── questions.js
    ├── services/
    │   └── audioService.js
    ├── ui/
    │   ├── sidebar.js
    │   ├── boardRenderer.js
    │   └── modals/
    │       ├── setupModal.js
    │       ├── diceModal.js
    │       ├── suspenseModal.js
    │       ├── questionModal.js
    │       └── endModal.js
    └── utils/
        ├── random.js
        └── helpers.js
```

---

## Fase 2 — Qualidade e manutenção

Objetivo: tornar o projeto menos frágil.

### Próximos passos

- adicionar testes unitários para regras críticas
- validar movimento, bombas, perguntas e tempestade
- criar camada de estado de jogo mais previsível
- padronizar nomes, eventos e constantes
- melhorar responsividade para resoluções diferentes
- revisar acessibilidade básica de textos e contraste

---

## Fase 3 — Multiplayer online entre computadores diferentes

Objetivo: permitir que um jogador enfrente outro pela internet, cada um em sua própria máquina.

### Caminho recomendado

A forma mais sólida não é improvisar sincronização dentro do mesmo arquivo. O caminho correto é separar cliente e servidor.

### Arquitetura sugerida

#### Front-end
- Phaser 3 para renderização e UX
- cliente responsável apenas por:
  - renderizar estado
  - capturar ações do jogador
  - enviar comandos ao servidor
  - receber atualizações da partida

#### Back-end
- Node.js com WebSocket usando `Socket.IO` ou `ws`
- servidor autoritativo responsável por:
  - criar salas
  - controlar ordem dos turnos
  - validar jogadas
  - resolver dado e eventos
  - impedir fraude
  - sincronizar estado entre os clientes

#### Regras de rede
- cada jogador entra em uma sala
- o servidor decide quem joga
- o cliente envia ações como:
  - `join_room`
  - `ready`
  - `start_charge`
  - `release_dice`
  - `answer_question`
- o servidor responde com eventos como:
  - `room_updated`
  - `turn_started`
  - `dice_resolved`
  - `player_moved`
  - `question_opened`
  - `storm_advanced`
  - `player_eliminated`
  - `game_over`

### Etapas práticas

1. separar o estado do jogo da renderização
2. transformar jogadas em comandos
3. criar modelo de sala no servidor
4. sincronizar estado completo por evento
5. adicionar tela de lobby
6. permitir criação e entrada por código de sala
7. travar regras no servidor
8. adicionar reconexão
9. testar latência e consistência

### MVP do multiplayer

O MVP online deve ser enxuto:

- partida para 2 jogadores
- criação de sala
- entrada por código
- sincronização de turno
- dado resolvido pelo servidor
- perguntas sincronizadas
- tempestade sincronizada
- tela de vitória e derrota

Sem chat, sem ranking e sem conta no primeiro momento.

---

## Melhorias futuras além do multiplayer

- modo solo contra bot
- matchmaking online
- ranking
- estatísticas por jogador
- temas visuais
- novas categorias
- efeitos especiais mais sofisticados
- salvamento de progresso
- versão mobile adaptada corretamente

---

## Conclusão

**Fuja da Tempestade** já passou da fase de experimento raso. Hoje ele é um protótipo jogável com identidade, tensão, regras claras e espaço real de evolução.

O próximo salto de qualidade não é só adicionar mais efeito visual. É fazer duas coisas do jeito certo:

1. **refatorar a arquitetura**
2. **transformar o jogo local em experiência online confiável**

Esse projeto já mostra capacidade técnica, senso de produto e potencial de expansão. A base existe. Agora o ganho real vem da organização estrutural e da evolução para multiplayer.
