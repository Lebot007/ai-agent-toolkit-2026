# AI em Xadrez e Go

## Xadrez

### Motores Classicos
- Stockfish: stockfishchess.org (open-source, top)
- Komodo
- Leela Chess Zero (LCZero): neural network

### Deep Blue (1997)
- IBM vs Kasparov
- 200 milhoes posicoes/segundo
- Minimax + alpha-beta pruning
- Evaluation functions hand-crafted

### AlphaZero (2017)
- DeepMind
- Self-play reinforcement learning
- Derrotou Stockfish em 4 horas
- Monte Carlo Tree Search + neural net

## Go

### Desafios
- 10^170 posicoes legais (vs 10^47 xadrez)
- Dificil avaliar posicoes
- Intuicao mais importante

### AlphaGo (2016)
- Derrotou Lee Sedol 4-1
- Treinado em jogos humanos + self-play
- Policy network + value network + MCTS

### AlphaGo Zero (2017)
- Apenas self-play, sem dados humanos
- Derrotou AlphaGo 100-0
- 3 dias de treino

### AlphaZero (2017)
- Um unico algoritmo para Go, xadrez, shogi
- Generaliza entre jogos

## MuZero (2019)

- Nao precisa regras do jogo
- Aprende modelo do ambiente
- Dominou Go, xadrez, shogi, Atari
- Repo: github.com/deepmind/muzero (papers)

## LLMs e Jogos

### Desafios
- LLMs nao sao bons em jogos deterministicos
- Nao tem state tracking robusto
- Nao aprendem de experiencia

### Possibilidades
- Analisar partidas (comentarios)
- Explicar estrategias
- Gerar problemas taticos
- Ensinar aberturas

## Recursos
- chessprogramming.org
- lichess.org (open-source, analise)
- kaggle.com/competitions (Go, chess)