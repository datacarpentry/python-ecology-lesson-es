---
title: Indexación, segmentación y creación de subconjuntos a partir de DataFrames en Python
teaching: 30
exercises: 30
questions:
    - "¿Cómo puedo acceder a un dato específico en mi 'dataset'?"
    - "¿Cómo pueden ayudarme Python y Pandas a analizar mis datos?"
objectives:
    - "Describir que es indexación en base-0."
    - "Manipular y extraer datos usando encabezados de columnas e índices."
    - "Usar 'slicing' para seleccionar conjuntos de datos de un 'DataFrame'."
    - "Emplear etiquetas e índices enteros para seleccionar rangos de datos en un 'DataFrame'."
    - "Reasignar valores dentro de subconjuntos de datos de un 'DataFrame'."
    - "Crear una copia de un 'DataFrame'."
    - "Consultar/Seleccionar un subconjunto de datos usando un conjunto de criterios utilizando los siguientes operadores: =, !=, >, <, >=, <=."
    - "Localizar subconjuntos de datos utilizando máscaras."
    - "Describir objetos tipo 'boolean' en Python y manipular datos usando 'booleans'."
keypoints:
    - "En Python, fragmentos de datos pueden ser accedidos usando índices, 'slices', encabezados de columnas, y subconjuntos basados en condiciones."
    - "Python usa indexación base-0, en la cual el primer elemento de una lista, tupla o cualquier otra structura de datos tiene un indice de 0."
    - "'Pandas' permite usar procedimientos comunes de exploración de datos como indexación de datos, 'slicing' y creación de subconjuntos basados en condiciones."
    
---

En la lección 01, leímos un archivo CSV y cargamos los datos en un  pandas **DataFrame**. 
Aprendimos:

- como guardar el **DataFrame** en un objeto,
- como realizar operaciones matemáticas básica sobre datos,
- como calcular resúmenes estadísticos, y
- como crear gráficos a partir de los datos.

En esta lección, exploraremos **formas de acceder a diferentes partes de los datos**
usando:

- indexación,
- segmentación, y
- creación de subconjuntos.

## Cargando nuestros datos

Vamos a continuar usando el dataset **surveys** que usamos con la lección
anterior. Reabrámoslo y leamos los datos de nuevo:

~~~
# Asegura que panda este disponible
import pandas as pd

# lee el archivo **surveys** CSV
surveys_df = pd.read_csv("data/surveys.csv")
~~~
{: .language-python}

## Indexando y Fragmentando en Python

A menudo necesitamos trabajar con subconjuntos de un objeto **DataFrame**. Existen diferentes 
maneras de lograr esto, incluyendo: usando etiquetas (encabezados de columnas), rangos numéricos, 
o índices de localizaciones específicas x,y.

## Seleccionando datos mediante el uso de Etiquetas (Encabezados de Columnas)

Utilizamos corchetes `[]` para seleccionar un subconjunto de un objeto en Python. Por ejemplo, 
podemos seleccionar todos los datos de una columna llamada `species_id`  del `surveys_df` **DataFrame** 
usando el nombre de la columna. Existen dos maneras de hacer esto:

~~~
# Sugerencia: usa el método .head() que vimos anteriormente para hacer la salida más corta
# Método 1: selecciona un 'subconjunto' de los datos usando el nombre de la columna
surveys_df['species_id']

# Método 2: usa el nombre de la columna como un 'atributo'; esto produce la misma salida
surveys_df.species_id
~~~
{: .language-python}

También podemos crear un nuevo objeto que contiene solamente los datos de la 
columna `species_id` de la siguiente manera:

~~~
# Crea un objeto, `surveys_species`, que solamente contenga la columna `species_id`
surveys_species = surveys_df['species_id']
~~~
{: .language-python}

También podemos pasar una lista de nombres de columnas, a manera de índice para seleccionar las columnas en ese orden. 
Esto es útil cuando necesitamos reorganizar nuestros datos.

**NOTA:** Si el nombre de una columna no esta incluido en el `DataFrame`, 
se producirá una excepción (error).

~~~
# Selecciona las especies y crea un gráfico con las columnas del **DataFrame**
surveys_df[['species_id', 'plot_id']]

# ¿Qué pasa cuando invertimos el orden?
surveys_df[['plot_id', 'species_id']]

# ¿Qué pasa si preguntamos por una columna que no existe?
surveys_df['speciess']
~~~
{: .language-python}

Python nos informa que tipo de error es en el rastreo, en la parte inferior dice `KeyError: 'speciess'` lo que significa 
que `speciess` no es un nombre de columna (o **Key** que está relacionado con el diccionario de tipo de datos de Python).

