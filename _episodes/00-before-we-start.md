---
title: Antes de comenzar
teaching: 30
exercises: 0
questions:
  - "¿Qué es Python y por qué debería aprenderlo?"
objectives:
  - "Describir el propósito del editor, consola, ayuda, el panel explorador de variables y el panel explorador de archivos de Spyder."
  - "Organizar los archivos y directorios para un conjunto de análisis como proyecto de Python, y entender el propósito del directorio de trabajo."
  - "Saber donde buscar ayuda."
  - "Demostrar como proporcionar suficiente información para solucionar problemas junto con la comunidad de usuarios de Python."
keypoints:
  - "Python es un lenguaje de programación de código libre y plataforma independiente."
  - "SciPy es un ecosistema para Python que provee las herramientas necesarias para la computación científica."
  - "Jupyter Notebook y la Spyder IDE son excelentes herramientas para escribir código e interactuar con Python. Con su gran comunidad es fácil encontrar ayuda en internet."
---


## ¿Qué es Python?

Python es un lenguaje de programación de tipo general que soporta un desarrollo rápido de aplicaciones de análisis de datos. La palabra "Python" es usada para referirse tanto al lenguaje de programación, como a la herramienta que ejecuta los **scripts** escritos en el lenguaje "Python".

Sus principales ventajas son:

* Es gratis
* De código abierto
* Disponible para todas las plataformas más importantes (macOS, Linux, Windows)
* Es mantenido por la Python Software Foundation
* Soporta múltiples paradigmas de programación
* Tiene una gran comunidad
* Tiene un rico ecosistema de paquetes de terceros

*Entonces, ¿por qué necesitas Python para el análisis de datos?*

### Fácil de aprender
Python es más fácil de aprender que otros lenguajes de programación. Esto es importante debido a que al tener barreras de aprendizaje más bajas es más fácil para los nuevos miembros de la comunidad ponerse al día.

### Reproducibilidad
La reproducibilidad es la habilidad de obtener los mismos resultados usando los mismos datos y análisis.

Un análisis de datos escrito en un **script** de Python puede ser reproducido en cualquier plataforma.
Es más, si recolectas más datos o corriges datos existentes, ¡puedes volver a ejecutar los análisis de manera rápida y sencilla!

Cada vez más revistas científicas y agencias de financiación esperan que los análisis sean reproducibles, por lo tanto, saber Python te dará una ventaja sobre estos requisitos.

### Versatilidad
Python es un lenguaje versátil que se integra con varias aplicaciones existentes para permitir hacer cosas sorprendentes.
Por ejemplo, uno puede usar Python para generar manuscritos, de tal forma que si necesitas actualizar tus datos, procedimientos de análisis, o cambiar algo más, puedes volver a generar todas las figuras rápidamente y tu manuscrito se actualizará automáticamente.

Python puede leer archivos de texto, conectarse a bases de datos, y a muchos otros formatos de datos, ya sea en tu computadora o en la web.

### Interdisciplinario y extensible
Python provee un marco de trabajo que permite que cualquier persona combine enfoques de diferentes disciplinas de investigación (y no solo de investigación) para ajustarse mejor a tus necesidades de análisis.

