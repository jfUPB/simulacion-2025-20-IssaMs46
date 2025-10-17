# Evidencias de la unidad 7

# ACTIVIDAD 01

## Analiza la técnica: para 3-4 ejemplos que te llamen la atención, describe brevemente cómo la manipulación visual de la palabra refuerza o representa su significado. ¿Qué elementos gráficos o tipográficos utiliza

1. Elevator: Juega con la v y con la a (que es una v invertida) para representar los botones de subir y bajar que tienen los ascensores.
2. Gravity: Despues de un momento, las letras caen, por la gravedad, entonces se representa en si el significado de la palabra.
3. Clock: modifican la O para representar un reloj.
4. Moon: la segunda O es un satelite de la primera, asi como la luna es un satelite natural de la tierra.

## Genera tus propias ideas (estáticas): elige 2-3 palabras diferentes. Para cada una, piensa y describe (o haz un boceto muy simple) cómo podrías representarla visualmente siguiendo el concepto “Word as Image”, sin pensar aún en animación o física. ¿Cómo alterarías las letras o la composición para evocar el significado?

1. Tree: Se puede usar la T para representar un arbol
2. Game: la M con forma de control de consola
3. Light: siendo la I un bombillo

# ACTIVIDAD 02
## 3.. Intenta replicar en p5.js al menos dos experimentos básicos mostrados en el video de Patt Vira o en los ejemplos del sitio web.

