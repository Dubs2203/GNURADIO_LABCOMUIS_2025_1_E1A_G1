# Laboratorio de Comunicaciones
## Universidad Industrial de Santander



# Práctica 1: GNURADIO para el procesamiento de señales - Mediciones de potencia y frecuencia

### Integrantes
- **DUBAN YESID CORTÉS TABARES** - 2214644
- **ELKIN YESID LOZADA CABRERA** - 2204219

Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones  
Universidad Industrial de Santander

### Fecha
4 de marzo de 2025

---

## Declaración de Originalidad y Responsabilidad
Los autores de este informe certifican que el contenido aquí presentado es original y ha sido elaborado de manera independiente. Se han utilizado fuentes externas únicamente como referencia y han sido debidamente citadas.

Asimismo, los autores asumen plena responsabilidad por la información contenida en este documento. 

Uso de IA: Se utilizó ChatGPT para reformular secciones del texto y verificar gramática, pero el contenido técnico fue desarrollado íntegramente por los autores.

---
## Contenido

### Resumen
En esta práctica, se realizaron mediciones de potencia y frecuencia utilizando herramientas de radio definido por software (SDR) y equipos de laboratorio como el USRP 2920, el osciloscopio R&S RTB2004 y el analizador de espectros R&S FPC1000.

Se comenzó con la revisión de especificaciones y configuración de los equipos. Luego, se generaron y analizaron señales en GNU Radio para comprender su comportamiento en los dominios del tiempo y la frecuencia. Posteriormente, se transmitieron señales con el USRP 2920 y se midieron parámetros clave como potencia, ancho de banda y relación señal a ruido (SNR) utilizando el analizador de espectros y el osciloscopio.

Finalmente, se compararon los resultados obtenidos en simulación y experimentación, evaluando la influencia del ruido y la configuración de los equipos en la calidad de la señal, además de analizar los cambios observados en las señales de tiempo - frecuencia al variar sus parámetros en cada una.

**Palabras clave:** Frecuencia, potencia, ruido, atenuación, calidad de la señal

### Introducción

El procesamiento de señales en el ambito de las telecomunicaciones es una pieza clave en los sistemas de comunicación modernos, en dónde la correcta selección de la frecuencia de muestreo y el uso correcto de herramientas (En este caso GNURadio) puede marcar la diferencia entre una señal legible y una completamente distorionada. En esta práctica se experimentará con estos conceptos. A través de la simulación y medición de señales se logrará entender el impacto del límite de Nyquist. 

En un laboratorio de comunicaciones, herramientas como GNU Radio ofrecen un entorno flexible para experimentar con señales en tiempo real. Sin embargo, ¿cuáles son sus principales ventajas en comparación con otros sistemas? ¿Qué ocurre cuando se asigna una frecuencia de muestreo inadecuada? Estas cuestiones serán abordadas a lo largo de la práctica, permitiendo una comprensión más profunda del muestreo y su papel en la transmisión y procesamiento de señales digitales.

---

### Procedimiento


## Actividad 1: Revisión de Especificaciones de los Equipos

## **Objetivo** 
Familiarizarse con las especificaciones técnicas de los equipos de laboratorio y entender cómo configurarlos para realizar mediciones.

#### USRP -2920 
Es un transceptor de RF ajustable con un convertidor analogico-digital de alta 
velocidad y un convertidor digital-analogico para la transmision de señales de 
banda base. TIene aplicaciones en emisión FM, seguridad pública, entre otras. 

Especificaciones: 
Rango de frecuencias (Transmisor y receptor): 50MHz to 2.2GHZ

Máxima potencia de salida:  

50mW to 100mW (17dBm to 20 dBm) entre 50MHz y 1.2GHZ. 

30mW to 70mW (15dBm to 18 dBm) entre 1.2GHz y 2.2GHZ. 

Rango de ganancia: 0dB to 31dB 

Frecuencia de paso: <1kHz 

Potencia: DE 12 a 15W (Máximo 18W)

#### Osciloscopio R&S RTB2004 

Dispositivo de medición de alta calidad diseñado para ofrecer precisión, 
visualización y herramientas de control para el manejo de señales electrónicas. 

Especificaciones: 

Ancho de banda: 70MHz to 300MHz 

Número de canales: 4 

