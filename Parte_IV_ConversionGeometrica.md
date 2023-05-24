Sensores: preprocesado, corrección y fusión de imágenes (IV)
# CONVERSIÓN GEOMÉTRICA

Jessica Bernal Borrego
27/02/22

##### El concepto de corrección geométrica incluye cualquier cambio en la posición que ocupan los píxeles en la imagen. Algunas de las funciones de transformación que se aplican son las siguientes: 
> ![image](https://user-images.githubusercontent.com/100314590/158054367-c7f5ceae-6062-4528-a36b-64b39d836608.png)


##### En la práctica, se trata de identificar puntos en la imagen a corregir que coinciden con puntos de otra imagen o cartografía que se adopte como referencia, por lo que esencialmente se trata de una nueva georreferenciación de la imagen. Para nuestro ejemplo se va a utilizar una imagen carente de SRC. 

![image](https://user-images.githubusercontent.com/100314590/158054376-009b8a69-ecd5-400b-a411-c3a2761f1359.png)

### 1. Localización de los puntos de control comunes a la imagen y mapa.
##### Abrimos el georreferenciador de QGIS (*Ráster --> Georreferenciador*) y cargamos el ráster a georreferenciar o corregir.
 
![image](https://user-images.githubusercontent.com/100314590/158054393-eaa3e05d-0c97-4a79-b8d4-56680a673166.png)



### 2. Cálculo de las funciones de transformación entre coordenadas imagen y mapa, comprobando que RMS< tamaño píxel.

##### Antes de comenzar a marcar los puntos, es conveniente establecer los parámetros de configuración:
 
![image](https://user-images.githubusercontent.com/100314590/158054399-bbde09e2-3c36-4c83-a129-847c96f5f9f9.png)


##### Empezaremos con el tipo de transformación Polinomial. Establecemos el directorio de salida e indicamos que se guarden los puntos tras la ejecución del proceso. Si queremos generar un informe, también podemos indicarlo aquí.




### 3. Transferencia de los ND originales a la nueva posición.

##### Procedemos a la introducción de los nuevos puntos, uno a uno, primero marcando este en nuestra imagen a georreferenciar y después en el lienzo del mapa (salvo que las coordenadas de cada punto que se va a muestrear ya se conozcan en cuyo caso se indican directamente).

![image](https://user-images.githubusercontent.com/100314590/158054409-c339a744-91d4-4aa9-a368-d812cf50849a.png)
 
![image](https://user-images.githubusercontent.com/100314590/158054413-17d8d043-1e55-490d-8c7e-e507661b6ec8.png)
###### Lienzo mapa (arriba), georrefenciador (abajo). Vemos los puntos marcados en rojo.
 
![image](https://user-images.githubusercontent.com/100314590/158054421-fff8c912-cd9b-46c9-88ca-714b6237fbe0.png)



##### Vemos, en la parte inferior derecha, que la transformación Polinomial 1 arroja un error medio muy alto (> 1m), por lo que entramos en la configuración para probar si encontramos una ecuación de mejor ajuste. 

![image](https://user-images.githubusercontent.com/100314590/158054426-09a80f07-b07f-48cf-9846-9392047a3b81.png)




 

##### La Polinomial 2 arroja un error medio de 0 desactivando uno de los puntos, lo cual es aceptable. Antes de proseguir, podemos guardar los puntos para el caso de que la georreferenciación no se ejecute correctamente (*Archivo --> Save GCP Point as…*) 

![image](https://user-images.githubusercontent.com/100314590/158054431-7b4b0cd8-4f60-4597-bf0a-3ccaa2126cf7.png)





### 4. Resultado 

##### Se ha dado color a la imagen para mejor visualización:

![image](https://user-images.githubusercontent.com/100314590/158054435-ae8f2a6b-2f0e-4101-97ee-233756bb8b27.png)


### Informe:
 
![image](https://user-images.githubusercontent.com/100314590/158054451-dfb50789-295a-4b83-a512-9b6b51972b45.png)


