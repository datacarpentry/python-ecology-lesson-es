---
title: Breve introducción a la Programación en Python
teaching: 0
exercises: 0
questions:
    - "¿Qué es Python?"
    - "¿Porqué deberías aprender Python?"
objectives:
    - "Describir las ventajas de usar programación vs. completar tareas repetitivas a mano."
    - "Definir los tipos de datos en Python: **cadenas**, **enteros**, y números de **punto flotante**."
    - "Realizar operaciones matemáticas en Python utilizando operadores básicos."
    - "Dentro del contexto de Python definir: **listas**, **tuplas**, y **diccionarios**."
keypoints:
    - "Python es un lenguaje interpretado que puede ser usado interactivamente (ejecutando un comando a la vez) o en modo scripting (ejecutando una serie de comandos guardados en un archivo)."
    - "Se puede asignar un valor a una variable en Python. Esas variables pueden ser de varios tipos, tales como cadenas, y números: enteros, de punto flotante y complejos."
    - "Las listas y las tuplas son similares en el sentido de que son listas ordenadas de elementos; difieren en que una tupla es inmutable (sus elementos no pueden ser modificados)."
    - "Los diccionarios son estructuras de datos desordenadas que proporcionan mapeos entre claves y valores."

---

## Intérprete

Python es un lenguaje interpretado que puede ser usado de dos formas:

* Modo "Interactivo": cuando lo usas como una "calculadora avanzada" ejecutando
  un comando a la vez. Para iniciar Python en este modo, simplemente ejecuta `python`
  en la línea de comandos:

~~~
$ python
~~~
{: .language-bash}

~~~
Python 3.5.1 (default, Oct 23 2015, 18:05:06)
[GCC 4.8.3] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
~~~
{: .output}

Los res símbolos de mayor que `>>>` forman un indicador interactivo en Python, que significa que está esperando tu
entrada de datos.

~~~
2 + 2
~~~
{: .language-python}

~~~
4
~~~
{: .output}

~~~
print("Hello World")
~~~
{: .language-python}
~~~
Hello World
~~~
{: .output}

* Modo "Script": cuando ejecutas una serie de "comandos" guardados en un archivo de texto,
  generalmente con una extensión `.py` después del nombre de tu archivo:
~~~
$ python my_script.py
~~~
{: .language-bash}

~~~
Hello World
~~~
{: .output}

## Introducción a los tipos de datos incorporados en Python

### Strings, integers, and floats

Una de las cosas más básicas que podemos hacer en Python es asignar valores a las variables:

~~~
text = "Data Carpentry"  # Un ejemplo de string
number = 42  # Un ejemplo de integer
pi_value = 3.1415  # Un ejemplo de float
~~~
{: .language-python}

Aquí hemos asignado datos a las variables `text`,` number` y `pi_value`,
utilizando el operador de asignación `=`. Para revisar el valor de una variable, nosotros
podemos escribir el nombre de la variable en el intérprete y presionar <kbd>Return</kbd>:

~~~
text
~~~
{: .language-python}
~~~
"Data Carpentry"
~~~
{: .output}


Todo en Python tiene un tipo. Para obtener el tipo de algo, podemos pasarlo
a la función `type`:

~~~
type(text)
~~~
{: .language-python}
~~~
<class 'str'>
~~~
{: .output}

~~~
type(number)
~~~
{: .language-python}
~~~
<class 'int'>
~~~
{: .output}

~~~
type(6.02)
~~~
{: .language-python}
~~~
<class 'float'>
~~~
{: .output}


La variable `text` es de tipo 'str', abreviatura de **string** o cadena de caracteres. Las cadenas almacenan
secuencias de caracteres, que pueden ser letras, números, puntuación
o formas más exóticas de texto (¡incluso emoji!).

También podemos ver el valor de algo usando otra función incorporada, `print`:

