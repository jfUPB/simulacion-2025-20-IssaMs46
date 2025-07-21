# Unidad 1

## 🛠 Fase: Apply

### Actividad 01
La aleatoriedad en el arte generativo permite que una misma obra pueda tener múltiples resultados únicos, expresando emociones distintas y dándole al azar un rol creativo casi tan importante como el del artista.

### Actividad 02
Siento que en la obra de Sofi usa la aleatoriedad en cuanto a la direccion o el sentido en el que se van a "mover" las ondas, este movimiento también está conectado al sonido, otra caracteristica aleatoria podrían ser los colores que toma cada "raíz", los cuales van variando a medida que pasa el tiempo, me parece algo genial porque se pueden evocar diferentes experiencias y tambien se puede adaptar a diferentes ritmos. (La verdad me pareció un poryecto muy genial y siento que el que la aleatoriedad tenga  un pepel tan importante hace que el proyecto se sienta más mágico)

Y, en cuanto a mi area (programacion de videojuegos) siento que la aleatoriedad puede servirnos para dar una especie de giro inesperado o hacer alguna cosa más interesante, como por ejemplo: si mi personaje va a girar una ruleta para conseguir una recompensa (como por ejemplo, la ruleta de recompenzas en forza horizon 5), los valores o el item puede ser escogido aleatoriamente, asi como el patron de ataque de ciertos enemigos (aumentando la dificultad al ser impredecible, escogiendo un valor random, teniendo un minimo y un máximo), también se puede hacer con la generación de niveles, situando elementos aleatorios en lugares previamente definidos como permitidos (un ejemplo de esto puede ser los niveles y enemigos que aparecen en The Binding Of Isaac, la verdad hace que el juego sea mucho mas interesante y que ninguna partida sea igual a la anterior)

### Actividad 03
modifiqué el codigo para que cuando salga el valor 5 en step (es decir, añadí un nuevo valor posible al random), el fondo cambie de color, luego vi que al tenerlo por encima del punto, no iba a verse, entonces le puse opacidad (esto luego de ejecutarlo por primera vez), también le cambié el color a mi punto y le cambie las dimensiones porque sentí que se veía muy pequeño.

Esperaba que al ejecutar el codigo, el fondo cambiara entre colores vivos y se viera el cuadradito mas grande y nítido, al ejecutar el codigo me di cuenta de que no es como que los colores del fondo sean MUY intensos y también caí en cuenta de que por la opacidad, al punto le quedaba una especie de rastro, a medida que se movía, luego desaparecía ese rastro, por lo que cambia bastante al compararlo con el codigo inicial. este es mi codigo:

// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com
//

<pre>
  <code>
    let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(255);
    strokeWeight(5)
    point(this.x, this.y);
  }

  step() {
    const choice = floor(random(5));
    if (choice == 0) 
    {
      this.x++;
    } 
    else if (choice == 1) 
    {
      this.x--;
    } 
    else if (choice == 2) 
    {
      this.y++;
    } 
    else if (choice == 3)
    {
      this.y--;
    }
    else 
    {
      background(random(255), random(255), random(255), 20)
    }
  }
}

</code>
</pre>


### Actividad 04

<b> En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.</b>

Básicamente, en la distribución uniforme todas las partes tiene la misma probabilidad de aparecer (por ejemplo, undado) pero ya si hablamos de una probabilidad uniforme, sería todo lo contrario, hay valores que van a ser más propensos a salir que otros, por lo que no es algo balanceado.

<b> Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha. </b>


<pre>
<code>


let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() 
{
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    strokeWeight(3)
    point(this.x, this.y);
  }

  step() 
  {
   
    let stepX = randomGaussian(); 
    stepX = stepX + 1;
    let stepY = randomGaussian(); 

    this.x += stepX;
    this.y += stepY;


    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
    
  }
}


</code>
</pre>

al añadir el randomGaussian de por si shace que la distribucion de probabilidades no sea uniforme y al agregarle +1 hacemos que tenga el sezgo hacia la derecha (también lo apliqué con el eje y pero sin el sezgo) y pues ahi básicamente podemos ver que al ejecutar el código nuestro puntito se va hacia la derecha

