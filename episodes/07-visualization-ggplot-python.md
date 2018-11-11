---
title: Creando gráficos con plotnine
teaching: 40
exercises: 50
questions:
    - "¿Cómo puedo visualizar datos en Python?"
    - "¿Qué es la 'gramática de gráficos'?"
objectives:
    - "Crear un objeto `plotnine`."
    - "Establecer configuraciones para gráficos."
    - "Modificar un objeto `plotnine` existente."
    - "Cambiar la estética de un gráfico, como el color."
    - "Editar las etiquetas de los ejes."
    - "Construir gráficos complejos paso a paso."
    - "Crear gráficos de dispersión, gráficos de caja y gráficos de series."
    - "Usar los comandos `facet_wrap` y `facet_grid` para crear una colección de gráficos que dividen los datos por una variable categórica."
    - "Crear estilos personalizados para tus gráficos."
keypoints:
    - "Las variables `data`, `aes` y` geometry` son los elementos principales de un gráfico de `plotnine`."
    - "Con el operador `+ `, se agregan elementos adicionales al gráfico, por ejemplo `scale_*`, `theme_*`, `xlab`, `ylab` y `facet_*`."
---

## Nota

Python tiene muy buenos recursos para crear gráficos incorporados en el paquete `matplotlib`, pero para éste episodio, utilizaremos el paquete [`plotnine`] (https://plotnine.readthedocs.io/en/stable/), que facilita la creación de gráficos informativos usando datos estructurados. El el paquete `plotnine` está basado en la implementación R de [`ggplot2`](http://ggplot2.org/) y [La gramática de gráficos](http://link.springer.com/book/10.1007%2F0-387-28695-0)
por Leland Wilkinson. Además el paquete [`plotnine`](https://plotnine.readthedocs.io/en/stable/) está construido sobre `matplotlib` e interactúa bien con `pandas`.

Al igual que con los otros paquetes, `plotnine` necesita ser importado. Es bueno
practicar usando una abreviatura como usamos `pd` para `pandas`:

~~~
%matplotlib inline
import plotnine as p9
~~~
{: .language-python }

Desde ahora todas las funciones de `plotnine` se pueden acceder usando `p9.` por delante.

Para los ejercicios usaremos los datos de `surveys.csv` descartando los valores
nulos `NA`.

~~~
import pandas as pd

surveys_complete = pd.read_csv('data/surveys.csv')
surveys_complete = surveys_complete.dropna()
~~~
{: .language-python}

# Creando gráficos con plotnine

El paquete `plotnine` (es parte de [La gramática de gráficos] (http://link.springer.com/book/10.1007%2F0-387-28695-0)) se usa para la creación de gráficos complejos a partir de los datos en un `DataFrame`. Utiliza configuraciones por defecto, que ayudan a crear gráficos con calidad de
 publicación con unos pocos ajustes.

Los gráficos `plotnine` se construyen paso a paso agregando nuevos elementos uno
 encima del otro usando el operador `+`. Poniendo cada paso entre paréntesis `()` proporciona una sintaxis compatible con Python.

Para construir un gráfico `plotnine` necesitamos:

- Conectar el gráfico a un `DataFrame` específico usando el argumento `data`:

~~~
(p9.ggplot(data=surveys_complete))
~~~
{: .language-python}

Como no hemos definido nada más, solo un marco vacío está disponible y
es presentado.

- Define estéticas (`aes`), seleccionando las variables usadas en el gráfico y
'mapearlas' a una presentación como tamaño, color, forma, etc.
Puedes interpretar ésto como: las variables que se usan en el gráfico y son
modificadas por objetos o geometrías:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length')))
~~~
{: .language-python}

Las asignaciones más importantes son: `x`,` y`, `alpha`,` color`, `colour`,
`fill`,` linetype`, `shape`,` size` y `stroke`.

- Todavía no tenemos un gráfico, primero tenemos que definir qué tipo de geometría
utilizar. Lo más sencillo es probablemente usar puntos.
Puntos es una de las opciones de geometría `geoms`, que define la representación gráfica de los datos.
Otras geometría son líneas, barras, etc. Para agregar un `geom` al gráfico usa el símbolo `+`:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length'))
    + p9.geom_point()
)
~~~
{: .language-python}

El símbolo `+` en el paquete `plotnine` es particularmente útil porque te permite
modificar los objetos `plotnine` existentes. Esto significa que puedes configurar fácilmente el gráfico con *plantillas* y explorar convenientemente diferentes tipos de gráficos.  El gráfico anterior también se puede generar con código como este:

~~~
# Crea un gráfico
surveys_plot = p9.ggplot(data=surveys_complete,
                         mapping=p9.aes(x='weight', y='hindfoot_length'))

# Dibuja los puntos en el marco
surveys_plot + p9.geom_point()
~~~
{: .language-python}

![png](../fig/06_first_plot.png)

> ## Desafío - gráfico de barras
> Trabajando con los datos de `survey_complete`, usa la columna `plot-id` para
> crear un gráfico de barra `geom_bar` que cuenta el número de registros en cada plot-id. (Mira la documentación de la geometría de barra para manejar los conteos).
>
> > ## Respuestas
> >
> > ~~~
> > (p9.ggplot(data=surveys_complete,
> >            mapping=p9.aes(x='plot_id'))
> >     + p9.geom_bar()
> > )
> > ~~~
> > {: .language-python}
> >
> > ![png](../fig/06_challenge_bar.png)
> {: .solution}
{: .challenge}

Notas:

- Cualquier ajuste en la función `ggplot()` se visualiza en las capas del gráfico
(por ejemplo, las configuraciones universales). Esto incluye los ejes `x` y `y`
 que configuraste en las capa de estéticas `aes()`.
- También puedes especificar la estética para un `geom` independientemente de las
estéticas definida globalmente en la función `ggplot()`.

# Construyendo tus gráficos de forma iterativa

La construcción de gráficos con `plotnine` es típicamente un proceso iterativo. Empezamos definiendo el conjunto de datos que usaremos, colocaremos los ejes y elegiremos un geom. Por lo tanto, los elementos mínimos de cualquier gráfico son
 `data`,` aes` y `geom-*`:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length'))
    + p9.geom_point()
)
~~~
{: .language-python}

Luego, comenzamos a modificar este gráfico para extraer más información. Por
ejemplo, podemos agregar transparencia (alfa) para evitar la obstrucción visual
por aglomeración de puntos:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length'))
    + p9.geom_point(alpha=0.1)
)
~~~
{: .language-python}

![png](../fig/06_alpha_plot.png)

¡También puedes agregar color a los puntos!


~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length'))
    + p9.geom_point(alpha=0.1, color='blue')
)
~~~
{: .language-python}

