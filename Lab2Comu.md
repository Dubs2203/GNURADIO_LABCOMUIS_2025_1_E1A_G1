# Laboratorio de Comunicaciones
## Universidad Industrial de Santander


# Práctica 2: Modelo del canal    

### Integrantes
- **DUBAN CORTÉS** - 2214644
- **Elkin Lozada** - 2204219

Escuela de Ingenaierías Eléctrica, Electrónica y de Telecomunicaciones  
Universidad Industrial de Santander

### Fecha
28 de marzo de 2025

---

## Declaración de Originalidad y Responsabilidad
El contenido aquí presentado es original y ha sido elaborado de manera independiente. Se han utilizado fuentes externas únicamente como referencia y han sido debidamente citadas.

Uso de IA: Se utilizo chatGPT para realizar algunas gráficas mediante python y mejorar la grámatica en el informe.

## Contenido


### Resumen
La práctica tiene cómo finalidad analizar cómo las caracteristicas del canal afectan la calidad de una señal que se transmite, además se evaluaran parámetros cómo 
el SNR, Noise Floor, etc, para determinar la eficiencia de transmisión de datos. También será posible ver otros efectos que se producen y que son inherentes al canal, tales cómo el retardo, la atenuación o la distorsión consolidando lo visto teóricamente con lo práctico.


### Introducción
El filtrado de señales tiene un rol fundamental en la conservación de la calidad de la información que se transmite. Al suprimir las frecuencias elevadas, se disminuyen los elementos de alta frecuencia, lo que puede suavizar la señal pero también suprimir detalles cruciales, en particular en señales con componentes armónicos vitales para su adecuada reconstrucción. Mantener un filtrado excesivamente cerccano a la frecuencia fundamental puede distorsionar la forma de onda y modificar su espectro. En contraposición, el filtrado de bajas frecuencias suprime elementos de baja frecuencia, lo cual puede impactar en la envolvente de la señal y alterar su estructura global. La supresión de armónicos afecta principalmente a las señales periódicas, dado que estos elementos son los encargados de su forma distintiva; sin ellos, la señal podría perder su definición y tornarse irreconocible.

El desvío de frecuencia en una señal captada puede generar cambios espectrales que impactan su adecuada interpretación, provocando interferencias o desajustes en los sistemas de demodulación. En estas situaciones, si los filtros no están adecuadamente diseñados, pueden alterar aún más la señal, empeorando la pérdida de información en vez de rectificarla. Adicionalmente, la degradación de la señal se intensifica a medida que se incrementa el nivel de ruido, lo cual puede medirse mediante indicadores como la relación entre señal y ruido (SNR). Para mejorar la relación señal a ruido, es posible emplear técnicas como filtrado adaptativo, amplificación selectiva o codificación de canal.

La calidad de la señal recibida puede evaluarse utilizando diferentes criterios según el tipo de señal. En señales analógicas, se pueden analizar la relación señal a ruido y la distorsión armónica total (THD).

Durante la práctica, se utilizarán equipos como el radio definido por software USRP 2920 y herramientas como GNU Radio para simular y analizar estos efectos en distintos escenarios, permitiendo una comprensión más profunda de la transmisión y recepción de señales en entornos reales.


### Procedimiento


## Actividad 1: Actividades de simulación de canal en GNU Radio 
Se configuro la frecuencia de muestreo para n=8, e inicialmente se analizó el efecto de variar las frecuencias de corte del filtro utilizando una señal triangular.

![Networking](practica2/F1_NOffset.png)

En la práctica, fue posible observar que a medida que la frecuencia de corte del filtro estaba más cercana a la frecuencia del mensaje, este se ve represntado más fielmente mientras que si aún está por debajo, pero cerca, la señal puede verse igual pero un poco atenuada.

Además es posible observar que, en frecuencia desaparecen todos los armónicos que están por fuera de la frecuencia produciendo así un espectro de la señal mucho más limpio. Luego, se obtienen los mismos resultados con la frecuencia de una señal sinusoidal.

![Networking](practica2/F21Freq.png)

![Networking](practica2/F21.png)

Analizando ahora los efectos del ruido, se configuró el flujograma para la reproducción de audio, y se aumentó el noise voltage hasta que fuera irreconocible el mismo, obteniendo así:

![Networking](practica2/UmbralFreqsinruido.png)

![Networking](practica2/Umbralfreqruido.png)

![Networking](practica2/Umbralruido.png)

Podemos ver que, cuando la amplitud de los armónicos del ruido son mayores a los de la misma señal, esta se vuelve imposible de reconstruir, además de que su forma en el tiempo se vuelve totalmente errante. 

Para analizar la SNR antes y después de aplicar el ruido, se utilizó el siguiente código de python:

