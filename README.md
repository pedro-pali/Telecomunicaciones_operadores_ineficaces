# Telecomunicaciones_operadores_ineficaces
Se considera que un operador es ineficaz si tiene una gran cantidad de llamadas entrantes perdidas (internas y externas) y un tiempo de espera prolongado para las llamadas entrantes. Además, si se supone que un operador debe realizar llamadas salientes, un número reducido de ellas también será un signo de ineficacia.

## Paso 1. Análisis exploratorio de los datos
Analizamos el dataset 
Limpiamos los datos del dataset 'telecom_dataset_new.csv' al cual convertimos a un DataFrame llamado 'dataset'
- Convertimos la columna 'date' a formato Datetime.
- Convertimos la columna 'internal' a Booleano.
- Los valores nulos los vamos a eliminar ya que hayamos juntado los dos datasets y creado una copia.
Limpiamos los datos del dataset 'telecom_clientes.csv' el cual convertimos a un Dataframe llamado 'clients'
- Convertimos la columna 'date_start' a tipo Datetime.

Combinamos los dos DataFrames en uno solo llamada 'df'. Creamos una copia de este y la llamamos 'df_copy' para trabajar en ella. La decisión de borrar los valores ausentes es:
Debido a que la única columna con valores ausentes es la de los operadores, imposibilita con los datos actuales, identificarlos para saber si son ineficaces o no, entonces he decidido borrarlos y trabajar solo con los que están debidamente identificados.

## Paso 2. Identificar operadores ineficaces
Plan de trabajo que utilicé para identificarlos fue:
- Calcular las llamadas perdidas por usuario utilizando groupby() y calcular la tasa de llamadas perdidas individuales por usuario.
- Calcular el tiempo de espera promedio para llamadas entrantes restando la columna 'total_call_duration' menos 'call_duration'.
- Calcular el número de llamadas salientes para cada operador y su respectiva tasa.
- Graficar todos los resultados en graficos de barras para visualizarlos mejor y buscar la correlación entre la tasa de llamadas perdidas y el tiempo de espera promedio.
### Conclusiones:
Con un total de 1092 operadores debidadmente registrados con sus ID, obtuvimos las métricas para conocer cuales son los operadores más ineficaces según los siguientes criterios:
#### 1. Operadores con más llamadas perdidas (top 20):
- ID = 885876, 135 llamadas perdidas
- ID = 891410    131, llamadas perdidas
- ID = 893804    130, llamadas perdidas
- ID = 901880    128, llamadas perdidas
- ID = 891414    126, llamadas perdidas
- ID = 901884    115, llamadas perdidas
- ID = 885890    110, llamadas perdidas
- ID = 887276    101, llamadas perdidas
- ID = 879898    100, llamadas perdidas
- ID = 905538     99, llamadas perdidas
- ID = 880026     94, llamadas perdidas
- ID = 891416     94, llamadas perdidas
- ID = 880028     91, llamadas perdidas
- ID = 890404     90, llamadas perdidas
- ID = 882686     88, llamadas perdidas
- ID = 905566     87, llamadas perdidas
- ID = 905542     85, llamadas perdidas
- ID = 890410     84, llamadas perdidas
- ID = 921818     84, llamadas perdidas
- ID = 900892     84, llamadas perdidas

Sin embargo; considero que realmente lo que definiría en este rubro si el operador es ineficas o no es la tasa (%) de llamadas perdidas respecto al total de llamadas contadas individualmente, esto debido a que nos da un mejor entendimiento de la situación rael. Siendo un 7% la tasa de llamadas perdiddas por operador los siguientes 20 se encuentran muy por arriba del promedio. Considerando aquellos operadores que tienen igual o más de 10 llamadas contadas como elementos activos y debidamente registrados, obtenemos que aquellos con la más alta tasa de llamadas perdidas son:
- ID = 953460, con 70.0%
- ID = 898434, con 50.0%
- ID = 888406, con 40.0%
- ID = 933996, con 40.0%
- ID = 894232, con 38.1%
- ID = 940788, con 36.4%
- ID = 918888, con 36.4%
- ID = 881278, con 35.0%
- ID = 894230, con 33.3%
- ID = 894226, con 32.0%
- ID = 956298, con 31.2%
- ID = 892800, con 30.0%
- ID = 939212, con 30.0%
- ID = 939718, con 30.0%
- ID = 947610, con 29.2%
- ID = 891156, con 29.2%
- ID = 957022, con 28.6%
- ID = 892530, con 28.6%
- ID = 906392, con 27.5%
- ID = 937604, con 27.0%

