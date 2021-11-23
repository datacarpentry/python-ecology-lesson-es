---
title: Flujos de trabajo y automatización
teaching: 40
exercises: 50
questions:
    - "¿Puedo automatizar operaciones en Python?"
    - "¿Qué son las función y por qué debería usarlas?"
objectives:
    - "Describir por qué se usan los bucles en Python."
    - "Usar bucles for para automatizar el análisis de datos."
    - "Escribir nombres de archivo únicos en Python."
    - "Construir código reusable en Python."
    - "Escribir funciones usando condicionales (if, then, else)."
keypoints:
   - "Los bucles nos permiten repetir una serie de acciones un número dado de veces
    o mientras una condición es cierta."
   - "Podemos automatizar tareas que se deben repetir un número predefinido de veces
    utilizando bucles `for`."
   - "Una tarea de automatización típica en programación es generar secuencias de
    archivos con nombres distinos que siguen un patrón, esto se puede realizar
    fácilmente manipulando cadenas de caracteres con el nombre de los archivos
    dentro de bucles de repetición a medida que se van creando."
   - "Es conveniente definir funciones para establecer bloques de código reutilizables.
    Las funciones se pueden diseñar para que acepten argumentos de entradas para
    generalizar su funcionalidad y devolver distintos tipos de resultados."
   - "Las sentencias `if` permiten elegir cuales bloques de código ejecutar según según se cumplan o no distintas condiciones."
---

Hasta este momento, hemos usado Python y la librería Pandas para explorar y
manipular **datasets** a mano, tal y como lo haríamos en una planilla de cálculo.
Sin embargo la belleza de usar un lenguaje de programación como Python viene de
la posibilidad de automatizar el procesamiento de los datos a través del uso de
bucles y funciones.

## Bucles **for**

Los bucles nos permiten repetir un flujo de trabajo (o una serie de acciones)
cierto número dado de veces o mientras una condición es cierta. Podríamos
usar un bucle para procesar automáticamente la información que está contenida en
múltiples archivos (valores diarios con un archivo por año, por ejemplo). Los
bucles nos alivian nuestra tarea al hacer tareas repetitivas sin que tengamos que
involucrarnos directamente, y hace menos probable que introduzcamos errores al
equivocarnos mientras procesamos cada archivo manualmente.

Escribamos un bucle **for** sencillo que simule lo que un niño podría ver
durante una visita al zoológico:

~~~
animals = ['lion', 'tiger', 'crocodile', 'vulture', 'hippo']
print(animals)
~~~
{: .language-python}

~~~
['lion', 'tiger', 'crocodile', 'vulture', 'hippo']
~~~
{: .output}

~~~
for creature in animals:
    print(creature)
~~~
{: .language-python}

~~~
lion
tiger
crocodile
vulture
hippo
~~~
{: .output}

La línea que define el bucle debe comenzar con un **for** y terminar con el caracter dos
puntos, y el cuerpo del bucle debe estar indentado.

Eh este ejemplo, `creature` es la variable del bucle que toma el valor de la
siguiente entrada en `animals` cada vez que el bucle hace una iteración. Podemos
darle a la variable del bucle el nombre que querramos. Después que se termina el bucle,
la variable del bucle continuará existiendo y tendrá el valor de la última entrada en
la colección.

~~~
animals = ['lion', 'tiger', 'crocodile', 'vulture', 'hippo']
for creature in animals:
    pass
~~~
{: .language-python}

~~~
~~~
{: .output}

~~~
print('The loop variable is now: ' + creature)
~~~
{: .language-python}

~~~
The loop variable is now: hippo
~~~
{: .output}

Acá no le estamos pidiendo a Python que imprima el valor de la variable del
bucle, pero el bucle todavía corre y el valor de `creature` cambia en cada
iteración. La palabra clave `pass` en el cuerpo del bucle significa solamente
"no hagas nada".

