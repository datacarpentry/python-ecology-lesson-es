---
title: Acceso a base de datos SQLite usando Python y Pandas
teaching: 20
exercises: 25
questions:
    - ¿Cómo conectarse a una base de datos SQLite desde Python?
    - ¿Cómo extraer datos de una base de datos SQLite a un DataFrame de Python?
    - ¿Cuáles son los beneficios de usar una base de datos en vez de un archivo CSV?
objectives:
    - "Usa el módulo sqlite3 para interactuar con una base de datos SQL."
    - "Accede a los datos almacenados en SQLite usando Python."
    - "Describe las diferencias de interactual con datos almacenados en un archivo CSV y datos almacenados en SQLite."
    - "Describe los beneficios de acceso a datos usando una base de datos en comparación con un archivo CSV."
keypoints:
    - "Crea una conexión con `sqlite3.connect()`, luego un cursor para consultas con `.cursor()`."  
    - "Ejecuta consultas usando `.execute()`."
    - "Usa Pandas `.read_sql_query()` para extraer datos directamente a un DataFrame."   
    - "Escribe los datos de un nuevo DataFrame en una nueva tabla en SQLite usando `.to_sql()`."
    - "Al final, no olvides cerrar la puerta de la conexión usando el comando `.close()`."
---

## Python y SQL

Cuando lees un archivo con datos en Python y luego lo asignas a una variable estás usando la memoria de tu computadora para guardar los datos. Pero si accesas datos almacenados en una base de datos es mucho más eficiente y te permite extraer un subconjunto de los datos que necesites.

Aquí aprenderás como conectarte a una base de datos, por ejemplo SQL o SQLite.

### El módulo `sqlite3`

Con el módulo [sqlite3] uno puede conectarse e interactuar con bases de datos SQLite de manera sencilla. Primeramente, se crea un objeto de conexión usando `sqlite3.connect()`, esto abre la puerta a la base de datos. Mientras la conexión esté abierta se puede interactuar con la base de datos haciendo consultas. Para hacer consultas necesitas crear un objeto cursor usando el comando `.cursor()`. Luego, el objeto cursor puede hacer operaciones usando el comando `.execute()`. Al final, no olvides cerrar la puerta de la conexión usando el comando `.close()`.

[sqlite3]: https://docs.python.org/3/library/sqlite3.html

~~~
# Importa el módulo sqlite3
import sqlite3

# Crea un objeto de conexión a la base de datos SQLite
con = sqlite3.connect("data/portal_mammals.sqlite")

# Con la conexión, crea un objeto cursor
cur = con.cursor()

# El resultado de "cursor.execute" puede ser iterado por fila
for fila in cur.execute('SELECT * FROM species;'):
    print(fila)

# No te olvides de cerrar la conexión
con.close()
~~~
{: .language-python}

### Consultas

Una de las formas más comunes de interactuar con una base de datos es haciendo consultas para extraer datos. Las consultas se hacen con unas declaraciones y palabras clave. Por ejemplo *SELECT* es la palabra clave de una declaración.

Una consulta nos devuelve o retorna datos que pueden ser una o varias filas y columnas, a este resultado también se llama tupla. Para filtrar las tuplas usa la palabra *WHERE* que recibe una o más condiciones en la declaración.

~~~
# Importa el módulo sqlite3
import sqlite3

# Crea un objeto de conexión a la base de datos SQLite
con = sqlite3.connect("data/portal_mammals.sqlite")

# Con la conexión, crea un objeto cursor
cur = con.cursor()

# Ejecuta la consulta 1
cur.execute('SELECT plot_id FROM plots WHERE plot_type="Control"')
# Extrae todos los datos
cur.fetchall()

# Ejecuta la consulta 2
cur.execute('SELECT species FROM species WHERE taxa="Bird"')
# Extrae sólo la primera tupla
cur.fetchone()

# No te olvides de cerrar la conexión
con.close()
~~~
{: .language-python}

##  Acceso datos en SQLite usando Python y Pandas

Usando pandas, podemos extraer los resultados de una consulta en SQLite a un *DataFrame*. Recuerda que puedes usar los mismos comandos o sintaxis de SQL de la lección de SQL.

Por ejemplo para usar Pandas y SQLite:

~~~
# Importa pandas y sqlite3
import pandas as pd
import sqlite3

# Crea un objeto de conexión a la base de datos SQLite
con = sqlite3.connect("data/portal_mammals.sqlite")
# Usa read_sql_query de pandas para extraer el resultado
# de la consulta a un DataFrame
df = pd.read_sql_query("SELECT * from surveys", con)

# Verifica que el resultado de la consulta SQL está
# almacenado en el DataFrame
print(df.head())

# No te olvides de cerrar la conexión
con.close()
~~~
{: .language-python}

## Almacenando datos: CSV vs SQLite

Almacenar datos en una base de datos SQLite incrementa el rendimiento sustancialmente. Por ejemplo el tiempo de lectura / escritura en comparación con CSV. La diferencia en el rendimiento se hace más notable a medida que crece el tamaño del conjunto de datos (por ejemplo [estos puntos de referencia] en inglés).

[estos puntos de referencia]: http://sebastianraschka.com/Articles/2013_sqlite_database.html#results-and-conclusions


> ## Desafío - SQL
>
> 1. Crea una consulta que contenga datos de encuestas recopilados
> entre 1998 y 2001 para observaciones de sexo "masculino" o "femenino"
> que incluyan el genus de la observación, la especie y el tipo de sitio
> de la muestra. ¿Cuántos registros se devuelven?
>
> 2. Crea un DataFrame que contenga el número total de observaciones
> (count) de todos los años, y la suma de los pesos de observaciones
> de cada sitio, ordenados por el ID del sitio.
{: .challenge}

## Almacenando datos: Crea nuevas tablas usando Pandas

También podemos usar pandas para crear nuevas tablas dentro de una base de datos SQLite. Aquí, volveremos a hacer un ejercicio que hicimos antes con archivos CSV usando nuestra base de datos SQLite. Primero leemos los datos de nuestra encuesta, luego seleccionamos solo los resultados de la encuesta en el año 2002 y luego los guardamos en su propia tabla para que podamos trabajar con ellos por su cuenta más adelante.

~~~
# Importa pandas y sqlite3
import pandas as pd
import sqlite3

# Crea un objeto de conexión a la base de datos SQLite
con = sqlite3.connect("data/portal_mammals.sqlite")

# Extrae los datos de la consulta directamente a un DataFrame
surveys_df = pd.read_sql_query("SELECT * from surveys", con)

# Selecciona sólo datos en el año 2002
surveys2002 = surveys_df[surveys_df.year == 2002]

# Escribe los datos del nuevo DataFrame en una nueva tabla en SQLite
surveys2002.to_sql("surveys2002", con, if_exists="replace")

# No te olvides de cerrar la conexión
con.close()
~~~
{: .language-python}

> ## Desafío - Guardando tus datos
>
> 1. ¿Cuándo sería buena idea guardar los resultados de tus consultas en
> la base de datos? y ¿Cuáles serían algunas de las razones por las que
> sería mejor no guardar los resultados en la base de datos?
{: .challenge}

{% include links.md %}