* Crear un mundo con gravedad y añadir algunos cuerpos simples (círculos, cajas) que caigan y colisionen.
  link: [https://editor.p5js.org/isams2004.1/sketches/ixzkzPgOK ](https://editor.p5js.org/isams2004.1/sketches/ixzkzPgOK)
```js

let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies;

let engine;
let world;
let boxes = [];
let ground;

function setup() {
  createCanvas(800, 600);

  // Crear el motor y el mundo
  engine = Engine.create();
  world = engine.world;

  // Crear el suelo (estático)
  let options = {
    isStatic: true
  };
  ground = Bodies.rectangle(400, height - 50, 810, 60, options);
  World.add(world, ground);
}

function mousePressed() {
  // Crear una caja nueva donde se haga clic
  let box = Bodies.rectangle(mouseX, mouseY, random(20, 60), random(20, 60));
  World.add(world, box);
  boxes.push(box);
}

function draw() {
  background(30);
  Engine.update(engine);

  // Dibujar cajas
  fill(200, 150, 255);
  noStroke();
  for (let b of boxes) {
    push();
    translate(b.position.x, b.position.y);
    rotate(b.angle);
    rectMode(CENTER);
    rect(0, 0, 50, 50);
    pop();
  }

  // Dibujar suelo
  fill(100);
  rectMode(CENTER);
  rect(ground.position.x, ground.position.y, 810, 60);
}

 ```

<img width="751" height="614" alt="image" src="https://github.com/user-attachments/assets/307fa5a6-96ac-4d86-a20b-59a62fff5f0f" />

*ejemplo 2,Interacción con el mouse (MouseConstraint)
[https://editor.p5js.org/isams2004.1/sketches/O1GPYvKls](https://editor.p5js.org/isams2004.1/sketches/O1GPYvKls)
```js
// ----- Experimento 2: Interacción con el mouse -----

let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies,
    Mouse = Matter.Mouse,
    MouseConstraint = Matter.MouseConstraint;

let engine;
let world;
let circles = [];
let ground;
let mConstraint;

function setup() {
  createCanvas(800, 600);

  engine = Engine.create();
  world = engine.world;

  // Crear suelo
  let options = { isStatic: true };
  ground = Bodies.rectangle(400, height - 50, 810, 60, options);
  World.add(world, ground);

  // Crear algunos círculos
  for (let i = 0; i < 5; i++) {
    let c = Bodies.circle(random(100, 700), random(50, 200), random(20, 40));
    World.add(world, c);
    circles.push(c);
  }

  // Crear MouseConstraint
  let canvasmouse = Mouse.create(canvas.elt);
  let optionsMC = {
    mouse: canvasmouse
  };
  mConstraint = MouseConstraint.create(engine, optionsMC);
  World.add(world, mConstraint);
}

function draw() {
  background(25);
  Engine.update(engine);

  // Dibujar círculos
  fill(255, 180, 100);
  noStroke();
  for (let c of circles) {
    ellipse(c.position.x, c.position.y, c.circleRadius * 2);
  }

  // Dibujar suelo
  fill(120);
  rectMode(CENTER);
  rect(ground.position.x, ground.position.y, 810, 60);
}

```

<img width="784" height="651" alt="image" src="https://github.com/user-attachments/assets/df68b5f0-6839-4f50-bb4a-106d04dcab8c" />


## 4. Explica los conceptos: basándote en tu experimentación y lectura, explica con tus propias palabras qué es y para qué sirve cada uno de los conceptos clave listados en el paso 2 (Engine, World, Bodies, Constraint, MouseConstraint).

Engine: es lo que controla la simulación de las fisicas
Wold: Es el "ambiente" que contiene todos lo objetos, bodies y constraints
Body: es un objeto fisico individual en la simulación, tiene su propia forma y propiedades
Bodies: es por asi decirlo un grupo para crear tipos de boies especificos con propiedades determinadas
Composite: Es un conjunto de bodies y constrants que se manejan como una sola unidad, pa estructuras jerarquicas.
Render: visualiza la simulacion física.
Runner: hace update al engine en los intervalos fixeados
MouseConstraint: Se usan para permitir la interaccion del usuario, para mover objetos o interactuar con ellos a traves del mouse o touch.


# APPLY

## Actividad 03

## Indica claramente la palabra elegida.

FLOTAR

## Explica tu idea conceptual: ¿Cómo la animación física representa el significado de la palabra?
La idea es representar la palabra flotar usando el concepto de ligereza, suspencion y movimiento que esta relacionada con la palabrajjs, queria que cada letra fuera independiente para que interactuaran entre ellas, y queria usar colores azules que pudieran ser interpretados como "cielo" o "agua" entonces si.

## Describe brevemente los aspectos técnicos clave de tu implementación: ¿Cómo formaste las letras con Matter.js? ¿Qué propiedades físicas fueron importantes? ¿Usaste restricciones?
Estoy usando la libreria Matter.js, inicializo el motor Engine y el mundo haciendo uso de engine.world.gravity.y = 0 para que las letras no se cayeran.

Cada letra de la palabra se genera con un cuerpo rectanfular que usa las propiedades fisicas de frictionAir (para simular la resistencia del aire y suavizar el movimiento), restitution (para darles como un mini rebote cuandointeractuen con fuerzas xternas) y density ( para controlar la masa total del cuerpo).

Las letras en si no son construidas con geometria sino como cuerpos indiviuales con un text(), cada cuerpo se ve afectado por uan fuerza de dlotacion personalizada.

Impementé interaccion, loq ue pasa es que cuando mantengo click se aplica una fuerza de repulsion que genera la ilusion de que se están soplando las letras.


## Codigo
```js

let Engine = Matter.Engine;
let World = Matter.World;
let Bodies = Matter.Bodies;
let Body = Matter.Body;

let engine, world;
let letters = [];
let walls = [];
let bubbles = [];

let t = 0;
let spawnTimer = 0;
let currentLetter = 0;
let spawning = true;

const word = ["F", "L", "O", "T", "A", "R"];

function setup() {
  createCanvas(900, 520);
  engine = Engine.create();
  world = engine.world;
  engine.world.gravity.y = 0;

  textAlign(CENTER, CENTER);
  textFont("Arial");
  textSize(110);
  rectMode(CENTER);

  // límites invisibles
  const thick = 60;
  const wallOpts = { isStatic: true, restitution: 0.5 };
  const left = Bodies.rectangle(-thick / 2, height / 2, thick, height + thick, wallOpts);
  const right = Bodies.rectangle(width + thick / 2, height / 2, thick, height + thick, wallOpts);
  const topW = Bodies.rectangle(width / 2, -thick / 2, width + thick, thick, wallOpts);
  const bottom = Bodies.rectangle(width / 2, height + thick / 2, width + thick, thick, wallOpts);
  walls = [left, right, topW, bottom];
  World.add(world, walls);

  // burbujas de fondo
  for (let i = 0; i < 40; i++) {
    bubbles.push({
      x: random(width),
      y: random(height),
      r: random(1, 3),
      spd: random(0.2, 0.6)
    });
  }
}

function draw() {
  drawBackground();
  Engine.update(engine, 1000 / 60);
  t += 0.01;

  // aparición secuencial (una letra cada 70 frames)
  if (spawning) {
    spawnTimer++;
    if (spawnTimer > 70 && currentLetter < word.length) {
      const x = width / 2 - 330 + currentLetter * 130;
      const y = height + 80;
      const body = Bodies.rectangle(x, y, 70, 90, {
        frictionAir: 0.08,
        restitution: 0.3,
        density: 0.002
      });
      World.add(world, body);
      letters.push({ body: body, char: word[currentLetter] });
      currentLetter++;
      spawnTimer = 0;
      if (currentLetter >= word.length) spawning = false;
    }
  }

  // movimiento grupal tipo brisa
  const targetYBase = height * 0.35;
  const amplitudeY = 20;
  const waveSpeed = 0.5;
  const kBuoy = 0.0005;
  const kDamp = 0.005;

  for (let i = 0; i < letters.length; i++) {
    const body = letters[i].body;
    const phase = i * 0.5;
    const targetY = targetYBase + sin(t * waveSpeed + phase) * amplitudeY;

    const dy = targetY - body.position.y;
    const vy = body.velocity.y;
    const fy = (kBuoy * dy - kDamp * vy) * body.mass;
    const fx = sin(t * waveSpeed + phase) * 0.00005 * body.mass;
    Body.applyForce(body, body.position, { x: fx, y: fy });

    // interacción del mouse (soplo)
    if (mouseIsPressed) {
      const dx = body.position.x - mouseX;
      const dy2 = body.position.y - mouseY;
      const distSq = dx * dx + dy2 * dy2;
      const r = 150;
      if (distSq < r * r) {
        const d = sqrt(distSq) + 0.0001;
        const nx = dx / d;
        const ny = dy2 / d;
        const strength = 0.0009 * (1 - d / r) * body.mass;
        Body.applyForce(body, body.position, { x: nx * strength, y: ny * strength });
      }
    }
  }

  drawScene();
}

function drawBackground() {
  // gradiente vertical
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);
    let c = lerpColor(color(10, 20, 40), color(60, 100, 160), inter);
    stroke(c);
    line(0, y, width, y);
  }

  // burbujas flotantes
  noStroke();
  fill(255, 255, 255, 35);
  for (let b of bubbles) {
    ellipse(b.x, b.y, b.r * 2);
    b.y -= b.spd;
    if (b.y < -5) {
      b.y = height + 5;
      b.x = random(width);
    }
  }
}

function drawScene() {
  noStroke();
  fill(160, 200, 255);

  for (let l of letters) {
    const body = l.body;
    push();
    translate(body.position.x, body.position.y);
    rotate(body.angle);
    text(l.char, 0, 0); // letra real dibujada
    pop();
  }

  fill(230);
  
}


```

<img width="900" height="520" alt="descargar (3)" src="https://github.com/user-attachments/assets/525dc0b9-1073-4b1a-9ac4-ec90cc819770" />




https://github.com/user-attachments/assets/ea17c21a-ba4a-4868-9318-00069499a810