## Extrayendo subconjuntos basados en rangos: Segmentando

**RECORDATORIO**: Python usa Indexación en base-0

Recordemos que Python usa indexación en base-0.
Esto quiere decir que el primer elemento en un objeto esta localizado en la posición 0.
Esto es diferente de otros lenguajes como R y Matlab que indexan elementos dentro 
de objetos iniciando en 1.

~~~
# Crea una lista de números:
a = [1, 2, 3, 4, 5]
~~~
{: .language-python}

![indexing diagram](../fig/slicing-indexing.png)
![slicing diagram](../fig/slicing-slicing.png)


> ## Desafío - Extrayendo datos
>
> 1. ¿Qué valor devuelve el siguiente código?
>
>    ~~~
>    a[0]
>    ~~~
>    {: .language-python }
>
> 2. ¿Qué valor devuelve este?:
>
>    ~~~
>    a[5]
>    ~~~
>    {: .language-python }
>
> 3. En el ejemplo anterior, llamar a `a [5]` devuelve un error. ¿Por qué?
>
> 4. ¿Qué tal este?
>
>    ~~~
>    a[len(a)]
>    ~~~
>    {: .language-python }
{: .challenge}


## Segmentando Subconjuntos de Filas en Python

La segmentación utilizando el operador `[]` selecciona un conjunto de filas y/o columnas de 
un **DataFrame**. Para segmentar un conjunto de filas, usa la siguiente sintaxis: `data[start:stop]`. 
Cuando se hace segmentación en pandas, el límite inicial (**start**) se incluye en los datos de salida. 
El límite final (**stop**) es un paso MÁS ALLÁ de la fila que desea seleccionar. 
Así que si deseas seleccionar las filas 0, 1 y 2, tu código se vería así:

~~~
# Selecciona las filas 0, 1, 2 (la fila 3 no es seleccionada)
surveys_df[0:3]
~~~
{: .language-python}

El límite final en Python es diferente del que puedes estar acostumbrado a usar 
en Lenguajes como Matlab y R.

~~~
# Selecciona las primeras cinco filas (con índices 0, 1, 2, 3, 4)
surveys_df[:5]

# Selecciona el último elemento de la lista
# (el segmento comienza en el último elemento y finaliza al final de la lista)
surveys_df[-1:]
~~~
{: .language-python}

También podemos reasignar valores dentro de subconjuntos de nuestro **DataFrame**.

Pero antes de hacerlo, veamos la diferencia entre el concepto de copiar objetos y el 
concepto de referenciar objetos en Python.

## Copiar Objetos vs Referenciar Objetos en Python

Empecemos con un ejemplo:

~~~
# Usando el método 'copy()'
true_copy_surveys_df = surveys_df.copy()

# Usando el operador '='
ref_surveys_df = surveys_df
~~~
{: .language-python}

Puedes pensar que el código `ref_surveys_df = surveys_df` crea una copia nueva y 
distinta de objeto **DataFrame** `surveys_df`. Sin embargo, usar el operador `=` en 
una instrucción simple de la forma `y = x` **no** crea una copia de nuestro **DataFrame**. 
En lugar de esto, `y = x` crea una variable nueva `y` que hace referencia al **mismo** 
objeto al que `x` hace referencia. Para decirlo de otra manera, solamente hay **un** 
objeto (el **DataFrame**), y ambos objetos `x` y `y` hacen referencia a él.

En contraste, el método `copy()` de un **DataFrame** crea una copia verdadera del
**DataFrame**.

Veamos lo que sucede cuando reasignamos los valores dentro de un subconjunto del
**DataFrame** que hace referencia a otro objeto **DataFrame**:

~~~
# Asigna el valor `0` a las primeras tres filas de datos en el **DataFrame**
ref_surveys_df[0:3] = 0
~~~
{: .language-python}

Probemos el siguiente código:

~~~
# ref_surveys_df fue creado usando el operador '='
ref_surveys_df.head()

# surveys_df es el **DataFrame** original
surveys_df.head()
~~~
{: .language-python}

¿Cuál es la diferencia entre estos dos **DataFrames**?

Cuando asignamos a las tres primeras filas el valor de `0` usando el **DataFrame** `ref_surveys_df`,
el **DataFrame** `surveys_df` también es modificado. Recuerda que creamos el objeto `ref_survey_df` 
arriba usando la instrucción `ref_survey_df = surveys_df`. Por lo tanto `surveys_df` y `ref_surveys_df` hacen 
referencia exactamente al mismo objeto **DataFrame**. Si cualquiera de los dos objetos (`ref_survey_df`, `surveys_df`) 
es modificado, el otro objeto va a observar los mismos cambios.

**Revisar y Recapitular**:

- Para crear una **copia** de un objeto, usamos el método **copy()** de un `DataFrame`

  ~~~
  true_copy_surveys_df = surveys_df.copy()
  ~~~
  {: .language-python }
- Para crear una **referencia** a un objeto usamos el operador `=`

  ~~~
  ref_surveys_df = surveys_df
  ~~~
  {: .language-python }

Muy bien, hora de practicar. Vamos a crear un nuevo objeto `dataframe` a partir
del archivo CSV con los datos originales.

~~~
surveys_df = pd.read_csv("data/surveys.csv")
~~~
{: .language-python}

## Segmentando Subconjuntos de Filas y Columnas en Python

Podemos seleccionar subconjuntos de datos, contenidos en rangos específicos de filas y columnas,
usando etiquetas o indexación basada en números enteros.

- `loc` es usado principalmente para indexación basada en *etiquetas*. Permite usar *números enteros* pero
  son interpretados como una *etiqueta*.
- `iloc` es usado para indexación basada en *números enteros*

Para seleccionar un subconjunto de filas **y** columnas de nuestro objeto **DataFrame**, podemos usar
el método `iloc`. Por ejemplo, podemos seleccionar `month`, `day` y `year` (que corresponden a las columnas 2, 3
y 4 si empezamos a contar las columnas en 1) para las primeras tres filas, de la siguiente manera:

~~~
# iloc[segmentación de fila, segmentación de columna]
surveys_df.iloc[0:3, 1:4]
~~~
{: .language-python}

lo cual nos produce la siguiente **salida**

~~~
   month  day  year
0      7   16  1977
1      7   16  1977
2      7   16  1977
~~~
{: .output}

Ten en cuenta que pedimos un segmento de 0:3. Esto produjo 3 filas de datos. Cuando
pides un segmento de 0:3, le estas diciendo a **Python** que comience en el índice 0 y seleccione las filas
0, 1, 2 **hasta 3 pero sin incluir esta última**.

Exploremos otras maneras de indexar y seleccionar subconjuntos de datos:

~~~
# Selecciona todas las columnas para las filas con índices entre 0 y 10
surveys_df.loc[[0, 10], :]

# ¿Qué produce el la siguiente instrucción?
surveys_df.loc[0, ['species_id', 'plot_id', 'weight']]

# ¿Que pasa cuando ejecutas el siguiente código?
surveys_df.loc[[0, 10, 35549], :]
~~~
{: .language-python}

**NOTA**: Las etiquetas utilizadas deben estar incluidas en el **DataFrame** o se obtendrá un error de tipo `KeyError`.

Indexing by labels `loc` differs from indexing by integers `iloc`.
With `loc`, the both start bound and the stop bound are **inclusive**. When using
`loc`, integers *can* be used, but the integers refer to the
index label and not the position. For example, using `loc` and select 1:4
will get a different result than using `iloc` to select rows 1:4.

We can also select a specific data value using a row and
column location within the DataFrame and `iloc` indexing:

~~~
# Syntax for iloc indexing to finding a specific data element
dat.iloc[row, column]
~~~
{: .language-python}

In this `iloc` example,

~~~
surveys_df.iloc[2, 6]
~~~
{: .language-python}

gives the **output**

~~~
'F'
~~~
{: .output}

Remember that Python indexing begins at 0. So, the index location [2, 6]
selects the element that is 3 rows down and 7 columns over in the DataFrame.



> ## Challenge - Range
>
> 1. What happens when you execute:
>
>    - `surveys_df[0:1]`
>    - `surveys_df[:4]`
>    - `surveys_df[:-1]`
>
> 2. What happens when you call:
>
>    - `dat.iloc[0:4, 1:4]`
>    - `dat.loc[0:4, 1:4]`
>
> - How are the two commands different?
{: .challenge}


## Subsetting Data using Criteria

We can also select a subset of our data using criteria. For example, we can
select all rows that have a year value of 2002:

~~~
surveys_df[surveys_df.year == 2002]
~~~
{: .language-python}

Which produces the following output:

~~~
record_id  month  day  year  plot_id species_id  sex  hindfoot_length  weight
33320      33321      1   12  2002        1         DM    M     38      44
33321      33322      1   12  2002        1         DO    M     37      58
33322      33323      1   12  2002        1         PB    M     28      45
33323      33324      1   12  2002        1         AB  NaN    NaN     NaN
33324      33325      1   12  2002        1         DO    M     35      29
...
35544      35545     12   31  2002       15         AH  NaN    NaN     NaN
35545      35546     12   31  2002       15         AH  NaN    NaN     NaN
35546      35547     12   31  2002       10         RM    F     15      14
35547      35548     12   31  2002        7         DO    M     36      51
35548      35549     12   31  2002        5        NaN  NaN    NaN     NaN