> ## Desafío - **Bucles**
>
> 1. ¿Qué pasa si no incluimos la palabra clave `pass`?
>
> 2. Reescribe el bucle de tal forma que los animales estén separados por comas
>    y no por una línea nueva.
>    (Pista: Puedes concatenar cadenas de caracteres usando el signo más. Por
>    ejemplo, `print(string1 + string2)` resulta en 'string1string2').
{: .challenge}

## Automatizando el procesamiento de datos usando bucles **For**

El archivo que hemos estado usando hasta este momento, `surveys.csv`, contiene
25 años de información y es muy grande. Nos encantaría separar esta información
por años y guardar un archivo por cada año.

Comencemos por crear un nuevo directorio en nuestra carpeta `data` para guardar
todos estos archivos usando el módulo `os`

~~~
import os

os.mkdir('data/yearly_files')
~~~
{: .language-python}

El comando `os.mkdir` es equivalente a escribir `mkdir` en la terminal. Solo
para estar seguros, podemos verificar que nuestro nuevo directorio fue creado en
la carpeta `data`:

~~~
os.listdir('data')
~~~
{: .language-python}
~~~
['plots.csv',
 'portal_mammals.sqlite',
 'species.csv',
 'survey2001.csv',
 'survey2002.csv',
 'surveys.csv',
 'surveys2002_temp.csv',
 'yearly_files']
~~~
{: .output}

El comando `os.listdir` es equivalente a usar `ls` en la terminal.

En episodios anteriores, vimos cómo usar la librería Pandas para cargar
en memoria, a través de **DataFrame**,  información sobre las especies; vimos cómo
seleccionar un subconjunto de esos datos usando ciertos criterios, y vimos
también cómo escribir esa información en un archivo CSV. Escribamos un
**script** que realiza esos tres pasos en secuencia para el año 2002:

~~~
import pandas as pd

# Cargamos los datos en un DataFrame
surveys_df = pd.read_csv('data/surveys.csv')

# Seleccionamos solo los datos del año 2002
surveys2002 = surveys_df[surveys_df.year == 2002]

# Escribimos el nuevo DataFrame en un archivo CSV
surveys2002.to_csv('data/yearly_files/surveys2002.csv')
~~~
{: .language-python}

Para crear los archivos con los datos anuales, podemos repetir estos últimos dos
comandos una y otra vez, una vez por cada año de información. Sin embargo, repetir
código no es ni elegante ni práctico, y hace muy probable que introduzcamos
errores en nuestro código. Queremos convertir lo que acabamos de escribir en un
bucle que repita estos últimos dos comandos para cada año en nuestro **dataset**.

Comencemos con un bucle que solamente imprima los nombres de los archivos que
queremos crear - El dataset que estamos usando va desde 1977 hasta 2002, y vamos
a crear un archivo por separado para cada año. Listar los nombres de los archivos
es una buena estrategia, porque así podemos confirmar que nuestro bucle se
está comportando como esperamos.

Hemos visto que podemos iterar sobre una lista de elementos, entonces necesitamos una lista de años sobre la cual iterar. Podemos obtener los años en nuestro **DataFrame** con:

~~~
surveys_df['year']
~~~
{: .language-python}
~~~
0        1977
1        1977
2        1977
3        1977
         ...
35545    2002
35546    2002
35547    2002
35548    2002
~~~
{: .output}

pero queremos solamente años únicos, y esto lo podemos obtener usando el método
`unique` que ya hemos visto.

~~~
surveys_df['year'].unique()
~~~
{: .language-python}
~~~
array([1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984, 1985, 1986, 1987,
       1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998,
       1999, 2000, 2001, 2002], dtype=int64)
~~~
{: .output}

Escribiendo esto en un bucle **for** obtenemos

~~~
for year in surveys_df['year'].unique():
   filename='data/yearly_files/surveys' + str(year) + '.csv'
   print(filename)
