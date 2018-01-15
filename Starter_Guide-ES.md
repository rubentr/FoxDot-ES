# Guí­a de inicio

Python es un lenguaje de programación orientado a objetos que se centra en la flexibilidad y la legibilidad. Contiene una gran biblioteca de funciones y tiene una gran comunidad de usuarios. Así que ya era hora (tocaba) que pudiesemos hacer música programada (o codificada) con el.

Si alguna vez te quedas atascado o quieres saber más acerca de una función o clase, solo tienes que escribir `help` seguido del nombre entre paréntesis:

```python
help(object)
```

FoxDot proporciona una interfaz de Python en SuperCollider - principalmente como una abstracción rápida y fácil de usar para las clases de SuperCollider, Pbind y SynthDef. Si quieres saber más, puedes leer la documentación de SuperCollider.

Un `SynthDef` es esencialmente un instrumento digital y FoxDot crea objetos llamados players que usan estos instrumentos con tu guía. Para ejecutar código en FoxDot, asegúrate de que el cursor se encuentra en el 'bloque' de código (sección de texto no separadas por líneas en blanco) y presiona `Ctrl + Return`. La salida de cualquier código ejecutado se muestra en la consola en la mitad inferior de la ventana.

Escribe `2 + 2` y mira lo que obtienes.

Ahora intenta algo de (que abarca) varias líneas:

```python
for n in range(10):
    sq = n*n
    print n, sq
```

## 1. Objetos Player

Es posible, de hecho, crear SynthDefs de SuperCollider usando FoxDot, aunque está fuera del alcance de esta guía. Puedes echar un vistazo a la biblioteca existente (aún bastante pequeña, por desgracia) de los SynthDefs que existen en FoxDot, ejecutando:

```python
print SynthDefs
```

Escoje uno y crea un objeto *player* utilizando la sintaxis de la doble flecha `>>` como en el ejemplo siguiente. Si el SynthDef elegido fuese "pluck", entonces podríamos crear un objeto "p1":

```python
p1 >> pluck()
```

Para detener un objeto *player* ejecuta `p1.stop()`. Para detener todos los objetos *player*, presiona `Ctrl +.`, que es un atajo de teclado para el comando `Clock.clear()`.

En Python el símbolo `>>` suele estar reservado para un tipo de operación, como `+` o `-`, pero no es el caso en FoxDot, y la razón se aclarará en breve. Si añades al objeto *player* algunos argumentos, puedes cambiar las notas que suenan. En el primer argumento, el grado de nota (*degree*), no necesitas indicar el nombre, pero es necesario indicarlo en cualquier otro argumento que quieras cambiar, como la duración (*dur*) o el volumen (*amp*).

```python
p1 >> pluck([0,2,4], dur=[1,1/2,1/2], amp=[1,3/4,3/4])
```

Estos argumentos se relacionan con el `SynthDef` correspondiente ("pluck" en el ejemplo), con algunas excepciones:

    - degree
    - dur
    - scale
    - oct

Estos argumentos son utilizados por FoxDot para calcular las frecuencias de las notas que se van a reproducir y cuándo reproducirlas. Puedes ver el código de SuperCollider (aunque no es fácil de leer) ejecutando el comando `print pluck`, por ejemplo. Puedes agrupar los sonidos poniendo varios valores dentro de un argumento entre paréntesis como:

```python
b >> bass([(0,9),(3,7)], dur=4, pan=(-1,1))
```
Observa que no necesitas poner valores individuales entre corchetes? FoxDot se encarga de eso para usted. Puedes incluso tener un objeto *player* seguiendo a otro!

```python
b >> bass([0,2,3,4], dur=4)
p >> pluck(dur=1/2).follow(b) + (0,2,4) # Añade una tríada a las notas del bajo
```

Los *samples* también se pueden reproducir utilizando el objeto `Sample Player`, que se crea de la siguiente manera:

```python
d >> play("x-o-")
```

Cada carácter corresponde a un archivo de audio diferente. Para reproducir *samples* simultáneamente, simplemente crea un nuevo objeto player:

```python
d1 >> play("xxox")
hh >> play("---(-=)", pan=0.5)
```

Los carácteres entre paréntesis se alternan en cada loop (conocidos como lazos) de tal manera que el objeto player anterior,`hh`, es literalmente `hh >> play ('-------=')` que te ahorrará mucho de escribir! Poner caracteres entre corchetes los reproduce dos veces más rápido y puedes poner  un único carácter entre corchetes. Pruébalo:

```python
d1 >> play("x[--]o(=[-o])")
```

## 2. Patterns

Los objetos *player* utilizan un tipo de listas de Python, conocidas comúnmente como *arrays*, para secuenciarse. Ya has utilizado estos anteriormente, pero no son muy flexibles para manipularlos. Por ejemplo, intenta multiplicar una lista por dos de la siguiente manera:

