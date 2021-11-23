---
title: Tipos de datos y formatos
teaching: 20
exercises: 25
questions:
  - "¿Qué tipos de datos pueden estar contenidos en un DataFrame?"
  - "¿Por qué es importante el tipo de datos?"
objectives:
    - "Describir cómo se almacena la información en un DataFrame de Python."
    - "Examinar la estructura de un DataFrame."
    - "Modificar el formato de los valores en un DataFrame."
    - "Describir cómo los tipos de datos afectan a las operaciones."
    - "Definir, manipular e interconvertir integers y floats en Python."
    - "Analizar datasets que tienen valores faltantes/nulos (valores NaN)."
    - "Escribir datos manipulados a un archivo."
keypoints:
   - "Pandas usa otros nombres para tipos de datos que Python, por ejemplo: `object`
    para datos textuales."
   - "Una columna en un DataFrame sólo puede tener un tipo de datos."
   - "El tipo de datos de la columna de un DataFrame puede ser comprobado usando `dtype`."
   - "Es necesario tomar decisiones conscientes sobre cómo manejar los datos faltantes."
   - "Un DataFrame puede ser guardado en un archivo CSV usando la función `to_csv`."
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
**DataFrame** u objeto Python afecta a lo que podemos hacer con él y también a
los resultados de los cálculos. Hay dos tipos principales de datos
que estaremos explorando en esta lección: tipos de datos numéricos y de texto.

## Tipos de Datos Numéricos

Los tipos de datos numéricos incluyen enteros (**integer**) y números de punto flotante (**float**). Un número de
punto flotante tiene puntos decimales incluso si
el valor del punto decimal es 0. Por ejemplo: 1.13, 2.0, 1234.345. Si tenemos
una columna que contiene tanto enteros como números de punto flotante, Pandas asignará el tipo
de dato `float` a toda la columna, de modo tal que los puntos decimales no se
pierdan.

Un **integer** nunca tendrá un punto decimal. Así que, si quisiéramos almacenar
1.13 como un entero de tipo **integer** se almacenará como 1. Del mismo modo, 1234.345 se
almacenará como 1234. A menudo, en Python verás el tipo de dato `Int64`
que representa un entero de 64 bits. El 64 simplemente se refiere a la
memoria asignada para almacenar datos en cada celda; eso se refiere
a la cantidad de dígitos que puede efectivamente almacenar cada "celda".
Asignar espacio antes de tiempo permite a las computadoras optimizar
el almacenamiento y hacer más eficiente el procesamiento.

## Tipo de Datos de Texto

En Python, el tipo de datos de texto se conoce como secuencia de caracteres (**string**).
En Pandas se los conoce como objetos (**object**). Las secuencias de caracteres pueden
contener números y / o caracteres. Por ejemplo, una secuencia de caracteres
puede ser una palabra, una oración, o varias oraciones. Un objeto Pandas
también podría ser un nombre de gráfico como 'plot1'. Una secuencia de
caracteres también puede contener o consistir en números. Por ejemplo, '1234'
podría ser almacenado como una secuencia de caracteres. También '10.23'
podría ser almacenado como secuencia de caracteres. Sin embargo, ¡**las
las secuencias de caracteres que contienen números no se pueden utilizar en
operaciones matemáticas**!


Pandas y Python básico utilizan nombres ligeramente diferentes para los tipos
de datos. Más sobre esto en la tabla de abajo:

| Tipo en Pandas | Tipo en Python Nativo | Descripción |
|----------------|-----------------------|-------------|
| object | string | El **dtype** más general. Será asignado a tu columna si la columna contiene tipos mixtos (números y secuencias de caracteres). |
| int64  | int | Caracteres numéricos. 64 se refiere a la memoria asignada para almacenar el caracter. |
| float64 | float | Caracteres numéricos con decimales. Si una columna contiene números y NaNs (ver más abajo), Pandas usará float64 por defecto, en caso de que los datos faltantes contengan decimales. |
| datetime64, timedelta[ns] | N/D (ver el módulo [datetime] en la biblioteca estandar de Python) | Valores destinados a contener datos de tiempo. Mira en estos para experimentos con series de tiempo. |

[datetime]: http://doc.python.org/2/library/datetime.html


## Comprobando el formato de nuestros datos

Ahora que tenemos una comprensión básica de los tipos de datos numéricos
y de texto, exploremos el formato de los datos de nuestra encuesta. Estaremos trabajando
con el mismo **dataset**  `survey.csv` que hemos usado en lecciones anteriores.

~~~
# Ten en cuenta que se usa `pd.read_csv` porque importamos pandas con el alias `pd`
survey_df = pd.read_csv ("data/survey.csv")
~~~
{: .language-python}

Recuerda que podemos comprobar el tipo de un objeto de la siguiente manera:

~~~
type(surveys_df)
~~~
{: .language-python}

**OUTPUT:** `pandas.core.frame.DataFrame`

