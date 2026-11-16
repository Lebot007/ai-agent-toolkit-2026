# Frontend Canvas - HTML5 Canvas e Graficos

## O que e
API JavaScript para desenhar graficos 2D e 3D no browser.

## Canvas 2D

### Setup Basico
<canvas id="myCanvas" width="500" height="500"></canvas>

<script>
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');
</script>

### Formas Basicas
// Retangulo
ctx.fillStyle = '#ff0000';
ctx.fillRect(10, 10, 100, 50);

// Retangulo com borda
ctx.strokeStyle = '#000000';
ctx.lineWidth = 2;
ctx.strokeRect(10, 10, 100, 50);

// Circulo
ctx.beginPath();
ctx.arc(150, 75, 50, 0, 2 * Math.PI);
ctx.fillStyle = '#00ff00';
ctx.fill();

// Linha
ctx.beginPath();
ctx.moveTo(0, 0);
ctx.lineTo(200, 100);
ctx.strokeStyle = '#0000ff';
ctx.stroke();

### Texto
ctx.font = '30px Arial';
ctx.fillStyle = '#000000';
ctx.fillText('Hello Canvas', 10, 50);

// Texto com borda
ctx.strokeStyle = '#ff0000';
ctx.strokeText('Hello Canvas', 10, 100);

### Gradientes
// Linear
const gradient = ctx.createLinearGradient(0, 0, 200, 0);
gradient.addColorStop(0, 'red');
gradient.addColorStop(1, 'blue');
ctx.fillStyle = gradient;
ctx.fillRect(10, 10, 150, 80);

// Radial
const radialGradient = ctx.createRadialGradient(75, 50, 5, 90, 60, 100);
radialGradient.addColorStop(0, 'red');
radialGradient.addColorStop(1, 'white');
ctx.fillStyle = radialGradient;
ctx.fillRect(10, 10, 150, 80);

### Imagens
const img = new Image();
img.src = 'image.jpg';
img.onload = function() {
    ctx.drawImage(img, 0, 0);
    
    // Com dimensoes
    ctx.drawImage(img, 10, 10, 150, 180);
    
    // Crop
    ctx.drawImage(img, 50, 50, 100, 100, 10, 10, 100, 100);
};

## Animacoes

### requestAnimationFrame
let x = 0;

function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    
    // Desenhar
    ctx.fillStyle = '#ff0000';
    ctx.fillRect(x, 100, 50, 50);
    
    // Atualizar
    x += 2;
    if (x > canvas.width) x = 0;
    
    requestAnimationFrame(animate);
}

animate();

### Loop com Delta Time
let lastTime = 0;

function animate(currentTime) {
    const deltaTime = currentTime - lastTime;
    lastTime = currentTime;
    
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    
    // Atualizar com delta time
    x += speed * (deltaTime / 1000);
    
    // Desenhar
    ctx.fillRect(x, 100, 50, 50);
    
    requestAnimationFrame(animate);
}

requestAnimationFrame(animate);

## Transformacoes

### Translate
ctx.save();
ctx.translate(100, 100);
ctx.fillRect(0, 0, 50, 50);
ctx.restore();

### Rotate
ctx.save();
ctx.translate(100, 100);
ctx.rotate(Math.PI / 4);  // 45 graus
ctx.fillRect(-25, -25, 50, 50);
ctx.restore();

### Scale
ctx.save();
ctx.scale(2, 2);
ctx.fillRect(10, 10, 50, 50);
ctx.restore();

## Interatividade

### Eventos de Mouse
canvas.addEventListener('mousemove', function(e) {
    const rect = canvas.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    
    // Verificar se mouse esta sobre elemento
    if (x > 50 && x < 150 && y > 50 && y < 150) {
        console.log('Mouse sobre elemento');
    }
});

canvas.addEventListener('click', function(e) {
    const rect = canvas.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    
    console.log('Click em:', x, y);
});

## WebGL (3D)

### Setup
<canvas id="glCanvas" width="500" height="500"></canvas>

<script>
const canvas = document.getElementById('glCanvas');
const gl = canvas.getContext('webgl') || canvas.getContext('experimental-webgl');

if (!gl) {
    alert('WebGL nao suportado');
}
</script>

### Bibliotecas WebGL
- Three.js: threejs.org
- Babylon.js: babylonjs.com
- PixiJS: pixijs.com
- Phaser: phaser.io

## Bibliotecas Canvas

### Chart.js
// Graficos
const chart = new Chart(ctx, {
    type: 'bar',
    data: {
        labels: ['Red', 'Blue', 'Yellow'],
        datasets: [{
            label: 'Votes',
            data: [12, 19, 3],
            backgroundColor: ['red', 'blue', 'yellow']
        }]
    }
});

### p5.js
function setup() {
    createCanvas(400, 400);
}

function draw() {
    background(220);
    ellipse(50, 50, 80, 80);
}

### Fabric.js
// Objetos interativos
const canvas = new fabric.Canvas('c');

const rect = new fabric.Rect({
    left: 100,
    top: 100,
    fill: 'red',
    width: 20,
    height: 20
});

canvas.add(rect);

## Performance

### Otimizacoes
// Offscreen canvas
const offscreen = new OffscreenCanvas(500, 500);
const offCtx = offscreen.getContext('2d');

// Desenhar offscreen
offCtx.fillRect(0, 0, 500, 500);

// Copiar para canvas principal
ctx.drawImage(offscreen, 0, 0);

### Best Practices
- Usar requestAnimationFrame (nao setInterval)
- Limpar canvas antes de redesenhar
- Minimizar operacoes de estado
- Batch drawing operations
- Usar offscreen canvas para trabalho pesado

## Casos de Uso
- Jogos 2D
- Visualizacoes de dados
- Editores de imagem
- Animacoes
- Efeitos visuais
- Simulacoes

## Quando Usar
- Graficos customizados
- Animacoes complexas
- Jogos
- Visualizacoes interativas
- Quando bibliotecas nao sao suficientes
