# Unidad 1

## 🤔 Fase: Reflect

# Parte 1

## Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?

Bueno, hola, como dice el nombre, random es básicamente escoger un numero aleatorio que haga parte de un rango previamente establecido, lo cual lo puede llegar a hacer algo caótico porque básicamente es eso, números al azar, los cambios son más bruzcos y aleatorios, mientras que el ruido perlin es algo un poco más suave y "continuo", porque el próximo número tiene relación con el número anterior, los resultados varían lentamente. Entonces pues, se ve que hay una diferencia y ambos tienen diferentes aplicaciones.

## Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?

En cuanto a la distribuccion de probabilidad (en general) es básicamente todas las formas en las que puede resultar una especie de "experimento" me refiero, pueden ser valores al azar (tipo, tirar un dado, que sería distribución uniforme, toddas las opciones con las mismas probabilidades de salir) o valores que sean usualmente más tirando para el promedio (lo que sería la distribucion normal).
Ya si hablamos de la diferencia visual que produce una caminata aleatoria, con distribucion uniforme el caminante tiene la posibilidad de caminar por cualquier parte por igual porque todos los valores tienen la misma probabilidad de salir se va a ver desorganizado y es porbable que pase por los mismos pasos/puntos una y otra vez, como pasó en el primer ejemplo de la unidad, mientras que si es una caminata normal, es más probable que se vea más fluida y el caminante pase por puntos relacionados y sea como más lógico por asi decirlo.

## ¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple

Como había comentado en puntos pasados, la aleatoriedad le brinda un aire nuevo al arte generativo, ninguna obra/presencacion será igual a la anterior porque hay muchos factores que van variando continuamente, entonces eso dá una vibra diferente y nueva creando experiencias únicas y refrescantes. En cuanto a las dos funciones distintas, vemos que nos enffocamos bastante en la parte visual, entonces puede ser tan simple como cambiarla forma o color de algún elemento dependiendo de su significado en el momento de la obra, el hecho de que se permita que vaya cambiando (y le permita al artista ir alterando su obra dependiendo de su significado)

## Piensa en tu obra final (Actividad 08). Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.

Usé el concepto de ruido perlin para hacer la variación de las ondas de la flor, pues, como la variacion en cada pétalo, para darle una sensacion de que está viva y de que va fluyendo con el tiempo de alguna u otra manera, siento que lo logré bastante bien porque se ve bonito JAJAJ y también porque es un cambio bastante suave y continuo, las cuales son cualidades bastante importantes al hablar de ruido perlin.

## ¿Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?

Al hablar del paseo o caminata, podemos decir que representa el como funciona cada tipo de aleatoriedad, siento que ayudó bastante para poder entender visualmente cómo se comportan las diferentes herramientas. Es mostrár el trazo de la caminata o movimiento del punto. Lo que hace el Lévy flight es que cada tanto se hacen "saltos" entre los valores aleatorioes escogidos, lo que hace que no pasé varias veces por el mismo lugar, es como si se dibujaran puntitos (estos saltos se establecen a partir de probabilidades y así)


# Parte 2: reflexión sobre tu proceso (Metacognición)

