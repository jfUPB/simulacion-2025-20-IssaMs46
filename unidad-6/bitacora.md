# Evidencias de la unidad 6

# SET
<img width="713" height="715" alt="image" src="https://github.com/user-attachments/assets/00af89ed-7601-480b-a108-8008ea5f0bc1" />
<img width="457" height="459" alt="image" src="https://github.com/user-attachments/assets/dbd5d440-6111-421e-bfc6-b73fee42bc84" />

Estas imagenes me llaman la atencion porque siento que el flujo con el que se mueven (pues, no se mueven, pero igual da la sensacion de que se muevenn) es muy interesante, el hecho de que se concentran en formas diferentes o se expresan diferente,, me parece muy genial la verdad.

Me inspira porque nuevamente se pueden ver la cantidad de posibilildades que hay a la hora de ilustrar arte generativo, el hecho de que con un simple codigo se pueden crear cosas tan diferentes y tan personalizadas me parece algo increible la verdad, encima teniendo enc uenta el hecho de que ES CON CODIGO eso siempre me va a causar fascinacion.

# SEEK

# Actividad 2

## ¿Qué es una fuerza de dirección (steering force)?
Una fuerza de direccion o steering force, es un vector fuera que se calcula para guiar el movimiento de un agente hacia un objetivo o para modificar su trayectoria, en si, no es la velocidad sino la correccion que se aplica para cambiar la velocidad actual hacia una velocidad deseada.
Básicamente es la fuerza correctora que ajusta la velocidad actual hacia la deseada, para tener un movimiento natural y controlado.

## ¿Qué diferencia tiene este tipo de fuerza con las que ya hemos estudiado en el contexto de la simulación de agentes?

De por si los tipos de fuerzas que hemos visto son mas como para modelar interacciones fisicas (gravedad, friccion, repulsion, atraccion, etc) y se basan en las leyes de Newton, su direccion y magnitud dependen de las propiedades del entorno, ya sean el campo gravitatorio, la distancia, la velocidad relativa, etc.

Por otro lado, la fuerza de direccion es una fuerza "artificial" o de control, no es propiamente derivada de una ley fisica real, de por si su objetivo es modificar el vector de velocidad del agente para que se acerque a un comportamiento deseado

## ¿Qué relación tiene la steering force con Craig Reynolds y su trabajo en simulación de comportamiento animal?

La steering force es la herramienta central que Reynolds diseñó para traducir las inteciones de cada boid (separarse, alinearse, acercarse) en un movimiento realista, si no lo usara, este modelo no tendria la suavidad y el realismo que lo hico tan influyente en la simulacion de comportamiento animal y en la animacion por computador.

# Actividad 3

## Identifica la estructura del campo: en el código (usualmente en una clase FlowField), localiza cómo se almacena el campo de flujo. ¿Qué estructura de datos se usa (ej: un array 2D)? ¿Qué representa cada elemento de esa estructura? ¿Cómo se calcula inicialmente el vector en cada punto?

Se usa un arreglo bidimensional (array 2D), el primer indice i son las columnas del campo, el segundo indice j son las filas del campo, y cada celda de ese arreglo contiene un objeto p5.Vector.

Cada elemento this.field[i][j] es un vector de direccion en ese punto de la grilla, en cuanto a la magnitud, en el ejemplo se deja en 1 cuando se crea con p5.Vector.fromAngle(angle) y el angulo indica la direccion de flujo en esa celda, basicamente cada celda de la cuadricula es una flecha que marca la direccion local del campo de flujo.

ya enc uanto al calculo inicial de los vectores, la funcion init() genera los vectores usando ruido perlin (noise(xoff,yoff)) para obtener un valor suave entre 0 y 1, ese valor se mapea a un angulo en el rango 0 a 2pi, y ya con p5.Vector.fromAngle(angle) se crea un vector unitario apuntando en esa direccion.

## Analiza el comportamiento del agente: en el código de la clase del vehículo/agente (Vehicle), encuentra la función follow(). Explica con tus palabras:

## ¿Cómo determina el agente qué vector del campo de flujo debe seguir basándose en su posición actual? (pista: implica mapear la posición a índices de la cuadrícula).

Lo que se hace es que se divide la coordenada x por el tamaño de la celda (resolution) y obtiene la columna, luego se divide la coordenada y por le tamaño de la celda y se obtiene la fila, lugo se hace uso de floor() y constrain(), con eso se asegura de que el indice quede en el rango valido, y ya con estos indices accede a la celda del campo de flujo y se devuelve el vector de direccion correspondiente

## Una vez que tiene el vector deseado del campo, ¿Cómo lo utiliza para calcular la fuerza de dirección (steering force)? (pista: implica calcular la diferencia con la velocidad actual y limitar la fuerza). 