![png](../fig/06_blue_plot.png)

Si quieres usar un color diferente para cda especie, tienes que conectar la
columna `species_id` con la estética del color:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight',
                          y='hindfoot_length',
                          color='species_id'))
    + p9.geom_point(alpha=0.1)
)
~~~
{: .language-python}

![png](../fig/06_color_plot.png)

Aparte de las configuraciones en los argumentos `data`, ` aes`
y los elementos `geom-*`, también se pueden agregar elementos adicionales,
 usando el signo `+`:

- Cambiando las etiquetas:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length', color='species_id'))
    + p9.geom_point(alpha=0.1)
    + p9.xlab("Weight (g)")
)
~~~
{: .language-python}

![png](../fig/06_color_label_plot.png)

- Puedes también cambiar las escalas de colores, ejes, etc. Por ejemplo,
una versión del gráfico usando el logarítmo de los números en el eje x
podría ayudar a una mejor interpretación de los números más pequeños:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length', color='species_id'))
    + p9.geom_point(alpha=0.1)
    + p9.xlab("Weight (g)")
    + p9.scale_x_log10()
)
~~~
{: .language-python}

![png](../fig/06_log_plot.png)

- También puedes cambiar el tema (`theme_*`) o algunos elementos específicos del tema (`theme`).
Por lo general, los gráficos con fondo blanco parecen más legibles cuando se imprimen. Entonces, podemos configurar el fondo a blanco usando la función `theme_bw()`.

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length', color='species_id'))
    + p9.geom_point(alpha=0.1)
    + p9.xlab("Weight (g)")
    + p9.scale_x_log10()
    + p9.theme_bw()
    + p9.theme(text=p9.element_text(size=16))
)
~~~
{: .language-python}

![png](../fig/06_white_plot.png)

