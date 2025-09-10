# Evidencias de la unidad 5

# SEEK

# ACTIVIDAD 02

## Revisa detalladamente el ejemplo 4.2: an Array of Particles. 
¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

La creacion se particulas se gestiona a punta de: particles.push(new Particle(width / 2, 20)); Básicamente, en la funcion draw, cada vez que se llama esa inea, se crea/ se dibuja una nueva particula.

La desaparicion, teniendo enc uenta que cada particula tiene un lifespan, y usamos un ciclo para ir disminuyendolo, cuando llegue a isDead() hacemos un splice, que básicamente es quitar la referencia de la particula. El arreglo se recorre de atras para adelante para evitar errores.

La memoria se gestiona de la siguiente manera, cuando le aplicamos el splice a una particula, hace que la instancia eliminada se quede sin referencias y eso hace que el garbage collector del sistema, que lo que hace es agarrarla y borrarla, porque no se está usando. Eso hace que el sistema no se sature, teniendo enc eunatq ue cuando una particula muere, se crea otra, ahi loq eu hacemos es que no se sobre sature todo y explote.

## 