~~~
print(text)
~~~
{: .language-python}
~~~
Data Carpentry
~~~
{: .output}
~~~
print(11)
~~~
{: .language-python}
~~~
11
~~~
{: .output}

Esto puede parecer redundante, pero de hecho es la única forma de mostrar resultados en un script:

*example.py*
~~~
# En un archivo script de Python
# los comentarios en Python inician con #
# Las siguientes líneas asignan la cadena "Data Carpentry" a la variable "text".
text = "Data Carpentry"

# ¡La siguiente línea no hace nada!
text

# La siguiente línea usa la función print para imprimir el valor asignado a "text"
print(text)
~~~
{: .language-python}

*Ejecutando el script*
~~~
$ python example.py
~~~
{: .language-bash}

~~~
Data Carpentry
~~~
{: .output}

Nota que "Data Carpentry" se imprime una vez.

**Sugerencia**: `print` y `type` son funciones incorporadas en Python. Más adelante en esta
lección, veremos métodos y funciones definidas por el usuario. La documentación
de Python es excelente para darte una referencia sobre las diferencias entre ellos.


### Operadores

Podemos realizar cálculos matemáticos en Python usando los operadores básicos
 `+, -, /, *, %`:

~~~
2 + 2  # Suma
~~~
{: .language-python}

~~~
4
~~~
{: .output}

~~~
6 * 7  # Multiplicación
~~~
{: .language-python}
~~~
42
~~~
{: .output}
~~~
2 ** 16  # Potencia
~~~
{: .language-python}
~~~
65536
~~~
{: .output}
~~~
13 % 5  # Módulo
~~~
{: .language-python}
~~~
3
~~~
{: .output}


También podemos utilizar operadores de comparación y lógicos:
`<,>, ==,! =, <=,> =` y declaraciones de identidad como
`and, or, not`. El tipo de datos devuelto por estos operadres es
llamado _**boolean**_ y retorna verdadero o falso, como ves a continuación.

~~~
3 > 4
~~~
{: .language-python}
~~~
False
~~~
{: .output}

~~~
True and True
~~~
{: .language-python}
~~~
True
~~~
{: .output}

~~~
True or False
~~~
{: .language-python}
~~~
True
~~~
{: .output}

~~~
True and False
~~~
{: .language-python}
~~~
False
~~~
{: .output}

## Secuencias: Listas y Tuplas

### Listas

**list** (o listas) son una estructura de datos común para almacenar una secuencia ordenada de
elementos. Se puede acceder a cada elemento mediante un índice. Ten en cuenta que en Python,
los índices comienzan con 0 en lugar de 1:

~~~
numbers = [1, 2, 3]
numbers[0]
~~~
{: .language-python}
~~~
1
~~~
{: .output}

Se puede usar un bucle `for` para acceder a los elementos de una lista u otras
estructuras de datos de Python, uno a la vez:

~~~
>>> for num in numbers:
...     print(num)
...
~~~
{: .language-python}

~~~
1
2
3
~~~
{: .output}

Usar **sangría** es muy importante en Python. Ten en cuenta que la segunda línea en el
ejemplo de arriba está sangrada (o indentada). Al igual que los tres `>>>` son un
indicador interactivo en Python, los tres puntos `...` son indicadores de
líneas multiples en Python. Esta es la manera en que Python marca un bloque de código. [Nota: no
tienes que escribir `>>>` o `...`.]

Para agregar elementos al final de una lista, podemos usar el método `append`. Los métodos
son una forma de interactuar con un objeto (una lista, por ejemplo). Podemos invocar un
método usando el punto `.` seguido del nombre del método y una lista de argumentos
entre paréntesis. Veamos un ejemplo usando `append`:

~~~
numbers.append(4)
print(numbers)
~~~
{: .language-python}

~~~
[1, 2, 3, 4]
~~~
{: .output}

Para averiguar qué métodos están disponibles para un
objeto, podemos usar el comando incorporado `help`:

~~~
help(numbers)