Cuando ya se obtiene el vvector deseado, escala el vector deseado a su velocidad maxima (maxspeed) para que represente la velocidad objetivo en esa direcicion de flujo y ya despues calcula la velocidad deseada (steer = desired - velocity) esa diferencia es la aceleracion necesaria para corregir la trayectoria hacia el flujo, tambien cabe resaltar que se limita la fuerza (steer.limit(this.maxforce)) para que la aceleracion no sea mayor a la capacidad del agente, evitando cambios bruscos, y ya despues se aplica la fuerza (applyForce(steer)) sumandola a la aceleracion total del ciclo.

## Identifica parámetros clave: localiza en el código las variables que controlan aspectos importantes como: La resolución del campo de flujo (el tamaño de las celdas de la cuadrícula). La velocidad máxima (maxspeed) y la fuerza máxima (maxforce) de los agentes.

la variable de resolucion del campo de flujo es la variable this.resolution y se encuentra en el constructor de FlowField, indica el tamaño en pixeles de cada celda de la malla de flujo, si es un valor pequeño son mas celdas, unc apo mas detallado, si es un valor grande son menos celdas, un capo mas grueso.

La velociad maxima del agente es la variable this.maxspeed, se define en el constructor de vehicle, su "significado" es la velocidad tope que el eagente puede alcanzar cuando sigue el flujo, y su ujso clase es en follow(), escala el vector deseado para que el agente se mueva como macimo a esta velocidad.

La fuerza máxima de dirección es la variable this.maxforce, que se define en el constructor de Vehicle, es el límite superior para la magnituud de la steering force, sy uso clade es en follow(), asegurandose que el agente no gire ni acelere mas ráido de lo permitido, para asi mantener movimiento suaves.

## Experimenta con modificaciones: realiza al menos una de las siguientes modificaciones en el código, ejecuta y describe el efecto observado en el comportamiento de los agentes: Modifica sustancialmente la resolución del campo de flujo (hazla mucho más fina o mucho más gruesa).

en mi caso la linea que modifique ffue la creacion del flowfield, let flow = new FlowField(5); haciendo de esta fforma que sean muchas celdas pequeñas, loque hace quelos vehiculos se muevan "nerviosamene" y cambiando de dirección con mucha frecuencia.

<img width="715" height="266" alt="image" src="https://github.com/user-attachments/assets/379065e1-0acd-4441-bc5d-bc7ffe03e9f9" />


# Actividad 4

## Identifica las tres reglas:

* Separación (Separation): evitar el hacinamiento con vecinos cercanos.
Para esta regla se hace uso del metodo separate(boids), este metodo revisa los void cercanos a una distancia menos a desiredSeparation = 25, si hay vecinoss muy proximoos, calcula un vector que apunte a la direccion opuesta del vecino (resta posiciones), el vector se normaliza y se ajusta por la distancia y luego se limita por maxforce

* Alineación (Alignment): dirigirse en la misma dirección promedio que los vecinos cercanos.
Se usa la funcion align(boids), este metodo calcula la velocidad promedio de los vecinos cercanos dentro de un radio (neighborDistance = 50), luego normaliza esa velocidad promadio, ajusta a maxspeed y la compara con la velocidad actual ( steer = desired - velocity), en ese caso, el boid ajusta su direccion para allinearse con la direccion promedio del grupo

* Cohesión (Cohesion): moverse hacia la posición promedio de los vecinos cercanos.
Este étodo obtiene la posicion promedio de los vecinos cercanos (tambiene stando dentro del neighborDistance = 50), luego llama al metoo seek(sum) para generar una fuerza de dirección hacia ese centro, entonces el boid se mueve hacia el grupo, manteniendose unido con los demás.

``` js
flock(boids) {
  let sep = this.separate(boids); // Separación
  let ali = this.align(boids);    // Alineación
  let coh = this.cohere(boids);   // Cohesión
  
  // Pesos diferentes para cada regla
  sep.mult(1.5);
  ali.mult(1.0);
  coh.mult(1.0);

  this.applyForce(sep);
  this.applyForce(ali);
  this.applyForce(coh);
}
```

## Explica las reglas: para cada una de las tres reglas, explica con tus propias palabras: ¿Cuál es el objetivo de la regla?, ¿Cómo calcula el agente la fuerza de dirección correspondiente?

*Separación: evitar el hacinamiento, la regla hace que un boid se aleje de los vecinos que estén demasiado cerca, para que no choquen o se amontonen. La regla se calcula de la siguiente manera: revisa todos los boids dentro de un radio definido ( desiredSeparation = 25) si otro boid eestá demasiado cerca, se calcula un vector que apunta desde el vecino hacia el boid actual (direccion de alejamiento), se normaliza el vector y se pondera por la distancia (más fuerte si está mmás pegado) y se suman todos los vecinos, ya finalmente se ajusta a la maxspeed y se limita por maxforce para obtener la fuerza de dirección.