#### 2. Operadores con más tiempo de espera
El top 20 de operadores con promedio de tiempo de espera más alto medido en segundos son los siguientes: 
- ID = 919794,    1039.5 Seg
- ID = 906070,     853.3 Seg
- ID = 919790,     839.8 Seg
- ID = 931458,     655.2 Seg
- ID = 906076,     611.5 Seg
- ID = 921318,     607.5 Seg
- ID = 919204,     579.3 Seg
- ID = 919552,    556.8 Seg
- ID = 913938,     535.0 Seg
- ID = 919554,     518.2 Seg
- ID = 906406,     433.5 Seg
- ID = 919166,    398.6 Seg
- ID = 919792,     389.5 Seg
- ID = 919206,     360.9 Seg
- ID = 913942,     350.9 Seg
- ID = 939762,    338.6 Seg
- ID = 958460,     332.7 Seg 
- ID = 906404,     331.4 Seg
- ID = 882690,     299.8 Seg
- ID = 919164,     298.7 Seg

A simple vista, podemos notar que son diferentes operadores los más altos en la tasa de llamadas perdidas y el promedio de espera para llamadas entrantes, sin embargo, para confirmar que no están relacionados uno con otro y poder descartar que las causas de que este sucediendo una situación o la otra tienen relacionan, calculamos la correlación de Pearson entre ellos, el resultado fue de -0.23, el gráfico nos indica que cuando el tiempo de espera aumenta, las llamadas perdidas tienden a disminuir, pero muy ligeramente, el valor está muy lejos de -1 así que no hay una relación fuerte, el tiempo de espera explica muy poco el comportamiento de las llamadas perdidas.
Puede haber otros factores más influyentes externos.
 
 ### 3. Operadores con más llamadas salientes
 Como último rublo a considerar para catalogar un operador ineficiente son pocas llamadas salientes, sin embargo, en este caso también consideraremos la tasa de llamadas salientes en lugar se solo el número menor de llamadas salientes, y los 20 operadores con menor tasa de llamadas salientes son:
- ID = 919206,    0.1%
- ID = 937956,    0.1%
- ID = 925922,    0.2%
- ID = 929428,    0.3%
- ID = 908640,    0.3%
- ID = 885876,    0.3%
- ID = 885890,    0.3%
- ID = 919204,    0.5%
- ID = 940630,    0.6%
- ID = 929426,    0.6%
- ID = 940588,    0.7%
- ID = 919794,    0.7%
- ID = 919554,    0.7%
- ID = 919364,    0.8%
- ID = 919790,    0.8%
- ID = 919166,    0.9%
- ID = 905862,    0.9%
- ID = 945286,    0.9%
- ID = 945904,    0.9%
- ID = 945900,    1.0%

## Paso 3. Hipótesis estadística
Realizamos histogramas y gráficos Q-Q para visualizar si los datos tienen una distribución normal, a lo que noté que no es así, por lo tanto, y como las poblaciones son en tamaños muy diferente entre una y otra decidí realizar el test de Mann_Whitney_U.

### Conclusiones:
Del top 20 con los niveles más altos según los tres rubros para catalogar si un operador es ineficiente hemos obtenido a través de una hipótesis Mann_Whitney_U que en todos los casos, existe evidencia estadística de diferencia entre las distribuciones. En otras palabras, hay una diferencia real y no producto del azar entre el top 20 de cada rubro y el resto de los operadores.