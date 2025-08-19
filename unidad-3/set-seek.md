# Unidad 3

## 🔎 Fase: Set + Seek}

## Actividad 1, 2, 3 y 4 son mas de observacion (completadas)

# Actividad 5

## ¿Qué problema le ves a este planteamiento?
El problema lo vi en el método applyFlorce ()

this.acceleration = force;

El problema está ahí porque lo que hace es sobre escribir la aceleracion con cada fuerza que se le aplique, en vez de sumarlas, básicamente el objeto no está recibiendo el efecto combinado de todas las fuerzas, sino que solo recibe la ultima fuerza que se le aplicó.

## ¿Qué solución propones?
Lo que yo haría seria, en vez de asignar la fuerza directamente, la sumaría/acumularia las fuerzas para obtener la aceleracion total de ese frame (usanso la ecuacion de newton que habiamos visto)

Es decir, básicamente reemplazaria el  this.acceleration = force;  por  this.acceleration.add(force);  y ya cuando actualice la posicion y la velocidad, reseteo la aceleracion a cero para que en el siguiente frame se vuelvan a calcular las fuerzas

## ¿Cómo lo implementaría en p5.js?
Lo que haría sería, en vez de reemplazar la aceleracion con cada fuerza, las acumularía (las fuerzas) usando this.acceleration.add(). Aplicaría todas las fuerzas y luego las actualizaría, para finalmente resetear la aceleracion para el siguiente fframe.


# Actividad 6

## ¿Por qué es necesario multiplicar la aceleración por cero en cada frame?

Porque la acelaración e etá acumulando como la sumatorioa de toda la fuerzas aplicadas en ese frame, es decir, si no se pone multiplicadapor cero en cada frame, la aceleración también se multiplicaría entre frames. Básicamente, la velocidad si debe acumularse pero la aceleracion no y por eso la multiplicamos por cero en cada frame.

## ¿Por qué se multiplica por cero justo al final de update()?

Porque el update() es el ultimo paso del ciclo de simulacion en cada frame, entonces ya se sumaron las fuerzas con el applyForce(), esas fuerzas ya modificaron la aceleracion y esa misma aceleracion ya la usamos para mactualizar la velocidad y la posicion, entonces como ya completamos todo eso, ahí si podemos multiplicarla por cero para dejarla lista para el siguiente frame.

# Actividad 7

## ¿Qué ves raro?

BUENO, inicialmente el hecho de que force se esta pasando por referencia y no por valor, entonces cuando hacemos force.div(10) estamos alterando el vector original de la funcion, haciendo que wind y gravity e vean modificadas permanentemente y pues CLARAMENTE eso no es lo que queremos, la idea sería trabajar con una copia del vector.

# Actividad 8 

## ¿Cuál es la diferencia entre las dos líneas?

el this.velocity.copy() crea un nuevo vector con los mismos valores de this.velocity, siendo ambos objetos diferentes.

el let friction = this.velocity() no crea un nuevo vector sinoq ue hace que friction apunte a la misma referencia en memoria que this. velocity (siendo el mismo objeto, si cambio uno cambia el otro)

## ¿Qué podría salir mal con let friction = this.velocity;?

si lo usamos de esa forma, cuando queramos moficicar friction, tambien vamos a estar modificando directamente la velocidad del objeto, entonces la friccion no se comportaria como una fuerza aparte sino que se estaria alterando la velocidad original y todo mal laverdad.

## En el fragmento de código ¿Cuándo es por VALOR y cuándo por REFERENCIA.

si hablamos del codigo:
-let friction = this.velocity.copy() es por valor, osea, se crea un nuevo objeto con los mismos datos.
-let friction  = this.velocity es por referencia, entonces ambas variables apuntan al mismo objeto en memoria.


# Actividad 9

# FRICCIÓN

## Explica cómo modelaste cada fuerza.
La parte de la friccion la hice teniendo en cuenta que esta se modela como una fuerza opuesta al movimiento, en este caso, opuesta al movimiento del bloque. Ya hablando del código, lo que hago es copiar el vector velocidad, lo normalizo y lo multiplico por -0.1 para que quede en el sentido contrario.

## Conceptualmente cómo se relaciona la fuerza con la obra generativa.
en mi caso, mi obra consta de un cubo el cual puede ser empujado muchas veces pero tarde o temprano va a ser detenido por la friccion. En esta obra, la fuerza de friccion es una especie de forma de expresion (si lo demos desde una forma un tanto rebuscada jaj), puesto a que define el ritmo con el que el cubo aparece, se desplaza, frena y se desaparece, toda interaccion depende enteramente de las perturbaciones que genere el usuario, cuanto empuje el cubo y durante cuanto tiempo.