### Python tiene una comunidad grande y amable
Miles de personas usan Python diariamente. Muchos de ellos están dispuestos a ayudarte a través de listas de correo y sitios web, tales como [Stack Overflow](https://stackoverflow.com) y el portal de la [comunidad de Anaconda](https://www.anaconda.com/community/).

### Gratis y de código abierto (FOSS por sus siglas en inglés)... y multi-plataforma
Sabemos que ya hemos nombrado esto, de todas formas, vale la pena repetirlo.

<br />
## Conociendo a Anaconda
La distribución de Python [Anaconda](https://www.anaconda.com) incluye montones de paquetes populares como la consola Ipython, Jupyter Notebook, y Spyder IDE.
Échale un vistazo al Navegador Anaconda. Puedes ejecutar programas desde el Navegador o usar la línea de comando.

[Jupyter Notebook](https://jupyter.org) es una aplicación web de código abierto que permite crear y compartir documentos que permiten crear de manera sencilla documentos que combinan código, gráficos y texto narrativo.

[Spyder](https://spyder-ide.github.io) es un **Entorno de Desarrollo Integrado** (IDE por sus siglas en inglés) que permiten escribir **scripts** de Python e interactuar con el software de Python desde una interfaz única.

Anaconda también viene con un gestor de paquetes llamado [conda](https://conda.io/docs/), el cual hace que sea fácil instalar y actualizar paquetes adicionales.

<br />
## Proyecto de Investigación: Buenas Prácticas

Es una buena idea guardar los grupos de datos relacionados, análisis, y texto en una única carpeta.
Por lo tanto, todos los **scripts** y archivos de texto dentro de esta carpeta pueden usar **paths** relativos hacia los archivos de datos.
Trabajar de esta manera hace que sea mucho más fácil mover tu proyecto y compartirlo con otras personas.

### Organizando tu directorio de trabajo

Usar una estructura de carpetas de forma consistente a través de tus proyectos te ayudará a mantener las cosas organizadas, y hará que sea fácil encontrar/archivar cosas en el futuro. Esto puede ser especialmente útil cuando tienes múltiples proyectos. En general, podrías llegar a querer crear directorios separados para tus **scripts**, datos, y documentos.


- **`data/`**: Usa esta carpeta para guardar tus datos crudos. Por el bien de la transparencia y procedencia, siempre deberías guardar una copia de tus **datos crudos**. Si necesitas limpiar tus datos, hazlo de manera programática (*i.e.*, con **scripts**) y asegúrate de separar los datos limpios de los crudos. Por ejemplo, puedes guardar los datos crudos en `./data/raw/` y los limpios en `./data/clean/`.

- **`documents/`**: Usa esta carpeta para guardar esquemas, borradores, y otro texto.

- **`scripts/`**: Usa esta carpeta para guardar tus **scripts** (de Python) para limpieza de datos, análisis y generación de gráficos que uses en este proyecto en particular.

Puede que tengas que crear directorios adicionales dependiendo de las necesidades de tu proyecto, pero los que nombramos deberían ser el eje del directorio. Para este workshop, vamos a necesitar una carpeta `data/` para almacenar nuestros datos crudos, y luego vamos a tener que crear la carpeta `data_output/` cuando aprendamos como exportar datos como archivos CSV.

## ¿Qué es Programación y Codificación?

Programación es el proceso de escribir _"programas"_ que una computadora pueda ejecutar produciendo algún resultado (útil).
La programación es un proceso de múltiples pasos que implican:

1. Identificar los aspectos de un problema de la vida real que pueda ser resuelto computacionalmente.
2. Identificar la (mejor) solución computacional.
3. Implementar la solución en un lenguaje de programación específico.
4. Testear, validar, y ajustar la solución implementada.

Mientras que _"Programar"_ se refiere a todos los pasos nombrados, _"Codificación"_ se refiere solo al paso 3: _"Implementar la solución en un lenguaje de programación específico"_.

#### Si trabajas con Jupyter notebook:

Puedes tipear código de Python en una celda de código y luego ejecutarla presionando <kbd>Shift</kbd>+<kbd>Enter</kbd>.

El output se imprimirá directamente bajo la celda de input.
Se puede reconocer a una celda de código mediante el `In[ ]:` al principio de la celda y a una celda de output por el `Out[ ]:`.

Presionar el botón __+__ en la barra de menú agregará una nueva celda.

Todos tus comandos tal como los outputs serán guardados con el notebook.

#### Si trabajas con Spyder:

Puedes usar tanto la consola o un archivo de **script** (archivos de texto plano que contienen tu código).
El panel de consola (el panel abajo a la derecha, en Spyder) es el lugar donde los comandos escritos en el lenguaje de programación Python pueden ser tipeados y ejecutados inmediatamente por la computadora. También es donde se mostrarán los resultados.
Puedes ejecutar los comandos directamente en la consola presionando <kbd>Enter</kbd>, pero serán "perdidos" cuando cierres la sesión.
Spyder usa la consola [IPython](http://ipython.org) por defecto.

Debido a que queremos que nuestro código y flujo de trabajo sea reproducible, es mejor tipear los comandos en el editor de **scripts**, y guardarlos como un **script**. De esta manera, hay un registro completo de lo que hicimos, y cualquiera (¡incluyendo nuestros yo futuros!) pueden reproducir los resultados en su computadora de forma sencilla.

Spyder permite ejecutar comandos directamente desde el editor de **scripts** usando los botones de ejecución en la parte superior.

Para ejectuar el **script** entero haz clic en _Run file_ o presiona <kbd>F5</kbd>. Para ejecutar la línea actual haz clic en _Run selection or current line_ o presiona <kbd>F9</kbd>, otros botones de ejecución permiten ejecutar celdas de **scripts** o activar el modo **debug**. Cuando se usa <kbd>F9</kbd>, el comando en la línea actual del **script** (indicada por el cursor) o todos los comandos en el actual texto seleccionado serán enviados a la consola y ejecutados.

En algún punto en tu análisis podrías llegar a desear comprobar el contenido de una variable o la estructura de un objeto, sin necesariamente guardar un registro en tu **script**. Puedes tipear estos comandos y ejecutarlos directamente en la consola. Spyder provee los atajos <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>E</kbd> y <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>I</kbd> que te permitirán "saltar" entre el panel de **scripts** y el de la consola.

Si Python está listo para aceptar comandos, la consola IPython muestra un aviso `In [..]:` con el número de línea actual en la consola entre corchetes `[]`. Si recibe un comando (mediante tipeo, copiando y pegando o enviado desde el editor de scripts) Python lo va a ejecutar, mostrar los resultados en la celda `Out [..]:`, y luego volver con un nuevo aviso  `In [..]:` a la espera de nuevos comandos.

Si Python todavía está esperando a que ingreses mas datos debido a que todavía no has terminado, la consola mostrará un aviso `...:`. Significa que no has terminado de ingresar un comando completo.

Esto es debido a que no has tipeado un paréntesis de cierre (`)`, `]`, o `}`) o comillas.
Cuando sucede esto, y pensaste que habías terminado de tipear tu comando, haz clic dentro de la ventana de la consola y presiona <kbd>Esc</kbd>; esto cancelará el comando incompleto y te retornará al aviso `In [..]:`.

## ¿Cómo aprender más luego del taller?

El material que cubrimos durante este taller te dará una prueba inicial de cómo puede usarse Python para analizar datos de tu propia investigación. Sin embargo, todavía necesitarás aprender más sobre operaciones más avanzadas tal como la limpieza de tu **dataset**, usar métodos estadísticos, o crear gráficos bonitos. La mejor manera de hacerse competente y eficiente en Python, así como con cualquier otra herramienta, es empleándola para abordar tus propias preguntas de investigación. Como principiante, puede sentirse desalentador tener que escribir un **script** desde el inicio, y dado que muchas personas comparten su código en la web, modificar código existente para adaptarlo a tus propósitos puede hacer que comenzar sea más fácil.

## Buscando ayuda

* revisa el menú _Ayuda_
* tipea `help()`
* tipea `?object` o `help(object)` para obtener información sobre un objeto
* [Documentación de Python](https://www.python.org/doc/)

Finalmente, una búsqueda genérica en Google o internet de "Python tarea_a_buscar" usualmente te enviará a la documentación del módulo apropiado o a un foro dónde alguien más ya ha hecho la misma pregunta.

Estoy atorada... tengo un mensaje de error que no entiendo.
Empieza por googlear el mensaje de error. Sin embargo, esto no siempre funciona muy bien debido a que a veces, los desarrolladores emplean los mensajes de error provistos por Python. Por ello terminas con mensajes de error genéricos que podrían no llegar a ser de ayuda para diagnosticar un problema (Ej.: "subscript out of bounds"). Si el mensaje es muy genérico, quizás deberías incluir en tu consulta el nombre de la función o paquete que estés usando.

Sin embargo, deberías chequear Stack Overflow. Buscar usando la etiqueta [python]. La mayoría de las preguntas ya han sido respondidas, el desafío es usar la combinación de palabras apropiadas en la búsqueda para encontrar las respuestas: <http://stackoverflow.com/questions/tagged/python>.

### Pidiendo ayuda

La clave para recibir ayuda de alguien es que ellos entiendan rápidamente tu problema. Deberías hacer que sea lo más fácil posible identificar dónde podría estar el inconveniente.

Trata de usar las palabras correctas para describir el problema. Por ejemplo, un paquete no es lo mismo que una biblioteca. La mayoría de las personas entenderán lo que quieres decir, pero otras tienen fuertes sentimientos sobre la diferencia en el significado. El punto clave es que puede hacer que las cosas sean confusas para las personas que tratan de ayudarte.
Trata de ser tan precisa como sea posible cuando describes tu problema.

Si es posible, trata de resumir lo que no funciona en un ejemplo simple y reproducible. Si puedes reproducir el problema usando una pequeña cantidad de datos en lugar de tus 50.000 filas y 10.000 columnas, proporciona el **dataset** pequeño con la descripción de tu problema. Cuando sea apropiado, trata de generalizar lo que estas haciendo, así incluso las personas que no están familiarizadas con tu campo de estudio podrán entender tu pregunta. Por ejemplo, en lugar de usar un subconjunto de tu **datase** real, crea uno pequeño (3 columnas, 5 filas) y genérico.

### ¿Dónde pedir ayuda?

* A la persona sentada junto a tu durante el taller. No dudes en hablar con tu vecina durante el taller, compara tus respuestas, pide ayuda. También podrías estar interesada en organizar reuniones regularmente luego del taller para seguir aprendiendo una de otra.
* Tus amigables colegas: si conoces a alguien con mas experiencia que tu, ellas podrían estar capacitadas y dispuestas a ayudarte.
* [Stack Overflow](http://stackoverflow.com/questions/tagged/python): si tu pregunta no ha sido contestada con anterioridad y además está bien planteada, hay chances de que obtengas una respuesta en 5 minutos. Recuerda seguir los lineamientos de cómo preguntar correctamente.
* [Listas de correo de Python](https://www.python.org/community/lists/)

## Más recursos

[PyPI - the Python Package Index](https://pypi.python.org/pypi)

[The Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/)

[Dive into Python 3](http://getpython3.com/diveintopython3/)

{% include links.md %}