~~~
{: .language-python}
~~~
data/yearly_files/surveys1977.csv
data/yearly_files/surveys1978.csv
data/yearly_files/surveys1979.csv
data/yearly_files/surveys1980.csv
data/yearly_files/surveys1981.csv
data/yearly_files/surveys1982.csv
data/yearly_files/surveys1983.csv
data/yearly_files/surveys1984.csv
data/yearly_files/surveys1985.csv
data/yearly_files/surveys1986.csv
data/yearly_files/surveys1987.csv
data/yearly_files/surveys1988.csv
data/yearly_files/surveys1989.csv
data/yearly_files/surveys1990.csv
data/yearly_files/surveys1991.csv
data/yearly_files/surveys1992.csv
data/yearly_files/surveys1993.csv
data/yearly_files/surveys1994.csv
data/yearly_files/surveys1995.csv
data/yearly_files/surveys1996.csv
data/yearly_files/surveys1997.csv
data/yearly_files/surveys1998.csv
data/yearly_files/surveys1999.csv
data/yearly_files/surveys2000.csv
data/yearly_files/surveys2001.csv
data/yearly_files/surveys2002.csv
~~~
{: .output}

Ahora podemos agregar el resto de pasos que necesitamos para crear archivos
separados:

~~~
# Load the data into a DataFrame
surveys_df = pd.read_csv('data/surveys.csv')

for year in surveys_df['year'].unique():

    # Select data for the year
    surveys_year = surveys_df[surveys_df.year == year]

    # Write the new DataFrame to a CSV file
    filename = 'data/yearly_files/surveys' + str(year) + '.csv'
    surveys_year.to_csv(filename)
~~~
{: .language-python}

Mira dentro del directorio `yearly_files` y verifica un par de los archivos que
acabaste de crear para confirmar que todo funcionó como esperabas.

## Escribiendo nombres de archivo únicos

Nota que en el código anterior creamos un nombre de archivo único para cada año.

~~~
filename = 'data/yearly_files/surveys' + str(year) + '.csv'
~~~
{: .language-python}

Descompongamos las partes de este nombre:

* La primera parte es simplemente un texto que especifica el directorio en el que
  vamos a guardar nuestro archivo (data/yearly_files/) y la primera parte del
  nombre del archivo (surveys): `'data/yearly_files/surveys'`
* Podemos concatenar esto con el valor de una variable, en este caso `year`, al
  usar el signo más y la variable que le queremos añadir al nombre del archivo:
  `+ str(year)`
* Por último añadimos la extensión del archivo usando otra cadena de caracteres:
  `+ '.csv'`

Nota que usamos comillas sencillas para añadir las cadenas de caracteres y que la
variable no está entre comillas. Este código produce la cadena de caracteres
`data/yearly_files/surveys2002.csv` que contiene tanto el **path** como el
nombre del archivo.

> ## Desafío - Modificando bucles
>
> 1. Algunas de las encuestas que guardaste tienen datos faltantes (tienen valores
>    nulos que salen como `NaN` - No es un número (en inglés) - en los DataFrames
>    y no salen en los archivos de texto). Modifica el bucle **for** para que las
>    entradas que tengan valores nulos no sean incluidas en los archivos anuales.
>
> 2. Supongamos que solo quieres revisar los datos cada cierto múltiplo de años.
>    ¿Cómo modificarías el bucle para generar un archivo de datos cada cinco
>    años comenzando desde 1977?
>
> 3. En vez de separar la información por años, un colega tuyo quiere hacer el
>    análisis separando por especies. ¿Cómo escribirías un único archivo CSV
>    por cada especie?
{: .challenge}

## Construyendo código modular y reusable usando funciones

Supón que separar archivos enormes en archivos anuales individuales es una tarea
que tenemos que realizar frecuentemente. Podríamos escribir un bucle **for**
como el que hicimos arriba cada vez que lo necesitemos, pero esto tomaría
mucho tiempo y podría introducir errores en el código. Una solución más elegante
sería crear una herramienta reusable que realice esta tarea con el mínimo
esfuerzo del usuario. Para hacerlo, vamos a convertir el código que ya
escribimos en una función.

