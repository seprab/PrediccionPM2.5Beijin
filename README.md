# PrediccionPM2.5Beijin
Espacio para realizar mis predicciones del siguiente concurso: 
[Link a los juegos del hambre](https://www.kaggle.com/c/datamex102020/overview/description)

> A continuación realizare mis primeras impresiones sobre la información a la que tengo acceso previo a realizar alguna predicción, escribir código o cosas asi.

La idea del proyecto es realizar la predicción PM2.5 de la [base de datos de test](https://github.com/seprab/PrediccionPM2.5Beijin/blob/main/test.csv).

#### ¿Qué son las PM2.5?
Son particulas de contaminación inferiores a 2.5 micras de tamaño (polvo, cenizas, hollín, particulas metalicas, cemento, polen, etc). Principalmente provienen de:
* Emisiones de vehiculo de combustión
* Plantas de electricidad
* Quema agricultural
* Incendio de bosques
* Oxigeno + Agua + Dioxido de sulfuro gaseoso
* Industrias
* Comercios domesticos

Especificamente en ***Beijing***, las principales causas de PM2.5 son:
* ***45%*** son emisiones de vehiculos, barcos y maquinas de construcción.
* ***+50%*** Proveniente de las ciudades alrededor de Beijing.

![Promedio mensual de concentración de PM2.5](https://static-01.hindawi.com/articles/amete/volume-2018/1724872/figures/1724872.fig.001.svgz)

> Este es un promedio mensual que se repite año a año y en las diferentes regios de beijing y alrededores.

![Promedio anual de PM 2.5 en Beijing](http://img2.chinadaily.com.cn/images/201804/07/5ac805b2a3105cdce0a12ac1.jpeg)


> La densidad de PM2.5 en Beijing y regiones aledañas se redujo desde 2013 dado las campañas gubernamentales.

La causa en el crecimiento de contaminación, uso vehicular y emisiones es principalmente por la estación del año. En invierno, las personas buscan formas de calentar sus espacios y en 'spring' los vientos son mas fuertes lo que transporta mas particulas.

A travez de los años no se ha evidenciado ninguna disminución en el uso vehicular... Pero si el uso de gas natural y menos quema de carbón.


Links
* [ecologistasenaccion.org](https://www.ecologistasenaccion.org/17842/que-son-las-pm25-y-como-afectan-a-nuestra-salud/)
* [blissair.com](https://blissair.com/what-is-pm-2-5.htm?__cf_chl_captcha_tk__=774e79d38de76055070eb1c26ffe3a20945daf66-1605851740-0-AXl_5JCb4zM_2nVItcq7mgCv1Z6bsjiaHbBD04F3OkcBM046MngeI8yLG9XQneREvGfKJbqLzpbNVRp8WNlEpZvaqHwFuK8TpCQRhYtSYEIwCsayfj_FW8hBASLuB-t-knw3llIQN4AzVGePB9_U0HX-Jqy8PB53-15zjkuyY_ErvF8RgOr_nV5mVImZ44QHpHMeU_q8Z6hB6UJWRXnwI--HvxIp5OQsTd3NlGrQ6vU1TIEtkMBdFB_hkkJ8wCpfvXrCzIS45BPxKF9QMGlDZ8ztduGN7-hIG1DKJO1FlDLwta1TFFFIHFUmS50jiRiwS4i3Hli4tr6EyAsY-hwcVLWWNP4Ax_AxniCLEfpVePfQR9Gl9EQ_ArCuMmuYdgLMpvjs5XuHJySvHb7I3fUI3ujoqeQdiVd_8mE6-MqAPdKNIITRxUxxUhikxlhn-nN3B7pKKaRfxvNWb-fUYqxwtt3LJ5HUi5fzCToxGrW_PIQIY70PA5_CBvwh3T4Yp6FUYr8belO5N_1DIRRPWgRL_Q0BLJmQcyE7KKTdsBVgKLxU)
* [laqm.defra.gov.uk](https://laqm.defra.gov.uk/public-health/pm25.html)
* [chinadily.com.cn](http://www.chinadaily.com.cn/a/201804/07/WS5ac805b2a3105cdcf65168a7.html)
* [hindawi.com](https://www.hindawi.com/journals/amete/2018/1724872/)

#### La base de datos comprende de:
Columna| Descripción | Consideraciones Tempranas 
------------ | ------------- | ------------- 
No | row number | Usar como índice de tabla
year | year of data in this row | Dado que los años del set de entrenamiento y testing comprende desde 2013, es un dato importante. Ya que desde el 2013 inicia la camapaña de descontaminación. Pienso que podría estandarizar este año, donde 2013 es 0 y en adelante lo categorizamos. Ej. 2014:1, 2015:2, 2016:3, etc.
month | month of data in this row | Este es un dato muy clave, ya que describe la temporada del años que se esta viviendo. Aunque, si tengo temperatura y viento, podriamos eliminar esta columna.
day | day of data in this row | Mis impresiones de este dato son las mismas que el mes. Numericamente pienso que este dato podría añadir ruido, ya que no describe si es un día en el que se usa mucho o poco carro, mucha industria o poca.
hour | hour of data in this row | Sin explorar la BD podría pensar que la hora si podría describir horas laborales y de transporte. Importante!
*** PM2.5 *** | PM2.5 concentration (ug/m^3) | *** Dato a predecir ***
PM10 | PM10 concentration (ug/m^3) | Muy posiblemente, este sea un dato directamente proporcional al dato a predecir. Importante!
SO2 | SO2 concentration (ug/m^3) | En la investigación encontre que la suma de este elemento con agua y oxigeno se generan muchas particulas de contaminación. Importante!
NO2 | NO2 concentration (ug/m^3) | x
CO | CO concentration (ug/m^3) | x
O3 | O3 concentration (ug/m^3) | x
TEMP | temperature (degree Celsius) | Ciertamente, la temperatura es el principal factor que ocasiona el aumento en la contaminación. Tambien es el descriptor de las temporadas... razón por la que pienso podría eliminar los meses y días.
PRES | pressure (hPa) | x
DEWP | dew point temperature (degree Celsius) | x
RAIN | precipitation (mm) | Ciertamente, los días de lluvia las particulas caen al suelo y no viajan por el aire. Importante!
wd | wind direction | Por lo que leí, en el sur siempre esta la mayor concentración de contaminación. De esta forma, es posible asumir que vientos con dirección al norte puede aumentar los indicadores en el pais. Importante!
WSPM | wind speed (m/s) | Entre mas alta la velocidad, mayor la distribución de particulas. Importante!
station | name of the air-quality monitoring site | Mis consideraciones de esta columna son las mismas que mes y día. Podría eliminarla y hacer un mejor uso de indicadores numericos y climaticos.