Freq. Muestreo:  1.25GSa/s por canal y 2X2.5 GSa/s intercalado (Usando dos 
canales) 

Profundidad de memoria: 10Mpts por canal y 2x20Mpts intercalado. 

Rango de voltaje: El RTB2004 tiene un rango de entrada típico de ±50 V (en modo 
diferencial). 

#### Analizador de Espectros R&S FPC1000: 

Herramienta utilizada para el análisis y localización de fuentes de perturbaciones durante 
el desarrollo y tratamiento de señales. Permite visualizar en una pantalla las componentes 
espectrales pudiendo ser ésta cualquier tipo de ondas eléctricas, acústicas u ópticas. 

Especificaciones: 

Rango de frecuencias: 5kHz a 1GHz 

Nivel de ruido promedio visualizado: ± 1,5 % de escala completa 

Incertidumbre absoluta de frecuencia (De 20° a 30°c): <0.3dB 

Incertidumbre de respuesta en frecuencia (de +20°C a +30°C): <1dB 

Ancho de banda de resolución de hasta 1Hz


## Actividad 2: Simulación de Señales en GNU Radio

## **Objetivo**  
Generar y analizar señales en GNU Radio para entender cómo se comportan diferentes formas de onda en los dominios del tiempo y la frecuencia.  
## **Evidencias**  
A continuación, se presentan capturas de pantalla de las señales analizadas:

### **1. Señal Original (Onda Triangular)**  
Se observa la señal original antes de aplicar modificaciones.  
![Señal original - Onda triangular](Original.png)  

### **2. Configuración del Flujograma**  
Se muestra la señal, luego de realizar todos los cambios.  
![Configuración del Flujograma](Config_Flujo.png)  

### **3. Nueva Señal Generada (Onda Senoidal)**  
Tras modificar los parámetros iniciales, se genera una onda senoidal, la cual presenta una transición más suave en comparación con la onda triangular.  
![Nueva señal generada - Onda seno](Señal_gen.png)  

### **4. Cambio en la Amplitud**  
Se incrementa la amplitud de la onda senoidal, lo que hace que los valores máximos y mínimos sean más pronunciados, aumentando su energía.  
![Cambio en amplitud](Camp.png)  

### **5. Cambio en la Frecuencia**  
Al aumentar la frecuencia, la señal oscila más rápido en el mismo intervalo de tiempo, lo que se traduce en una mayor cantidad de ciclos dentro de la misma ventana de observación.  
![Cambio en frecuencia](Cfrec.png)  

### **6. Cambio en el Offset**  
Se agrega un desplazamiento, lo que provoca un corrimiento espectral de la señal sin alterar su forma en el dominio del tiempo.  
![Cambio en offset de frecuencia](Coffset.png)  

### **7. Resultado Final - Configuración de la Señal Senoidal**  
Configuración final de la señal senoidal después de todas las modificaciones. Se observa cómo los cambios aplicados afectan la señal en los dominios del tiempo y la frecuencia.  
![Configuración final - Onda seno](Config_seno.png) 


## Actividad 3: Transmisión y Medición de Señales con el USRP 2920

## **Objetivo** 
Transmitir señales usando el USRP 2920 y medir parámetros clave como potencia, ancho de banda, piso de ruido y relación señal a ruido (SNR).

### **1. Señal Original**  
Se observa la señal original antes de aplicar modificaciones.  
![Señal original](Freqoriginal.jpeg)  

### **2. Cambio en la Amplitud**  
Se ha modificado la amplitud de la señal, lo que afecta la potencia de la misma en el espectro.  
![Cambio en amplitud](Freqamp.jpeg)  

### **3. Cambio en la Frecuencia y Fase**  
El cambio en la fase de la señal no es visible en el dominio de la frecuencia, ya que el espectro muestra solo la magnitud. Sin embargo, una variación en la fase podría afectar la coherencia con otras señales, mientras que en la frecuencia podemos observar cómo los picos de la señal senoidal se corren hacia la frecuencia seleccionada  
![Cambio en frecuencia](Freqfreq.jpeg)  

### **4. Cambio en el Offset de Frecuencia**  
Se ha aplicado un desplazamiento en la frecuencia de la señal, lo que genera un cambio en la posición de los picos espectrales.  
![Cambio en offset de frecuencia](Freqoffset.jpeg)  

