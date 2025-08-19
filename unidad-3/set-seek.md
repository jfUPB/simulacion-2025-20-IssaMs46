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
