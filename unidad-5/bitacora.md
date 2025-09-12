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























