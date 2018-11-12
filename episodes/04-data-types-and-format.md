---
title: Tipos de datos y formatos
teaching: 20
exercises: 25
questions:
  - "¿Qué tipos de datos pueden estar contenidos en un DataFrame?"
  - "¿Por qué es importante el tipo de datos?"
objectives:
    - "Describir cómo se almacena la información en un DataFrame de Python."
    - "Definir los dos tipos de datos principales en Python: texto y numéricos."
    - "Examinar la estructura de un DataFrame."
    - "Modificar el formato de los valores en un DataFrame."
    - "Describir cómo los tipos de datos afectan a las operaciones."
    - "Definir, manipular e interconvertir integers y floats en Python."
    - "Analizar datasets que tienen valores faltantes/nulos (valores NaN)."
    - "Escribir datos manipulados a un archivo."
keypoints:
    - "FIXME"
---

El formato de columnas y filas individuales afectará el análisis realizado en
un dataset leído en Python. Por ejemplo, no se pueden realizar cálculos
matemáticos sobre una secuencia de caracteres (datos con formato de texto).
Esto puede parecer obvio, sin embargo, a veces en Python los valores numéricos
son leídos como secuencias de caracteres. En esta situación, cuando intentas
realizar cálculos con datos numéricos sobre datos formateados como secuencias
de caracteres, obtienes un error.

En esta lección repasaremos maneras de explorar y comprender mejor la
estructura y formato de nuestros datos.

# Tipos de Datos

La forma en que se almacena la información en un
DataFrame u objeto Python afecta a lo que podemos hacer con él y también a
los resultados de los cálculos. Hay dos tipos principales de datos
que estaremos explorando en esta lección: tipos de datos numéricos y de texto.

## Tipos de Datos Numéricos

Los tipos de datos numéricos incluyen enteros y números de punto flotante. Un número de
**punto flotante** (conocido como float) tiene puntos decimales incluso si
el valor del punto decimal es 0. Por ejemplo: 1.13, 2.0, 1234.345. Si tenemos
una columna que contiene tanto integers como floats, Pandas asignará el tipo
de dato float a toda la columna,de modo tal que los puntos decimales no se
pierdan.

Un ** integer ** nunca tendrá un punto decimal. Así, si quisiéramos almacenar
1.13 como un integer se almacenará como 1. Del mismo modo, 1234.345 se
almacenará como 1234. A menudo, en Python verás el tipo de dato `Int64`
que representa un integer de 64 bits. El 64 simplemente se refiere a la
memoria asignada para almacenar datos en cada celda; eso se refiere
a la cantidad de dígitos que puede efectivamente almacenar en cada "celda".
Asignar espacio antes de tiempo permite a las computadoras optimizar
el almacenamiento y hacer más eficiente el procesamiento.

## Tipo de Datos de Texto

En Python, el tipo de datos de texto se conoce como secuencia de caracteres.
En Pandas se los conoce como Objetos. Las secuencias de caracteres pueden
contener números y / o caracteres. Por ejemplo, una secuencia de caracteres
puede ser una palabra, una oración, o varias oraciones. Un objeto Pandas
también podría ser un nombre de gráfico como 'plot1'. Una secuencia de
caracteres también puede contener o consistir en números. Por ejemplo, '1234'
podría ser almacenado como una secuencia de caracteres. También '10 .23'
podría ser almacenado como secuencia de caracteres. Sin embargo **las
las secuencias de caracteres que contienen números no se pueden utilizar en
operaciones matemáticas**!


Pandas y Python básico utilizan nombres ligeramente diferentes para los tipos
de datos. Más sobre esto en la tabla de abajo:

| Tipo en Pandas | Tipo en Python Nativo | Descripción |
|----------------|-----------------------|-------------|
| object | string | El dtype más general. Será asignado a tu columna si la columna contiene tipos mixtos (números y secuencias de caracteres). |
| int64  | int | Caracteres numéricos. 64 se refiere a la memoria asignada para almacenar el caracter. |
| float64 | float | Caracteres numéricos con decimales. Si una columna contiene números y NaNs (ver más abajo), Pandas usará float64 por defecto, en caso de que los datos faltantes contengan decimales. |
| datetime64, timedelta[ns] | N/A (but see the [datetime] module in Python's standard library) | Values meant to hold time data. Look into these for time series experiments. |

[datetime]: http://doc.python.org/2/library/datetime.html


## Checking the format of our data

Now that we're armed with a basic understanding of numeric and text data
types, let's explore the format of our survey data. We'll be working with the
same `surveys.csv` dataset that we've used in previous lessons.

~~~
# Note that pd.read_csv is used because we imported pandas as pd
surveys_df = pd.read_csv("data/surveys.csv")
~~~
{: .language-python}

Remember that we can check the type of an object like this:

~~~
type(surveys_df)
~~~
{: .language-python}

**OUTPUT:** `pandas.core.frame.DataFrame`

Next, let's look at the structure of our surveys data. In pandas, we can check
the type of one column in a DataFrame using the syntax
`dataFrameName[column_name].dtype`:

~~~
surveys_df['sex'].dtype
~~~
{: .language-python}

**OUTPUT:** `dtype('O')`

A type 'O' just stands for "object" which in Pandas' world is a string
(text).

~~~
surveys_df['record_id'].dtype
~~~
{: .language-python}

**OUTPUT:** `dtype('int64')`

The type `int64` tells us that Python is storing each value within this column
as a 64 bit integer. We can use the `dat.dtypes` command to view the data type
for each column in a DataFrame (all at once).

~~~
surveys_df.dtypes
~~~
{: .language-python}

which **returns**:

~~~
record_id            int64
month                int64
day                  int64
year                 int64
plot_id              int64
species_id          object
sex                 object
hindfoot_length    float64
weight             float64
dtype: object
~~~
{: .language-python }

Note that most of the columns in our Survey data are of type `int64`. This means
that they are 64 bit integers. But the weight column is a floating point value
which means it contains decimals. The `species_id` and `sex` columns are objects which
means they contain strings.

## Working With Integers and Floats

So we've learned that computers store numbers in one of two ways: as integers or
as floating-point numbers (or floats). Integers are the numbers we usually count
with. Floats have fractional parts (decimal places).  Let's next consider how
the data type can impact mathematical operations on our data. Addition,
subtraction, division and multiplication work on floats and integers as we'd expect.

~~~
print(5+5)
10

print(24-4)
20
~~~
{: .language-python}

If we divide one integer by another, we get a float.
The result on Python 3 is different than in Python 2, where the result is an
integer (integer division).

~~~
print(5/9)
0.5555555555555556

print(10/3)
3.3333333333333335
~~~
{: .language-python}

We can also convert a floating point number to an integer or an integer to
floating point number. Notice that Python by default rounds down when it
converts from floating point to integer.

~~~
# Convert a to an integer
a = 7.83
int(a)
7

# Convert b to a float
b = 7
float(b)
7.0
~~~
{: .language-python}

# Working With Our Survey Data

Getting back to our data, we can modify the format of values within our data, if
we want. For instance, we could convert the `record_id` field to floating point
values.

~~~
# Convert the record_id field from an integer to a float
surveys_df['record_id'] = surveys_df['record_id'].astype('float64')
surveys_df['record_id'].dtype
~~~
{: .language-python}

**OUTPUT:** `dtype('float64')`


> ## Challenge - Changing Types
>
> Try converting the column `plot_id` to floats using
>
> ~~~
> surveys_df.plot_id.astype("float")
> ~~~
> {: .language-python}
>
> Next try converting `weight` to an integer. What goes wrong here? What is Pandas telling you?
> We will talk about some solutions to this later.
{: .challenge}

## Missing Data Values - NaN

What happened in the last challenge activity? Notice that this throws a value error:
`ValueError: Cannot convert NA to integer`. If we look at the `weight` column in the surveys
data we notice that there are NaN (**N**ot **a** **N**umber) values. **NaN** values are undefined
values that cannot be represented mathematically. Pandas, for example, will read
an empty cell in a CSV or Excel sheet as a NaN. NaNs have some desirable properties: if we
were to average the `weight` column without replacing our NaNs, Python would know to skip
over those cells.

~~~
surveys_df['weight'].mean()
42.672428212991356
~~~
{: .language-python}
Dealing with missing data values is always a challenge. It's sometimes hard to
know why values are missing - was it because of a data entry error? Or data that
someone was unable to collect? Should the value be 0? We need to know how
missing values are represented in the dataset in order to make good decisions.
If we're lucky, we have some metadata that will tell us more about how null
values were handled.

For instance, in some disciplines, like Remote Sensing, missing data values are
often defined as -9999. Having a bunch of -9999 values in your data could really
alter numeric calculations. Often in spreadsheets, cells are left empty where no
data are available. Pandas will, by default, replace those missing values with
NaN. However it is good practice to get in the habit of intentionally marking
cells that have no data, with a no data value! That way there are no questions
in the future when you (or someone else) explores your data.

### Where Are the NaN's?

Let's explore the NaN values in our data a bit further. Using the tools we
learned in lesson 02, we can figure out how many rows contain NaN values for
weight. We can also create a new subset from our data that only contains rows
with weight values > 0 (i.e., select meaningful weight values):

~~~
len(surveys_df[pd.isnull(surveys_df.weight)])
# How many rows have weight values?
len(surveys_df[surveys_df.weight> 0])
~~~
{: .language-python}

We can replace all NaN values with zeroes using the `.fillna()` method (after
making a copy of the data so we don't lose our work):

~~~
df1 = surveys_df.copy()
# Fill all NaN values with 0
df1['weight'] = df1['weight'].fillna(0)
~~~
{: .language-python}

However NaN and 0 yield different analysis results. The mean value when NaN
values are replaced with 0 is different from when NaN values are simply thrown
out or ignored.

~~~
df1['weight'].mean()
38.751976145601844
~~~
{: .language-python}

We can fill NaN values with any value that we chose. The code below fills all
NaN values with a mean for all weight values.

~~~
 df1['weight'] = surveys_df['weight'].fillna(surveys_df['weight'].mean())
~~~
{: .language-python}

We could also chose to create a subset of our data, only keeping rows that do
not contain NaN values.

The point is to make conscious decisions about how to manage missing data. This
is where we think about how our data will be used and how these values will
impact the scientific conclusions made from the data.

Python gives us all of the tools that we need to account for these issues. We
just need to be cautious about how the decisions that we make impact scientific
results.

> ## Challenge - Counting
> Count the number of missing values per column. Hint: The method .count() gives you
> the number of non-NA observations per column. Try looking to the .isnull() method.
{: .challenge}

## Writing Out Data to CSV

We've learned about using manipulating data to get desired outputs. But we've also discussed
keeping data that has been manipulated separate from our raw data. Something we might be interested
in doing is working with only the columns that have full data. First, let's reload the data so
we're not mixing up all of our previous manipulations.

~~~
surveys_df = pd.read_csv("data/surveys.csv")
~~~
{: .language-python}
Next, let's drop all the rows that contain missing values. We will use the command `dropna`.
By default, dropna removes columns that contain missing data for even just one row.

~~~
df_na = surveys_df.dropna()

~~~
{: .language-python}

If you now type `df_na`, you should observe that the resulting DataFrame has 30676 rows
and 9 columns, much smaller than the 35549 row original.

We can now use the `to_csv` command to do export a DataFrame in CSV format. Note that the code
below will by default save the data into the current working directory. We can
save it to a different folder by adding the foldername and a slash before the filename:
`df.to_csv('foldername/out.csv')`. We use 'index=False' so that
pandas doesn't include the index number for each line.

~~~
# Write DataFrame to CSV
df_na.to_csv('data_output/surveys_complete.csv', index=False)
~~~
{: .language-python}

We will use this data file later in the workshop. Check out your working directory to make
sure the CSV wrote out properly, and that you can open it! If you want, try to bring it
back into Python to make sure it imports properly.


## Recap

What we've learned:

+ How to explore the data types of columns within a DataFrame
+ How to change the data type
+ What NaN values are, how they might be represented, and what this means for your work
+ How to replace NaN values, if desired
+ How to use `to_csv` to write manipulated data to a file.

{% include links.md %}
