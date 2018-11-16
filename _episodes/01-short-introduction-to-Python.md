---
title: Leve Introcducción a Programar en Python
teaching: 0
exercises: 0
questions:
    - "¿Qué es Python?"
    - "¿Por qué debo aprender Python?"
objectives:
     - "Describir las ventajas de utilizar programación en vez de llevar a cabo tareas repetitivas a mano."
    - "Definir los siguientes tipos de datos en Python: **strings, integers, and floats**."
    - "Llevar a cabo operaciones matemáticas en Python utilizando operadores básicos."
    - "Definir los siguientes términos en cómo se relacionan a Python: **lists, tuples, and dictionaries**."
keypoints:
    - "FIXME"
---

## Interpreter

Python es un lenguaje interpretado (**interpreted language**) que se puede utilizar de dos maneras:

* "Interactivamente": cuando lo utilizas como si fuera una “calculadora avanzada”, ejecutando un comando a la vez. Para empezar a usar Python de este modo, ejecuta `python` en la línea de comandos

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

Los tres símbolos de mayor que `>>>`, indican que Python está esperando una interacción con el usuario. Es decir que está esperando por tu **input**

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

* A modo de **Scripting**: se ejecutan una serie de “comandos” guardados en un archivo de texto. Normalmente estos archivos tienen `.py` al final de su nombre: 
~~~
$ python my_script.py
~~~
{: .language-bash}

~~~
Hello World
~~~
{: .output}

## Introduction to Python built-in data types

### Strings, integers, and floats

Una de las cosas más básicas que podemos hacer en Python es asignar valores a variables:

~~~
text = "Data Carpentry"  # An example of a string
number = 42  # An example of an integer
pi_value = 3.1415  # An example of a float
~~~
{: .language-python}

Aquí le hemos asignado datos a las variables  `text`, `number` y `pi_value`,
utilizando el operador de asignar `=`. Para revisar el valor de una variable, podemos escribir el nombre de la variable en el interpretador y presionar <kbd>Return</kbd>:

~~~
text
~~~
{: .language-python}
~~~
"Data Carpentry"
~~~
{: .output}

Todo en Python tiene un tipo. Para poder saber el tipo de una variable, la podemos pasar por la función incorporada `type`:

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

La variable `text` es un tipo de `str`, lo cual es **"string"** acortado. Los **strings** contienen secuencias de caracteres y las mismas pueden ser letras, números, símbolos de puntuación o incluso otras formas de texto más extravagantes (¡incluso emoji!). 

Podemos también ver el valor de algo utilizando otra función incorporada, `print`:

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

Esto pudiera parecer redundante, sin embargo es la única manera de demostrar en pantalla el **output** de un **script**:

*example.py*
~~~
# A Python script file
# Comments in Python start with #
# The next line assigns the string "Data Carpentry" to the variable "text".
text = "Data Carpentry"

# The next line does nothing!
text

# The next line uses the print function to print out the value we assigned to "text"
print(text)
~~~
{: .language-python}

*Running the script*
~~~
$ python example.py
~~~
{: .language-bash}

~~~
Data Carpentry
~~~
{: .output}

Note que **“Data Carpentry”** se “imprime” solo una vez.

**Tip**: `print` y `type` son funciones incorporadas de Python. Más tarde en esta lección vamos a presentar métodos y funciones definidas por el usuario. La documentación de Python es una referencia excelente para ver la diferencia entre ellos.
### Operators

Podemos llevar a cabo cálculos matemáticos en Python utilizando operadores básicos
 `+, -, /, *, %`:

~~~
2 + 2  # Addition
~~~
{: .language-python}

~~~
4
~~~
{: .output}

~~~
6 * 7  # Multiplication
~~~
{: .language-python}
~~~
42
~~~
{: .output}
~~~
2 ** 16  # Power
~~~
{: .language-python}
~~~
65536
~~~
{: .output}
~~~
13 % 5  # Modulo
~~~
{: .language-python}
~~~
3
~~~
{: .output}

También podemos utilizar operadores lógicos y de comparación:
`<, >, ==, !=, <=, >=` además de enunciados de identidad, tales como
`and, or, not`. El tipo de dato devuelto por estas operaciones son _boolean_.


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

## Sequences: Lists and Tuples

### Lists

