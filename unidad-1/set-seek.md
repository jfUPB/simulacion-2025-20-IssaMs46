# Unidad 1

## 🔎 Fase: Set + Seek

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


``` js
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

```


### Actividad 04

<b> En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.</b>

Básicamente, en la distribución uniforme todas las partes tiene la misma probabilidad de aparecer (por ejemplo, undado) pero ya si hablamos de una probabilidad uniforme, sería todo lo contrario, hay valores que van a ser más propensos a salir que otros, por lo que no es algo balanceado.

<b> Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha. </b>


``` js


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


```

al añadir el randomGaussian de por si shace que la distribucion de probabilidades no sea uniforme y al agregarle +1 hacemos que tenga el sesgo hacia la derecha (también lo apliqué con el eje y pero sin el sesgo) y pues ahi básicamente podemos ver que al ejecutar el código nuestro puntito se va hacia la derecha

### Actividad 05
Holi, bueno, básicamente intenté recrear la campana de gauss y pues que se vea un poco más el hecho de que es más probable que salgan valores cercanos a la media que los valores que están en los extremos

``` js
let veces = [];
let numCajas = 100;

function setup() 
{
  createCanvas(640, 360);
  background(255);
  
  for (let i =0; i<numCajas ; i++)
    {
      veces[i]=0;
    }
}

function draw() 
{
  let value = randomGaussian();
  
  let sd=1;
  let mean = 0;
  
  let x= floor(map(value, mean - 3 * sd, mean + 3 *sd, 0, numCajas));
  
  if(x>=0 && x<numCajas)
    {
      veces[x]++;
    }
  
  background(255);
  stroke(0);
  fill(100, 100, 255);
  
   let w = width / numCajas;
  for(let i = 0; i < numCajas; i++) {
    
     let h = veces[i];
     rect(i*w, height, w, -h)
   }
 }
                     
```

este es el link al sketch en p5.js https://editor.p5js.org/isams2004.1/sketches/X67z1WhZC

y esta es la imagen:
<img width="1771" height="737" alt="image" src="https://github.com/user-attachments/assets/03e2c514-8c9f-49e3-9bef-6f850a04cf65" />

### Actividad 06

Adicioné el Levy FLight al ejemplo que habiamos visto del Walker, porque asi como lo definieron en el link adjunto, inicialmente se veía que el walker pasaba por varias partes repetitivamente y pues adicionando el levy ESPERO que la caminata se vea un poco más natural o fluida, como si "estuviera buscando algo", y pues que se vea fluido, asi como se vio inicialmente en el ejercicio de caminata, solo que sta vez espero que el  trayecto del caminante sea distinta.

``` js
let walker;

function setup() 
{
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() 
{
  walker.step();
  walker.show();
}

class Walker 
{
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() 
  {
    stroke(0);
    strokeWeight(3);
    point(this.x, this.y);
  }

  step() 
  {
    let xstep, ystep;
    let r = random(1);

    if (r < 0.01) 
    {
      // 1% de probabilidad de gran salto
      xstep = random(-100, 100);
      ystep = random(-100, 100);
    } 
    else 
    {
      // 99% de probabilidad de pasos pequeños
      xstep = random(-1, 1);
      ystep = random(-1, 1);
    }
    
     this.x += xstep;
    this.y += ystep;

    // Evitar que se salga del canvas
    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }
}

```

BUENO, no fue como esperaba la verdad, porque yo sé que decía que hacia saltos o tomaba pasos largos, pero en mi mente se veía distinto, de igual manera tiene sentido.

https://editor.p5js.org/isams2004.1/sketches/ixzkzPgOK

<img width="1363" height="768" alt="image" src="https://github.com/user-attachments/assets/55cce97f-c0b7-4730-a9ef-ee4f09fdb71b" />

### Actividad 07

Bueno, en la página mostraron el ruido perlin como una linea que va cambiando suavemente a lo largo del tiempo (como ejemplo) entonces pensé que se podría hacer con un circulo y pues que vaya cambiando suavemente (distintos puntos de ella), tambien le añadí el efecto estela que habíamos visto antes porque me quedó gustando jeje. (para este código pedí un poco de ayuda a chat gpt para entender mejor la realizacion del código y cómo llevarlo a cabo)

``` js
let noiseMax = 5; // Qué tan caótico es el borde
let zoff = 0;     // Offset para animación

function setup() 
{
  createCanvas(400, 400);
  background(255);
  stroke(0);
  noFill();
}

function draw() 
{
  background(255, 50); 

  translate(width / 2, height / 2);
  beginShape();

  let t = frameCount * 5; 

  for (let a = 0; a < TWO_PI; a += 0.1) 
  {
    //acá aplico el perlin
    let xoff = map(cos(a), -1, 1, 0, noiseMax);
    let yoff = map(sin(a), -1, 1, 0, noiseMax);
    let r = map(noise(xoff, yoff, zoff), 0, 1, 100, 200);
    let x = r * cos(a);
    let y = r * sin(a);
    vertex(x, y);
  }

  endShape(CLOSE);
  zoff += 0.01;
}
```

https://editor.p5js.org/isams2004.1/sketches/oSkS8gj_W

<img width="1201" height="600" alt="image" src="https://github.com/user-attachments/assets/716bf5d7-4956-4b7f-a703-a87581c06841" />

