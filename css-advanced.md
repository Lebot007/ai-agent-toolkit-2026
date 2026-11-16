# CSS Avancado - Tecnicas Modernas de CSS

## O que e
Tecnicas avancadas de CSS para layouts complexos e design moderno.

## CSS Grid

### Grid Basico
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto;
  gap: 20px;
}

### Grid Areas
.layout {
  display: grid;
  grid-template-areas:
    'header header header'
    'sidebar main main'
    'footer footer footer';
  grid-template-columns: 250px 1fr 1fr;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }

### Grid Responsivo
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

## Flexbox Avancado

### Centralizar Perfeitamente
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

### Sticky Footer
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1;
}

## Custom Properties (CSS Variables)

### Definir e Usar
:root {
  --primary-color: #3b82f6;
  --secondary-color: #10b981;
  --spacing-unit: 8px;
}

.button {
  background: var(--primary-color);
  padding: calc(var(--spacing-unit) * 2);
}

### Temas Dinamicos
[data-theme='dark'] {
  --bg-color: #1f2937;
  --text-color: #f9fafb;
}

[data-theme='light'] {
  --bg-color: #ffffff;
  --text-color: #111827;
}

## Animations

### Keyframes
@keyframes slideIn {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.element {
  animation: slideIn 0.3s ease-out;
}

### Transitions
.button {
  transition: all 0.2s ease-in-out;
}

.button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}

## Pseudo-classes e Pseudo-elements

### Pseudo-classes
.list-item:nth-child(odd) {
  background: #f3f4f6;
}

.list-item:first-child {
  font-weight: bold;
}

.input:not(:placeholder-shown):valid {
  border-color: green;
}

### Pseudo-elements
.quote::before {
  content: '"';
  font-size: 2em;
  color: #9ca3af;
}

.highlight::selection {
  background: yellow;
}

## Modern Selectors

### :has()
.card:has(img) {
  border: 2px solid blue;
}

form:has(input:invalid) {
  border-color: red;
}

### :is() e :where()
:is(h1, h2, h3) {
  color: #1f2937;
}

:where(.container, .wrapper) {
  max-width: 1200px;
}

## Container Queries

### Query por Container
.card-container {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card {
    display: flex;
    flex-direction: row;
  }
}

## Scroll-Driven Animations

### Scroll Progress
.progress-bar {
  animation: grow linear;
  animation-timeline: scroll();
}

@keyframes grow {
  from { width: 0%; }
  to { width: 100%; }
}

## CSS Modules

### Usar com React
// Button.module.css
.button {
  background: blue;
}

// Button.jsx
import styles from './Button.module.css';

function Button() {
  return <button className={styles.button}>Click me</button>;
}

## Styled Components

### React
import styled from 'styled-components';

const Button = styled.button`
  background: ${props => props.primary ? 'blue' : 'white'};
  color: ${props => props.primary ? 'white' : 'blue'};
  padding: 10px 20px;
  border: 2px solid blue;
  border-radius: 4px;
  
  &:hover {
    opacity: 0.8;
  }
`;

function App() {
  return <Button primary>Click me</Button>;
}

## Tailwind CSS

### Classes Utilitarias
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Click me
</button>

### Custom Config
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: '#3b82f6',
        secondary: '#10b981',
      }
    }
  }
}

## Performance

### Otimizacoes
- Usar transform e opacity para animacoes (GPU accelerated)
- Evitar layout thrashing
- Usar will-change com cuidado
- Minificar CSS
- Remover CSS nao usado (PurgeCSS)

### Critical CSS
-- Extrair CSS critico para above-the-fold
-- Inline no HTML
-- Carregar resto assincronamente

## Acessibilidade

### Focus States
.button:focus {
  outline: 2px solid blue;
  outline-offset: 2px;
}

### Reduced Motion
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}

## Best Practices

### Organizacao
- Usar metodologia (BEM, SMACSS, ITCSS)
- Agrupar por componente
- Usar variaveis CSS
- Documentar codigo complexo

### Performance
- Minificar CSS
- Usar CDN
- Lazy load CSS nao critico
- Evitar seletores muito especificos

### Manutencao
- Usar pre-processador (Sass, Less) ou PostCSS
- Componentizar estilos
- Testar em multiplos browsers
- Usar linter (stylelint)

## Quando Usar
- Layouts complexos
- Design systems
- Aplicacoes web modernas
- Sites responsivos