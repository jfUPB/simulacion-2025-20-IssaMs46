# Unidad 2


## 🛠 Fase: Apply

## 1. Describe el concepto de tu obra generativa.

La idea es hacer una especie de "pecera" en la que se vean las figuritas que van a ser como circulos, la idea es que el movimiento esté influenciado por aceleraciones generadas por medio de un algoritmo de ruido perlin combinado con salto levy para que se vea un movimiento mas suavizado y "natural". ya con lo de salto levy quiero que sea un movimiento no tan predecible pero tampoco caótico. Quiero que en vez de ser la aceleracion hacia el mouse, quiero que las particulas/peces se "asusten" y su aceleracion sea en dirección contraria al mouse.

## 2. ¿Cómo piensas aplicar el marco MOTION 101 y por qué?

La idea es que cada partícula/pez tenga una posicion, velocidad y aceleracion diferente y que la aceleracion se va a calcular usando la combinacion entre ruido perlin (pa suavizar) y saltos levy (para cambios bruscos ocasionales). La idea tambien es que se la velocidad se limite para evitar que las particulas se descontrolen y se sienta mas orgánico.
Adicional a esto, quiero implementar una especie de aceleracion hacia el mouse pero diferente, que en vez de ser en direccion al mouse, sea en la dirección contraria.

## 3. ¿Qué algoritmo de aceleración vas a utilizar? ¿Por qué?
voy a usar dos algoritmos, base de ruido perlin para gener un movimiento suave y continuo y tambien voy a usar perturbaciones tipo levy para meter saltos largos ocasionales y que se rompa la monotonía de lo del movimiento. Voy a usar estas dos para hacer que el movimiento se sienta natural y también para repasar un poquito lo que habíamos visto en la unidad pasada.
