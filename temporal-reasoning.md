# Raciocinio Temporal

## Conceitos

### Temporal Logic
- Linear Temporal Logic (LTL)
- Computational Tree Logic (CTL)
- Operadores: always, eventually, until, next

### Allen's Interval Algebra
- 13 relacoes entre intervalos
- before, meets, overlaps, during, starts, finishes
- E suas inversas

### Temporal Constraints
- A antes de B
- A e B simultaneos
- A dura X unidades

## Desafios para LLMs

### Problemas Tipicos
- Ordering events from narrative
- Duration calculations
- Time zone conversions
- Relative time (ontem, amanha, semana passada)

### Exemplo
- Joao chegou antes de Maria
- Maria saiu quando Pedro chegou
- Quem esteve la ao mesmo tempo?

## Estrategias

### Timeline Construction
- Listar eventos
- Ordenar cronologicamente
- Marcar sobreposicoes

### ISO 8601
- Formato padrao para datas
- YYYY-MM-DDThh:mm:ssZ
- Facilita calculos

### Ferramentas
- Python: datetime, dateutil
- JavaScript: date-fns, moment
- LLMs: chamar funcoes de data

## Benchmarks
- TRACIE: temporal reasoning
- TimeDial: temporal commonsense
- MATRES: multi-axis temporal