> ## Desafío - retocando un gráfico de barras
> Usa el código del ejercicio anterior y cambia la estética de color por la
> variable `sex`, también cambia la geometría para tener un gráfico de barras,
> finalmente, cambia la escala `scale` del color de relleno para que tengas una barra
> azul y una naranja usando `blue` y `orange` (mira este link en inglés de la referencia [API reference plotnine](https://plotnine.readthedocs.io/en/stable/api.html#Color-and-fill-scales) para encontrar la función que necesitas).
>
> > ## Respuestas
> >
> > ~~~
> > (p9.ggplot(data=surveys_complete,
> >            mapping=p9.aes(x='plot_id',
> >                           fill='sex'))
> >     + p9.geom_bar()
> >     + p9.scale_fill_manual(["blue", "orange"])
> > )
> > ~~~
> > {: .language-python}
> > ![png](../fig/06_challenge_color_bar.png)
> {: .solution}
{: .challenge}



# Plotting distributions

Visualizing distributions is a common task during data exploration and
analysis. To visualize the distribution of `weight` within each `species_id`
group, a boxplot can be used:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='species_id',
                          y='weight'))
    + p9.geom_boxplot()
)
~~~
{: .language-python}

![png](../fig/06_boxplot.png)

By adding points of the individual observations to the boxplot, we can have a
better idea of the number of measurements and of their distribution:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='species_id',
                          y='weight'))
    + p9.geom_jitter(alpha=0.2)
    + p9.geom_boxplot(alpha=0.)
)
~~~
{: .language-python}

![png](../fig/06_point_boxplot.png)

> ## Challenge - distributions
>
> Boxplots are useful summaries, but hide the *shape* of the distribution.
> For example, if there is a bimodal distribution, this would not be observed
> with a boxplot. An alternative to the boxplot is the violin plot (sometimes
> known as a beanplot), where the shape (of the density of points) is drawn.
>
> In many types of data, it is important to consider the *scale* of the
> observations.  For example, it may be worth changing the scale of the axis
> to better distribute the observations in the space of the plot.
>
> - Replace the box plot with a violin plot, see `geom_violin()`
> - Represent weight on the log10 scale, see `scale_y_log10()`
> - Add color to the datapoints on your boxplot according to the plot from which
>   the sample was taken (`plot_id`)
>
> Hint: Check the class for `plot_id`. By using `factor()` within the `aes`
> mapping of a variable, `plotnine` will handle the values as category values.
>
> > ## Answers
> >
> > ~~~
> > (p9.ggplot(data=surveys_complete,
> >            mapping=p9.aes(x='species_id',
> >                           y='weight',
> >                           color='factor(plot_id)'))
> >     + p9.geom_jitter(alpha=0.3)
> >     + p9.geom_violin(alpha=0, color="0.7")
> >     + p9.scale_y_log10()
> > )
> > ~~~
> > {: .language-python}
> > ![png](../fig/06_challenge_boxplot.png)
> {: .solution}
{: .challenge}


# Plotting time series data

Let's calculate number of counts per year for each species. To do that we need
to group data first and count the species (`species_id`) within each group.

~~~
yearly_counts = surveys_complete.groupby(['year', 'species_id'])['species_id'].count()
yearly_counts
~~~
{: .language-python}

When checking the result of the previous calculation, we actually have both the
`year` and the `species_id` as a row index. We can reset this index to use both
as column variable:

~~~
yearly_counts = yearly_counts.reset_index(name='counts')
yearly_counts
~~~
{: .language-python}

Timelapse data can be visualised as a line plot (`geom_line`) with years on `x`
axis and counts on the `y` axis.


~~~
(p9.ggplot(data=yearly_counts,
           mapping=p9.aes(x='year',
                          y='counts'))
    + p9.geom_line()
)
~~~
{: .language-python}

Unfortunately this does not work, because we plot data for all the species
together. We need to tell `plotnine` to draw a line for each species by
modifying the aesthetic function and map the species_id to the color:

~~~
(p9.ggplot(data=yearly_counts,
           mapping=p9.aes(x='year',
                          y='counts',
                          color='species_id'))
    + p9.geom_line()
)
~~~
{: .language-python}

![png](../fig/06_time_plot.png)

# Faceting

As any other library supporting the Grammar of Graphics, `plotnine` has a
special technique called *faceting* that allows to split one plot into multiple
plots based on a factor variable included in the dataset.

Consider our scatter plot of the `weight` versus the `hindfoot_length` from the
previous sections:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight',
                          y='hindfoot_length',
                          color='species_id'))
    + p9.geom_point(alpha=0.1)
)
~~~
{: .language-python}

We can now keep the same code and at the `facet_wrap` on a chosen variable to
split out the graph and make a separate graph for each of the groups in that
variable. As an example, use `sex`:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight',
                          y='hindfoot_length',
                          color='species_id'))
    + p9.geom_point(alpha=0.1)
    + p9.facet_wrap("sex")
)
~~~
{: .language-python}
![png](../fig/06_facet_plot.png)

