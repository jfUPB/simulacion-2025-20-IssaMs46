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


# Actividad 4

#Actividad 5

``` js
function setup() {
    createCanvas(400, 400);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(200, 0);
    let v2 = createVector(0, 200);
    
    let finRojo = p5.Vector.add(v0,v1);
    let finAzul = p5.Vector.add (v0,v2);
    let vecVerde = p5.Vector.sub(v2, v1);
  
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(finRojo, vecVerde, 'green')
  
  //moviemiento moradito
    let raw = (frameCount % 400) / 200; 
    let t = raw <= 1 ? raw : 2 - raw;  
    let movimientoMorado = p5.Vector.lerp(finRojo, finAzul, t);
    let vecMorado = p5.Vector.sub(movimientoMorado, v0);
  
    let rojo = color(255, 0, 0);
    let azul = color(0, 0, 255);
  
    let colorMorado = lerpColor(rojo, azul, t);
    drawArrow(v0, vecMorado, colorMorado);
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```

## ¿Cómo funciona lerp() y lerpColor().
El lerp, de por si funciona para interpolar suavemente (teniendo en cuenta que vamos a usar un t(tiempo)) entre dos valores, en nuestro caso usamos el lerp para determinar el movimiento del vector morado  (interpolandolo entre finRojo y finAzul en el tiempo t indicado. Y en cuanto al lerpColor, es lo mismo, interpola entre dos valores, en ete caso, el color rojo y el color azul dependiendo de en qué momento del tiempo está (0 es rojo y 1 es azul), entonces eso nos dá como resultado que el vector va cambiando su direccion y su color dependiendo del momento/tiempo en el que se encuentre.

## ¿Cómo se dibuja una flecha usando drawArrow()?
El draw arrow está basicamente compuesto por (inicio, final, color), le indicamos donde va a iniciar el vector/linea, y donde va a terminar, luego también le indicamos el color y ya :) 

