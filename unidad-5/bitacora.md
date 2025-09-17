# Evidencias de la unidad 5

# SEEK

# ACTIVIDAD 02

## 1. Revisa detalladamente el ejemplo 4.2: an Array of Particles. 
¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

La creacion se particulas se gestiona a punta de: particles.push(new Particle(width / 2, 20)); Básicamente, en la funcion draw, cada vez que se llama esa inea, se crea/ se dibuja una nueva particula.

La desaparicion, teniendo enc uenta que cada particula tiene un lifespan, y usamos un ciclo para ir disminuyendolo, cuando llegue a isDead() hacemos un splice, que básicamente es quitar la referencia de la particula. El arreglo se recorre de atras para adelante para evitar errores.

La memoria se gestiona de la siguiente manera, cuando le aplicamos el splice a una particula, hace que la instancia eliminada se quede sin referencias y eso hace que el garbage collector del sistema, que lo que hace es agarrarla y borrarla, porque no se está usando. Eso hace que el sistema no se sature, teniendo enc eunatq ue cuando una particula muere, se crea otra, ahi loq eu hacemos es que no se sobre sature todo y explote.

## 2. Analiza el ejemplo 4.4: a System of Systems.
¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

La creacion se gestiona de la siguiente forma: en cada draw() el programa agrega nuevas particulas a cada ParticleSystem con el ps.addParticle(), y tambien que cuando el usuario hace click, se crea un nuevo Particle system que tiene en cuenta la posicion del click, generando su propio flujo de particulas y haciendo que se vea como una fuente.

La gestion de la desaparicion es que el sistema recorre la lista de particulas al reves (como lo vimos en clase jeje) y cuando la particula cumple con p.isDeadd(), se eliminan con el splice, básicamente cuando uns istema ya no tiene particulas activas y deja de ser necesario, se elimina tambien del arreglo global con el mismo metodo.

La parte de la memoria es que al remover o eliminar una particula de su lista o del arreglo globarl, las referencias quedan inaccesibles entonces el garbage collector de js las agarra y las elimina basicamente, liberando la memoria automaticamente.


## 3. Analiza el ejemplo 4.5: a Particle System with Inheritance and Polymorphism.
¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

la creacion es que en cadacuadro draw() en cada ParticleSystem se llama addPArticle(), y ese metodo decide aleatoriamente si a nueva particula va a ser de clase paticle o de la subclase confettu, y ya cuando decide la añade al arreglo interno de particle.

en cuanto a la desaparicion, en el metodo run() se recorre la lista de particulas de atras hacia adelante, como amos visto anteriormente, a cada una se le llama run() que básicamente dibuja y acualiza, si la particula tiene que isDead es true, se elimina con el particles.splice(i,1)

ya con lo de la memoria, es lo mismo, cuando la particula muere se elimina del arreglo y ya no tiene ninguna referencia entonces el garbage collector de js elimina su memoria. La herencia y el polimorfismo realmente no cambian este proceso.

# 4. Analiza el ejemplo 4.6: a Particle System with Forces.
¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

Para la creacion, en cada fotograma draw() el ParticleSystem llama addParticle(), y eso crea una nueva particula y la agrega a su siistema interno, antes de actualizar cada particula se apica una fuerza global a todas ellas usando p.applyForce(gravity)

