# Unidad 3


## 🛠 Fase: Apply

## Diseña e implementa tu obra generativa interactiva en tiempo real.

Mi obra se basa en un sistema de n cuerpos gravitacionales que se atraten entre ellos, cada cuerpo tiene una masa, velocidad y aceleración indpendientes, todas interactuan entre ellas por fuerza de atraccion.

Hablando de la parte interativa, al hacer click los cuerpos se ven atraidos hacia la posicion del cursor (aunque se demoran un poquito en llegar). Al presionar las tecclas + o -, se añaden o se disminuye la camntidad de particulas existentes en uno (1).

También intenté tener los colores caracteristicos que usa calder (amarillo, azul, rojo, nero, blanco) pero no sé si se note mucho. La obra recuerda a un móvil de Alexander Calder


## Debes usar al menos dos algoritmos diferentes de la unidad 1, además de random.
En el proyecto estoy usando varios algorimos:
-Random Gaussian: lo uso para deinir la masa inicial de los cuerpos, para que haya una distribucion mas natural de los tamaños.

-Ruido Perlin: lo uso para interpolar suavemente entre colores de la paleta que escogi, para las variaciones sean mas organicas y bonitas

-simulacion problema de los n cuerpos: lo uso para calcular las fuerzs entre todos los pares de cuerpos segun la ley de gravitacion universal simplificada


## Explica cómo modelaste el problema de los n-cuerpos en tu obra.
mi obra se basa en als siguiente reglas: cada cuerpo tiene posicion, velocidad, aceleracion y masa. en cada frame se calcula la fuerza de atraccion de cada cuerpo sobre los demás y la fuera resulante se aplica como aceleracion.

Se actualizan las velocidades y posiciones con integracion sencilla (euler) y tambien puse para que si un cuerpo llega a chocar con un borde, rebote y no se sala de la pantalla, tambien la interaccion con mouse, que se genera una especie de fuerza adicional de atraccion para que los cuerpos se vean atraidos hacia ese punto.

## Copia el enlace a tu simulación en p5.js.
https://editor.p5js.org/isams2004.1/full/Wn3-NCpYs

##Copia el código.
``` js 
let bodies = [];
let G = 1.5; // Constante gravitacional
let palette = [];

function setup() {
  createCanvas(600, 600);
  
  // Paleta Calder
  palette = [
    color(255, 255, 255), // blanco
    color(0, 0, 0),       // negro
    color(255, 0, 0),     // rojo
    color(255, 204, 0),   // amarillo
    color(0, 102, 204)    // azul
  ];
  
  // Crear cuerpos iniciales
  for (let i = 0; i < 10; i++) {
    let mass = abs(randomGaussian(20, 8));
    let x = random(width);
    let y = random(height);
    bodies.push(new Body(x, y, mass));
  }
}

function draw() {
  // Fondo con opacidad → deja estelas
  background(0, 25);
  
  // Atracción entre cuerpos
  for (let i = 0; i < bodies.length; i++) {
    for (let j = 0; j < bodies.length; j++) {
      if (i !== j) {
        let force = bodies[j].attract(bodies[i]);
        bodies[i].applyForce(force);
      }
    }
  }
  
  // Interacción con el mouse → ATRACCIÓN MÁS FUERTE
  if (mouseIsPressed) {
    for (let b of bodies) {
      let mousePos = createVector(mouseX, mouseY);
      let dir = p5.Vector.sub(mousePos, b.pos);
      let d = constrain(dir.mag(), 5, 200);
      dir.normalize();
      
      // Fuerza aumentada para que se note el jalón
      let strength = (G * b.mass * 800) / (d * d); 
      dir.mult(strength);
      
      b.applyForce(dir);
      
      // EXTRA → darles un empujón extra (para que se sienta más dinámico)
      b.vel.add(dir.copy().mult(0.05));
    }
  }
  
  // Actualizar y mostrar cuerpos
  for (let b of bodies) {
    b.update();
    b.show();
  }
}

function keyPressed() {
  if (key === '+') {
    let mass = abs(randomGaussian(20, 8));
    let x = random(width);
    let y = random(height);
    bodies.push(new Body(x, y, mass));
  } else if (key === '-') {
    if (bodies.length > 0) {
      bodies.pop();
    }
  }
}

class Body {
  constructor(x, y, m) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(0.5, 1.5)); // un poco más rápido
    this.acc = createVector(0, 0);
    this.mass = m;
    this.colNoise = random(1000);
  }
  
  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acc.add(f);
  }
  
  attract(other) {
    let force = p5.Vector.sub(this.pos, other.pos);
    let d = constrain(force.mag(), 10, 80); 
    force.normalize();
    let strength = (G * this.mass * other.mass) / (d * d);
    force.mult(strength);
    return force;
  }
  
  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    
    // Rebote en bordes con freno
    if (this.pos.x < 0 || this.pos.x > width) this.vel.x *= -0.8;
    if (this.pos.y < 0 || this.pos.y > height) this.vel.y *= -0.8;
  }
  
  show() {
    noStroke();
    
    // Interpolación suave entre colores
    let t = noise(this.colNoise + frameCount * 0.005) * palette.length;
    let i = floor(t) % palette.length;
    let j = (i + 1) % palette.length;
    let amt = t - floor(t);
    
    let c = lerpColor(palette[i], palette[j], amt);
    fill(c);
    ellipse(this.pos.x, this.pos.y, this.mass * 2);
  }
}

```

## Captura una imagen representativa de tu ejemplo.

![Uploading image.png…]()