Las funciones son piezas de código reusable y autónomo que pueden ser
llamadas mediante un solo comando. Están diseñadas para aceptar argumentos como
entrada y retornar valores, pero no necesitan hacerlo necesariamente. Las
variables declaradas adentro de las funciones solo existen mientras la función
se está ejecutando, y si una variable adentro de una función (una variable
local) tiene el mismo nombre de otra variable en alguna parte del código, la
variable local no sobrescribe a la otra.

Todo método usado en Python (como por ejemplo `print`) es una función, y las
librerías que importamos (`pandas`, por ejemplo) son una colección de funciones.
Solo usaremos las funciones que están contenidas en el mismo código que las
usan, pero es sencillo también escribir funciones que puedan ser usadas por
programas diferentes.

Las funciones se declaran usando la siguiente estructura general:

~~~
def this_is_the_function_name(input_argument1, input_argument2):

    # El cuerpo de la función está indentado
    # Esta función imprime los dos argumentos en pantalla
    print('The function arguments are:', input_argument1, input_argument2, '(this is done inside the function!)')

    # And returns their product
    return input_argument1 * input_argument2
~~~
{: .language-python}

La declaración de la función comienza con la palabra clave `def`, seguida del
nombre de la función y los argumentos entre paréntesis, y termina con un dos
puntos. El cuerpo de la función está indentado justo como ocurría con los
bucles. Si la función retorna algo al ser llamada, entonces incluimos la palabra
clave `return` al final.

Así es como llamamos a la función:

~~~
product_of_inputs = this_is_the_function_name(2,5)
~~~
{: .language-python}

~~~
The function arguments are: 2 5 (this is done inside the function!)
~~~
{: .output}

~~~
print('Their product is:', product_of_inputs, '(this is done outside the function!)')
~~~
{: .language-python}

~~~
Their product is: 10 (this is done outside the function!)
~~~
{: .output}

> ## Desafío - Funciones
>
> 1. Cambia los valores de los argumentos en la función y mira su salida.
> 2. Intenta llamar a la función usando la cantidad equivocada de argumentos
>    (es decir, diferente de 2) o sin asignar la llamada de la función a una
>    variable (sin poner `product_of_inputs =`).
> 3. Declara una variable dentro de una función y prueba a encontrar en dónde
>    existe (Pista: ¿puedes imprimirla desde fuera de la función?)
> 4. Explora qué sucede cuando una variable tiene el mismo nombre adentro y
>    afuera de la función. ¿Qué le ocurre a la variable global cuando cambias el
>    valor de la variable local?
{: .challenge}

Ahora podemos convertir el código para guardar archivos con datos anuales en una
función. Hay muchas "partes" de este código que podemos convertir en funciones,
y podríamos inclusive crear funciones que llaman a otras funciones adentro de
ellas. Comencemos escribiendo una función que separa los datos para un año y los
guarda en un archivo:

~~~
def one_year_csv_writer(this_year, all_data):
    """
    Escribe un archivo csv con los datos para un año dado.

    this_year --- el año del que vamos a extraer los datos
    all_data --- DataFrame con datos de múltiples años
    """

    # Seleccionamos los datos para el año
    surveys_year = all_data[all_data.year == this_year]

    # Escribimos el nuevo DataFrame a un archivo csv
    filename = 'data/yearly_files/function_surveys' + str(this_year) + '.csv'
    surveys_year.to_csv(filename)
~~~
{: .language-python}

El texto que está entre los dos grupos de tres comillas dobles se llama el
**docstring** y contiene la documentación de la función. No hace nada al
ejecutar la función y por tanto no es necesario, pero es una excelente práctica
incluir docstrings para recordar y explicar qué hace el código. Los docstrings
en las funciones también se vuelven parte de la documentación "oficial":

~~~
one_year_csv_writer?
~~~
{: .language-python}

~~~
one_year_csv_writer(2002, surveys_df)
~~~
{: .language-python}