### Cálculo de parametros para otra respuesta en frecuencia
![Respuesta en frecuencia de una señal triangular](Triang.jpg)

#### -Piso de ruido normalizado
Para calcular el piso de ruido normalizado a la frecuencia portadora, primero se estima una aproximación del nivel de ruido en el espectro, que en este caso fue de -115 dBm. Una vez obtenido el nivel de ruido, se normaliza a 1 Hz utilizando un ancho de banda de resolución (RBW) de 300 Hz.

$P_{\text{ruido normalizado}} = P_{\text{ruido}} - 10 \cdot \log_{10}(RBW)$

$P_{\text{ruido normalizado}} = -115 - 24.77 \approx -139.77 \ \text{dBm/Hz}$

Ahora, teniendo el ruido normalizado, se procede a calcular el piso de ruido normalizado, para lo cual se utiliza una potencia portadora de -70 dBm.

$L(f) = P_{\text{portadora}} - P_{\text{ruido normalizado}}$

$L(f) = -70 - (-139.77) = 69.77 \ \text{dBc/Hz}$

#### -Potencia de la señal
Para el cálculo de la potencia, se observa que en el espectro el valor más alto del pico es de -70 dBm.

$P(W) = 10^{\frac{P(\text{dBm}) - 30}{10}}$

$P(W) = 10^{\frac{-70 - 30}{10}} = 10^{\frac{-100}{10}} = 0.1 \ \text{nW}$

#### -Ancho de banda
Para determinar el ancho de banda, se miden las frecuencias $f_{\text{max}}$ y $f_{\text{min}}$ que delimitan el pico de la señal, y a través de una resta se obtiene el ancho de banda. En este caso, $f_{\text{min}}$ tiene un valor de 49.999 MHz y $f_{\text{max}}$ un valor de 50.001 MHz, por lo que el ancho de banda corresponde a 2 kHz.

Replicando los calculos anteriores pero ahora aplicados para nuestra señal seno tenemos los siguientes resulados:

$P_{\text{ruido normalizado}} = -134.77 \ \text{dBm/Hz}$

$L(f) = 74.77 \ \text{dBc/Hz}$

$P(W) = 1 \ \text{nW}$

${\text{Ancho de banda}} = 2 \ \text{kHz}$

Se realizó un análisis del espectro de señales FM utilizando el analizador de espectros. Se conectó una antena adecuada a la entrada del analizador para ver señales en el rango de 88 MHz a 108 MHz. Se midieron la frecuencia central, el ancho de banda y la potencia de transmisión de dos estaciones diferente. También se analizó la variación en la respuesta en frecuencia del canal.

### **Captura de señal en 91.7 MHz**  
![Señal en 91.7 MHz](FM917.jpg)  

Para calcular la potencia de transmisión de la señal FM, se toma la medida de potencia del analizador de espectros, que en este caso arroja aproximadamente -103.43 dBm. Sin embargo, dado que se utiliza un RBW (ancho de banda de resolución) de 30 Hz, esto indica que la potencia se está midiendo en un ancho de banda muy estrecho, por lo que es necesario aplicar un factor de corrección a la potencia utilizando el ancho de banda de la señal FM.

$P_{total} = P_{RBW} + 10 \log\left(\frac{Ancho de Banda}{RBW}\right)$

$P_{total} \approx -103.43 + 38.24 \approx -65.19 \ \text{dBm}$

Esta misma operación debe realizarse para calcular el nivel de ruido. Por lo tanto, si el espectro proporciona un nivel de ruido de aproximadamente -120 dBm, se determina que $P_{ruido}$ es de -81.76 dBm, con lo que ya se podrá calcular el SNR.

$\text{SNR (dB)} = P_{\text{señal}} - P_{\text{ruido}}$

$\text{SNR} = -65.19 - (-81.76) = 16.57 \ \text{dB}$

- **Potencia de transmisión: 302.69 pW**  
- **Ancho de banda: 200 KHz**  
- **Relación señal a ruido (SNR): 16.57 dB**  

### **Captura de señal en 96.9 MHz (Instante 1)**  
![Señal en 96.9 MHz - Instante 1](FM969.jpg)  

- **Potencia de transmisión: 1.05 nW**  
- **Ancho de banda: 100 KHz**  
- **Relación señal a ruido (SNR): 30 dB**  

