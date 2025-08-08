# Unidad 2


## 🛠 Fase: Apply

## 1. Describe el concepto de tu obra generativa.
La idea es hacer una especie de "pecera" en la que se vean las figuritas que van a ser como circulos, la idea es que el movimiento esté influenciado por aceleraciones generadas por medio de un algoritmo de ruido perlin combinado con salto levy para que se vea un movimiento mas suavizado y "natural". ya con lo de salto levy quiero que sea un movimiento no tan predecible pero tampoco caótico. Quiero que en vez de ser la aceleracion hacia el mouse, quiero que las particulas/peces se "asusten" y su aceleracion sea en dirección contraria al mouse.

## 2. ¿Cómo piensas aplicar el marco MOTION 101 y por qué?
La idea es que cada partícula/pez tenga una posicion, velocidad y aceleracion diferente y que la aceleracion se va a calcular usando la combinacion entre ruido perlin (pa suavizar) y saltos levy (para cambios bruscos ocasionales). La idea tambien es que se la velocidad se limite para evitar que las particulas se descontrolen y se sienta mas orgánico.
Adicional a esto, quiero implementar una especie de aceleracion hacia el mouse pero diferente, que en vez de ser en direccion al mouse, sea en la dirección contraria.

## 3. ¿Qué algoritmo de aceleración vas a utilizar? ¿Por qué?
voy a usar dos algoritmos, base de ruido perlin para gener un movimiento suave y continuo y tambien voy a usar perturbaciones tipo levy para meter saltos largos ocasionales y que se rompa la monotonía de lo del movimiento. Voy a usar estas dos para hacer que el movimiento se sienta natural y también para repasar un poquito lo que habíamos visto en la unidad pasada.

## 4. ¿Cómo será interactivo?
Si el mouse se mueve, las particulas se alejan de la posicion en la que esté, sintiendo una especie de "repulsion" y tambien alterando su aceleración.
También quiero hacer interacción por medio de teclas, alterando el tamaño de los peces, la idea es que al presionar g, se hagan mas grandes y al presionar p se hagan mas pequeñas.

## 5. El código de la aplicación.

``` js
let particles = [];
let noiseScale = 0.005;
let levyFactor = 0.2;

function setup() 
{
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100); 
  for (let i = 0; i < 150; i++) 
  {
    particles.push(new Particle());
  }
}

function draw() 
{
  background(240, 10, 10, 10);
  for (let p of particles) 
  {
    p.update();
    p.show();
  }
}

class Particle 
{
  constructor() 
  {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.maxSpeed = 3;
    this.size = 10;

    this.xOff = random(1000);
    this.yOff = random(1000);

    // Colores: actual y objetivo
    this.color = color(random(360), 80, 100, 100); 
    this.targetColor = color(random(360), 80, 100, 100);
    this.colorLerpAmt = 0;
  }

  update() 
  {
    // Movimiento con ruido Perlin
    let angle = noise(this.xOff, this.yOff) * TWO_PI * 2;
    let perlinForce = p5.Vector.fromAngle(angle);
    perlinForce.setMag(0.1);
    this.xOff += noiseScale;
    this.yOff += noiseScale;

    // Salto Lévy
    if (random(1) < 0.005) 
    {
      let jump = p5.Vector.random2D().mult(random(20, 60) * levyFactor);
      this.acc.add(jump);
    }

      // "Repulsión" del mouse 
    let mouse = createVector(mouseX, mouseY);
    let d = this.pos.dist(mouse);
    if (d < 150) 
    {
      let repulsion = p5.Vector.sub(this.pos, mouse); 
      repulsion.setMag(map(d, 0, 150, 0.5, 0.05)); 
      this.acc.add(repulsion);
    }

    // Movimiento Motion 101
    this.acc.add(perlinForce);
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.edges();

    // Interpolación de color
    this.color = lerpColor(this.color, this.targetColor, 0.01);
    this.colorLerpAmt += 0.01;
    if (this.colorLerpAmt >= 1) 
    {
      this.targetColor = color(random(360), 80, 100, 100);
      this.colorLerpAmt = 0;
    }
  }

  edges() 
  {
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }

  show() 
  {
    noStroke();
    fill(this.color);
    ellipse(this.pos.x, this.pos.y, this.size);
  }

  changeSize(delta) {
    this.size = constrain(this.size + delta, 1, 20);
  }
}

function keyPressed() 
{
  if (key === 'G') {
    for (let p of particles) 
    {
      p.changeSize(1);
    }
  }
  if (key === 'P') 
  {
    for (let p of particles) 
    {
      p.changeSize(-1);
    }
  }
}

```

## 6. Un enlace al proyecto en el editor de p5.js.

https://editor.p5js.org/isams2004.1/sketches/zcNAGCuEw

## 7. Una captura de pantalla representativa de tu pieza de arte generativo.

<img width="1854" height="883" alt="image" src="https://github.com/user-attachments/assets/1b297001-8dd9-43dc-869c-d9ae58a3c694" />



