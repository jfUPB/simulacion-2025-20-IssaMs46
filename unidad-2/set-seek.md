# Unidad 2

## 🔎 Fase: Set + Seek


## Unidad 1

## ¿Cómo funciona la suma dos vectores en p5.js?

De por si, al usar vectores, no los podemos sumar como sumaríamos dos números, entonces nos toca usar unso métodos diferentes: podemos usar un .add(), en este caso sería position.add(velocity); con esto lo que esoty haciendo es sumar velocity a position directamente, es decir, el que estoy modificando es position.

La otra forma es usando p5.Vector.add(), que es crear un nuevo vector, en nuestro caso sería let result = p5.Vector.add(position, velocity); y ahi no estamos ACTUALIZANDO sino que estamos CREANDO un nuevo vector que sea la suma de position y velocity, sin modificar los originales.

## ¿Por qué esta línea position = position + velocity; no funciona?
No funciona porque dentro de p5, positon y velocity son objetos y no numeros (por lo que no se pueden sumar directamente), si hacemos eso estaríamos concatenando dos objetos como cadenas de texto y pues, en matemáticas eso mucho sentido no tiene. Por esa razón usamos el .add, el cual suma los COMPONENTES  de un vector con los de otro componente por componente.

## Unidad 2