We can apply the same concept on any of the available categorical variables:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight',
                          y='hindfoot_length',
                          color='species_id'))
    + p9.geom_point(alpha=0.1)
    + p9.facet_wrap("plot_id")
)
~~~
{: .language-python}

![png](../fig/06_facet_all_plot.png)

The `facet_wrap` geometry extracts plots into an arbitrary number of dimensions
to allow them to cleanly fit on one page. On the other hand, the `facet_grid`
geometry allows you to explicitly specify how you want your plots to be
arranged via formula notation (`rows ~ columns`; a `.` can be used as a
placeholder that indicates only one row or column).

~~~
# only select the years of interest
survey_2000 = surveys_complete[surveys_complete["year"].isin([2000, 2001])]

(p9.ggplot(data=survey_2000,
           mapping=p9.aes(x='weight',
                          y='hindfoot_length',
                          color='species_id'))
    + p9.geom_point(alpha=0.1)
    + p9.facet_grid("year ~ sex")
)
~~~
{: .language-python}
![png](../fig/06_select_plot.png)

> ## Challenge - facetting
> Create a separate plot for each of the species that depicts how the average
> weight of the species changes through the years.
>
> > ## Answers
> > yearly_weight = surveys_complete.groupby(['year', 'species_id'])['weight'].mean().reset_index()
> >
> > ~~~
> > (p9.ggplot(data=yearly_weight,
> >            mapping=p9.aes(x='year',
> >                           y='weight'))
> >     + p9.geom_line()
> >     + p9.facet_wrap("species_id")
> > )
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}


> ## Challenge - facetting
> Based on the previous exercise, visually compare how the weights of male and
> females has changed through time by creating a separate plot for each sex and
> an individual color assigned to each `species_id`.
>
> > ## Answers
> > yearly_weight = surveys_complete.groupby(['year', 'species_id', 'sex'])['weight'].mean().reset_index()
> >
> > (p9.ggplot(data=yearly_weight,
> >            mapping=p9.aes(x='year',
> >                           y='weight',
> >                           color='species_id'))
> >     + p9.geom_line()
> >     + p9.facet_wrap("sex")
> > )
> > {: .language-python}
> {: .solution}
{: .challenge}


# Further customization

As the syntax of `plotnine` follows the original R package `ggplot2`, the
documentation of `ggplot2` can provide information and inspiration to customize
graphs. Take a look at the `ggplot2` [cheat sheet](https://www.rstudio.com/wp-content/uploads/2015/08/ggplot2-cheatsheet.pdf), and think of ways to improve the plot. You can write down some
of your ideas as comments in the Etherpad.

The theming options provide a rich set of visual adaptations. Consider the
following example of a bar plot with the counts per year.

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='factor(year)'))
    + p9.geom_bar()
)
~~~
{: .language-python}

![png](../fig/06_overlap_bars.png)

Notice that we use the `year` here as a categorical variable by using the
`factor` functionality. However, by doing so, we have the individual year
labels overlapping with eachother. The `theme` functionality provides a way to
rotate the text of the x-axis labels:

~~~
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='factor(year)'))
    + p9.geom_bar()
    + p9.theme_bw()
    + p9.theme(axis_text_x = p9.element_text(angle=90))
)
~~~
{: .language-python}

![png](../fig/06_good_bars.png)

When you like a specific set of theme-customizations you created, you can save
them as an object to easily apply them to other plots you may create:


~~~
my_custom_theme = p9.theme(axis_text_x = p9.element_text(color="grey", size=10,
                                                         angle=90, hjust=.5),
                           axis_text_y = p9.element_text(color="grey", size=10))
(p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='factor(year)'))
    + p9.geom_bar()
    + my_custom_theme
)
~~~
{: .language-python}

![png](../fig/06_theme_plot.png)

> ## Challenge - customization
> Please take another five minutes to either improve one of the plots
generated in this exercise or create a beautiful graph of your own.
>
> Here are some ideas:
>
> * See if you can change thickness of lines for the line plot .
> * Can you find a way to change the name of the legend? What about its labels?
> * Use a different color palette (see http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/)
{: .challenge}


After creating your plot, you can save it to a file in your favourite format.
You can easily change the dimension (and its resolution) of your plot by
adjusting the appropriate arguments (`width`, `height` and `dpi`):


~~~
my_plot = (p9.ggplot(data=surveys_complete,
           mapping=p9.aes(x='weight', y='hindfoot_length'))
    + p9.geom_point()
)
my_plot.save("scatterplot.png", width=10, height=10, dpi=300)
~~~
{: .language-python}

{% include links.md %}