A continuación, veamos la estructura de datos de nuestras encuestas. En pandas,
podemos comprobar el tipo de datos de una columna en un **DataFrame** usando la sintaxis
`dataFrameName[column_name].dtype`:

~~~
surveys_df['sex'].dtype
~~~
{: .language-python}

**OUTPUT:** `dtype('O')`

Un tipo 'O' solo significa "objeto" que en el mundo de Pandas es una secuencia
de caracteres (texto).

~~~
surveys_df['record_id'].dtype
~~~
{: .language-python}

**OUTPUT:** `dtype('int64')`

El tipo `int64` nos dice que Python está almacenando cada valor dentro de esta columna
como un entero de 64 bits. Podemos usar el comando `dat.dtypes` para ver el tipo de datos
de cada columna de un **DataFrame** (todos a la vez).

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

Ten en cuenta que la mayoría de las columnas en nuestros datos de encuesta son
del tipo `int64`. Esto significa que son enteros de 64 bits. Pero la columna de
peso (weight) es un valor de punto flotante o `float`, lo que significa que contiene
decimales. Las columnas `species_id` y `sex` son objetos, lo cual significa que
contienen secuencias de caracteres `string`.

## Trabajando con **integers** y **floats**

Así que hemos aprendido que las computadoras almacenan los números de una de
dos maneras: como enteros `integer` o como números de punto flotante `float`. Los
**integers** son los números que usualmente usamos para contar. Los **float**
tienen parte fraccionaria (decimal). Consideremos ahora cómo el tipo de datos
puede impactar en las operaciones matemáticas entre nuestros datos. La suma,
la resta, la división y la multiplicación funcionan en **float** e **integer**
como es de esperar.

~~~
print(5+5)
10

print(24-4)
20
~~~
{: .language-python}

Si dividimos un **integer** por otro, obtenemos un **float**.
El resultado en Python 3 es diferente al de Python 2, donde el resultado es un
**integer** (porque Python 2 hace una división entera).

~~~
print(5/9)
0.5555555555555556

print(10/3)
3.3333333333333335
~~~
{: .language-python}

También podemos convertir un número de punto flotante en un entero, o un entero en
un número de punto flotante. Ten en cuenta que Python redondea por defecto cuando
convierte de **float** a **integer**.

~~~
# Convertir 'a' a integer
a = 7.83
int(a)
7

# Convertir 'b' a float
b = 7
float(b)
7.0
~~~
{: .language-python}

# Trabajando con los datos de nuestra encuesta

Volviendo a nuestros datos, si lo deseamos, podemos modificar el formato de los
valores dentro de nuestros datos. Por ejemplo, podríamos convertir el campo
 `record_id` a **float**

~~~
# Convertir el campo record_id de integer a float
surveys_df['record_id'] = surveys_df['record_id'].astype('float64')
surveys_df['record_id'].dtype
~~~
{: .language-python}

**OUTPUT:** `dtype('float64')`

> ## Desafío - Cambiando tipos
>
> Intenta convertir la columna `plot_id` a **float** usando
>
> ~~~
> surveys_df.plot_id.astype("float")
> ~~~
> {: .language-python}
>
> A continuación, intenta convertir `weight` (peso) en un **integer**. ¿Qué te
dice Pandas? ¿Qué es lo que va mal ahí?
> Más adelante, hablaremos acerca de algunas soluciones a esto.

{: .challenge}

## Valores de datos faltantes o nulos - NaN

¿Qué ocurrió en en el desafío? Ten en cuenta que esto arroja un error de valor:

`ValueError: Cannot convert NA to integer`.

Si observamos la columna `weight`
(peso) de los datos de las encuestas, notamos que hay valores NaN (**N**ot **a**
**N**umber) (no es número). Los valores **NaN ** son valores que no están definidos
y que no se pueden representar matemáticamente. Pandas, por ejemplo, leerá
como NaN aquellas celdas vacías de una hoja CSV o Excel. Los valores NaN tienen
algunas propiedades deseables: si tuviéramos que promediar la columna `weight`
(peso) sin reemplazar los valores NaN, Python sabría saltarse las celdas vacías.

~~~
surveys_df['weight'].mean()
42.672428212991356
~~~
{: .language-python}
Tratar con valores de datos faltantes siempre es un desafío. A veces es dificil
saber por qué faltan valores. ¿Fue debido a un error de entrada de datos? ¿O
son datos que alguien no pudo recoger? ¿Debe considerarse el valor como 0?
Para tomar buenas decisiones, necesitamos saber qué representan los valores
faltantes del **dataset**. Si tenemos suerte, tendremos algunos metadatos que
nos dirán más acerca de cómo fueron manejados los valores nulos.

Por ejemplo, en algunas disciplinas, como el sensado remoto, los valores de
datos faltantes suelen definirse como -9999. Tener un montón de valores -9999 en
tus datos podría realmente alterar los cálculos numéricos. A menudo, en las
hojas de cálculo, las celdas se dejan vacías cuando no hay datos disponibles.
Por defecto, Pandas reemplazará esos valores nulos con **NaN**.
Sin embargo, es una buena práctica adquirir el hábito de marcar intencionalmente
aquellas celdas que no tienen datos con un valor que represente "sin datos"!
De esa manera, en el futuro, no habrá preguntas cuando tu (o alguna otra persona)
explore los datos.

