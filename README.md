# Proyecto del Primer Cuatrimestre Fundamentos de Programación (Curso  20/21)
Autor/a: Jairo Escánez García;   uvus:&lt;uvus del autor&gt;

Revisión, reestructuración y adaptación para FP: Toñi Reina

Este es un ejemplo de proyecto realizado por un estudiante en el curso 2020/21. El código del estudiante se ha corregido, reestructurado y adaptado.


El proyecto tiene como objetivo analizar los datos de pobreza publicados en el dataset de Kaggle que se puede descargar de la siguiente URL (https://www.kaggle.com/johnnyyiu/predicting-poverty). El dataset original tiene 59 columnas, ninguna de las cuales es de tipo fecha. Así que, por una parte, se ha recortado el número de columnas escogiendo sólo 13 de las 59 columnas, y se han añadido dos columnas, una de tipo entero que recoge el dinero que tiene en el banco la persona, y otra columna de tipo fecha, que se ha generado con fechas aleatorias y que representa la fecha en la que se perdió el trabajo.


## Estructura de las carpetas del proyecto

* **/src**: Contiene los diferentes módulos de Python que conforman el proyecto.
    * **poverty.py**: Contiene funciones para explotar los datos sobre pobreza.
    * **poverty_test.py**: Contiene funciones de test para probar las funciones del módulo `poverty.py`. En este módulo está el main
    * **parsers.py**: Contiene funciones de parseo de datos.
    * **graficas.py**: Contiene funciones para dibujar gráficas 
* **/data**: Contiene el dataset o datasets del proyecto
    * **poverty_data.csv**: Archivo con los datos de pobreza que van a ser explotados.
        
## Estructura del *dataset*

Cada fila del dataset recoge los datos anonimizados de una persona, es decir, no sabemos sus nombre ni sus apellidos. Para cada persona se registran 15 datos. Por lo tanto, el dataset está compuesto por 15 columnas, con la siguiente descripción:

* **row_id**: de tipo int, es un identificador entero.
* **country**: de tipo str, representa la inicial del país del registro.
* **is_urban**: de tipo boolean, representa si el país es urbano o no.
* **age**: de tipo int, representa la edad de la persona.
* **female**: de tipo boolean, representa si es de género femenino o no.
* **married**: de tipo boolean, representa si está casado o no.
* **religion**: de tipo str, representa la religión de la persona.
* **relationship_to_hh_head**: de tipo str, representa la situación familiar, si es cabeza de familia, padre.
* **education_level**: de tipo int, representa el nivel de estudios de la persona.
* **can_add**: de tipo boolean, representa si sabe sumar.
* **num_times_borrowed_last_year**: de tipo int, representa el número de veces endeudado en el último año.
* **can_use_internet**: de tipo boolean, representa si la persona sabe usar internet.
* **phone_ownership**: de tipo int, representa el número de móviles que posee la persona.
* **dinero_en_banco**: de tipo int, representa el dinero que posee la persona en el banco. Esta columna se ha generado con datos aleatorios.
* **fecha_ultimo_trabajo**: de tipo date, representa la fecha de la última vez que estuvo trabajando. Esta columna se ha generado con datos aleatorios.


## Tipos implementados

Para trabajar con los datos del dataset se ha definido la siguiente tupla con nombre:

`Info = namedtuple('Info','id, pais, es_urbano, edad, genero, casado, religion, situacion_familiar,nivel_educacion,sabe_sumar,
                           veces_endeudado,puede_usar_internet,num_moviles,dinero_banco,fecha_ultimo_trabajo')`

en la que los tipos de cada uno de los campos son los siguientes:

`Info(int, str, boolean, int, str. boolean, str, str, in, boolean, int, boolean, int, int, datetime.date)`

Las decisiones de diseño más destacadas de este tipo son:
* El campo genero es de tipo str, en lugar de boolean como aparece en el dataset original, y puede tomar los valores 'Hombre' o 'Mujer'.

## Funciones implementadas
En este proyecto se han implementado las siguientes funciones, que están clasificadas según los bloques y tipos de funciones que se requieren en cada una de las entregas.
El módulo principal es el módulo poverty.py, así que aquí es donde se hará referencia a cada uno de los bloques de las entregas.
### Módulo poverty

#### Entrega 1

* **Bloque 0**  
  * **lee_fichero(fichero)**: lee los datos del fichero csv y devuelve una lista de tuplas de tipo Info con los datos del fichero. Para implementar esta función se han definido las siguientes funciones auxiliares en el [módulo `parsers`](#módulo-parsers):
    * **parsea_booleano(cadena)**: Función para convertir de cadena a booleano.
    * **parsea_genero(cadena)**: Función para convertir de cadena (con valores True o False) a género.
    * **parsea_fecha(cadena)**: Función para convertir de cadena a fecha.   
 
 #### Entrega 2

 * **Bloque 1**
   * **selecciona_registros_de_genero_y_pais(registros,genero='Hombre',pais='A')**: Dadas una lista de tuplas de tipo Info, un género y un pais, devuelve una lista de tuplas de tipo Info con los datos de las personas del género y pais dados como parámetros.

 * **Bloque 2**
   * **cuenta_endeudados(registros,genero='Hombre')**: Dadas una lista de tuplas de tipo Info y un género, devuelve el número de personas del género dado como argumento que se han endeudado.
   * **calcula_porcentaje_endeudados(registros,genero='Hombre')**: Dadas una lista de tuplas de tipo Info y un género, devuelve el porcentaje de personas endeudadas del género dado como parámetro con respecto al total de personas de ese género. Si el porcentaje no se puede calcular, devuelve None.

* **Bloque 3**
  * **obten_registros_mas_dinero_banco(registros)**: Dada una lista de tuplas de tipo Info, devuelve una lista de tuplas de tipo Info con la información de las personas que tienen más dinero en el banco.

#### Entrega 3

* **Bloque 4**

  * **obten_n_registros_menor_num_moviles(registros,genero='Hombre',n=3)**: Dadas una lista de tuplas de tipo Info, un género y un pais, devuelve una lista de tuplas de tipo Info con los datos de las n personas endeudadas con menor número de móviles.
  * **calcula_total_veces_endeudados_por_situacion_familiar(registros,edad)**: Dadas una lista de tuplas de tipo Info y una edad, devuelve un diccionario en el que las claves representan una situación familiar, y los valores son el total de veces que se han endeudado las personas con la edad dada como parámetro que están en la situación familiar representada por la clave.

* **Bloque 5**
  * **obten_media_edad_por_nivel_educacion(registros)**: Dada una lista de tuplas de tipo Info, devuelve un diccionario en el que las claves representan el nivel de educacion y los valores la media de edad de las personas que tienen ese nivel de educación. Para implementar esta función se han definido las dos siguientes funciones auxiliares:
    * **calcula_media_edad(registros)**:  Dada una lista de tuplas de tipo Info, devuelve la media de edad de las personas cuya información se recoge en la lista de tuplas dada como parámetro. Si no se puede calcular eleva la excepcion StatisticsError.
    * **agrupa_por_nivel_educacion (registros)**: Dada una lista de tuplas de tipo Info, devuelve un diccionario en el que las claves representan el nivel de educación, y los valores son listas de los registros que tienen ese nivel de educación.

  * **obten_media_dinero_banco_segun_nivel_educacion(registros)**: Dada una lista de tuplas de tipo Info, devuelve un diccionario en el que las claves representan el nivel de educación, y el valor es la media de dinero que tienen en el banco las personas de ese nivel de educación. Para implementar esta función se han definido las siguientes funciones auxiliares:
    * **calcula_media_dinero_banco(registros)**: Dada una lista de tuplas de tipo Info, devuelve la media de la cantidad que tienen en el banco las personas cuya información se recoge en la lista de tuplas dada como parámetro. Si no se puede calcular se eleva la excepcion StatisticsError.
    * **agrupa_por_nivel_educacion (registros)**: Es la misma función auxiliar definida para implementar la función obten_media_edad_por_nivel_educacion.
    
  * **muestra_dinero_banco_por_nivel_educacion(registros)**:  Dada una lista de tuplas de tipo Info, muestra un diagrama de barras en el que por cada nivel de educacion se muestra la media del dinero en el banco de las personas que tienen ese nivel de educación. Para implementar esta función se usan las siguientes funciones:
    *  **obten_media_dinero_banco_segun_nivel_educacion(registros)**: Función ya implementada en el bloque 5.
    *  **dibujar_grafica_barras(X, Y, titulo, etiqueta_eje_x, etiqueta_eje_y)**: Función definida en el [módulo `graficas`](#módulo-graficas).
    
### Módulo poverty_test
En el módulo de pruebas se han definido las siguientes funciones de pruebas, cada una de las cuales se usa para probar la función con que tiene el mismo nombre (pero sin comenzar por `test\_` del módulo `poverty`. Por ejemplo, la función `test_lee_fichero` prueba la función `lee_fichero`.

* **test_lee_fichero(fichero)**
* **test_selecciona_registros_de_genero_y_pais(registros,  genero='Hombre', pais='A')**
* **test_obten_registros_mas_dinero_banco(registros)**:
* **test_cuenta_endeudados (registros, genero='Hombre')**
* **test_obten_n_registros_menor_num_moviles(registros, genero='Hombre', n=3)**
* **test_calcula_porcentaje_endeudados(registros, genero='Hombre')**
* **test_obten_media_edad_por_nivel_educacion (registros)**
* **test_calcula_total_veces_endeudados_por_situacion_familiar(registros, edad)**
* **test_muestra_dinero_banco_por_nivel_educacion(registros)**

En este módulo también se definido dos funciones auxiliares:
* **mostrar_registros (registros)**
* **mostrar_diccionario(dicc)**

### Módulo parsers

Este módulo contiene las siguientes funciones de parseo de datos:

* **parsea_booleano(cadena)**: Dada una cadena, devuelve `True` si la cadena contiene el literal 'verdadero' (independientemente de si está escrtio en mayúsculas o minúsculas); devuelve `False`, si contiene el literal 'falso'; y en cualquier otro caso devuelve `None`.
* **parsea_genero(cadena)**: Dada una cadena, devuelve 'Mujer'  si la cadena contiene el literal 'verdadero' (independientemente de si está escrtio en mayúsculas o minúsculas);  devuelve 'Hombre' si la cadena contiente el literal 'falso'; y en cualquier otra caso, devuelve None.
* **parsea_fecha(cadena)**: Dada una cadena una fecha en formato dia/mes/año (\%d/\%m/\%Y), devuelve un objeto de tipo date con la fecha a la que se refiere la cadena de entrada.   
 
### Módulo graficas

Este módulo contiene las siguientes funciones para dibujar gráficas:
* **dibujar_grafica_barras(etiquetas, valores, titulo, etiqueta_eje_x=None,etiqueta_eje_y=None)**: Dados una lista de cadenas con las etiquetas que se dibujarán en el eje X de la gráfica, una lista de enteros o reales con la altura de cada una de las barras, una cadena que representa el título del gráfico, y, opcionalmente, una cadena para etiquetar el eje X y/o otra cadena para etiquetar el eje Y, dibuja una gráfica de barras con esos datos. Un ejemplo del tipo de gráfica generado es el siguiente:

![image](https://user-images.githubusercontent.com/72299672/136940053-229cf29e-b7fb-4af8-b0d0-180070ba03fb.png)

