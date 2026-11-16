# Raciocinio Espacial

## Tipos de Raciocinio Espacial

### Mental Rotation
- Rotacionar objetos 3D mentalmente
- Vandenberg & Kuse Mental Rotations Test
- Dificil para LLMs (sem visao)

### Spatial Visualization
- Manipular formas complexas
- Paper folding, cutting

### Spatial Perception
- Orientacao em relacao a si mesmo
- Left/right, up/down

### Navigation
- Wayfinding
- Cognitive maps
- Landmark recognition

## Desafios para LLMs

### Problemas Comuns
- Tracking de posicoes apos movimentos
- Contar objetos em grids
- Descricoes de layouts
- Direcoes (norte, sul, leste, oeste)

### Exemplo
- Objeto em (2,3) move 2 direita, 1 cima
- LLMs frequentemente erram
- Necessario raciocinio explicito passo-a-passo

## Estrategias

### Coordinate Tracking
- Usar coordenadas (x,y,z)
- Atualizar passo a passo
- Verificar com exemplos simples

### Visualization Tools
- ASCII art para grids
- Descricoes sistematicas
- Enumerar elementos

## Benchmarks

### SpatialQA
- Questoes espaciais
- Objetos em cenas

### NLVR (Natural Language Visual Reasoning)
- Comparar imagens baseado em texto

### VQA (Visual QA)
- Perguntas sobre imagens
- Requer multimodalidade