[2229 rows x 9 columns]
~~~
{: .language-python}

Or we can select all rows that do not contain the year 2002:

~~~
surveys_df[surveys_df.year != 2002]
~~~
{: .language-python}

We can define sets of criteria too:

~~~
surveys_df[(surveys_df.year >= 1980) & (surveys_df.year <= 1985)]
~~~
{: .language-python}

### Python Syntax Cheat Sheet

Use can use the syntax below when querying data by criteria from a DataFrame.
Experiment with selecting various subsets of the "surveys" data.

* Equals: `==`
* Not equals: `!=`
* Greater than, less than: `>` or `<`
* Greater than or equal to `>=`
* Less than or equal to `<=`


> ## Challenge - Queries
>
> 1. Select a subset of rows in the `surveys_df` DataFrame that contain data from
>   the year 1999 and that contain weight values less than or equal to 8. How
>   many rows did you end up with? What did your neighbor get?
>
> 2. You can use the `isin` command in Python to query a DataFrame based upon a
>   list of values as follows:
>
>    ~~~
>    surveys_df[surveys_df['species_id'].isin([listGoesHere])]
>    ~~~
>    {: .language-python }
>
>   Use the `isin` function to find all plots that contain particular species
>   in the "surveys" DataFrame. How many records contain these values?
>
> 3. Experiment with other queries. Create a query that finds all rows with a
>   weight value > or equal to 0.
>
> 4. The `~` symbol in Python can be used to return the OPPOSITE of the
>   selection that you specify in Python. It is equivalent to **is not in**.
>   Write a query that selects all rows with sex NOT equal to 'M' or 'F' in
>   the "surveys" data.
{: .challenge}


# Using masks to identify a specific condition

A **mask** can be useful to locate where a particular subset of values exist or
don't exist - for example,  NaN, or "Not a Number" values. To understand masks,
we also need to understand `BOOLEAN` objects in Python.

Boolean values include `True` or `False`. For example,

~~~
# Set x to 5
x = 5

# What does the code below return?
x > 5

# How about this?
x == 5
~~~
{: .language-python}

When we ask Python what the value of `x > 5` is, we get `False`. This is
because the condition, `x` is not greater than 5, is not met since `x` is equal
to 5.

To create a boolean mask:

- Set the True / False criteria (e.g. `values > 5 = True`)
- Python will then assess each value in the object to determine whether the
  value meets the criteria (True) or not (False).
- Python creates an output object that is the same shape as the original
  object, but with a `True` or `False` value for each index location.

Let's try this out. Let's identify all locations in the survey data that have
null (missing or NaN) data values. We can use the `isnull` method to do this.
The `isnull` method will compare each cell with a null value. If an element
has a null value, it will be assigned a value of  `True` in the output object.

~~~
pd.isnull(surveys_df)
~~~
{: .language-python}

A snippet of the output is below:

~~~
      record_id  month    day   year plot_id species_id    sex  hindfoot_length weight
0         False  False  False  False   False      False  False   False      True
1         False  False  False  False   False      False  False   False      True
2         False  False  False  False   False      False  False   False      True
3         False  False  False  False   False      False  False   False      True
4         False  False  False  False   False      False  False   False      True

[35549 rows x 9 columns]
~~~
{: .language-python}

To select the rows where there are null values, we can use
the mask as an index to subset our data as follows:

~~~
# To select just the rows with NaN values, we can use the 'any()' method
surveys_df[pd.isnull(surveys_df).any(axis=1)]
~~~
{: .language-python}

Note that the `weight` column of our DataFrame contains many `null` or `NaN`
values. We will explore ways of dealing with this in Lesson 03.

We can run `isnull` on a particular column too. What does the code below do?

~~~
# What does this do?
empty_weights = surveys_df[pd.isnull(surveys_df['weight'])]['weight']
print(empty_weights)
~~~
{: .language-python}

Let's take a minute to look at the statement above. We are using the Boolean
object `pd.isnull(surveys_df['weight'])` as an index to `surveys_df`. We are
asking Python to select rows that have a `NaN` value of weight.


> ## Challenge - Putting it all together
>
> 1. Create a new DataFrame that only contains observations with sex values that
>   are **not** female or male. Assign each sex value in the new DataFrame to a
>   new value of 'x'. Determine the number of null values in the subset.
>
> 2. Create a new DataFrame that contains only observations that are of sex male
>   or female and where weight values are greater than 0. Create a stacked bar
>   plot of average weight by plot with male vs female values stacked for each
>   plot.
{: .challenge}

{% include links.md %}

