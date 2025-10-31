# Evidencias de la unidad 8

# ACTIVIDAD 01

## Sonar+D
Desde el inicio del video se logra percibir que la imagen no solo es decorativa, sino que los visuales reaccionan teniendo en cuenta el audio, ya sea expandirse, contraertse, cambiar de forma, ritmo,, etc. Por ejemplo, noto que cuando el sonido sube de intensidad los visuales haccen lo mismo, se genera una especie de estallido o expansion, y hacen el efecto contrario cuando la musica es mas calmada, es la sincronia entre ambos ellementos la que genera una experiencia significativa.
Algo que me llamó la atencion es la distribucion y representacion de los colores teniendo en cuenta el sonido, cuando una nota es grave suele ser mas oscura y si es aguda, mas clara.

## Le Parody
Sigue siendo arte generativo jeje, pero aplicado de unaform diferente, da una sensacion mas espacial o abstracta, de igualmanera la sincroniacion sonido-imagen sigue siendo algo super importante, porque sigue generando un feedback visual, no solo el auditivo de la voz.


Básicamente ambas muestran esa conexion entre sonido y visual, pero la de sonar+D se siente un poco más directa o minimalista, al menos yo me siento mas inmersa, mientras que con Le PArody no tuve esa sensacion

## Identifica elementos generativos
Basicamente estas obras crean arte visual en tiempo real, teniendo en cuenta quehay alguien que controla las visuales de acuerdo a la musica y al variar los parametros de las particulas o bodies pueden crear experiencias completamente nuevas en cada ocasion, siento que tambien se puede usar aleatoriedad para varios elementos, asi como gruos de bodies que siguen un mismo comportamiento como en "manada" para generar efectos más impactantes.

## Reflexiona sobre la “Liveness”
yo siento que nace de la respuesta casi que inmediata que hay entre imagen y sonido (nuevamente, dependiendo de quien controla los inputs), todos los cambios se perciben y genera una sensacion de expectacion o intriga por el hecho de poder ver VISUALMENTE un sonido a traves de todas estas interacciones



