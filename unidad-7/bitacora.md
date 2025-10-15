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

## 4. Explica los conceptos: basándote en tu experimentación y lectura, explica con tus propias palabras qué es y para qué sirve cada uno de los conceptos clave listados en el paso 2 (Engine, World, Bodies, Constraint, MouseConstraint).

Engine: es lo que controla la simulación de las fisicas
Wold: Es el "ambiente" que contiene todos lo objetos, bodies y constraints
Body: es un objeto fisico individual en la simulación, tiene su propia forma y propiedades
Bodies: es por asi decirlo un grupo para crear tipos de boies especificos con propiedades determinadas
Composite: Es un conjunto de bodies y constrants que se manejan como una sola unidad, pa estructuras jerarquicas.
Render: visualiza la simulacion física.
Runner: hace update al engine en los intervalos fixeados
MouseConstraint: Se usan para permitir la interaccion del usuario, para mover objetos o interactuar con ellos a traves del mouse o touch.



