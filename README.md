# Jogo de Dados com Phaser

Jogo de tabuleiro desenvolvido com **Phaser 3**, com foco em experiência casual local para **2 a 4 jogadores**, combinando progressão por dado, casas especiais, perguntas e uma mecânica de pressão crescente por meio de uma **tempestade progressiva**.

O projeto foi construído em **HTML, CSS e JavaScript**, com renderização via canvas e uso de elementos DOM em modais de configuração.

---

## Sumário

- [Visão geral](#visão-geral)
- [Objetivo do jogo](#objetivo-do-jogo)
- [Principais funcionalidades](#principais-funcionalidades)
- [Regras da partida](#regras-da-partida)
- [Arquitetura atual](#arquitetura-atual)
- [Estrutura do projeto](#estrutura-do-projeto)
- [Como executar](#como-executar)
- [Configurações atuais](#configurações-atuais)
- [Fluxo funcional](#fluxo-funcional)
- [Detalhamento técnico](#detalhamento-técnico)
- [Pontos fortes](#pontos-fortes)
- [Limitações atuais](#limitações-atuais)
- [Roadmap de evolução](#roadmap-de-evolução)
- [Próximos passos recomendados](#próximos-passos-recomendados)
- [Licença](#licença)

---

<img width="1526" height="925" alt="image" src="https://github.com/user-attachments/assets/b88c9c86-7cdd-4003-a116-2c9bba07e64a" />

## Visão geral

Este projeto implementa um jogo de percurso em tabuleiro, no qual os jogadores disputam avanço até a última casa enquanto lidam com riscos e eventos de penalidade e recompensa.

A experiência atual inclui:

- tabuleiro visual com **54 casas**
- suporte para **2, 3 ou 4 jogadores**
- configuração inicial de nomes dos jogadores
- dado animado
- movimentação progressiva dos peões
- casas especiais de **bomba** e **pergunta**
- sistema de **tempestade destrutiva** com eliminação
- modal de encerramento com vencedor
- reinício rápido da partida

O jogo já está funcional como protótipo jogável. O principal desafio agora não é "fazer rodar", mas **organizar a base para escalar com qualidade**.

---

## Objetivo do jogo

Ser o primeiro jogador a chegar à **casa 54**, ou sobreviver até o final enquanto os demais forem eliminados pela tempestade.

---

## Principais funcionalidades

### Mecânicas principais
- avanço por rolagem de dado
- turnos alternados entre jogadores ativos
- movimentação animada casa a casa
- condição de vitória por chegada ao final
- condição de vitória por sobrevivência

### Casas especiais
- **Bomba (`💣`)**
  - jogador volta **3 casas**
- **Pergunta (`?`)**
  - acertou: avança **1 casa**
  - errou: volta **1 casa**

### Sistema de eliminação
- jogadores podem ser eliminados quando:
  - entram em casa já destruída pela tempestade
  - terminam turno em casa destruída
  - recuam para casa destruída após bomba
  - avançam/recuam após pergunta para uma casa destruída
  - são alcançados diretamente pela tempestade

### Interface
- sidebar lateral com:
  - jogador da vez
  - mensagens do turno
  - status da tempestade
  - dado
  - legenda dos jogadores
  - botões de ação
- modais para:
  - configuração inicial
  - perguntas
  - fim de jogo

---

## Regras da partida

## Início
Ao abrir o jogo, é exibido um modal de configuração da partida com:

- quantidade de jogadores
- nome de cada jogador ativo

A partida exige no mínimo **2 jogadores** e no máximo **4**.

## Turno
Cada turno segue a sequência:

1. jogador da vez clica em **Jogar dado**
2. o dado é animado
3. o peão avança conforme o número sorteado
4. se cair em casa especial, o efeito é aplicado
5. ao final da rodada, pode haver avanço da tempestade

## Bombas
Casas definidas como bomba penalizam o jogador:

- recuo de **3 casas**

## Perguntas
Casas definidas como pergunta abrem um modal com múltipla escolha:

- resposta correta: **+1 casa**
- resposta errada: **-1 casa**

## Tempestade
A tempestade entra em ação a partir da **segunda rodada completa**.

Funcionamento:
- ao fim de cada rodada completa, a tempestade também "rola" um dado
- ela destrói casas progressivamente a partir do início
- qualquer jogador alcançado por ela é eliminado

## Encerramento
O jogo termina quando:
- um jogador alcança a casa final; ou
- resta apenas um jogador vivo; ou
- todos os jogadores são eliminados

---

## Arquitetura atual

A implementação atual é centralizada em uma única cena do Phaser:

```js
class DiceGameScene extends Phaser.Scene
````

Essa cena concentra responsabilidades de:

* layout
* renderização do tabuleiro
* controle de turnos
* regras do jogo
* animações
* controle de estado
* modais
* fluxo de vitória/eliminação

---

## Estrutura do projeto

Estrutura atual:

```bash
.
└── index.html
```

Hoje o projeto está inteiramente em um único arquivo contendo:

* HTML
* CSS
* lógica de jogo
* configuração do Phaser

### Próxima etapa

```bash
.
├── index.html
├── assets/
│   ├── audio/
│   │   ├── dice-roll.mp3
│   │   ├── bomb.mp3
│   │   ├── correct.mp3
│   │   ├── wrong.mp3
│   │   ├── storm.mp3
│   │   └── victory.mp3
│   ├── images/
│   │   ├── board/
│   │   └── ui/
│   └── fonts/
├── src/
│   ├── main.js
│   ├── config/
│   │   └── gameConfig.js
│   ├── scenes/
│   │   ├── BootScene.js
│   │   ├── MenuScene.js
│   │   └── DiceGameScene.js
│   ├── core/
│   │   ├── board.js
│   │   ├── player.js
│   │   ├── storm.js
│   │   ├── questions.js
│   │   └── rules.js
│   ├── ui/
│   │   ├── sidebar.js
│   │   ├── modals.js
│   │   └── buttons.js
│   └── utils/
│       ├── animations.js
│       ├── audio.js
│       └── responsive.js
└── README.md
```

---

## Como executar

## Opção 1: abrir diretamente no navegador

Salve o código em um arquivo chamado:

```bash
index.html
```

Depois, abra no navegador.

## Opção 2: servidor local

Mais indicado para evolução do projeto.

Exemplo com VS Code + Live Server:

1. abra a pasta no VS Code
2. instale a extensão **Live Server**
3. clique com o botão direito em `index.html`
4. escolha **Open with Live Server**

---

## Configurações atuais

### Dimensões do jogo

* largura: `1500`
* altura: `1000`

### Quantidade de jogadores

* mínimo: `2`
* máximo: `4`

### Total de casas

* `54`

### Casas de bomba

```js
[10, 19, 28, 36, 46, 50]
```

### Casas de pergunta

```js
[4, 8, 14, 17, 24, 26, 31, 39, 44, 48, 52, 34]
```

### Banco atual de perguntas

* perguntas fixas em memória
* múltipla escolha
* uma resposta correta por pergunta

---

## Fluxo funcional

## Inicialização

Na criação da cena, o jogo:

* define dimensões
* cria layout
* cria sidebar
* desenha o tabuleiro
* cria jogadores
* cria botões
* abre modal de configuração

## Durante a partida

A cada turno:

* valida se o jogo pode receber interação
* anima o dado
* move o jogador
* aplica regras especiais
* verifica vitória
* verifica tempestade
* alterna o jogador

## Fim de partida

Quando a condição de encerramento é atingida:

* o botão de rolagem é desabilitado
* o vencedor é destacado
* o modal final é exibido
* o usuário pode reiniciar a partida

---

## Detalhamento técnico

## Principais métodos

### Inicialização e renderização

* `create()`
* `drawLayout()`
* `createSidebar()`
* `drawBoard()`
* `createPlayers()`
* `createButtons()`

### Controle de turno

* `startTurn()`
* `advanceToNextAlivePlayer()`
* `updateHeaderNames()`

### Dado e movimentação

* `animateDiceRoll()`
* `rollStormDice()`
* `movePlayerStepByStep()`
* `moveTokenToPosition()`

### Regras especiais

* `handleBomb()`
* `handleQuestionHouse()`
* `advanceStormBy()`
* `handleStormDefeat()`
* `handleVictory()`

### Utilitários visuais

* `flashSpecialHouse()`
* `flashStormWarning()`
* `shakeToken()`

### Modais

* `showPlayerSetupModal()`
* `showQuestionModal()`
* `showEndModal()`

## Controle de estado

O jogo utiliza flags para impedir inconsistências de interação:

* `gameOver`
* `isAnimating`
* `isQuestionOpen`
* `isPlayerSetupOpen`
* `isEndModalOpen`

Isso evita:

* múltiplos cliques durante animações
* turno disparado com modal aberto
* rolagens indevidas após fim do jogo

Essa decisão é correta. Não resolve tudo, mas já cria uma base mínima de integridade de estado.

---

## Pontos fortes

* protótipo jogável e completo
* mecânicas fáceis de entender
* fluxo de partida consistente
* visual organizado
* suporte real para múltiplos jogadores
* tempestade adiciona tensão progressiva
* modais deixam a experiência mais guiada

---

## Limitações atuais

## Limitações de arquitetura

* toda lógica está concentrada em uma única cena
* forte acoplamento entre interface e regra
* baixa escalabilidade para novas features

## Limitações de interface

* layout fixo para resolução específica
* ausência de responsividade real
* experiência limitada em telas menores

## Limitações de experiência

* sem efeitos sonoros
* sem trilha sonora
* animações ainda simples
* feedback audiovisual pouco expressivo

## Limitações de conteúdo

* perguntas fixas no código
* ausência de categorias
* ausência de modo campanha, ranking ou progressão

---


## Próximos

## 1. Tornar o jogo responsivo

Hoje o projeto está preso a dimensões fixas (`1500x1000`). Isso é funcional em desktop grande, mas tecnicamente limitado.

### Passos

* substituir valores fixos por dimensões calculadas com base no `window.innerWidth` e `window.innerHeight`
* usar escala proporcional para:

  * largura da sidebar
  * tamanho das casas
  * espaçamento do tabuleiro
  * tamanho dos textos
  * tamanho dos peões
    
* definir breakpoints:

  * desktop grande
  * desktop médio
  * tablet
  * mobile landscape
    
* reorganizar layout em telas menores:

  * tabuleiro acima
  * sidebar abaixo
    
* limitar largura máxima do jogo e permitir centralização com scaling

---

## 2. Adicionar efeitos sonoros

Hoje o jogo funciona visualmente, mas falta resposta sensorial.

### Sons prioritários

* rolagem do dado
* explosão da bomba
* acerto de pergunta
* erro de pergunta
* avanço da tempestade
* vitória

---

## 3. Melhorar a animação

As atuais são básicas

### Melhorias prioritárias

* tornar a rolagem do dado mais convincente

  * rotação
  * escala
  * easing mais forte
    
* ao cair em bomba:

  * flash vermelho
  * vibração mais intensa
  * pequena explosão/partículas
    
* ao acertar pergunta:

  * brilho verde
  * avanço com impulso
    
* ao errar:

  * feedback vermelho e recuo com leve bounce
    
* na tempestade:

  * overlay escuro progressivo
  * tremor sutil nas casas destruídas
  * efeito sonoro sincronizado
    
* no fim do jogo:

  * destaque no vencedor
  * transição de entrada do modal final

---

## 5. Preparar o projeto para assets externos

Hoje quase tudo está embutido no código.

### Próximo passo correto

* mover perguntas para JSON
* mover sons para pasta `assets/audio`
* mover imagens/ícones para `assets/images`
* criar etapa de preload

---

## Licença

* **MIT**

```txt
MIT License
```

---

## Autor

Desenvolvido por **Alessandro**.
