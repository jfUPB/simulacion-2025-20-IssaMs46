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