### **Captura de señal en 96.9 MHz (Instante 2)**  
![Señal en 96.9 MHz - Instante 2](FM9692.jpg)  

Para el cálculo de la potencia de este espectro, se realizó el cálculo de la potencia en los picos principales y se sumó la potencia en escala lineal.

- **Potencia de transmisión: 237.6 pW**  
- **Ancho de banda: 100 KHz**  
- **Relación señal a ruido (SNR): 20.52 dB**  

###  Medición con el osciloscopio
Se visualizó una señal sinusoidal con la ayuda del osciloscopio.
### **1. Señal Original**
Se observa la señal original antes de aplicar modificaciones, donde se puede apreciar cómo es la señal ya modulada. 
![Señal original - Onda Seno](Senorigi.jpg)

### **2. Cambio en la Amplitud**  
Se ha modificado la amplitud de la señal al doble, lo que muestra que también se observa un aumento proporcional en la señal modulada. 
![Cambio en amplitud](Senamp.jpg)  

### **3. Cambio en la Frecuencia**  
Un cambio de frecuencia en la señal transmitida representa la misma variación en la señal observada en el osciloscopio, donde se aprecia que la frecuencia se ha aumentado al doble.
![Cambio en frecuencia](Senfrec.jpg)

## Actividad 4: Análisis de Resultados y Conclusiones
### Comparacion de resultados
En la simulación con GNU Radio, las señales fueron generadas y modificadas en un entorno ideal sin ruido ni pérdidas. Sin embargo, en la transmisión real con el USRP 2920, la potencia medida resultó menor debido a las atenuaciones y el ruido presentes en el canal.

Las mediciones realizadas con un osciloscopio permitieron analizar la señal en el dominio del tiempo, observando cambios en la amplitud y la frecuencia. Por otro lado, el uso de un analizador de espectros facilitó la evaluación de la potencia, el ancho de banda y la relación señal-ruido (SNR).
### Reflexion sobre la SNR:
La relación señal-ruido (SNR) es fundamental en las comunicaciones inalámbricas, ya que determina la calidad de la señal recibida. Una SNR alta permite una mejor transmisión con menos errores, mientras que una SNR baja puede provocar interferencias y pérdida de datos. 

El piso de ruido influye directamente en la capacidad de detectar señales débiles, ya que si es demasiado alto, las señales de baja potencia quedan ocultas, reduciendo la sensibilidad del receptor y afectando la comunicación efectiva.

### Conclusiones
El laboratorio permitió comprender el comportamiento de las señales en el dominio del tiempo y la frecuencia, comparando los resultados obtenidos en simulación y en transmisión real. Se evidenció que, aunque la simulación en GNU Radio proporciona un entorno ideal sin interferencias, la transmisión con el USRP 2920 está sujeta a efectos como atenuación, ruido y variaciones en la potencia de la señal. Además, se analizó la relación señal-ruido (SNR) como un factor determinante en la recepción y calidad de las señales inalámbricas, destacando cómo el piso de ruido influye en la detección de señales débiles.

### Referencias
-J. Proakis y M. Salehi, Fundamentals of Communication Systems, 2ª ed. Inglaterra: Pearson Education Limited, 2014, pp. 164-165, 346, cap. 5. [En línea]. Disponible: https://uis.primo.exlibrisgroup.com/permalink/57UIDS_INST/63p0of/cdi_askewsholts_vlebooks_9781292015699.

-National Instruments, "USRP-2920 Specifications," National Instruments, [En línea]. Disponible: https://www.ni.com/docs/en-US/bundle/usrp-2920-specs/page/specs.html.

-Rohde & Schwarz, "R&S®RTB2000 Oscilloscope Specifications," Rohde & Schwarz, [En línea]. Disponible: https://www.rohde-schwarz.com/lat/productos/prueba-y-medicion/osciloscopios/rs-rtb2000-oscilloscope_63493-266306.html.

-Rohde & Schwarz, "R&S®FPC Spectrum Analyzer Data Sheet," Rohde & Schwarz, [En línea]. Disponible: https://scdn.rohde-schwarz.com/ur/pws/dl_downloads/dl_common_library/dl_brochures_and_datasheets/pdf_1/FPC_dat-sw_en_5214-7112-22_v0600.pdf.

---

Volver al [INICIO](#Laboratorio-de-Comunicaciones)