desaparicion, dentro del run(), el sistema recorre el arreglo de particulas de atras hacia adelante, a cada particula se le llama run (que esta vez, como estamos usando lo de la gravedad, actualiza la posicion/ velocidad con la fuerza aplicada y despues la dibuja, si isDead devuelve true, se elimina con el particle.splice(i,1)

ya en cuanto a la memoria, SIGUE SIENDO LO MISMO, cuando es eliminada del arreglo la particula, no hay referencias y el garbge collecot de js elimina su memoria automaticamete, cabe resaltar que el uso de fuerzas no altera este proceso.


## 5. Analiza el ejemplo 4.7: a Particle System with a Repeller.
¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

Para la creacion, en cada cuadro draw() el particleSystem invoca addParticle, que genera una nueva particula, y la agrega al arreglo interno, como hemos estado haciendo en puntos anteriores. pero antes de actualizar cada particula, se calcula y apica la fuerza de repulsion que proviene del objeto repeller

Ya cuando hablamos de la desaparicio, sigue siendo lo mismo que en los otros ejercicios AHHH, en el metodo run el sistema recorre el arreglo de particulas de atras hacia adelante, a cada particula se le aplican las fuerzas de gravedad y repulsion, se acualiza con run y si la particula en isDead da true, se elimina con el splice

la gestion de la memoria, LO MISMOOOOO, con el garbage collector.


# EXPERIMENTOS

## ejemplo 4.2: an Array of Particles. 
Voy a usar el concepto de movimiento básico y vectores, usando atraccion hacia la posicion del mouse. queria que siguierea siendo tipo cascada, pero que esta vez fuera un poco más dinámica y por eso tomé la decision de que fuera interactivo con el mouse. lo que hago es normalizar el vextor y escalarlo con setMAg(0.5) para que la fuerza de magnitud sea constante y ya ahi si luego se lo aplico a la particula con el applyForce().
En la clase de la particula, la fuerza se aculula en la aceleracion y en el update la aceleracion modifica la velocidad y la posicion, ya despues de cada frame la aceleracion se reinicia para que no explote.

Añadi en el draw un calculo de un vector de direccion desde la posiicion de cada particula hasta la posicion actual del mouse, con:

``` js
let dir = createVector(mouseX - p.position.x, mouseY - p.position.y);
dir.setMag(0.05);
p.applyForce(dir);
```

link: [https://editor.p5js.org/isams2004.1/sketches/71NCsnPS-](https://editor.p5js.org/isams2004.1/sketches/71NCsnPS-)

el codigo commpleto es el siguiente:

``` js
let particles = [];

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);
  // crear una nueva partícula en cada frame
  particles.push(new Particle(width / 2, 20));

  // recorrer de atrás hacia adelante para eliminar las muertas
  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];

    // --- Fuerza hacia el mouse ---
    let dir = createVector(mouseX - p.position.x, mouseY - p.position.y);
    dir.setMag(0.05);       // intensidad de la atracción
    p.applyForce(dir);      // aplicar aceleración hacia el mouse

    p.run();
    if (p.isDead()) {
      particles.splice(i, 1);
    }
  }
}
```

<img width="657" height="259" alt="image" src="https://github.com/user-attachments/assets/750ec8bf-b9f5-404f-8152-35a0efd862c6" />



## ejemplo 4.4: a System of Systems.

En este caso busque aplicar el ruido perlin, en la funcion mousePressed() , loq eu hago es generar una coordenada horizontal para el nuevo sistema usando el ruido perlin, la idea es tener un recorrido de lado a lado en ellienzo pero no lo logré muy bien, se supone que eso lo hago rampeando la salida de [0,1], a [-1,1] ara lo del recorrido.

la idea era que la posicion de origen de cada nuevo sistema oscilara, pero pues no me dio, ya solo se usa el ruido perlin ara determinar su nueva posicion., el ruido perlinde por si da variaciones continuas y naturalles, capaz no se ve muy bien porque hay muchas particulas, no lo se la verdad. INTENTAR GAUSS

lo que cambia es mas que todo esta parte:


``` js
let n = noise(frameCount * 0.02) * 2 - 1;     // ruido en [-1,1]
let x = width / 2 + n * (width / 2);          // centro + amplitud mitad del ancho
emitters.push(new Emitter(x, 20));

```

y este es el codigo completo:

``` js
// The Nature of Code – Ejemplo 4.4 modificado
// Sistema de sistemas con oscilación lateral marcada
// del origen de cada nuevo emisor usando ruido Perlin.

let emitters = [];

function setup() {
  createCanvas(640, 240);
  createP("haz click para agregar particle systems");
}

function draw() {
  background(255);

  // ejecutar y actualizar cada sistema existente
  for (let emitter of emitters) {
    emitter.run();
    emitter.addParticle();
  }
}

function mousePressed() {
  // --- NUEVO: ruido Perlin remapeado para una oscilación amplia ---
  // noise() -> [0,1]  →  *2 -1  →  [-1,1]
  // luego lo centro en width/2 y le doy amplitud width/2
  let n = noise(frameCount * 0.02) * 2 - 1;
  let x = width / 2 + n * (width / 2);
  //let y = 20;
  emitters.push(new Emitter(x, 20));
}

```
Link al codigo: [https://editor.p5js.org/isams2004.1/sketches/wBdu2jdth](https://editor.p5js.org/isams2004.1/sketches/wBdu2jdth)

<img width="599" height="265" alt="image" src="https://github.com/user-attachments/assets/933aaecb-293b-4ceb-adc9-0286cb713b0e" />

## ejemplo 4.5: a Particle System with Inheritance and Polymorphism.

LO que quería hacer era que los cuadrados dieran vueltas mas notoriamente usando angulos, en ete caso theta, el cual va a aumentar de foma constante. lo que stoy repasando es el movimiento rotacional, aqui lo aplico de fona en que el angulo cambie con el tiempo para producir una especie de giro uniforme.

los cambios que hice fueron en la subclase confetti, y fueron los siguientes:

``` js
this.theta += 0.1;   //  para la velocidad de giro
```

y en show puse:

``` js
push();
translate(this.position.x, this.position.y);
rotate(this.theta);
square(0, 0, 12);
pop();
```
entonces si, pues el cuadrado se dibuje en el mismo luhar pero rote en torno a su propio cento o eje usando el angulo theta.


llink al codigo: [https://editor.p5js.org/isams2004.1/sketches/GVLZ28aKc](https://editor.p5js.org/isams2004.1/sketches/GVLZ28aKc)

codigo de la subclase que fue el que cambió:

``` js
// Child class constructor
class Confetti extends Particle {
  constructor(x, y) {
    super(x, y);
    this.theta = 0; // ángulo de rotación que irá creciendo
  }

  update() {
    super.update();
    this.theta += 0.1; // controla la velocidad de giro
  }

  // Override the show method
  show() {
    rectMode(CENTER);
    fill(127, this.lifespan);
    stroke(0, this.lifespan);
    strokeWeight(2);
    push();
    translate(this.position.x, this.position.y);
    rotate(this.theta);   // usar el ángulo acumulado, no el mapeo por x
    square(0, 0, 12);
    pop();
  }
}
```

en la imagen se ve casi que igual pero al darle play se ve levemente diferente
<img width="632" height="270" alt="image" src="https://github.com/user-attachments/assets/9f5a2b40-57d3-4753-b984-1b9e0a91797c" />


## Ejemplo 4.6 a Particle System with Forces.

Quería cambiar un poco la trayectoria de las particulas por lo que usé un atrractor, basicamente en el draw()principal, antes de actualizar las particulas loque hago es calcular la fuerza de atraccion de cada particula hacia el attractor y ya despues se la aplico, el ApplyForce añade esa fuerza a la aceleracion de cada parrticula, haciendo que en el update la velocidad y la posicion cambien teniendo en cuenta esa aceleracion.

esto repasa lo de la le de gravitacion :)
 añadí varias cosas, pero principalmente la clase de attractor
 
``` js
// Clase Attractor: aplica fuerza de atracción tipo Ley de Newton
class Attractor {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.mass = 20;   // masa del atractor
    this.G = 1;       // constante gravitacional simplificada
  }

  attract(p) {
    // vector que apunta del objeto p al Attractor
    let force = p5.Vector.sub(this.pos, p.pos);
    let distance = force.mag();
    // limitar la distancia para evitar fuerzas extremas
    distance = constrain(distance, 5, 25);
    force.normalize();
    // Ley de la gravitación: F = G * m1 * m2 / d^2
    let strength = (this.G * this.mass * p.mass) / (distance * distance);
    force.mult(strength);
    return force;
  }

  display() {
    noStroke();
    fill(50, 150, 255);
    ellipse(this.pos.x, this.pos.y, this.mass * 2);
  }
}
```

LINK: [https://editor.p5js.org/isams2004.1/sketches/AnsGtM80g](https://editor.p5js.org/isams2004.1/sketches/AnsGtM80g)


<img width="578" height="246" alt="image" src="https://github.com/user-attachments/assets/0555f799-8fdc-4d84-8621-08a03c63ed82" />
