*Alineacion: Busca lograr que el void se mueva en la misa dirección promedio que sus vecinos cercanos, imitando el comportamiento de bandadas y cardúmenes. Para calcular la fuerza mira todos los boids dentro de unr adio de percepció (neighborDistance = 50), suma sus velocidades, promedia ese vectori y lo normaliza. Escala la velocidad promedio al valor máximo (maxspeed) y calcla el vector deireccion como la difrerencia entre esa velocidad deseada y la actual ( steer = desired - velocity) y limita el resultado con maxforce

*Cohesion, Su objevito es mantener la unión del grupo, hace que el boid tienda a moverse hacia el centro del grupo de vecinos, evitando que se disperse. Ya para calcular la fuerza, considera a los vecinos dentro de un raio (neighborDistance = 50) suma todas sus posiciones y sac el pomedio, llama a al funcion seek(sum) para generar un vector que apunte hacia ee punto medio, ese vector tambinén se limita con maxforce.

## Parámetros clave

1.Radio/distancia de percepción: Para separacion desiredSeparation = 25, para alineacion y cohesion, neighborDistance = 50

2.Pesos o multiplicadores de influencia relativa: están en flock(boids)
```js
sep.mult(1.5);
ali.mult(1.0);
coh.mult(1.0);
```
ahí separacion tiene  mayor peso (1.5), loq ue significa que evitar choques es mas prioritario que seguir o acercarse al grupo

3.Velocidad máxima y fuerza máxima: Definidas en el constructor:
```js
this.maxspeed = 3;   // Velocidad máxima
this.maxforce = 0.05; // Fuerza de giro máxima
```
estas limitaciones evitan que los voids cambien brucamente de direccion o aceleren de forma irreal


## experimenta con modificaciones:

Cambié el peso de una regla para que la separacion seamuhco mas fuerte, por lo que cada void prioriza alejarse de los demás, adicional a esto, desactivé la cohesion entonces no hay fuerza que los vuelva a juntar. Todo esto hace que los boids tiendan a dispersarse en el espacio, moviendose de una forma más aislada o en grupos muy pequeños, se pierde la sensación de bandada.

```js
sep.mult(3.0);  
ali.mult(1.0);
coh.mult(0.0); 
```

También modifique el radio de percepcion, haciendo que los voids consideren muchos mas vecinos como parte de su grupo, haciendo que el movimiento colectivo se vuelva mucho mas uniforme porque cada void trata de alinearse y cohesionarse con casi todos a la vez

```js
let neighborDistance = 200;
```

<img width="722" height="273" alt="image" src="https://github.com/user-attachments/assets/2e68d803-3031-4e60-979e-4e00f45ca496" />


## Actividad 4

