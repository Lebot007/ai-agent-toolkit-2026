# Raciocinio Logico e Puzzles

## Tipos de Logica

### Logica Proposicional
- AND, OR, NOT, IMPLIES
- Tabelas verdade
- SAT solvers (Z3, MiniSat)

### Logica de Primeira Ordem
- Quantificadores: forall, exists
- Predicados, variaveis
- Provers: Prover9, E

### Logica Modal
- Necessidade, possibilidade
- Conhecimento, crenca

## Puzzles Classicos

### Knights and Knaves
- Cavaleiros sempre dizem verdade
- Patifes sempre mentem
- Deduzir quem e quem

### Einstein Riddle (Zebra Puzzle)
- 5 casas, 5 nacionalidades, 5 bebidas
- Constraints logicos
- Resolve via constraint solving

### River Crossing
- Lobo, cabra, repolho
- Planejamento de estados

### Sudoku
- Constraint satisfaction
- Backtracking + heuristics

## Ferramentas

### Z3 Theorem Prover
- Repo: github.com/Z3Prover/z3
- Microsoft Research
- SMT solver

### Python Constraint
- Biblioteca para CSP
- Domino, N-Queens, Sudoku

### Prolog
- Linguagem logica
- SWI-Prolog
- Ideal para puzzles

## Tecnicas para IAs

### Formalizar antes de resolver
- Traduzir enunciado para logica
- Identificar constraints explicitas
- Identificar implicitas

### Chain-of-Thought estruturado
- Listar premissas
- Aplicar regras de inferencia
- Derivar conclusoes passo a passo