**Lists** Son una estructura de datos común que contienen una secuencia ordenada de elementos. Cada elemento puede ser accesado por medio de un índice. Note que en Python los índices empiezan en 0 y no en 1:
~~~
numbers = [1, 2, 3]
numbers[0]
~~~
{: .language-python}
~~~
1
~~~
{: .output}

Un `for` loop puede ser utilizado para accesar los elementos en una lista o en otras estructuras de datos en Python de manera individual:
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

**Indentation** Es importante en Python. Observe que en la segunda línea del ejemplo anterior hay sangría. 
De la misma manera que los tres símbolos de mayor que `>>>`, indican interacción, los tres puntos `...` le dicen a Python que hay varias líneas. De esta manera Python marca los bloques de código. [Ojo: Tu no escribes `>>>` o `...`]

Para añadir elementos al final de una lista podemos utilizar el método de `append`. Métodos son una manera de interactuar con un objeto (por ejemplo una lista). Podemos llamar un método utilizando un punto `.` seguido del nombre del método y una lista de argumentos en paréntesis. Veamos un ejemplo utilizando `append`:

~~~
numbers.append(4)
print(numbers)
~~~
{: .language-python}

~~~
[1, 2, 3, 4]
~~~
{: .output}

Para saber qué métodos están disponibles en un objeto podemos utilizar la función integrada `help`:
~~~
help(numbers)

Help on list object:

class list(object)
 |  list() -> new empty list
 |  list(iterable) -> new list initialized from iterable's items
 ...
~~~
{: .output}

### Tuples

Una tupla es similar a una lista en el sentido que ambas son una secuencia de elementos ordenados. Sin embargo las tuplas no pueden ser alteradas una vez que se crean (son “inmutables”). Las tuplas se crean escribiendo valores separados por comas dentro de paréntesis`()`.  

~~~
# Tuples use parentheses
a_tuple = (1, 2, 3)
another_tuple = ('blue', 'green', 'red')

# Note: lists use square brackets
a_list = [1, 2, 3]
~~~
{: .language-python}

> ## Tuples _vs._ Lists
> 1. ¿Qué ocurre cuando ejecutas `a_list[1] = 5` ?
> 2. ¿Qué ocurre cuando ejecutas `a_tuple[2] = 5`?
> 3. ¿Qué te dice`type(a_tuple)` acerca de `a_tuple`?
>
{: .challenge}


## Dictionaries

Un **dictionary** Es un contenedor que aguanta un par de objetos - **keys** y valores.

~~~
translation = {'one': 1, 'two': 2}
translation['one']
~~~
{: .language-python}
~~~
1
~~~
{: .output}

Los **dictionaries** funcionan de manera similar a las listas - con la excepción de que su índices son **keys**. Los **keys** son una forma de identificar de manera única a un conjunto de valores de un **dictionary**. Solo algunos tipos de datos pueden ser **keys** ya que deben ser **“hashable”**. Los **strings** y los tipos numéricos son aceptados como **keys**, sin embargo los **list** no.
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

En Python un **“Traceback”** es un código de error en varias líneas que se muestra al usuario. 

Para añadir información a un **dictionary**, le asignamos un valor a un **key** nuevo:

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

Utilizar `for` loops en un **dictionary** es más complejo. Hay dos maneras en las que podemos utilizarlos.
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

or

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

> ## Changing dictionaries
>
> 1. Primero haga **print** al valor del **dictionary** `rev` a la pantalla.
> 2. Reasigne el segundo valor (en el **key value pair**) de tal manera que ya no lea **“two”** y en vez lea **“apple-sauce”**.
> 3. Dele **print** al valor de `rev` a la pantalla nuevamente y observe si a cambiado el valor.
>
>
{: .challenge}

Es importante resaltar que los **dictionaries** no son ordenados y no se acuerdan la secuencia de información (es decir, el orden en el que se añadió cada entrada al **dictionary**). Debido a esto, el orden en el que las entradas son devueltas de los **loops**, desde los **dictionaries** pudiera parecer aleatorio e incluso pusieran cambiar con el tiempo. 


## Functions

La manera en la que se define una sección de código como función en Python es utilizando la palabra clave `def`. Por ejemplo, una función que toma dos argumentos y devuelve su suma puede ser definido de la siguiente manera:
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

