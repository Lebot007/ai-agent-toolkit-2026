# Raciocinio Dedutivo

## Definicao

- Premissas garantem conclusao
- Se premissas verdadeiras, conclusao necessariamente verdadeira
- Logica formal

## Formas Validas

### Modus Ponens
- Se P entao Q
- P
- Logo Q

### Modus Tollens
- Se P entao Q
- Nao Q
- Logo nao P

### Silogismo Hipotetico
- Se P entao Q
- Se Q entao R
- Logo se P entao R

### Silogismo Disjuntivo
- P ou Q
- Nao P
- Logo Q

## Sistemas Formais

### Logica Proposicional
- Atomos: P, Q, R
- Conectivos: AND, OR, NOT, IMPLIES, IFF
- Tabelas verdade

### Logica de Primeira Ordem
- Predicados: P(x), R(x,y)
- Quantificadores: forall, exists
- Mais expressiva

### Logica de Segunda Ordem
- Quantificar sobre predicados
- Mais poderosa, menos decidivel

## Ferramentas

### SAT Solvers
- Z3: github.com/Z3Prover/z3
- MiniSat: minisat.se
- Glucose

### Theorem Provers
- Coq: coq.inria.fr
- Lean: leanprover.org
- Isabelle: isabelle.in.tum.de

## Benchmarks
- LogiQA: 8k questoes
- ReClor: LSAT logical reasoning
- FOLIO: first-order logic
- ProofWriter: rule-based proofs