```python
print [1, 2, 3] * 2
```

¿Es el resultado que esperabas? Si quieres manipular los valores dentro de un array en Python, debes utilizar un bucle `for`:

```
l = []
for i in [1, 2, 3]:
    l.append(i * 2)
print l
```
o expresado de otra forma:

```python
print [i*2 for i in [1,2,3]]
```

¿Pero qué pasa si queremos multiplicar los valores de una lista por 2 y 3 de forma alterna? Esto es un poco lioso, especialmente si no conoces qué valores vas a usar. FoxDot utiliza un tipo de contenedor denominado `Patrón` ("Pattern") para ayudar a resolver este problema. Actúan como listas normales pero cualquier operación matemática realizada en él se realiza en cada componente de la lista y en parejas (*pair-wise*) si existe un segundo patrón. Un patrón estándar se puede crear de la siguiente manera:

```python
print P[1,2,3] * 2
>>> P[2, 4, 6]
print P[1,2,3] + [3,4]
>>> P[4, 6, 6, 5, 5, 7]
```
Observa cómo en la segunda operación, el resultado consiste en la combinaciones de los dos patrones, es decir, `[1 + 3, 2 + 4, 3 + 3, 1 + 4, 2 + 3, 3 + 4]`.

 - Prueba con otros operadores matemáticos y observa los resultados.
 - ¿Qué sucede cuando agrupas números entre paréntesis, como `P[1,2,3]*(1,2)`?

Existen más clases de patrones en FoxDot para generar arrays de números pero se comportan de la misma manera que el patrón estándar. Vamos a ver dos tipos más­, pero puedes ejecutar `print (Patterns.Sequences)` para ver los que existen.

En Python, puedes generar una secuencia de números enteros con la sintaxis `range(start, stop, step)`. Por defecto, start es 0 y step es 1. Puedes utilizar `PRange(start, stop, step)` para crear un objeto *Pattern* con los mismos valores:

```python
print range(10)
>>> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print PRange(10)
>>> P[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print PRange(10) * [1, 2]           # Pattern class behaviour
>>> P[0, 2, 2, 6, 4, 10, 6, 14, 8, 18]
```

Pero, ¿y si combinas patrones? En Python, puedes concatenar dos listas (añadir una a otra) utilizando el operador `+`, pero los Patrones de FoxDot lo utilizan para realizar una adición a los datos dentro de la lista. Para conectar dos objetos de patrón juntos, puede utilizar el símbolo de tuberia, `|`, con el que los usuarios de Linux estarán familiarizados. Éste se utiliza para conectar programas de línea de comandos enviando la salida de un proceso como entrada a otro.

```python
print PRange(4) | [1,7,6]
>>> P[0, 1, 2, 3, 1, 7, 6]
```

FoxDot convierte automáticamente cualquier objeto que se canaliza a un patrón a la clase de patrón de base por lo que no tiene que preocuparse de asegurarse de que todo es el tipo correcto. Existen varios tipos de secuencias de patrones en FoxDot (y la lista sigue creciendo) que hacen que la generación de estos números sea un poco más fácil. Por ejemplo, para reproducir la primera octava de una escala pentatónica de abajo hacia arriba y viceversa, puedes utilizar dos objetos `PRange`:

```python
p1 >> pluck(PRange(5) | PRange(5,0,-1), scale=Scale.default.pentatonic)
```

La clase `PTri` hace esto por ti:

```python
p1 >> pluck(PTri(5), scale=Scale.default.pentatonic)
```

## 3. TimeVars

`TimeVar` es una abreviatura de "Variable dependiente del tiempo" ("*Time Dependent Variable*") y es una caracterí­stica clave (importante) de FoxDot. Un `TimeVar` tiene una serie de valores que cambian según/entre una número/serie de *beats* predefinidos y se crea usando un objeto `var` con la sintaxis `var([list_of_values],[list_of_durations])`. Por ejemplo:

```python
a = var([0,3],4)           # La duración puede ser un único valor 
print int(Clock.now()), a  # 'a' inicialmente tiene un valor de 0
>>> 0, 0
print int(Clock.now()), a  # Despúes de 4 beats, el valor cambia a 3
>>> 4, 3
print int(Clock.now()), a  # Tras otros 4 beats, el valor es 0
>>> 8, 0
```

Cuando se utiliza un `TimeVar` en una operación matemática, los valores afectados también se convierten en `TimeVars` que cambian de estado cuando el `TimeVar` original cambia - incluso se pueden usar con patrones:

```python
a = var([0,3], 4)
print a + 5         # beat = 0
>>> 5
print a + 5         # beat = 4
>>> 8
b = PRange(4) + a
print b             # beat = 8 ('a' ahora vale 0)
>>> [0, 1, 2, 3]
print b             # beat = 12 ('a' ahora vale 3)
>>> [3, 4, 5, 6]
```


