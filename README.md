*Esta herramienta digital forma parte del catálogo de herramientas del **Banco Interamericano de Desarrollo**. Puedes conocer más sobre la iniciativa del BID en [code.iadb.org](https://code.iadb.org)*

<h1 align="center"> eMAPS Score QGIS Plugin</h1>
<p align="center"><img src="https://pbs.twimg.com/profile_images/1067450803894607872/VoRm04r0.jpg"  width="350"></p> 

## Tabla de contenidos:
---

- [Badges o escudos](#badges-o-escudos) 
- [Descripción y contexto](#descripción-y-contexto)
- [Guía de usuario](#guía-de-usuario) 
- [Guía de instalación](#guía-de-instalación) 
- [Cómo contribuir](#cómo-contribuir) 
- [Código de conducta](#código-de-conducta)
- [Autores](#autores) 
- [Información adicional](#información-adicional)
- [Licencia](#licencia)


## Badges o escudos
---



## Descripción y contexto
---
eMAPS.ec es una herramienta de código abierto para la evaluación en microescala de entornos peatonales desarrollada por el Grupo de Investigación LlactaLab Ciudades Sustentables en la [Universidad de Cuenca](http://llactalab.ucuenca.edu.ec/)

En esta documentación podrás aprender la metodología y herramientas para realizar el levantamiento de información en forma de encuestas de eMAPS, configuración del cálculo de score y convertirlos a puntajes de caminabilidad.
Las puntuaciones se calculan en tres niveles: elemento, subescala y total. La unidad de análisis es el segmento de la calle, y los puntajes del segmento de la calle se pueden agregar aún más (por ejemplo, vecindarios, zonas de amortiguamiento o isócronas, alrededor de las escuelas, etc.).

Esta herramienta se basa en el protocolo MAPS original (Cain KL, Millstein RA, Geremia CM (2012). Auditoría de microescala de paisajes urbanos peatonales (MAPS): Manual de recopilación y puntuación de datos. Universidad de California en San Diego. Disponible para descargar en: http://sallis.ucsd.edu/measures/maps)


## Guía de usuario
---
Para ejemplificar de mejor manera, vamos a poner en práctica la herramienta, en este tutorial vamos a calcular el score de caminabilidad eMAPS.ec para una escuela, caso de estudio en la ciudad de Cuenca, Ecuador.

Requisitos:

* Tener una instalación de QGIS https://www.qgis.org/

* Haber instalado el plugin eMAPS.ec en QGIS 

* Descargar los siguientes archivos:

	* [Capa ráster con Modelo Digital de Elevaciones para área de estudio](https://emaps.readthedocs.io/es/latest/_downloads/736f776c4f4d4894e6ccc98116869160/dem.tif)
	* [Capa vectorial de area de estudio](https://emaps.readthedocs.io/es/latest/_downloads/f23c3fa549a7be8f27a381888e7ad5c4/areas.gpkg) 
	* [Capa vectorial de segmentos de calle](https://emaps.readthedocs.io/es/latest/_downloads/b5c674e8dae3466686712297f9ddae0c/segments.gpkg)
	* [Datos de levantamiento de esegmentos de calle](https://emaps.readthedocs.io/es/latest/_downloads/2478752e4aedc5bb1f04a33d1e0c3f8f/segments_evaluation.csv)
	* [Datos de levantamiento de lotes](https://emaps.readthedocs.io/es/latest/_downloads/5c46100108ca7f820d78da06eac4ddb4/parcels_evaluation.csv)
	* [Archivo CSV de especificación de variables eMAPS.ec](https://emaps.readthedocs.io/es/latest/_downloads/a13cb7a8e8dabc0771878273e4f022c6/eMAPS_specification.csv) 
	* [Archivo CSV de parámetros generales](https://emaps.readthedocs.io/es/latest/_downloads/c673a0b38d0bc723e99b12cdf3dd4f2f/eMAPS_general_params.csv)

En este ejemplo ya hemos definido el área de estudio, realizado el levantamiento de información en campo y contamos con la información levantada en campo descargada desde la herramienta KoboToolBox mediante el plugin eMAPS.ec, por lo que vamos a realizar únicamente el pre-procesamiento y el cálculo del score.

**QGIS**

Como paso inicial cargamos las capas descargadas a QGIS
![](https://emaps.readthedocs.io/es/latest/_images/t1.png)

**Pre Procesamiento**

El algoritmo de preprocesamiento es parte del Plugin eMAPS para QGIS y es un paso opcional que permite para las capas vectoriales de segmentos de calle y área de estudio realizar una validación de las geometrías y calcular las columnas:

* `<emaps_len>` calcula la longitud en metros del segmento de calle
* `<emaps_slo>` calcula el porcentaje de pendiente del segmento de calle

Para ejecutar el algoritmo de pre-procesamiento es necesario proporcionar las siguientes entradas:

* Seleccionarl la Capa de Area de estudio `<areas.gpkg>`
* Seleccionarl la Capa de Segmentos de calle que vamos a evaluar `<segments.gpkg>`
* Seleccionar en»Ráster DEM File» el archivo ráster con el modelo digital de elevaciones `<dem.gif>`

![](https://emaps.readthedocs.io/es/latest/_images/t1.gif)

Como resultado obtenemos las capas de `<OUTPUT: Areas eMAPS>` y `<OUTPUT: Segments eMAPS>` validadas y con los atributos de pendiente y longitud que el algoritmo utilizará en el cálculo.

**Cálculo de Score eMAPS.ec**

En la caja de herramientas dentro de «eMAPS Análisis» seleccionamos el proceso «Score eMAPS» y seleccionamos nuestras capas de entrada con los archivos que nos descargamos y con las salidas del pre-procesamiento:

![](https://emaps.readthedocs.io/es/latest/_images/t2.png)

Ejecutado el proceso se cargan en QGIS las capas de salida con su simbología y las tablas de atributo con el score de caminabilidad eMAPS.ec para cada segmento evaluado y para el área de estudio:

![](https://emaps.readthedocs.io/es/latest/_images/t3.png)
![](https://emaps.readthedocs.io/es/latest/_images/t4.png)

Por defecto las simbología se aplica al score total calculado por segmento, pero podríamos mediante el editor de estilos de qGIS seleccionar cualquier escala, sub escala o variable para la visualización por ejemplo la variable `<intersections_positive_ramps>` de la escala «intersections» y sub escala «intersections_positive»:

![](https://emaps.readthedocs.io/es/latest/_images/t5.png)
 	
## Guía de instalación
---
Una vez descargado el plugin es necesario cargarlo en la sección de complementos de QGis desde el menú «Complementos -> Ver y Administrar Complementos -> Instala a partir de ZIP»:

![](https://emaps.readthedocs.io/es/latest/_images/git.png)

![](https://emaps.readthedocs.io/es/latest/_images/qgis.png)

Ya instalado el plugin eMAPS en QGIS podemos encontrar los procesos en el ToolBox o Caja de Herramientas, para la descacrga de los datos seleccionamos dentro de «eMAPS Análisis» el proceso «Download eMAPS data»

![](https://emaps.readthedocs.io/es/latest/_images/qgis2.png)

En el formulario de «Download eMAPS data» debemos llenar los siguientes datos:

* **URL KoboToolBox.-** por defecto apunta al servidores de [KoboToolBox](https://kf.kobotoolbox.org/), se debe cambiar si se tiene una propia instancia de Kobo.
* **Usuario KoboToolBox.-** nombre de usuario en la plataforma KoboToolBox
* **Contraseña KoboToolBox.-** password de usuario en la plataforma KoboToolBox
* **Código de formulario KoboToolBox.-** código del formulario KoboToolBox del que se va a descargar los datos, puede encontrar el código de formulario obserbando la URL en la aplicación KoboToolBox ej:

![](https://emaps.readthedocs.io/es/latest/_images/kobo2.png)

* **Código de estudio.-** cuando se utiliza el formulario Kobo para varios estudios, una de las preguntas en la encuesta solicita el código de estudio, si se especifica se descargará los datos solo para ese código de estudio, caso contrario se descargarán todos los datos levantados.

* **Nombre de usuario evaluador.-** en el formulario Kobo hay una pregunta para identificar al usuario que realiza la evaluación, si está especificado se descargará solo los datos de ése usuario.

* **Tipo de Levantamiento.-** en el formulario Kobo se especifica en una pregunta el tipo de levantamiento, se puede seleccionar los que se desee descargar, las opciones pueden ser:

	* Evaluación
	* Validación
	* Entrenamiento
	
* **Cabecera.-** especifica la forma en la que se descargarán las cabeceras de los archivos CSV las opciones son:

	* Etiquetas: los nombres de columnas contendrán los códigos de pregunta y la etiqueta
	* Códigos de pregunta.- los nombres de columnas contendrán únicamente los códigos de las preguntas
	
Al ejecutar el proceso, se descargarán los datos desde el servidor de KoboToolBox especificado y se añadiran las capas «eMAPS Segments Evaluation» y «eMAPS Parcels Evaluation» al proyecto QGIS en formato vectorial como capa de puntos, si se desea se puede exportar éstas capas a cualquier formato vectorial soportado por QGIS.


### Dependencias

Es necesario tener una instalación de [QGIS](https://www.qgis.org)
   
## Cómo contribuir 
---
Desde el punto de vista técnico del código, reportando issues y probando en diferentes plataformas y versiones de QGIS (el software sobre el que está montado el plugin)
También se pueden crear y publicar plantillas de scorer (eMAPS general params file) personalizadas  o adaptadas a otras ciudades o a otras prioridades, con lo cual podríamos tener un repositorio de archivos de parámetro.
Finalmente, se pueden compartir los resultados de la aplicación de la herramienta para publicarlos en nuestro geonode

## Código de conducta 
---


## Autores
---
Daniel Orellana (Conceptualización y adaptación metodológica)
Adriana Quezada (Adaptación metodológica y validación)
Ana María Andino (Desarrollo metodológico y validación)
Christian Peralta (Desarrollo metodológico y validación)
Javier García (Desarrollo y programación)

## Información adicional
---
Este proyecto fue financiado por la Dirección de Investigación de la Universidad de Cuenca y CEDIA

## Licencia 
---
[LICENCIA](https://github.com/EL-BID/Plantilla-de-repositorio/blob/master/LICENSE.md)

GNU General Public License v3.0