Cambiamos el nombre del archivo CSV para diferenciarlo del que escribimos
anteriormente. Busca en el directorio `yearly_files` el archivo que creamos.
¿Hizo la función lo que esperabas que hiciera?

Sin embargo, lo que nos encantaría hacer es crear archivos para múltiples años
sin tener que pedirlos uno a uno. Escribamos otra función que reemplace el bucle
**for** simplemente iterando a través de la secuencia de años y llamando repetidamente a la
función que acabamos de escribir, `one_year_csv_writer`:


~~~
def yearly_data_csv_writer(start_year, end_year, all_data):
    """
    Escribe archivos CSV separados para cada año de datos.

    start_year --- el primer año de datos que queremos
    end_year --- el último año de datos que queremos
    all_data --- DataFrame con datos de varios años
    """

    # "end_year" es el último año que queremos extraer, entonces iteramos hasta end_year+1
    for year in range(start_year, end_year+1):
        one_year_csv_writer(year, all_data)
~~~
{: .language-python}

Como la gente esperará naturalmente que el año final (`end_year`) sea el último,
el bucle **for** adentro de la función termina en `end_year + 1`. Al escribir el
bucle entero en la función, hemos hecho una herramienta reusable para cuando
necesitemos partir un archivo de datos grande en archivos anuales. Como podemos
especificar el primer y el último año para los cuales queremos crear archivos,
podemos inclusive usar esta función para crear archivos para un subconjunto de
los años disponibles. Así llamaríamos la función:

~~~
# Cargamos los datos en un DataFrame
surveys_df = pd.read_csv('data/surveys.csv')

# Creamos los archivos CSV
yearly_data_csv_writer(1977, 2002, surveys_df)
~~~
{: .language-python}

¡TEN CUIDADO! Si estás usando Jupyter Notebooks y estás modicando la función,
DEBES volver a ejecutar la celda para que la función cambiada esté disponible
para el resto del código. Nada cambiará visualmente cuando hagas esto, porque
definir una función sin *ejecutarla* no produce ninguna salida. Toda otra celda
que use la función (ahora cambiada) también tendrá que ser re-ejecutada para
cambiar su salida.

> ## Challenge- Más funciones
>
> 1. Añade dos argumentos a las funciones que escribimos que tomen el **path**
>    del directorio donde los archivos serán escritos y el root del nombre del
>    archivo. Crea un nuevo conjunto de archivos con un nombre diferente en un
>    directorio diferente.
> 2. ¿Cómo podrías usar la función `yearly_data_csv_writer` para crear un archivo
>    CSV para solo un año? (Pista: piensa sobre la sintaxis para `range`)
> 3. Haz que las funciones retornen una lista de los archivos que escribieron.
>    Hay muchas formas en las que puedes hacer esto (¡y deberías intentarlas
>    todas!): cualquiera de las dos funciones podría imprimir algo en pantalla,
>    cualquiera podría usar `return` para retornar números o cadenas de
>    caracteres cada vez que se llaman, o podrías hacer una combinación de estas
>    dos estrategias. Podrías también intentar usar la librería `os` para listar
>    los contenidos de directorios.
> 4. Explora qué sucede cuando las variables son declaradas dentro de cada una
>    de las funciones versus en el cuerpo principal de tu código (lo que está
>    sin indentar). ¿Cuál es el alcance de las variables (es decir, dónde son
>    visibles)?, ¿qué ocurre si tienen el mismo nombre pero valores diferentes?
{: .challenge}

Las funciones que escribimos exigen que les demos un valor para cada argumento.
Idealmente, nos gustaría que estas funciones fuesen tan flexibles e
independientes como fuera posible. Modifiquemos la función
`yearly_data_csv_writer` para que `start_year` y `end_year` sean por defecto el
rango completo de los datos si no son dados por el usuario. Se le pueden asignar
a los argumentos valores por defecto usando el signo igual a la hora de declarar
la función. Todos los argumentos en la función que no tengan un valor por
defecto (como aquí `all_data`) serán argumentos requeridos y DEBERÁN ir antes de
los argumentos que tengan valores por defecto (y que son opcionales al llamar la
función).