### ¿Dónde están los **NaN's**?

Exploremos un poco más los valores **NaN** en nuestros datos. Usando las herramientas
que hemos aprendido en la lección 02, podemos averiguar cuántas filas contienen
valores **NaN** en la columna weight (peso). También, partiendo de nuestros datos, podemos
crear un nuevo subconjunto que contenga solamente aquellas filas con peso mayor
a cero (es decir, seleccionar valores significativos de peso):

~~~
len(surveys_df[pd.isnull(surveys_df.weight)])
# How many rows have weight values?
len(surveys_df[surveys_df.weight> 0])
~~~
{: .language-python}

Usando el método `.fillna ()` podemos reemplazar todos los valores **NaN** por
ceros (después de hacer una copia de los datos de modo tal de no perder
nuestro trabajo):

~~~
df1 = surveys_df.copy()
# Completar todos los valores NaN con ceros
df1['weight'] = df1['weight'].fillna(0)
~~~
{: .language-python}

Sin embargo, **NaN** y cero arrojan diferentes resultados en el análisis. El valor
promedio resulta diferente cuando los valores **NaN** se reemplazan con
cero, comparando cuando los valores de **NaN** son descartados o ignorados.

~~~
df1['weight'].mean()
38.751976145601844
~~~
{: .language-python}

Podemos completar los valores **NaN** con cualquier valor que elijamos. El
código de abajo completa todos los Valores **NaN** con un promedio de los pesos.

~~~
 df1['weight'] = surveys_df['weight'].fillna(surveys_df['weight'].mean())
~~~
{: .language-python}

También podríamos elegir crear un subconjunto de datos, manteniendo solamente
aquellas filas que no contienen valores **NaN**.

La clave es tomar decisiones conscientes acerca de cómo administrar los datos
faltantes. Aquí es donde pensamos cómo se utilizarán nuestros datos y cómo estos
valores afectarán las conclusiones científicas que se obtengan de los datos.

Python nos brinda todas las herramientas que necesitamos para dar cuenta de estos
problemas. Solo debemos ser cautelosos acerca de cómo nuestras decisiones impactan
en los resultados científicos.

> ## Desafío - Contando
> Cuenta el número de valores perdidos por columna. Sugerencia: el método
> `.count()` te proporciona el número de observaciones que no son NA por columna.
> Examina el método `.isnull()`.
{: .challenge}

## Escribiendo datos a CSV

Hemos aprendido a manipular datos para obtener los resultados deseados.
Pero también hemos discutido acerca de mantener los datos que han sido manipulados
separados de los datos sin procesar. Algo que podríamos estar interesados en
hacer es trabajar solo con las columnas que tienen datos completos. Primero,
recarguemos los datos para no mezclar todas nuestras manipulaciones anteriores.

~~~
surveys_df = pd.read_csv("data/surveys.csv")
~~~
{: .language-python}
A continuación, vamos a eliminar todas las filas que contienen valores nulos.
Usaremos el comando `dropna`.
De forma predeterminada, `dropna` elimina las columnas que contienen valores nulos
incluso para una sola fila.

~~~
df_na = surveys_df.dropna()

~~~
{: .language-python}

Si ahora escribes `df_na`, deberías observar que el **DataFrame** resultante
tiene 30676 filas y 9 columnas, mucho menos que las 35549 filas originales.

Ahora podemos usar el comando `to_csv` para exportar un **DataFrame** a formato
CSV. Ten en cuenta que el código que se muestra a continuación por defector
guardará los datos en el directorio de trabajo en el que estamos parados.
Podemos guardarlo en otra carpeta agregando el nombre de la carpeta y una barra
inclinada antes del nombre del archivo: `df.to_csv('foldername/out.csv')`.
Usamos `index = False` para que Pandas no incluya el número de índice para cada
fila.

~~~
# Escribir DataFrame a CSV
df_na.to_csv('data_output/surveys_complete.csv', index=False)
~~~
{: .language-python}

Usaremos este archivo de datos más adelante en el taller. Revisa tu directorio
de trabajo para asegurarte de que el CSV se haya guardado correctamente y que
puedas abrirlo. Si lo deseas, intenta recuperarlo con Python para
asegurarte de que se importa correctamente.

## Resumen

Hemos aprendido:

+ Cómo explorar los tipos de dato de las colummnas de un **DataFrame**
+ Cómo cambiar el tipo de dato
+ Qué son los valores **NaN**, cómo deberían representarse, y lo que eso significa para tu trabajo
+ Cómo reemplazar los valores **NaN** si así lo quisieras
+ Como usar `to_csv` para guardar en un archivo los datos manipulados.

{% include links.md %}
