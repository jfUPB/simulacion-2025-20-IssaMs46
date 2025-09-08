# Evidencias de la unidad 4

## Explicación conceptual de la obra

* ¿Qué concepto de la unidad 4 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> 
>De la unidad 4 tomé manejo de ángulos, coordenadas polares, funciones sinusoides y ondas.

> -Con atan2 calculo el ángulo del mouse para rotar todo el sistema.

> -Uso coordenadas polares (r*cosθ, r*sinθ) para colocar las bolitas alrededor del círculo.

> -El contorno se deforma con una función sinusoidal (sin(theta*freq + offset)), generando ondulación.


> Además, implementé ondas expansivas que crecen y se desvanecen cuando el mouse está presionado.

* ¿Qué concepto de la unidad 3 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> 
>De la unidad 3 trabajé con el concepto de paso por referencia.

> -El arreglo waves almacena objetos (cada onda con sus atributos) que se actualizan directamente en cada frame: su radio aumenta y su transparencia disminuye sin necesidad de crear copias.
> -Esto me permitió mantener y modificar múltiples ondas de manera eficiente.

* ¿Qué concepto de la unidad 2 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> 
>De la unidad 2 usé principalmente vectores y el enfoque motion 101.

> -Apliqué vectores en la conversión polar a cartesiano para ubicar cada punto del contorno.

> -Motion 101 está presente en la forma en que las variables de estado (offset, rotationAngle, el crecimiento de las ondas) cambian progresivamente en cada frame, creando movimiento fluido y acumulativo.

* ¿Qué concepto de la unidad 1 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> 
>De la unidad 1 utilicé distribución normal y ruido Perlin.

> -Con randomGaussian asigno valores a los canales rojo y azul, generando variaciones suaves y con cierta tendencia alrededor de un promedio.

> -Con noise asigno el canal verde, lo que produce una variación continua y orgánica en el tiempo.
> -Estos dos enfoques combinados permiten que los colores sean generativos, únicos y dinámicos.

## ¿Cómo resolviste la interacción?
> Tu respuesta aquí:
> 
>La interacción se resolvió con el mouse:

> -El movimiento del mouse controla la rotación global de la obra a partir del ángulo calculado con atan2.

> -Al presionar el mouse se incrementa la amplitud de las ondas sinusoidales, haciendo que la figura se expanda visualmente.

> -Además, en cada clic se generan ondas expansivas que se propagan desde las bolitas, representando un pulso emitido por la acción del usuario.

## Enlace a la obra en el editor de p5.js

[Aquí está mi obra](https://editor.p5js.org/isams2004.1/full/0SSH0-OyD)

## Código de la obra 

``` js
let amplitude = 40;   // amplitud de la onda en el contorno
let offset = 0;
let rotationAngle = 0;   // controla la rotación global
let prevMouseAngle;

let waves = []; // aquí guardamos las ondas expansivas

function setup() {
  createCanvas(800, 600);
  noStroke();
  angleMode(RADIANS);
}

function draw() {
  background(20, 30, 40, 40);

  translate(width / 2, height / 2); // centro del canvas

  let baseRadius = 200;
  let currentAmp = amplitude;

  if (mouseIsPressed) {
    currentAmp *= 1.6;
  }

  // --- Ángulo actual del mouse respecto al centro ---
  let mouseAngle = atan2(mouseY - height / 2, mouseX - width / 2);

  if (prevMouseAngle !== undefined) {
    let deltaAngle = mouseAngle - prevMouseAngle;
    if (deltaAngle > PI) deltaAngle -= TWO_PI;
    if (deltaAngle < -PI) deltaAngle += TWO_PI;
    rotationAngle += deltaAngle;
  }
  prevMouseAngle = mouseAngle;

  // --- ROTAR todo el sistema según el mouse ---
  rotate(rotationAngle);

  let step = 0.2; // separación angular
  for (let theta = 0; theta < TWO_PI; theta += step) {
    let freq = 6; 
    let r = baseRadius + currentAmp * sin(theta * freq + offset);

    let x = r * cos(theta);
    let y = r * sin(theta);

    // colores generativos para las bolitas
    let redC = constrain(randomGaussian(150, 40), 0, 255);
    let greenC = constrain(noise(theta, frameCount * 0.01) * 255, 0, 255);
    let blueC = constrain(randomGaussian(200, 30), 0, 255);

    fill(redC, greenC, blueC, 180);
    circle(x, y, 20);

    // --- crear ondas SOLO si el mouse está presionado ---
    if (mouseIsPressed && frameCount % 3 === 0) { 
      waves.push({
        x: x + width/2, 
        y: y + height/2, 
        r: 0, 
        alpha: 200,
        col: color(redC, greenC, blueC, 180) // guardamos el color de esa bolita
      });
    }
  }

  offset += 0.05; 

  // --- Dibujar ondas expansivas ---
  noFill();
  strokeWeight(2);
  for (let i = waves.length - 1; i >= 0; i--) {
    let w = waves[i];
    stroke(w.col); // usamos el color propio de cada onda
    ellipse(w.x - width/2, w.y - height/2, w.r*2);

    w.r += 2;        // expansión
    w.alpha -= 3;    // desvanecimiento

    // actualizar transparencia
    w.col.setAlpha(w.alpha);

    if (w.alpha <= 0) {
      waves.splice(i, 1); // eliminar cuando ya muere
    }
  }
}


```

## Captura de pantalla representativa


<img width="867" height="668" alt="Captura de pantalla 2025-09-04 222601" src="https://github.com/user-attachments/assets/51297104-3d0c-4247-91d6-d7ee7ab7a5e6" />