~~~
def yearly_data_arg_test(all_data, start_year = 1977, end_year = 2002):
    """
    Modificación de yearly_data_csv_writer para probar argumentos con valores
    por defecto!

    start_year --- el primer año de datos que queremos --- por defecto: 1977
    end_year --- el último año de datos que queremos --- por defecto: 2002
    all_data --- DataFrame con datos de varios años
    """

    return start_year, end_year


start,end = yearly_data_arg_test (surveys_df, 1988, 1993)
print('Both optional arguments:\t', start, end)

start,end = yearly_data_arg_test (surveys_df)
print('Default values:\t\t\t', start, end)
~~~
{: .language-python}

~~~
Both optional arguments:	1988 1993
Default values:		1977 2002
~~~
{: .output}

Los "\t" en `print` son tabulaciones, y son usadas para alinear el texto y
facilitar la lectura.

Pero ¿qué sucede si nuestro **dataset** no comienza en 1977 ni termina en 2002?
Podemos modificar la función de tal forma que ella misma mire cuál es el primer
y cuál es el último año si estos argumentos no son provistos por el usuario:

~~~
def yearly_data_arg_test(all_data, start_year = None, end_year = None):
    """
    Modificación de yearly_data_csv_writer para probar argumentos con valores
    por defecto!

    start_year --- el primer año de datos que queremos --- por defecto: None - revisar all_data
    end_year --- el último año de datos que queremos --- por defecto: None - revisar all_data
    all_data --- DataFrame con datos de varios años
    """

    if start_year is None:
        start_year = min(all_data.year)
    if end_year is None:
        end_year = max(all_data.year)

    return start_year, end_year


start,end = yearly_data_arg_test (surveys_df, 1988, 1993)
print('Both optional arguments:\t', start, end)

start,end = yearly_data_arg_test (surveys_df)
print('Default values:\t\t\t', start, end)
~~~
{: .language-python}
~~~
Both optional arguments:	1988 1993
Default values:		1977 2002
~~~
{: .output}

Ahora los valores por defecto de los argumentos `start_year` y `end_year` en la
función `yearly_data_arg_test` son `None`. Esta es una constante incorporada en
Python que indica la ausencia de un valor - esencialmente indica que la variable
existe en el directorio de nombres de variables (el **namespace**) de la función pero que
no corresponde a ningún objeto existente.

> ## Challenge - Variables
>
> 1. ¿Qué tipo de objeto corresponde a una variable declarada como `None`?
>    (Pista: crea una variable con el valor `None` y usa la función `type()`)
>
> 2. Compara el comportamiento de la función `yearly_data_arg_test` cuando los
>    argumentos tienen `None` como valor por defecto y cuando no tienen valores
>    por defecto.
>
> 3. ¿Qué ocurre si solo incluimos un valor para `start_year` al llamar a la función?,
>    ¿puedes escribir una llamada a la función con solo un valor para `end_year`?
>    (Pista: piensa en cómo la función debe estar asignándole valores a cada uno
>    de sus argumentos - ¡esto está relacionado con la necesidad de poner los
>    argumentos que no tienen valores por defecto antes de los que sí tienen
>    valores por defecto en la definición de la función!)
{: .challenge}

## Sentencias **if**

El cuerpo de la función anterior ahora tiene dos condicionales **if** que
revisan los valores de `start_year` y `end_year`. Los condicionales if ejecutan
un segmento de código si una condición dada es cierta. Usualmente lucen así:

~~~
a = 5

if a<0:  # ¿es cierta esta primera condición?

    # si a ES menor que cero
    print('a is a negative number')

elif a>0:  # La primera condición no es cierta, ¿la segunda?

    # si a NO ES menor que cero y ES mayor que cero
    print('a is a positive number')

else:  # No se cumplieron las dos condiciones

    # si a NO ES menor que cero y NO ES mayor que cero
    print('a must be zero!')
~~~
{: .language-python}

lo cual retornaría:

