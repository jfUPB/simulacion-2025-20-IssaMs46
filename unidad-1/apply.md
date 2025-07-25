# Unidad 1

## 🛠 Fase: Apply

### Actividad 08

Hola, teniendo en cuenta que debía hacer una obra usando al menos 3 de los conceptos vistos, escogí: ruido perlin, distribucion gaussiana y random. La idea era modificar el "circulo" que había hecho en la actividad pasada pero esta vez que tuviera más alteraciones, quise usar el ruido perlin para deformar el contorno del circulo/flor suavemente, la distribucion gaussiana se usa cuando se hace click, generando un tamaño de base de radio diferente para cada circulo/flor, y el random para que tambien, cada vez que se haga click, cambie el color, la posición y la cantidad de "picos" de la figura. añadí un fondo negro con opacidad porque quería darle una especie de sensación neón, me apoyé en chatgpt para saber bien como implementar todo y entender paso a paso lo que estaba haciendo.

``` js
let t = 0;
let petals;
let baseRadius;
let color1, color2;
let centerX, centerY;
let angleOffset;

function setup() 
{
  createCanvas(600, 600);
  noFill();
  strokeWeight(3);
  generateFlower();
}

function draw() {
  background(0, 10); 

  translate(centerX, centerY);
  stroke(lerpColor(color1, color2, abs(sin(t)))); // colorcito bonito suave

  beginShape();
  for (let a = 0; a < TWO_PI; a += 0.05) 
  {
    // Aquí aplico el ruido perlin para que el contorno varíe
    let offset = map(noise(a * petals + t + angleOffset), 0, 1, -baseRadius * 0.5, baseRadius * 0.5);
    let r = baseRadius + offset;
    let x = r * cos(a);
    let y = r * sin(a);
    curveVertex(x, y);
  }
  endShape(CLOSE);

  t += 0.002; // pa que se mueva lentito
}

function generateFlower() 
{
  petals = random(4, 8); // randomrandom
  baseRadius = randomGaussian() * 20 + 150; //gaussss
  color1 = color(random(100, 255), random(100, 200), random(100, 255));
  color2 = color(random(100, 255), random(100, 255), random(100, 255));
  centerX = width / 2 + random(-50, 50);
  centerY = height / 2 + random(-50, 50);
  angleOffset = random(1000); // Fijo por figura
  t = 0; // Reinicia animación suave
}

function mousePressed() {
  generateFlower();
}

```

https://editor.p5js.org/isams2004.1/sketches/mnI-uixrt

<img width="1376" height="578" alt="image" src="https://github.com/user-attachments/assets/64f962df-b547-4008-8316-dd591fdb96b0" />