En esta actividad quiero intentar hacerle viuales a la cancion chlorine de twenty one pilots, la version de Mexico City, es una cancion calmada, estuve buscnado obras para inspirarme y me gustó mucho el fondo de un video (no muestran como hacerlo, solo es el fondo, ya que ene l video hablan de arte geenrativo:

<img width="822" height="466" alt="image" src="https://github.com/user-attachments/assets/dedb0cb5-a627-440a-a7e1-1c903e716a99" />

Dado esto, quiero intentar hacer varios cardumenes de particulas que se muevan y alteren su comportamiento teniendo en cuenta las entradas que yo haga por el teclado, quiero que el setting sean particulas amarillas en un fondo negro,voy a ver como ir implementando todo para que use el flocking, aunque ya tengo una idea de como queiro que se vea.


INPUTS: click izquiero para leve aumento de tamaño y leeve cambio de direcccion, tecla "a" para una semi explosion de particulas, teclas w y e para auementar y disminuir la velocidad de movimiento de las particulas

```js
let boids = [];
let MAX_BOIDS = 400; 
let globalMaxSpeed = 6.5;

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 255);
  background(0);

  for (let i = 0; i < 250; i++) {
    boids.push(new Boid(random(width), random(height)));
  }
}

function draw() {
  background(0, 15);

  for (let b of boids) {
    b.maxspeed = globalMaxSpeed; 

    if (frameCount % 2 === 0) {
      const sep = b.separate(boids).mult(1.5);
      const ali = b.align(boids).mult(1.0);
      const coh = b.cohesion(boids).mult(1.0);

      b.applyForce(sep);
      b.applyForce(ali);
      b.applyForce(coh);

      const tgt = b.seek(createVector(mouseX, mouseY)).mult(0.5);
      b.applyForce(tgt);
    }

    b.update();
    b.edges();
    b.show();
  }
}

// ----------------- explosión suave + aumento de tamaño -----------------
function mousePressed() {
  for (let b of boids) {
    let force = p5.Vector.random2D();
    force.mult(random(0.3, 1.0)); 
    b.applyForce(force);

    b.size += 4; 
  }
}

// ----------------- teclado -----------------
function keyPressed() {
  if (key === 'a' || key === 'A') {
    for (let i = 0; i < 100; i++) {
      if (boids.length < MAX_BOIDS) {
        boids.push(new Boid(mouseX, mouseY));
      }
    }
  }
  if (key === 'w' || key === 'W') {
    globalMaxSpeed += 0.5; 
    print("Velocidad ↑: " + globalMaxSpeed);
  }
  if (key === 'e' || key === 'E') {
    globalMaxSpeed = max(0.5, globalMaxSpeed - 0.5); 
    print("Velocidad ↓: " + globalMaxSpeed);
  }
}

// ----------------- clase Boid -----------------
class Boid {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.vel.setMag(random(2, 4));
    this.acc = createVector(0, 0);

    this.maxforce = 0.1;
    this.maxspeed = globalMaxSpeed; 

    this.size = 6; 
    this.hueOffset = random(TWO_PI); // cada boid oscila distinto
  }

  applyForce(f) { this.acc.add(f); }

  seek(target) {
    const desired = p5.Vector.sub(target, this.pos);
    if (desired.mag() === 0) return createVector(0, 0);
    desired.setMag(this.maxspeed);
    const steer = p5.Vector.sub(desired, this.vel);
    steer.limit(this.maxforce);
    return steer;
  }

  separate(boids) {
    const desiredSeparation = 25;
    let steer = createVector(0, 0);
    let count = 0;
    for (const other of boids) {
      const d = p5.Vector.dist(this.pos, other.pos);
      if (d > 0 && d < desiredSeparation) {
        const diff = p5.Vector.sub(this.pos, other.pos);
        diff.normalize();
        diff.div(d);
        steer.add(diff);
        count++;
      }
    }
    if (count > 0) steer.div(count);
    if (steer.mag() > 0) {
      steer.setMag(this.maxspeed);
      steer.sub(this.vel);
      steer.limit(this.maxforce);
    }
    return steer;
  }

  align(boids) {
    const neighborDist = 50;
    let sum = createVector(0, 0);
    let count = 0;
    for (const other of boids) {
      const d = p5.Vector.dist(this.pos, other.pos);
      if (d > 0 && d < neighborDist) {
        sum.add(other.vel);
        count++;
      }
    }
    if (count > 0) {
      sum.div(count);
      sum.setMag(this.maxspeed);
      const steer = p5.Vector.sub(sum, this.vel);
      steer.limit(this.maxforce);
      return steer;
    }
    return createVector(0, 0);
  }

  cohesion(boids) {
    const neighborDist = 50;
    let sum = createVector(0, 0);
    let count = 0;
    for (const other of boids) {
      const d = p5.Vector.dist(this.pos, other.pos);
      if (d > 0 && d < neighborDist) {
        sum.add(other.pos);
        count++;
      }
    }
    if (count > 0) {
      sum.div(count);
      return this.seek(sum);
    }
    return createVector(0, 0);
  }

  update() {
    this.vel.add(this.acc);
    this.vel.limit(this.maxspeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    this.size = lerp(this.size, 6, 0.05);
  }

  show() {
    noStroke();
    
    // Oscilar color entre 60 (amarillo) y 120 (verde)
    let h = map(sin(frameCount * 0.02 + this.hueOffset), -1, 1, 60, 120);

    // halo
    fill(h, 255, 255, 10);  
    ellipse(this.pos.x, this.pos.y, this.size * 3, this.size * 3);

    // núcleo
    fill(h, 255, 255, 150); 
    ellipse(this.pos.x, this.pos.y, this.size, this.size);
  }

  edges() {
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }
}

```

<img width="835" height="724" alt="image" src="https://github.com/user-attachments/assets/f5406714-79b8-4d9c-ac6c-ad1a7905f784" />

https://editor.p5js.org/isams2004.1/sketches/CFz5lzOIZ


Fotos del proceso:

<img width="864" height="705" alt="image" src="https://github.com/user-attachments/assets/d80f0563-e053-4b55-be28-f447c7d52fac" />
<img width="856" height="716" alt="image" src="https://github.com/user-attachments/assets/504d4df0-e8cf-47ea-ad37-c54cdb5924dc" />
<img width="857" height="718" alt="image" src="https://github.com/user-attachments/assets/627e2c99-8109-4edd-8e84-d6abd4d7d0c3" />


















