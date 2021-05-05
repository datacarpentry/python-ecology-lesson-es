---
layout: page
title: Setup
---

> ## Datos
> Los datos para esta lección son del **Portal Project Teaching Database** -
> [
disponible en **FigShare**](https://figshare.com/articles/Portal_Project_Teaching_Database/1314459).
>
> En esta lección usaremos los seis archivos enumerados a continuación.
> Descarga estos archivos a su computadora haciendo clic en
> [este enlace](https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/weecology/portal-teachingdb),
> luego tendrás todo en un archivo comprimido.
> Tienes que descomprimir este archivo después de descargarlo.
>
> O descarga cada archivo individualmente con los siguientes enlaces:
>
> - [surveys.csv](https://ndownloader.figshare.com/files/10717177)
> - [species.csv](https://ndownloader.figshare.com/files/3299483)
> - [speciesSubset.csv]({{ page.root }}/data/speciesSubset.csv)
> - [plots.csv](https://ndownloader.figshare.com/files/3299474)
> - [bouldercreek_09_2013.txt]({{ page.root }}/data/bouldercreek_09_2013.txt)
> - [SQL Database](https://ndownloader.figshare.com/files/11188550)
{: .prereq}



> ## Software
> [**Python**](http://python.org) es un lenguaje muy utilizado en
> la computación científica y también es ideal para la programación de propósito general.
> La instalación de todos los paquetes científicos individualmente puede ser
> un poco difícil, por lo que recomendamos un instalador todo en uno.
>
> Para este taller utilizamos la versión 3.x.
>
> ### Paquetes de **Python** requeridos para este taller
>
> * [Pandas](http://pandas.pydata.org/)
> * [Jupyter notebook](http://jupyter.org/)
> * [Numpy](http://www.numpy.org/)
> * [Matplotlib](http://matplotlib.org/)
> * [plotnine](https://github.com/has2k1/plotnine)
{: .prereq}

## Instalación de software

Usaremos **Anaconda** o **Miniconda** para instalar **Python** y los paquetes necesarios.
Ambos usan [Conda](https://conda.io/en/latest/), pero
Anaconda viene con **Pandas**, **Jupyter Notebook**, **Numpy** y **Matplotlib** preinstaladas,
mientras que Miniconda no lo hace.


### Instalación de **Anaconda**

**Anaconda** te instalará los paquetes.

#### Descarga e instala **Anaconda**

Descarga e instala [**Anaconda**](https://www.continuum.io/downloads).
Recuerde descargar e instalar el instalador para **Python** 3.x.

#### Descarga el paquete para crear gráficos.

El paquete para crear gráficos, `plotnine`, no está instalado por defecto.
Para instalarlo desde el terminal, escriba:

~~~
conda install -c conda-forge plotnine
~~~
{: .language-python}

### Instalación de **Miniconda**

**Miniconda** es una versión "ligera" de **Anaconda**.
Si haces la instalación usando **Miniconda**,
también necesitarás instalar los paquetes requeridos para el taller.

#### Descarga e instala **Miniconda**

Descarga e instala [**Miniconda**](http://conda.pydata.org/miniconda.html)
siguiendo las instrucciones. Recuerda descargar y ejecutar el instalador para
**Python** 3.x.

#### Compruebe la instalación de **Miniconda**

En la terminal, escribe:

~~~
conda list
~~~
{: .language-bash}

### Instala los paquetes requeridos con **Conda**

En la terminal, escribe:

~~~
conda install -y numpy pandas matplotlib jupyter
conda install -c conda-forge plotnine
~~~
{: .language-bash}

## Abre un **Jupyter Notebook**

Después de instalar **Python** y los paquetes requeridos,
abre un **Jupyter Notebook** escribiendo este comando en la terminal:

~~~
jupyter notebook
~~~
{: .language-bash}

Un **Jupyter Notebook** se abrirá automáticamente en tu navegador.
Si no es así, o si deseas utilizar un navegador diferente, abre este enlace: <http://localhost:8888>.


Para una breve introducción a **Jupyter Notebooks**, consulta nuestra página
["Introducción a Jupyter Notebooks"](jupyter_notebooks).