Help on list object:

class list(object)
 |  list() -> new empty list
 |  list(iterable) -> new list initialized from iterable's items
 ...
~~~
{: .output}

### Tuplas

Una tupla **tuple** es similar a una lista en que es una secuencia ordenada de elementos.
Sin embargo, las tuplas no se pueden cambiar una vez creadas (son "inmutables"). Las tuplas
se crean colocando valores separados por comas dentro de los paréntesis `()`.

~~~
# Las tuplas usan paréntesis
a_tuple = (1, 2, 3)
another_tuple = ('blue', 'green', 'red')

# Nota: las listas usan corchetes cuadrados
a_list = [1, 2, 3]
~~~
{: .language-python}

> ## Tuplas _vs._ Listas
> 1. ¿Qué sucede cuando ejecutas `a_list[1] = 5` ?
> 2. ¿Qué sucede cuando ejecutas `a_tuple[2] = 5`?
> 3. ¿Qué te dice `type(a_tuple)` sobre `a_tuple`?
>
{: .challenge}


## Diccionarios

Un diccionario **dictionary** es un contenedor que almacena pares de objetos - claves y valores.

~~~
translation = {'one': 1, 'two': 2}
translation['one']
~~~
{: .language-python}
~~~
1
~~~
{: .output}

Los diccionarios funcionan como listas, excepto que se crea el índice utilizando *claves*  **keys**.
Puedes pensar en una clave como un nombre o un identificador único para un conjunto de valores
en el diccionario. Las claves sólo pueden tener tipos particulares, tienen que ser
"**hashable**". Las cadenas y los tipos numéricos son aceptables, pero las listas no lo son.

~~~
rev = {1: 'one', 2: 'two'}
rev[1]
~~~
{: .language-python}
~~~
'one'
~~~
{: .output}

~~~
bad = {[1, 2, 3]: 3}
~~~
{: .language-python}
~~~
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
~~~
{: .output}

En Python, un "**Traceback**" es un bloque de error de varias líneas impreso para el
usuario.

Para agregar un elemento al diccionario, asignamos un valor a una nueva clave:

~~~
rev = {1: 'one', 2: 'two'}
rev[3] = 'three'
rev
~~~
{: .language-python}
~~~
{1: 'one', 2: 'two', 3: 'three'}
~~~
{: .output}

Usar bucles `for` con diccionarios es un poco más complicado. Podemos hacer
esto de dos maneras:
~~~
for key, value in rev.items():
    print(key, '->', value)
~~~
{: .language-python}

~~~
1 -> one
2 -> two
3 -> three
~~~
{: .output}

o

~~~
for key in rev.keys():
    print(key, '->', rev[key])
~~~
{: .language-python}
~~~
1 -> one
2 -> two
3 -> three
~~~
{: .output}


> ## Cambiando diccionarios
>
> 1. Primero, imprime el valor de `rev` del diccionario en la pantalla.
> 2. Reasigna el segundo valor (parar el *par clave: valor*) para que ya no
> lea "dos" sino "manzana".
> 3. Imprime el valor de `rev` en la pantalla nuevamente y ve si el valor ha cambiado.
>
{: .challenge}


Es importante tener en cuenta que los diccionarios están "desordenados" y no recuerdan
la secuencia de sus elementos (es decir, el orden en el que los pares clave: valor fueron
añadidos al diccionario). Debido a esto, el orden en que los elementos son
devuelto en los bucles sobre los diccionarios, puede aparecer al azar e incluso puede cambiar
con el tiempo.


## Funciones

Definir una sección de código como una función en Python se hace utilizando la palabra clave `def`.
Por ejemplo, una función que tome dos argumentos y devuelve su suma
puede ser definida como:

~~~
def add_function(a, b):
    result = a + b
    return result

z = add_function(20, 22)
print(z)
~~~
{: .language-python}
~~~
42
~~~
{: .output}

{% include links.md %}