# ACTIVIDDAD 02
## La pieza musical elegida (con enlace/archivo si es posible).
Misguided ghosts - paramore 
[https://www.youtube.com/watch?v=oGWeHPK3NC4&list=RDoGWeHPK3NC4&start_radio=1](https://www.youtube.com/watch?v=oGWeHPK3NC4&list=RDoGWeHPK3NC4&start_radio=1)

## La descripción de tu concepto visual.
Me gusta mucho la guitarra de la cancion entonces quería intenatr que se representara a traves de flowfields, usé los colores de la prtada del album (amarillo, negro y blanco), tambien quería imitar un poco la rapidez o ritmo de los arpegios que se hacen en la cancion, la verdad es muy significativa para mi y me gustó poder trabajar con ella, me parece que da una vibra traquila, de noche callada, por eso quise añadi una especie de "estrellas" titilantes en el fondo

quiero mucho esta cancion

## Los inputs seleccionados y la justificación de por qué los elegiste.
el mouse genera repulsion leve hacia las particulas en un inteno de cambiar un poco su trayectoria o hacerla mas interesannte, al presionar el click izquierdo las particulas se iluminan brevemente, lo cual hice para poder marcar un poco más el cambio de ritmo en la guitarra
y por ultimo, las teclas A y S, respectivamente, funcionan para disminuir o aumentar la rapidez de las particulas

## ¿Qué algoritmos o técnicas planeas usar (ej: flow fields, flocking, física, partículas, etc.) y por qué?
*FlowFields: para imitar las ondas de la guitarra o sus cuerdas, van a ser muchas mas que solo 6, pero la idea es que se alineen con la guitarra
*Particulas y fisicas basicas: motion 101 si señor, tiene aceleracion,velocidad y fuerza sin romperse
*spatian hashing: esto porque cuando trabajé con flowfields anteriormente, me pasaba que se juntaban todas las particulas y formaban una especie de linea, dejando el fondo muy vacio y era lo que menos quería en este caso
*repulsion: en este caso, por el mouse, es para generar leves cambios en los flujos de particulas

## Tus bocetos y una explicación de cómo los inputs influirán en los visuales.
*Las ondas de los flowfields representan la guitarra y sus ondas auditivas (aunque mas que todo el ritmo de los arpegios y las cuerdas)
*Repulsion del mouse: para causar pequeñas variaciones en caso de que las particulas de flowfield se alineen mucho y el fondo quede "vacio"
*click izq para generar una especie de brillo, siento que puede ser bonito y dar dinamica al arte, para que no siemrpe sea igual
*velocidad con teclas A y S: pequeñas variaciones asi de chill para poder controlar mejor en ciertos momentos rapidos o lentos de la cancion

## ACTIVIDAD 03

```js
// --- Visual generativo "Misguided Ghosts" (con repulsión al mouse) ---
let song, amp;

const STAR_COUNT = 160;
const FLOW_COUNT = 180;
const STAR_SIZE = 2.2;
const CANVAS_W = 900;
const CANVAS_H = 600;

const GRID_STEP = 48;
const FLOW_Z_SPEED = 0.002;
const FLOW_UPDATE_EVERY = 6;
const SEPARATION_DIST = 18;
const SEPARATION_FORCE = 0.45;
const MOUSE_REPEL_RADIUS = 80;   // 🔸 distancia de repulsión del mouse
const MOUSE_REPEL_FORCE = 1;   // 🔸 intensidad de la repulsión

let globalSpeed = 1;
let mouseHeld = false;

let stars = [];
let movers = [];
let cols, rows, field, zOff = 0;
let binSize = 28;
let bins = new Map();

function preload() {
  song = loadSound("Paramore - Misguided Ghosts (Official Audio).mp3");
}

function setup() {
  createCanvas(CANVAS_W, CANVAS_H);
  background(0);
  amp = new p5.Amplitude();
  noiseDetail(4, 0.5);

  for (let i = 0; i < STAR_COUNT; i++) stars.push(new Star());

  cols = floor(width / GRID_STEP) + 1;
  rows = floor(height / GRID_STEP) + 1;
  field = new Array(cols * rows);
  updateFlowField(true);

  for (let i = 0; i < FLOW_COUNT; i++) movers.push(new Mover());

  song.loop();
}

function draw() {
  background(0, 30);

  const level = amp.getLevel();
  const vol = map(level, 0, 0.3, 0, 1);

  // Estrellas
  for (let s of stars) s.updateAndDraw();

  // Flow field (mantiene estabilidad)
  if (frameCount % FLOW_UPDATE_EVERY === 0) {
    zOff += FLOW_Z_SPEED;
    updateFlowField(false);
  }

  // Bins
  bins.clear();
  for (let i = 0; i < movers.length; i++) {
    const m = movers[i];
    const bx = floor(m.pos.x / binSize);
    const by = floor(m.pos.y / binSize);
    const key = bx + "," + by;
    if (!bins.has(key)) bins.set(key, []);
    bins.get(key).push(i);
  }

  // Partículas
  for (let i = 0; i < movers.length; i++) {
    const m = movers[i];
    const ci = constrain(floor(m.pos.x / GRID_STEP), 0, cols - 1);
    const ri = constrain(floor(m.pos.y / GRID_STEP), 0, rows - 1);
    const v = field[ci + ri * cols];
    m.apply(v.x, v.y);

    applySeparationFromBins(i, m);
    m.applyMouseRepulsion(mouseX, mouseY); // 🔸 repulsión del mouse
    m.update(vol, globalSpeed);
    m.wrap();
    m.draw(mouseHeld);
  }
}

// --- Control de mouse ---
function mousePressed() {
  if (mouseButton === LEFT) mouseHeld = true;
}
function mouseReleased() {
  if (mouseButton === LEFT) mouseHeld = false;
}

// --- Control de velocidad ---
function keyPressed() {
  if (key === 'A' || key === 'a') globalSpeed = max(0.3, globalSpeed - 0.2);
  else if (key === 'S' || key === 's') globalSpeed = min(5, globalSpeed + 0.2);
}

function updateFlowField(initial) {
  let idx = 0;
  for (let r = 0; r < rows; r++) {
    const y = r * GRID_STEP;
    for (let c = 0; c < cols; c++) {
      const x = c * GRID_STEP;
      const angle = noise(x * 0.002, y * 0.002, zOff) * TWO_PI * 2;
      const jitter = (sin(c * 12.9898 + r * 78.233) * 43758.5453) % 0.1 - 0.05;
      const a = angle + jitter;
      if (initial || !field[idx]) field[idx] = createVector(cos(a), sin(a));
      else {
        field[idx].x = lerp(field[idx].x, cos(a), 0.35);
        field[idx].y = lerp(field[idx].y, sin(a), 0.35);
      }
      idx++;
    }
  }
}

function applySeparationFromBins(i, m) {
  const bx = floor(m.pos.x / binSize);
  const by = floor(m.pos.y / binSize);
  let fx = 0, fy = 0, count = 0;

  for (let oy = -1; oy <= 1; oy++) {
    for (let ox = -1; ox <= 1; ox++) {
      const key = (bx + ox) + "," + (by + oy);
      const arr = bins.get(key);
      if (!arr) continue;
      for (const j of arr) {
        if (j === i) continue;
        const o = movers[j];
        const dx = m.pos.x - o.pos.x;
        const dy = m.pos.y - o.pos.y;
        const d2 = dx * dx + dy * dy;
        if (d2 > 0 && d2 < SEPARATION_DIST * SEPARATION_DIST) {
          const inv = 1 / sqrt(d2);
          fx += (dx * inv) / 1.2;
          fy += (dy * inv) / 1.2;
          count++;
        }
      }
    }
  }

  if (count > 0) {
    fx /= count;
    fy /= count;
    const mag = sqrt(fx * fx + fy * fy) || 1;
    fx = (fx / mag) * SEPARATION_FORCE;
    fy = (fy / mag) * SEPARATION_FORCE;
    m.apply(fx, fy);
  }
}

// 🌟 Estrellas
class Star {
  constructor() {
    this.x = random(width);
    this.y = random(height);
    this.baseYellow = random(1) > 0.65;
    this.alpha = random(120, 255);
    this.t = random(1000);
    this.driftX = random(-0.02, 0.02);
    this.driftY = random(-0.02, 0.02);
    this.flashOdds = 0.004;
    this.baseSize = random(1.3, 2.4);
  }

  updateAndDraw() {
    this.x += this.driftX;
    this.y += this.driftY;
    if (this.x < 0) this.x += width;
    if (this.x > width) this.x -= width;
    if (this.y < 0) this.y += height;
    if (this.y > height) this.y -= height;

    let pulse = map(sin(this.t), -1, 1, 0.8, 1.4);
    this.t += 0.04;
    if (random() < this.flashOdds) pulse = 1.8;
    let currentSize = this.baseSize * pulse;

    noStroke();
    if (this.baseYellow) fill(255, 210, 70, this.alpha);
    else fill(255, this.alpha);
    ellipse(this.x, this.y, currentSize, currentSize);
  }
}

// 🌬️ Partículas del flujo
class Mover {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vx = 0;
    this.vy = 0;
    this.ax = 0;
    this.ay = 0;
    this.maxSpeed = 2.0;
    this.cYellow = random(1) > 0.5;
    this.alpha = random(140, 255);
    this.t = random(1000);
  }

  apply(fx, fy) {
    this.ax += fx;
    this.ay += fy;
  }

  applyMouseRepulsion(mx, my) {
    const dx = this.pos.x - mx;
    const dy = this.pos.y - my;
    const distSq = dx * dx + dy * dy;
    if (distSq < MOUSE_REPEL_RADIUS * MOUSE_REPEL_RADIUS) {
      const dist = sqrt(distSq) || 1;
      const strength = map(dist, 0, MOUSE_REPEL_RADIUS, MOUSE_REPEL_FORCE, 0);
      const fx = (dx / dist) * strength;
      const fy = (dy / dist) * strength;
      this.ax += fx;
      this.ay += fy;
    }
  }

  update(vol, speed) {
    this.vx += this.ax;
    this.vy += this.ay;
    const lim = this.maxSpeed * speed + vol * 3.5;
    const mag = sqrt(this.vx * this.vx + this.vy * this.vy);
    if (mag > lim) {
      this.vx = (this.vx / mag) * lim;
      this.vy = (this.vy / mag) * lim;
    }
    this.pos.x += this.vx;
    this.pos.y += this.vy;
    this.ax = 0;
    this.ay = 0;

    let baseAlpha = map(sin(this.t), -1, 1, 80, 255);
    this.t += 0.035;
    this.alpha = baseAlpha;
  }

  wrap() {
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }

  draw(isMouseHeld) {
    noStroke();
    let size = isMouseHeld ? 3.8 : 2.4;
    let extraAlpha = isMouseHeld ? 255 : this.alpha;
    if (this.cYellow) fill(255, 210, 70, extraAlpha);
    else fill(255, extraAlpha);
    ellipse(this.pos.x, this.pos.y, size, size);
  }
}

```

[https://editor.p5js.org/isams2004.1/sketches/2vw4VrCxH](https://editor.p5js.org/isams2004.1/sketches/2vw4VrCxH)

<img width="900" height="600" alt="descargar (5)" src="https://github.com/user-attachments/assets/19db4af5-0687-46f0-808c-a4848a04169b" />

<img width="900" height="600" alt="descargar (4)" src="https://github.com/user-attachments/assets/aa54ba92-b618-4b7f-a306-8e10fe98c359" />

# AUTOEVALUACION
NOTA 5: realicé las 3 actividades completas y la autoevaluación.