~~~
a is a positive number
~~~
{: .output}

Cambia los valores de `a` para ver cómo funciona este código. La palabra clave
`elif` significa "sino" (en inglés, "else if"), y todos los condicionales deben
terminar con un dos puntos.

Los condicionales if en la función `yearly_data_arg_test` verifican si hay algún
objeto asociado a los nombres `start_year` y `end_year`. Si estas variables son
`None`, los condicionales if retornan el booleano `True` y ejecutan cualquier
cosa que esté en su cuerpo. Por otra parte, si los nombres están asociados a
algún valor (es decir, recibieron un número al ser llamada la función), los
condicionales if retornarán `False` y no ejecutan su cuerpo. El condicional
opuesto, que retornaría `True` si las variables estuvieran asociadas con
objetos (es decir, si hubieran recibido valores al llamarse la función), sería
`if start_year` y `if end_year`.

Tal y como la hemos escrito hasta este momento, la función
`yearly_data_arg_test` asocia los valores que le pasamos cuando la llamamos con
los argumentos en la definición de la función solo basados en su orden. Si la
función recibe solo dos valores al ser llamada, el primero será asociado con
`all_data` y el segundo con `start_year`, sin importar cuál era nuestra
intención. Podemos solucionar este problema al llamar la función usando
argumentos **keyword**, en donde cada uno de los argumentos en la definición de
la función está asociado con una **keyword** y al llamar la función pasamos
valores a los parámetros usando estas keywords:

~~~
start,end = yearly_data_arg_test (surveys_df)
print('Default values:\t\t\t', start, end)

start,end = yearly_data_arg_test (surveys_df, 1988, 1993)
print('No keywords:\t\t\t', start, end)

start,end = yearly_data_arg_test (surveys_df, start_year = 1988, end_year = 1993)
print('Both keywords, in order:\t', start, end)

start,end = yearly_data_arg_test (surveys_df, end_year = 1993, start_year = 1988)
print('Both keywords, flipped:\t\t', start, end)

start,end = yearly_data_arg_test (surveys_df, start_year = 1988)
print('One keyword, default end:\t', start, end)

start,end = yearly_data_arg_test (surveys_df, end_year = 1993)
print('One keyword, default start:\t', start, end)
~~~
{: .language-python}
~~~
Default values:		1977 2002
No keywords:		1988 1993
Both keywords, in order:	1988 1993
Both keywords, flipped:	1988 1993
One keyword, default end:	1988 2002
One keyword, default start:	1977 1993
~~~
{: .output}

> ## Desafío - Modificando funciones
>
> 1. Reescribe las funciones `one_year_csv_writer` y `yearly_data_csv_writer`
>    para que tengan argumentos keyword con valores por defecto.
>
> 2. Modifica las funciones de tal forma que no creen archivos para un año si
>    éste no está en los datos y que muestre una alerta al usuario (Pista: usa
>    condicionales para esto. Si quieres un reto más, ¡usa `try`!)
>
> 3. Este código verifica si un directorio existe, sino lo crea. Añade un poco
>    de código a la función que escribe los archivos CSV para verificar si
>    existe el directorio al que piensas escribir.
>
> ~~~
>if 'dir_name_here' in os.listdir('.'):
>    print('Processed directory exists')
>else:
>    os.mkdir('dir_name_here')
>    print('Processed directory created')
> ~~~
> {: .language-python }
>
> 4. El código que has escrito hasta este momento usando el bucle **for** está
>    bastante bien, pero no necesariamente es reproducible con **datasets**
>    diferentes. Por ejemplo, ¿qué pasa con el código si tenemos datos para más
>    años? Usando las herramientas que aprendiste en las actividades anteriores,
>    crea una lista de todos los años representados en los datos. Después crea
>    un bucle para procesar tu información, comenzando desde el primer año y
>    terminando en el último usando la lista.
>    (Pista: puedes crear un bucle con la lista así: `for years in year_list:`)
{: .challenge}

{% include links.md %}
