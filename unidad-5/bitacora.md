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

La creacion se gestiona de la siguiente forma: en cada draw() el programa agrega nuevas particulas a cada PartycleSystem con el ps.addParticle(), y tambien que cuando el usuario hace click, se crea un nuevo Partycle system que tiene en cuenta la posicion del click, generando su propio flujo de particulas y haciendo que se vea como una fuente.

La gestion de la desaparicion es que el sistema recorre la lista de particulas al reves (como lo vimos en clase jeje) y cuando la particula cumple con p.isDeadd(), se eliminan con el splice, básicamente cuando uns istema ya no tiene particulas activas y deja de ser necesario, se elimina tambien del arreglo global con el mismo metodo.

La parte de la memoria es que al remover o eliminar una particula de su lista o del arreglo globarl, las referencias quedan inaccesibles entonces el garbage collector de js las agarra y las elimina basicamente, liberando la memoria automaticamente.






