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