## ¿Cuál fue el concepto más abstracto o difícil de “visualizar” para ti en esta unidad? ¿Qué hiciste para finalmente comprenderlo?
La verdad yo siento que el que más me costo (o los que más) fueron el Levy Flight y la distribución Gaussiana, porque, en cuando al Levy Flight, pensaba que visualmente se vería como si se hiciera una linea hacia el punto del salto, no el salto literalmente (aunque ya escribiendolo y habiendo buscado más sobre el tema, tiene batsntante sentido que sea un salto y no varios pasos pequeños hacia el punto de salto (no sé si me hago entender) entonces  por eso me costó, porque en mi mente se veía diferente. Para entenderlo pues lo grafiqué por código y le pedí a chatgpt que me explicara el concepto. 

Ya al hablar de la distribución Gaussiana, no entendia bien la diferencia entre que los valores den mas cercanos a la media y no tanto a los extremos, y que literalmente pudieran dar en cualquier parte de los valores seleccionados como limites (rango), entonces quería entender eso, algo que me ayudó bastate fue hacer la actividdad porque visualmente es más facil de comprender todo la verdad, tambien le pedi a chatgpt que me explicara eso.

## Describe un momento durante el desarrollo de tu obra final (Actividad 08) en el que un “error” o un resultado inesperado te llevó a una idea creativa interesante.
Pues, como tál, me pasó que cuando agregé lo del ruido perlin vi que iba super rapido, y se veía caótico, pero eso me llevó a entender mejor el concepto y su aplicación, tambien despues logré descubrir como hacer para que se moviera más lento y asi se veía mejor porque pues literal se veía como mera rueda de revolución super rápida JAJAJ, y al experientar con eso pude llegar al resultado final jeje.

## Al combinar diferentes técnicas de aleatoriedad, ¿Cuál fue el mayor desafío? ¿La interacción entre los sistemas, el control de los parámetros, el rendimiento?
Yo creo que el mayor desafío fue mezclar los conceptos, la interaccion entre ellos para que al hacer click y generar el cambio, las cosas fueran coherentes. Siento que esto fue porque en la mayoría o en todos los ejercicios antes del 8, solo usabamos un concepto, no varios, entonces siento que fue eso. También tuve que experimentar con los parámetros para  que el resultado fuera bonito y se viera como yo lo imaginaba.

## Si tuvieras que empezar la Actividad 08 de nuevo, ¿Qué harías de manera diferente basándote en lo que sabes ahora?
Primero, siento que no me habría estresado tanto JAJJA, y capaz le habría puesto varios elementos en vez de uno (al mismo tiempo) para que la visual se viera más interesante.

# Actividad 10


# Actividad 11

## Continuar: ¿Qué actividad, ejemplo o explicación de esta unidad te resultó más reveladora o útil para tu aprendizaje? ¿Qué deberíamos mantener sí o sí?

Me aparece que tener los links guias fue FUNDAMENTAL porque se entiende mejór, contiene ejemplos y el código y siento que eso es vital para entender correctamete un tema.  En cuanto a actividades, siento que la que más me ayudó fue la 8, porque es literal ya hacer todo de 0 y buscar la manera de hacer que todo se conecte entre si. En cuanto a mantener si o si, siento que todo está super bien la verdad JAJAJ

## Dejar de hacer: ¿Hubo alguna actividad o concepto que te pareció redundante, confuso o menos útil? ¿Hay algo que eliminarías o cambiarías por completo?
Siendo totalmente honesta siento que todo está melo, el hecho de que se permita hacer uso de IA para entender coneptos tambien facilita mucho todo (sin que te hagan el trabajo), no cambiaría nada.

## Empezar a hacer: ¿Qué te faltó en esta unidad? ¿Quizás más ejemplos de artistas, más desafíos técnicos, más teoría? ¿Qué idea tienes para hacerla mejor?
Siento que sería bueno poner obras de artistas en yt tipo videos y asi y una breve explicacion de qué conceptos usaron y asi, de esa manera podemos ver su aplicacion en el area laboral y tener un poco más de ideas de qué podemos realizar para poryecto final y que conceptos hay que fortalalecer teniendo en cuenta el proyecto final (tambien saber que cosas se pueeden hacer que no habíamos pensado antes y así)

## Balance Teoría-Práctica: ¿Cómo sentiste el equilibrio entre analizar los ejemplos del texto guía y ponerte a programar tus propios sketches? Explica tu respuesta.
Yo lo sentí bien, si es cierto que me tocó recurrir a ayuda por parte de la IA para escribir ciertas partes del codigo o modificar cosas que no me estaban dando, pero el hecho de que hayan ejemplos y se pueda ver el codigo ayuda porque asi uno puede saber como implementar los diferentes conceptos y se puede experimentar con los valores y ver su resultado..

## Comentario Adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad?
Todo bien, increible curso, la verdad estoy re emocionada y espero poder tener un buen proyecto final para mi portafolio jjiji.



