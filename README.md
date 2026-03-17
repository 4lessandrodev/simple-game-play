# Fuja da Tempestade

Jogo de tabuleiro local feito com **Phaser 3**, **HTML**, **CSS** e **JavaScript**. A partida suporta de **2 a 4 jogadores** e combina avanço por dado, casas especiais, perguntas de múltipla escolha e uma tempestade que elimina jogadores ao longo do jogo.

## Visão geral

- tabuleiro com **54 casas**
- suporte para **2, 3 ou 4 jogadores**
- modal inicial para configurar jogadores e categoria de perguntas
- dado com animação em modal próprio
- casas especiais de **bomba** e **pergunta**
- tempestade progressiva com eliminação
- efeitos sonoros para ações importantes
- modal final com reinício da partida

## Regras da partida

O objetivo é chegar primeiro à **casa 54** ou ser o último jogador sobrevivente.

### Fluxo do turno

1. o jogador da vez abre o modal de dado
2. o som do dado toca apenas ao clicar no botão de rolagem do modal
3. o peão avança conforme o valor sorteado
4. se cair em uma casa especial, o efeito correspondente é aplicado
5. após as rodadas, a tempestade pode avançar e destruir casas

### Casas especiais

- **Bomba (`💣`)**: o jogador volta **3 casas**
- **Pergunta (`?`)**: abre um modal com respostas
- acerto: avança **1 casa**
- erro: volta **1 casa**

### Tempestade

- começa a agir a partir da **segunda rodada**
- avança por rolagem própria
- destrói casas a partir do início do tabuleiro
- elimina jogadores que entrarem ou permanecerem em casas destruídas

## Áudio atual

Os áudios são carregados da pasta [`audio/`](/Users/4lessandrodev/Workspace/Projetos/Game/simple-game-play/audio) em arquivos `.wav`.

Principais eventos sonoros já usados no jogo:

- `dice_roll.wav`: rolagem do dado no clique do botão do modal
- `token_move.wav`: movimentação do peão
- `bomb_explosion.wav`: queda em bomba
- `correct_answer.wav`: resposta correta
- `wrong_answer.wav`: resposta incorreta
- `storm_advance.wav`: avanço da tempestade
- `storm_hit.wav`: impacto da tempestade
- `win_fanfare.wav`: vitória
- `player_eliminated.wav`: eliminação
- `modal_open.wav`: abertura do modal inicial
- `modal_action.wav`: abertura do modal de ação relacionado à casa
- `button_click.wav`: ações de botão

Observação: a função de reprodução valida os áudios pelo cache do Phaser antes de tocar o som.

## Modais

O jogo usa modais para organizar a experiência:

- modal inicial de configuração
- modal de rolagem do dado
- modal de ação ao cair em casa especial ou evento relevante
- modal de perguntas e respostas
- modal de fim de jogo

O modal de perguntas teve a largura das opções aumentada para melhorar textos longos.

## Configurações atuais

- tamanho do jogo: `1500 x 1000`
- jogadores: mínimo `2`, máximo `4`
- total de casas: `54`
- bombas: `10, 19, 28, 36, 46, 50`
- perguntas: `4, 8, 14, 17, 24, 26, 31, 34, 39, 44, 48, 52`

Categorias disponíveis:

- Tecnologia
- Sobre o Brasil
- Filmes
- Músicas
- Inglês
- K-pop

## Estrutura do projeto

```bash
.
├── README.md
├── index.html
└── audio/
```

Hoje a lógica do jogo está concentrada em [`index.html`](/Users/4lessandrodev/Workspace/Projetos/Game/simple-game-play/index.html), incluindo:

- estrutura HTML
- estilos CSS
- cena principal do Phaser
- regras do jogo
- modais
- animações
- carregamento e reprodução de áudio

## Como executar

### Opção 1

Abra [`index.html`](/Users/4lessandrodev/Workspace/Projetos/Game/simple-game-play/index.html) diretamente no navegador.

### Opção 2

Execute com um servidor local, como o **Live Server** do VS Code:

1. abra a pasta do projeto no VS Code
2. instale a extensão **Live Server**
3. clique com o botão direito em [`index.html`](/Users/4lessandrodev/Workspace/Projetos/Game/simple-game-play/index.html)
4. escolha **Open with Live Server**

## Estado atual da implementação

Pontos fortes:

- protótipo jogável e completo
- fluxo de turnos consistente
- boa quantidade de perguntas
- feedback visual e sonoro já integrado
- suporte a múltiplos jogadores locais

Limitações atuais:

- toda a lógica está em um único arquivo
- layout com dimensões fixas
- sem responsividade real para telas menores
- perguntas ainda ficam embutidas no código

## Próximos passos sugeridos

- separar a cena principal em arquivos menores
- mover perguntas e configurações para arquivos externos
- adicionar responsividade
- expandir feedback visual para eventos especiais
- adicionar testes para regras centrais do jogo