## Copia el enlace a tu ejemplo en p5.js.
https://editor.p5js.org/isams2004.1/sketches/WE6Kna-YK

## Copia el enlace a tu ejemplo en p5.js.

``` js
let mover;

function setup()
{
  createCanvas(600, 200);
  mover = new Mover();
}

function draw()
{
  background(240);

  // Dibujar el suelo
  fill(200);
  rect(0, height - 40, width, 40);

  // Aplicar fricción si el bloque está en movimiento
  let friction = mover.velocity.copy();
  if (friction.mag() > 0)
{
    friction.normalize();
    friction.mult(-0.1); // coeficiente de fricción
    mover.applyForce(friction);
  }

  mover.update();
  mover.display();
}

// Al hacer clic, damos un "empujón" al bloque
function mousePressed()
{
  let push = createVector(2, 0); // fuerza hacia la derecha
  mover.applyForce(push);
}

class Mover
{
  constructor()
{
    this.position = createVector(50, height - 60);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
    this.size = 40;
  }

  applyForce(force)
{
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update()
{
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);

    // Mundo envolvente
    if (this.position.x > width)
{
      this.position.x = -this.size;
    }
    if (this.position.x < -this.size)
{
      this.position.x = width;
    }
  }

  display()
{
    fill(100, 150, 250);
    rect(this.position.x, this.position.y, this.size, this.size);
  }
}


``` 

## Captura una imagen representativa de tu ejemplo.

la verdad no se ve muy  bien pero le juro que sirve jajaj
<img width="669" height="227" alt="image" src="https://github.com/user-attachments/assets/34fe8c1f-808c-423c-b877-980c30fd8b80" />


# Resistencia del aire y de fluidos.

## Explica cómo modelaste cada fuerza.
La resistencuia de los fluidos se modela como una fuerza opuesta al movimiento, y tambien hayq ue tener en cuenta que la magnitud depende de la velocidad al cuaderado (y del medio en el que se encuentra el objeto), lo hice usando la fórmula: fuerza de resistencia = -coeficiente de resistecia del medio * magnitud de la velocidad al cuiadrado * direcciond el movimiento.

En mi ejercicio dividi el espacio en dos, aire y agua,e sto con la finalidad de mostrar visualmente al diferencia de la resistencia en ambos medios (siendo mayor la resistencia en el eagua)

## Relación conceptual con la obra generativa
La obra es una especie de juego visual entre distintos medios, en este caso, aire y agua. En el aire, el circulo desciende rapidamente por la pocca resistencia que presenta el aire, y en el agua, el circulo se mueve mas lento y controlado, básicamente la fuerza de resistencia es el elemento expresivo, transformando la experiencia del movimiento y el ritmo de la animacion  (y bacano porque se puede usar en otras ocasiones) también el usuario puede interactuar por medio de un click haciendo que la pelotita vuelva a su posicion inicial.

## Copia el enlace a tu ejemplo en p5.js.
https://editor.p5js.org/isams2004.1/sketches/bX_DE7_07

## Copia el código.

``` js
let mover;
let cAir = 0.01;   // coeficiente en aire
let cWater = 0.2;  // coeficiente en agua

function setup() 
{
  createCanvas(600, 400);
  mover = new Mover();
}

function draw() 
{
  background(240);

  // Dibujar zona de agua
  fill(180, 220, 255);
  rect(0, height / 2, width, height / 2);

  // Gravedad
  let gravity = createVector(0, 0.2);
  mover.applyForce(gravity);

  // Calcular resistencia dependiendo de la zona
  let drag = mover.velocity.copy();
  if (drag.mag() > 0) {
    drag.normalize();
    let speedSq = mover.velocity.magSq();
    
    // Aire en la parte superior
    if (mover.position.y < height / 2) 
    {
      drag.mult(-cAir * speedSq);
    } 
    // Agua en la parte inferior
    else 
    {
      drag.mult(-cWater * speedSq);
    }
    mover.applyForce(drag);
  }

  mover.update();
  mover.display();
}

// Reiniciar con clic
function mousePressed() 
{
  mover = new Mover();
}

class Mover 
{
  constructor()
  {
    this.position = createVector(width / 2, 50);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
    this.size = 30;
  }

  applyForce(force) 
  {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() 
  {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);

    // Limite suelo
    if (this.position.y > height - this.size / 2) 
    {
      this.position.y = height - this.size / 2;
      this.velocity.mult(0);
    }
  }

  display() 
  {
    fill(250, 100, 100);
    ellipse(this.position.x, this.position.y, this.size);
  }
}

```

## Captura una imagen representativa de tu ejemplo.
<img width="672" height="446" alt="image" src="https://github.com/user-attachments/assets/37c859d7-8152-4eb7-96e6-65855ff87987" />










  