![Networking](practica2/Codepython.png)

En donde si suponemos que la señal original tiene una SNR infinita (Aproximadamente sin ruido), y con el cálculo después del ruido la SNR se reduce a 8.08 dB. Dado que la degradación es la diferendcia entre ambas SNR el resultado es infinito, lo que indica una pérdida total de la señal. 

## Actividad 2: Fenómenos de canal en el osciloscopio 
Se desactivaron los bloques correspondientes al USRP virtual, para luego enviar la señal de GNURadio al instrumento del laboratorio, manteniendo n=8 para el samp rate. Luego se partió de una frecuencia de 50M, y se ajustó el osciloscopio para su correcta visualización para ir variandola hasta 500M y observar su efecto en el canal.

![Networking](practica2/50M.jpeg)

![Networking](practica2/100M.jpeg)

![Networking](practica2/200M.jpeg)
Desde la frecuencia de 50MHz al ir aumentando se observa que la ganancia del USRP va disminuyendo a medida que esta aumenta, sin embargo ocurrió una anormalidad en la frecuencia de 200MHz que podría estar asociada a un fallo en el instrumento en determinada frecuencia o a alguno de los cables que pueda estar actuando como filtro. También se analizó los efectos vistos en la actividad 1, partiendo de una señal triangular de 1kHz, posteriormente cambiandola a 5kHz y variando su ruido. Es importante aclarar que el banco utilizado ha presentado fallas en el USRP generando señales muy distorsionadas e inestables.

![Networking](practica2/500M.jpeg)

Finalmente, se observa el efecto mencionado anteriormente con la ganancia, además de poder observar que la transmisión a frecuencias más altas reduce la calidad de la señal obdservada.

## Actividad 3: Fenómenos de canal en el analizador de espectro 
Se mantuvo la misma configuración de bloques del GNURadio de la acitividad 2, esta vez realizando las mediciones desde el analizador de espectros. 

Se inicio transmitiendo una señal triangular con una f de 1kHz y para realizar la comparación se desplazo a 3kHz y se aplicó un noise voltage de 0.3. 

![Networking](practica2/originalc3.jpg)

Podemos notar que los picos caen en un factor de 1/n^2, obteniendo un espectro más concentrado en bajas frecuencias. Adicional a esto, podemos verificar lo obtenido en el analizador de espectros reconstruyendo la señal a partir de su espectro de frecuencias.

![Networking](practica2/Codepython2.png)

También se puede observar que al subir el noise voltaje el nivel de piso de ruido sube en todo el espectro de frecuencias debido a su naturaleza gaussiana.

![Networking](practica2/originalc31.jpg)

Repitiendo el proceso con un tren de pulsos, observamos la relación de 1/n, pero con mayor contenido de altas frecuencias en comparación con la triangular. En presencia de ruido, la señal pulsada puede ser más sensible a la distorsión por interferencias.

![Networking](practica2/originalt3.jpg)

![Networking](practica2/originalt31.jpg)

Al utilizar cables coaxiales largo se observa una mayor atenuación en altas frecuencias, debido a que la respuesta del cable es mejor en bajas frecuencias. El modelo adecuado para estas mediciones es algún modelo de línea de transmisión, mientras que con el uso de antenas el modelo que mejor describe el canal es el de pérdida en el espacio libre.



### Conclusiones

- El experimento demostró que los efectos del canal, tales como la atenuación y la distorsión, están vinculados tanto con la frecuencia de la señal como con las condiciones de transmisión.

- Se verificó que el ruido no solo afecta la amplitud de la señal, sino que también altera su espectro de frecuencias, haciendo más difícil su reconstrucción cuando su nivel es elevado.

- Se evidenció que la calidad de la transmisión depende del medio utilizado, ya que los cables coaxiales introducen pérdidas diferentes a las observadas en transmisión inalámbrica.

- Se analizaron los retos que implica tener un nivel de ruido muy alto a la hora de reconstruir una señal y la importancia del muestreo a la hora de visualizar un mensaje.

### Referencias

- Scribd. (s.f.). GNU Radio. Scribd. https://es.scribd.com/document/183517250/Gnu-Radio
  
- OBDII Cable. "Efecto de la frecuencia en cables coaxiales". Disponible en:         
   https://www.obdiicable.com/es/blog/397.html.
  
- Ampligsm. (s.f.). Relación entre la longitud de los cables y la atenuación. Recuperado de https://www.ampligsm.com/blog-amplificadores-cobertura-telefono-movil/relacion-longitud-cables-atenuacion
  


## Inclusión de Imágenes

Anexo del barrido en frecuencia para las frecuencias de 300M y 400M

![Networking](my%20file/300M.jpeg)

![Networking](practica2/400M.jpeg)

