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
    - "Describe las diferencias de interactuar con datos almacenados en un archivo CSV y datos almacenados en SQLite."
    - "Describe los beneficios de acceso a datos usando una base de datos en comparación con un archivo CSV."
keypoints:
    - "Crea una conexión con `sqlite3.connect()`, luego un cursor para consultas con `.cursor()`."
    - "Ejecuta consultas usando `.execute()`."
    - "Usa Pandas `.read_sql_query()` para extraer datos directamente a un DataFrame."
    - "Escribe los datos de un nuevo DataFrame en una nueva tabla en SQLite usando `.to_sql()`."
    - "Al final, no olvides cerrar la puerta de la conexión usando el comando `.close()`."
---

## Python y SQL

Cuando lees un archivo de datos en Python y luego lo asignas a una variable estás usando la memoria de tu computadora para guardar esta variable. Acceder a tus datos desde una base de datos como SQL no es solo mas eficiente, sino que también te permite extraer e importar una parte o el subconjunto de datos que necesites.

En la siguiente lección, veremos algunos enfoques que se pueden tomar para conectarte a una base de datos, por ejemplo SQL o SQLite.

### El módulo `sqlite3`

Con el módulo [sqlite3] uno puede conectarse e interactuar con bases de datos SQLite de manera directa y sencilla. Primeramente, se crea un objeto de conexión usando `sqlite3.connect()`, esto abre la puerta a la base de datos. Mientras la conexión esté abierta cualquier interacción con la base de datos requiere que crees un objeto cursor con el comando `.cursor()`. Luego el cursor estará listo para realizar todo tipo de operaciones con el comando `.execute()`.
 Al final, no olvides cerrar la puerta de la conexión usando el comando `.close()`.

[sqlite3]: https://docs.python.org/3/library/sqlite3.html

~~~
# Importa el módulo sqlite3
import sqlite3

# Crea un objeto de conexión a la base de datos SQLite
con = sqlite3.connect("data/portal_mammals.sqlite")

# Con la conexión, crea un objeto cursor
cur = con.cursor()

# El resultado de "cursor.execute" puede ser iterado por fila
for row in cur.execute('SELECT * FROM species;'):
    print(row)

# No te olvides de cerrar la conexión
con.close()
~~~
{: .language-python}

### Consultas

Una de las formas más comunes de interactuar con una base de datos es haciendo consultas para extraer datos:
Para obtener datos basados en algunos parametros de búsqueda, usa la palabra de declaración **SELECT**.
Una consulta nos devuelve o retorna datos que pueden ser una o varias filas y columnas, a este resultado también se llama tupla. Para filtrar las tuplas basado en algun parametro usa la palabra **WHERE**. El filtro **WHERE** recibe una o más condiciones.

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

Usando pandas, podemos extraer los resultados de una consulta en SQLite a un *DataFrame*. Recuerda que puedes usar los mismos comandos o sintaxis de SQL de la lección de SQLite.

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
> 1. Crea una consulta que contenga datos de encuestas recopiladas entre 1998 y 2001
> para observaciones de sexo "masculino" o "femenino" que incluyan el género de la observación,
> la especie y el tipo de sitio de la muestra. ¿Cuántos registros se devuelven?
>
> 2. Crea un DataFrame que contenga el número total de observaciones
> **count** de todos los años, y la suma de los pesos de observaciones de cada sitio, ordenados por
> el ID del sitio.
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
> 1. Para cada uno de los desafios anteriores, bloquea y modifica tu codigo para guardar los resultados en sus propias tablas en el portal de base de datos.
>
> 2. ¿Cuáles son algunas de las razones para guardar los resultados de tus consultas en la misma base de datos? y
> ¿Cuáles serían algunas de las razones por las que sería mejor no guardar los resultados en la misma base de datos?
{: .challenge}

{% include links.md %}
