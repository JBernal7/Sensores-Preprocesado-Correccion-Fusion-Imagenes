# Sensores: preprocesado, corrección y fusión de imágenes

Este repositorio contiene documentación detallada sobre el análisis y estudio llevado a cabo en el campo de los sensores, centrándose en el preprocesado, corrección y fusión de imágenes. El trabajo se realiza utilizando el software QGIS.

## Contenido del repositorio

El repositorio se divide en cuatro partes, que abarcan diferentes aspectos del procesamiento de imágenes:

### Parte I: Fusión de imágenes Landsat 8

En esta sección, se describe el proceso de fusión de imágenes de un algoritmo no implementado en QGIS. Se explica paso a paso el desarrollo del algoritmo de fusión, centrándose en el método Á TROUS de pansharpening. Se aplica la fusión a un corte de imagen actual de Landsat 8 que incluye la zona afectada por un incendio en septiembre de 2021 en Sierra Bermeja, Málaga. Se utilizan una imagen multiespectral formada por 7 bandas con un tamaño de píxel de 30 m y una imagen pancromática de una única banda con un tamaño de píxel de 15 m.

### Parte II: Corrección atmosférica

Esta sección tiene como objetivo eliminar el efecto de la interacción de energía electromagnética reflejada o emitida por las cubiertas con la atmósfera, conocido como incremento de radiancia. La corrección atmosférica es fundamental para realizar combinaciones lineales entre bandas, transformar los Niveles Digitales (ND) en magnitudes físicas y realizar estudios multitemporales.

### Parte III: Conversión a parámetros físicos

En esta parte, se muestra la conversión de los valores de los Niveles Digitales (ND) en distintos parámetros físicos según la longitud de onda de las bandas. Antes de realizar estas operaciones, es necesario llevar a cabo una corrección atmosférica.

### Parte IV: Conversión geométrica

En esta sección se aborda el concepto de corrección geométrica, que incluye cualquier cambio en la posición que ocupan los píxeles en la imagen. Se presenta un ejemplo práctico de corrección geométrica.

## Requisitos y uso

Para reproducir los pasos y ejemplos descritos en cada parte, se requiere el software QGIS. Se proporcionan instrucciones detalladas junto con el código y ejemplos relevantes en cada archivo Markdown.

## Contribución
Dado que este repositorio está destinado a ser un archivo personal (registro de las actividades realizadas en el marco del Máster Oficial [Geoforest](https://mastergeoforest.es/) ), no estoy buscando contribuciones activamente. Sin embargo, si encuentras algún error o tienes alguna sugerencia de mejora, no dudes en abrir un issue.

Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a
[Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
