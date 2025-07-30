# Unidad 2

## 🔎 Fase: Set + Seek


# Actividad 1

## ¿Cómo funciona la suma dos vectores en p5.js?

De por si, al usar vectores, no los podemos sumar como sumaríamos dos números, entonces nos toca usar unso métodos diferentes: podemos usar un .add(), en este caso sería position.add(velocity); con esto lo que esoty haciendo es sumar velocity a position directamente, es decir, el que estoy modificando es position.

La otra forma es usando p5.Vector.add(), que es crear un nuevo vector, en nuestro caso sería let result = p5.Vector.add(position, velocity); y ahi no estamos ACTUALIZANDO sino que estamos CREANDO un nuevo vector que sea la suma de position y velocity, sin modificar los originales.

## ¿Por qué esta línea position = position + velocity; no funciona?
No funciona porque dentro de p5, positon y velocity son objetos y no numeros (por lo que no se pueden sumar directamente), si hacemos eso estaríamos concatenando dos objetos como cadenas de texto y pues, en matemáticas eso mucho sentido no tiene. Por esa razón usamos el .add, el cual suma los COMPONENTES  de un vector con los de otro componente por componente.

# Actividad 2

## Take one of the walker examples from Chapter 0 and convert it to use vectors.
¿Qué tuviste que hacer para hacer la conversión propuesta?

cambiamos los this.x this.y por this.position, y ya ahi está implicito el usar position.x y position.y, esto hace que el código sea mucho más compacto y bonito. Ah bueno y también usamos principalmente el position=createVector()

``` js

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    
    this.position = createVector(width/2, height/2);
    
    
    //this.x = width / 2;
    //this.y = height / 2;
  }

  show() {
    stroke(0);
    //point(this.position.x, this.position.y);
    point(this.position);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.position.x++;
    } else if (choice == 1) {
      this.position.x--;
    } else if (choice == 2) {
      this.position.y++;
    } else {
      this.position.y--;
    }
  }
}

```
# Actividad 3

## ¿Qué resultado esperas obtener en el programa anterior?
Al analizar lo que dice el código, se esperaba que primero apareciera el vector con los valores (6,9) y luego con los valores (20,30)

## ¿Qué resultado obtuviste?¿Qué resultado obtuviste?
ese mismo jeje
<img width="435" height="156" alt="image" src="https://github.com/user-attachments/assets/2374decc-4e68-4c3f-b686-4ff978a92268" />

## Recuerda los conceptos de paso por valor y paso por referencia en programación. Muestra ejemplos de este concepto en javascript.
