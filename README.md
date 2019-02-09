
# CSS-Grid

CSS Grids nos permite generar layouts o distribuciones de contenido  en nuestro sitio web de forma eficiente mediante cuadriculas compuesta por filas y columnas

## Indice

1. [Conceptos Generales](#conceptos)
2. [Uso y Propiedades](#uso-propiedades)
	- [grid-template](#grid-template)
		- [grid-template-rows](#grid-template-rows)
		- [grid-template-columns](#grid-template-columns)
		- [Consejos de Uso](#grid-template-consejos)
	- [grid-gap](#grid-gap)
		- [grid-row-gap](#grid-row-gap)
		- [grid-column-gap](#grid-column-gap)
	- [grid-row | grid-column](#grid-row-column)
		- [grid-row-start](#grid-row-start)
		- [grid-row-end](#grid-row-end)
		- [grid-column-start](#grid-column-start)
		- [grid-column-end](#grid-column-end)
		- [Consejos de Uso](#grid-row-column-consejos)
	- [grid-auto-flow](#grid-auto-flow)
		- [grid-auto-columns](#grid-auto-columns)
		- [grid-auto-rows](#grid-auto-rows)
	- [grid-template-areas](#grid-template-areas)
		- [grid-area](#grid-area)
	- [align-content | justify-content](#align-justify-content)
	- [align-items | justify-items](#align-justify-items)
		- [align-self](#align-self)
		- [justify-self](#justify-self)

<div id='conceptos'/>

## Conceptos Generales

1. **Grid Conatiner:** es una etiqueta que hace la función de contenedor o elemento padre, la cual, tiene asignado un `display: grid;`

2. **Grid Item:** son los hijos directos de un *Grid Container* y quienes componen la cuadricula que podremos personalizar a nuestra preferencia

3. **Grid Line:** son lineas invisibles divisoras horizontales y verticales dentro de la cuadricula.

4. **Grid Track:** es un espacio entre dos lineas adyacentes, comúnmente llamadas filas y columnas.

5. **Grid Cell:** es un espacio entre 2 filas adyacentes y 2 columnas adyacentes, comúnmente denominada como celda.

6. **Grid Area:** es un espacio rodeado por 4 *Grid Lines*, el cual, puede ser desde 1 celda a varias.

7. **Grid Implícito** - esta conformado por los elementos HTML que no están siendo contemplados por las filas y columnas definidas dentro de nuestro *Grid Container* siendo de tamaño automático según su contenido

<div id='uso-propiedades'/>

## Uso y Propiedades
Para disponer de todas las características que nos brinda CSS Grid primero debemos definir un *Grid Container*, es decir, definirle a una etiqueta que haga la función de contenedor en nuestro HTML un display de tipo grid. Cada uno de sus hijos directores (*Grid Items*) compondrán la cuadricula, lo que nos permitirá alinearlos a nuestro antojo.

~~~
body { 
	display: grid;
}
~~~

<div id='uso-propiedades'/>

## grid-template

Define el tamaño y disposición de filas y columnas que tendrá el Grid Container. Para definir una cuadricula simplemente colocamos el tamaño de cada una de sus filas y columnas separados por un espacio y las filas de columnas por una pleca (/).

~~~
body { 
	display: grid;
	grid-template: 500px 500PX / 200px 600px;
}
~~~

Aquí estaríamos definiendo en el *Grid Container* una cuadricula de 2*2, 2 filas de 500 y 500 pixeles y 2 columnas de 200 y 600 pixeles. 

<div id='grid-template-rows'/>

**grid-template-rows:** define únicamente la disposición de filas mediante su alto.

`grid-template-rows: 500px 500px;`

<div id='grid-template-columns'/>

**grid-template-columns:** define únicamente  la disposición de columnas mediante su ancho. 

`grid-template-columns: 200px 600px;`

<div id='grid-template-consejos'/>

*CONSEJOS DE USO*

Para definir el tamaño de las filas y columnas podemos utilizar cualquier unidad de medida, pero hay ciertos valores y funciones que nos pueden ayudar a hacerlo mas fácilmente:

 - **fracciones (fr)** - es una unidad de medida exclusiva para *CSS Grid* que representa una fracción del espacio disponible en el contenedor de la cuadricula. 
 
	 `grid-template: 100px / 100px 1fr 3fr;`
 
	 Define una cuadricula de 1*3, es decir, 1 fila de 100px y 3 columnas, la primera de 100px y las otras 2 de ancho flexible según el ancho restante en el *Grid Container*. La segunda columna tendrá un 25% del ancho restante y la tercera 3 veces mas en relación a la segunda, es decir, un 75% del ancho restante.

  - **auto** - define un tamaño automático para una fila o columna según el alto si es fila o ancho si es columna. 
  
	`grid-template: 100px / auto auto;` 

	Define una cuadricula de 1*2, es decir, 1 fila de 100px y 2 columnas de ancho definido por su contenido.

  - **repeat (cantidad, tamaño)** - esta función nos permite repetir un valor x cantidad de veces. 

	`grid-template: 100px / repeat(4, 250px);` 

	Define una cuadricula de 1*4, es decir, con 1 fila y 4 columnas de 250px.
  
  - **repeat (auto-fill, tamaño)** - si en vez de un numero llenamos la cantidad con el valor de *auto-fill* nos permitiría crear una cantidad de columnas o filas según quepan en el *Grid Container* con el tamaño definido. 

	`grid-template: 100px / repeat(auto-fill, 250px);` 

	Define una cuadricula con 1 fila de 100px y una cantidad de columnas basada en el ancho del contenedor, por ejemplo, si nuestro *Grid Container* fuese de 750px crearía una cuadricula de 1*3, es decir, con 3 columnas de 250px

 - **minmax ()** - define un ancho flexible entre 2 números (ancho minimo y maximo) para una fila o columna. 

	`grid-template: 100px / minmax(100px, 500px);` 

	Define una cuadricula de 1*1, es decir, 1 fila de 100px y 1 columnas de 500px solo si el *Grid Container* tiene un ancho mínimo de 500px, en caso contrario, el ancho de la columna podrá achicarse hasta llegar a los 100px como mínimo.

<div id='grid-gap'/>

## grid-gap

Define un espaciado entre filas y columnas sin añadirlo a los bordes externos de la cuadricula. Puede recibir un valor para ambos o 2 valores separados, uno para filas y otro para columnas;
~~~
body { 
	display: grid;
	grid-template: 200px 200px / 200px 200px;
	grid-gap: 10px 5px;
}
~~~

Aquí estaríamos definiendo una separación de 10px entre las filas y de 5px entre las columnas de nuestro Grid.

<div id='grid-row-gap'/>

**grid-row-gap** -  define el espaciado entre filas.
 
`grid-row-gap: 10px;`

<div id='grid-column-gap'/>

**grid-column-gap** - define el espaciado entre columnas.
 
`grid-column-gap: 5px;`

<div id='grid-row-column'/>

## grid-row | grid-column

Modifica el flujo normal de un *Grid Item* definiendo la fila | columna de comienzo y final, permitiendo también de esta manera definir cuantas filas | columnas abarcara. 

Estos valores se definen mediante 2 números separados por una /, los cuales hacen referencia a la *Grid Line* de comienzo y final.

~~~
body { 
	display: grid;
	grid-template: 200px 200px / 200px 200px;
}

	.primer-hijo {
		grid-row: 1 / 3;
		grid-column: 2 / 3;
	}
~~~
Aquí estamos definiendo un *Grid Container* o cuadricula de 2*2, en la cual modificamos el flujo normal de uno de sus *Grid Item* que es una etiqueta con la clase "primer-hijo". A este elemento le hemos dicho que abarque 2 filas, es decir, que comience desde la *Grid Line* #1 y termine en la #3 y que en su posición en columnas comience desde la *Grid Line* #2 y termine en la #3, es decir, se ubique en la 2da columna. El resultado se vería de la siguiente manera:
~~~
   1ra     2da     3ra
1ra |-------|-------|
    |       |   x   |
2da |-------|---x---|
    |       |   x   |
3ra |-------|-------|
~~~

<div id='grid-row-start'/>

**grid-row-start** - define únicamente la *Grid Line* en filas de comienzo para un *Grid Item*. 

`grid-row-start: 1;`

<div id='grid-row-end'/>

**grid-row-end** - define únicamente  la *Grid Line* en filas hasta donde llegara un *Grid Item*. 

`grid-row-end: 3;`

<div id='grid-column-start'/>

**grid-column-start** - define únicamente  la *Grid Line* en columnas de comienzo para un *Grid Item*. 

`grid-column-start: 2;`

<div id='grid-column-end'/>

**grid-column-end** - define únicamente  la *Grid Line* en columnas hasta donde llegara un *Grid Item*. 

`grid-column-end: 3;`

<div id='grid-row-column-consejos'/>

*CONSEJOS DE USO*

Para definir la cantidad de filas o columnas que abarcara un *Grid Item* o en donde comenzara podemos utilizar ciertos valores que nos pueden ayudar a hacerlo mas fácilmente:

 - **-1** - hace referencia a todas las filas existentes y lo podemos utilizar para indicarle a un *Grid Item* que abarque todas las columnas o filas de un contenedor. 

	`grid-row: 1 / -1;`
 
 - **span** - hace referencia directamente al numero de filas o columnas que abarcara y solo se puede utilizar con las propiedades grid-row y grid-column. 

	`grid-row: span 3;`
 
 - **auto** - define el final o inicio de una fila o columna de manera automática. 

	`grid-column: 2 / auto;`

<div id='grid-auto-flow'/>

## grid-auto-flow

Define la dirección en donde se ubicaran los elemento que no estén definidos como filas y columnas dentro del *Grid Container*, es decir, el *Grid Implicito*, el cual, por defecto los ubica como filas (row).

~~~
body { 
	display: grid;
	grid-template: 200px 200px / 200px 200px;
	grid-auto-flow: column;
}
~~~
Aquí estamos definiendo una cuadricula de 2*2, con un tamaño especifico para un numero limitado(4) de hijos directos (*Grid Item*). En caso que el contenedor tuviese mas hijos de los que hemos definido los añadiría a la cuadricula en forma de filas como opción por defecto, pero en este caso hemos modificado el *Grid Container* para que los añada como columnas.

<div id='grid-auto-columns'/>

**grid-auto-columns** - define el ancho de todas las posibles columnas no definidas en el *Grid Container*. `grid-auto-columns: 100px;`

<div id='grid-auto-rows'/> 

**grid-auto-rows** - define el alto de todas las posibles filas no definidas en el *Grid Container*. `grid-auto-rows: 100px;`

<div id='grid-template-areas'/>

## grid-template-areas

Define multiples *Grid Area* dentro del *Grid Container*, mediante un nombre personalizado para cada una de ellas, las cuales, nos permitirán modificar de manera dinámica la ubicación y cuantas filas o columnas abarcaran nuestros Grid Items en la cuadricula.

Para definir un *Grid Area* en nuestra cuadricula utilizamos comillas("") para indicar una fila y adentro definimos las columnas mediante un nombre personalizado o un punto(.) para que la celda valla vacía, y los valores los separamos con un espacio.

~~~
body {
	display: grid;
	grid-template: 100px calc(100vh - 200px) 100px / 1fr 1fr;
	grid-template-areas: "menu menu" "contenido publicaciones" ". footer"
}
~~~
Aquí estamos definiendo una cuadricula de 3*2 , en la cual, asignamos multiples *Grid Areas* identificadas con 4 nombres diferentes y un punto (celda vacía) que llenaran la cuadricula cuando los asignemos a los hijos directos (*Grid Item*) del *Grid Container*.

<div id='grid-area'/>

**grid-area** - asigna un *Grid Area* mediante su nombre a un *Grid Item*, y se usa en conjunto para poder trabajar con la propiedad *grid-template-areas*.
~~~
	.hijo-menu {
		grid-area: menu;
	}
	.hijo-contenido {
		grid-area: contenido;
	}
	.hijo-publicaciones {
		grid-area: publicaciones;
	}
	.hijo-footer {
		grid-area: footer;
	}
~~~
Aquí estamos asignando las *Grid Areas* que declaramos en el *Grid Container* a cada uno de los *Grid Items*, quedando como resultado lo siguiente:

~~~
|---------------||---------------|
|              menu              |
|---------------||---------------|
|               ||               |
|   contenido   || publicaciones |
|               ||               |
|---------------||---------------|
|               ||    footer     |
|---------------||---------------|
~~~

<div id='align-justify-content'/>

## align-content | justify-content

Define la distribución de las filas / columnas que componen el *Grid Container*, permitiendo alinear estos elementos de manera simétrica en su espacio vertical / horizontal.

Para definir el tipo de alineación de nuestros *Grid Items* podemos utilizar cualquiera de los siguientes valores:

  - **flex-start** - ubica la cuadricula al inicio de su espacio vertical (arriba) si la propiedad es *align-content* o  al inicio de su espacio horizontal (izquierda) si la propiedad es *justify-content*.
 
 - **flex-end** - ubica la cuadricula al final de su espacio vertical (abajo) si la propiedad es *align-content* o  al final de su espacio horizontal (derecha) si la propiedad es *justify-content*.
 
 - **center** - ubica la cuadricula centrada en su espacio vertical si la propiedad es *align-content* o en su espacio horizontal si la propiedad es *justify-content*.

  - **space-around** - ubica los *Grid Items* a lo largo de todo el espacio mediante un espaciado que se suma entre cada fila si la propiedad es *align-content* o entre cada columna si la propiedad es *justify-content*.
 
 - **space-evenly** - ubica los *Grid Items* a lo largo de todo el espacio mediante un espaciado del mismo ancho entre cada fila si la propiedad es *align-content* o entre cada columna si la propiedad es *justify-content*.
 
 - **space-between** - ubica los *Grid Items* a lo largo de todo el espacio  mediante un espaciado del mismo ancho entre cada fila o columna pero solamente interno, es decir, sin añadirlo a los extremos de las filas si la propiedad es *align-content* o de las columnas si la propiedad es *justify-content*.

<div id='align-justify-items'/>

## align-items | justify-items

Define la distribución de los elementos contenidos en los *Grid Items* permitiendo alinear estos elementos de manera simétrica en su espacio vertical / horizontal. 

Cualquiera de estas 2 propiedades se definen en el *Grid Container* y les podemos asignar los siguientes valores: 

  - **flex-start** - ubica los elementos al inicio de su espacio vertical (arriba) si la propiedad es *align-items* o  al inicio de su espacio horizontal (izquierda) si la propiedad es *justify-items*.
 
 - **flex-end**- ubica los elementos al final de su espacio vertical (abajo) si la propiedad es *align-items* o  al final de su espacio horizontal (derecha) si la propiedad es *justify-items*.
 
  - **center** - ubica los elementos centrados en su espacio vertical si la propiedad es *align-items* o en su espacio horizontal si la propiedad es *justify-items*.
 
 - **stretch** -  los elementos cubren todo el espacio que tienen disponible verticalmente si la propiedad es *align-items* o horizontalmente si la propiedad es *justify-items*.

Para alinear un *Grid Item* de manera individual podemos utilizar las siguientes propiedades:

<div id='align-self'/>

**align-self** - ubica los elementos de un *Grid Item* especifico en su espacio vertical.

<div id='justify-self'/>

**justify-self** - ubica los elementos de un *Grid Item* especifico en su espacio horizontal.