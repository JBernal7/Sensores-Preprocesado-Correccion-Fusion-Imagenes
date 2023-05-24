Sensores: preprocesado, corrección y fusión de imágenes (II)
# CORRECCIÓN ATMOSFÉRICA

Jessica Bernal Borrego
27/02/22

##### La presente tarea de corrección atmosférica tiene por objeto eliminar el incremento de la radiancia que le llega al sensor a causa de la interacción de energía electromagnética reflejada o emitida por las cubiertas con la atmósfera.  Esta corrección resulta fundamental si queremos realizar, por ejemplo, combinaciones lineales entre bandas, transformar los Niveles Digitales (ND) de la imagen en magnitudes físicas o realizar estudios multitemporales.
##### Si bien de forma paralela a la adquisición de las imágenes han de existir medidas de corrección, existen métodos basados en la predicción del efecto atmosférico que nos permiten hacerlo a partir de los datos de la imagen, como (1) la corrección del histograma por su valor mínimo, y (2) el método de Substracción de Píxeles Oscuros (SPO). En este ejercicio implementaremos ambos métodos utilizando para ello el software de código abierto QGIS 3.16. 

### 1.	Corrección del histograma por su valor mínimo
##### Es el método más sencillo. Con este, la reflectancia aparente (píxeles oscuros) situada en áreas con valores muy bajos de reflectancia se asimila a un producto de la dispersión atmosférica, por lo que puede ser usada como información para la calibración de la imagen (Chávez, 1988; 1999).
##### Generalmente, estos píxeles se corresponden con zonas de agua de cierta profundidad, baja eutrofización y escasa turbidez. En este sentido, aquellas imágenes en las que se recogen píxeles de océanos o mares la operación será más precisa, pues estos serán los píxeles que presenten los valores mínimos en el histograma. No obstante, si bien la reflectividad del agua es muy baja, esta presenta cierta reflectancia en las longitudes de onda más corta, siendo el grado de precisión de la corrección mayor a medida que aumentan las longitudes de onda. Esto es debido principalmente a lo que se conoce como dispersión Rayleigh, que aumenta rápidamente a medida que disminuye la longitud de onda. Para el agua, es a partir del infrarrojo cuando su reflectividad es prácticamente nula.

##### En este ejercicio se va a realizar la corrección atmosférica para la banda del infrarrojo cercano del satélite Landsat 8 (Banda 5). En nuestro caso, el recorte recoge una zona amplia de agua de mar, lo que permitirá realizar este tipo de corrección.

![image](https://user-images.githubusercontent.com/100314590/158053644-674d7997-2c89-4bbf-a2f4-18447f24dea6.png)
 

##### Para empezar, consultamos el valor mínimo de las bandas, esto lo podemos hacer a través de (*Ráster → Miscelánea → Información de ráster*) (ver Parte I), o haciendo clic derecho en la capa ráster que queremos consultar y, a continuación, en *Propiedades*:

 ![image](https://user-images.githubusercontent.com/100314590/158053652-4f0c348d-3bf0-4c07-a0cf-ae363762a288.png)



##### Cuando tenemos un archivo con varias bandas:
 
![image](https://user-images.githubusercontent.com/100314590/158053661-72978a9d-ae6b-42fd-8f6f-3009974636ab.png)


##### Vemos que cada banda presenta sus propios valores máximos y mínimos, siendo el valor mínimo mayor a medida que disminuye la longitud de onda (B3<B2<B1). Es por ello por lo que la corrección atmosférica debe hacerse para cada banda por separado. Para nuestro ejemplo con la banda 5, el valor mínimo es 5213. A continuación, utilizamos la calculadora ráster para restar el valor mínimo (*Ráster --> Calculadora ráster*):

![image](https://user-images.githubusercontent.com/100314590/158053664-d067819d-fb7f-406d-a460-6033289d3335.png)


##### Visualmente no observamos diferencias en el resultado, no obstante, podemos comprobar que ahora el valor mínimo estadístico es igual a 0:

![image](https://user-images.githubusercontent.com/100314590/158053667-247e51a6-cef9-4e1b-8e86-b1b703ab2ccd.png)
 

##### Una forma más precisa de aplicar este método del valor mínimo implicaría tomar valores en campo mediante un espectroradiómetro de una zona de agua limpia, calma y con suficiente profundidad para que el fondo no añada reflectividad. Por ejemplo, si la región del infrarrojo cercano equivalente a nuestra banda 5 mostrara una seña espectral transformada a ND de 23, el valor que debería restarse a toda la banda sería 5213-23 = 5190, de modo que nuestro valor mínimo quedara en esos 23 tomados in situ.

### 2.	SPO - Método de Substracción de Píxeles oscuros (DOS - *Dark Object Subtraction*)
##### En este caso, no se realiza una resta simple del valor mínimo, sino que se ajusta este mínimo según la mejor de una serie de fórmulas (la de mejor ajuste al metadato) que convierten los valores de ND más bajos de los píxeles en valores de radiancia (L). 

![image](https://user-images.githubusercontent.com/100314590/158053674-e7bf0010-5ddd-4a9d-b588-ebda8edddde3.png)

 

##### Por otro lado, lo más probable para la mayoría de las imágenes es que estas no contengan píxeles verdaderamente negros, en cuyo caso la corrección se aplica asumiendo un porcentaje de reflectancia del 1% en esas áreas; tal como lo señalan las siguientes expresiones:

![image](https://user-images.githubusercontent.com/100314590/158053680-3654bdd0-04f6-4c58-b492-5edddcceb4b5.png)


##### Para este método utilizamos el plugin SCP (*Semi-Automatic Classification Plugin*) de QGIS.  Una vez instalado, accediendo desde la pestaña del menú *SCP --> Preprocesamiento --> Landsat*. Tras señalar la carpeta contenedora de nuestras imágenes Landsat y del archivo MTL aparejado a estas (contenedor de los metadatos), marcaremos la opción “Aplicar corrección atmosférica DOS1” y ejecutaremos el proceso:

![image](https://user-images.githubusercontent.com/100314590/158053684-a4d2d46d-31c1-4b26-b2c4-e8e74b170d26.png)

 


##### Consultamos las estadísticas del ráster compuesto y comprobamos que el mínimo ahora es 0.

![image](https://user-images.githubusercontent.com/100314590/158053693-36502b8d-9f84-40db-8e86-b1926fb70d51.png)













