# Introducción a la dinámica de los sistemas lineales

## Conceptos básicos

Antes de comenzar a estudiar sistemas dinámicos, necesitamos introducir algunos conceptos básicos.

````{prf:definition} Señal
 :label: signal

 *Fís*. Variación de una corriente eléctrica u otra magnitud que se utiliza para transmitir información.
````

Tipos de señales eléctricas

* *Señal analógica*. Tiene una variación continua en el tiempo con un número infinito de valores.
* *Señal digital*. Tiene una variación discreta de valores en el tiempo con un número finito de valores.
* *Señal digital binaria*. Tiene sólo dos niveles de tensión $V+$ o $0$, en valores binarios $1$ y $0$.
* *Concepto de sistema*. Conjunto de componentes físicos relacionados que actúan como una unidad completa.

````{prf:definition} Modelo
 :label: model

 m. Esquema teórico, generalmente en forma matemática, de un sistema o de una realidad compleja, como la evolución económica de un país, que se elabora para facilitar su comprensión y el estudio de su comportamiento.
````

Sistemas seguidores

* La entrada de referencia cambia de valor frecuentemente.
* Ejemplo: servomecanismos; la salida es alguna posición, velocidad o aceleración mecánica.

Sistemas de regulación automática

* La entrada de referencia es o bien constante o bien varía lentamente con el tiempo, y donde la tarea fundamental consiste en mantener la salida en el valor deseado a pensar de las perturbaciones presentes.
* Ejemplos: el sistema de calefacción de una casa, un regulador de voltaje, un regulador de presión de suministro de agua.

Podemos utilizar alguna de las siguientes estrategias para obtener modelos que representen un sistema. Por ejemplo:

* *Modelación de sistemas*. El sistema se suele analizar como subsistemas más simples. Se suelen utilizar leyes físicas, enfoques como Euler-Lagrange  Hamilton, o bloques para el caso de los modelos compartimentales. Los modelos obtenidos suelen llamarse como *modelo de caja blanca* o *modelo interno*.
* *Identificación de sistemas*. Emplea observaciones de entrada y salida de un sistema para construir un modelo. No considera dinámicas internas sino en su respuesta ante una entrada determinada. En este punto se pueden utilizar estrategias poliniomiales o Redes Neuronales Artificiales, por mencionar algunas. Los modelos obtenidos suelen llamarse como *modelo de caja negra* o *modelo entrada-salida*.
* *Estrategia híbrida*. Es una combinación de las anteriores. Parte de un modelo obtenido de leyes físicas y los elementos desconocidos son identificados o estimados por alguna estrategia de identificación. Los modelos obtenidos suelen llamarse como *modelo de caja gris*.


En la literatura podemos encontrar la clasificación de los modelos de acuerdo con su tipo. Por ejemplo:


* *Modelos causales*. Dependen de las condiciones presentes y pasadas para determinar una futura. En otras palabras, hay una relación de causalidad.
* *Modelos no causales*.
* *Modelos estáticos*. Depende de las condiciones presentes y no de las pasadas.
* *Modelos dinámicos*. Los estados del sistema dependen de lo que haya sucedido con anterioridad debido a que suele haber algún tipo de almacenamiento de energía. Suelen llamarse también como *sistemas con memoria*.
* *Modelos estocásticos*. Incluye variables aleatorias que afectan el sistema. Por consiguiente, resulta imposible predecir el valor que éstas puedan tomar.
* *Modelos determinísticos*. Carecen de variables aleatorias. Por consiguiente, es posible conocer su comportamiento.
* *Modelos de parámetros concentrados*. Requiren de ecuaciones con derivadas o ecuaciones de diferencia ordinarias.
* *Modelos de parámetros distribuidos*. Su formulación implica ecuaciones diferenciales con derivadas parciales.
* *Modelos lineales*. Son sistemas que cumplen con la propiedad de proporcionalidad y superposición.


* *Modelos no lineales*. Modelos cuyos términos llevan multiplicidad entre los estados del sistema, potencias de los estados o funciones trascendentes cuyo argumento es alguna de las variables de estado del sistema.
* *Modelos invariantes en el tiempo*. Los parámetros del sistema se consideran constantes en el tiempo.
* *Modelos variantes en el tiempo*. Los parámetros del sistema varían en función del tiempo.
* *Modelos continuos*. Sistemas que dependen del tiempo $t$, donde $t$ es una variable continua que toma cualquier valor real.
* *Modelos discretos*. En este tipo de sistemas, el tiempo se considera que es una variable discreta denotada como $k$ y toma sólo unos valores en puntos específicos de la recta de los reales.

## Índices de error

Uno de los criterios que debe cumplir el modelo de un sistema es la validación. Para ello, evualuamos cuán preciso es para representar los datos experimentales del fenómeno que estamos estudiante. Es decir, evaluamos la diferencia entre los datos experimentales y los datos obtenidos por nuestro modelo. A esta diferencia le llamamos error y se puede cuantificar a partir de algunos de los siguientes índices.

### Criterios integrales

#### Integral del Error Absoluto (IAE)

$$
 \text{IAE} = \int_{0}^{\infty} | e(t) |\mathrm{d} t,
$$
donde

$$
 e(t) = y(t) - \hat{y}(t).
$$

* Fácil aplicación.
* No se pueden optimizar sistemas altamente sub ni altamente sobre amortiguados.
* Difícil de evaluar analíticamente.


####  Integral del Tiempo por el Error Absoluto (ITAE)

$$
 \text{ITAE} = \int_{0}^{\infty}t |e(t)|\mathrm{d}t.
$$

* Los errores tardíos son más castigados.
* Buena selectividad.
* Difícil de evaluar analíticamente.


####  Integral del Error Cuadrático (ISE)

$$
 \text{ISE} = \int_{0}^{\infty} e^{2}(t)\mathrm{d}t.
$$

* Da mayor importancia a los errores grandes.
* No es un criterio muy selectivo.
* Respuesta rápida pero oscilatoria, estabilidad pobre.


####  Integral del Tiempo por el Error Cuadrático (ITSE)

$$
 \text{ITSE} = \int_{0}^{\infty} te^{2}(t)\mathrm{d}t.
$$

* Los grandes errores iniciales tienen poco peso pero los que se producen más tarde son fuertemente penados.
* Mejor selectividad con respecto al ISE


### Criterios estadísticos

####  Mean Square Error (MSE)

$$
 \text{MSE} = \frac{1}{N} \sum_{k=0}^{N} e_{k}^{2}.
$$

* No recomendable para estudiar modelos de predicción.
* No tiene escala original el error porque está elevado al cuadrado.
* No se mide en unidades de los datos experimentales.

####  Root Mean Square Error (RMSE)

$$
 \text{RMSE} = \sqrt{\frac{1}{N} \sum_{k=0}^{N} e_{k}^{2}}.
$$

* Sensible a valores atípicos.
* No se ajusta a la demanda (¿qué es demanda?).
* Se mide en unidades de los datos experimentales.

####  Mean Absolute Error (MAE)

$$
 \text{MAE} = \frac{1}{N} \sum_{k=0}^{N} |e_{k}|.
$$

* Mide la precisión de los datos simulados.
* Se mide en unidades de los datos experimentales.
* No es sensible a valores atípicos.
* Utilizado para analizar series temporales.


####  Mean Absolute Percentage Error (MAPE)

$$
 \text{MAPE} = \frac{100\%}{N} \sum_{k=0}^{N} \frac{e_{k}}{y_{k}}.
$$

* Mide el error en porcentajes.
* Indicador de desempeño.
* Fácil interpretación.
* Ampliamente utilizado para evaluar modelos de predicción.

**Tabla de MAPE**
* Si $\text{MAPE}<10$, entonces el modelo es altamente preciso
* Si $10<\text{MAPE}<20$, entonces el modelo es bueno
* Si $20<\text{MAPE}<50$, entonces el modelo es razonable
* Si $\text{MAPE}>50$, entonces el modelo es impreciso

####  FIT

Obtiene el porcentaje de variación de salida que es explicado por un modelo

$$
 \text{FIT} = 100\left(1 - \frac{\|y - \hat{y}\|}{\|y - \bar{y}\|}\right).
$$


## Modelos analíticos de estudio de sistemas

**Modelo empírico**. Se obtiene a partir de las leyes físicas del sistema. Por ejemplo, las siguientes ecuaciones describen la zona líquida del flujo bifásico en un intercambiador de calor de doble tubo helicoidal

* Ecuación de continuidad

$$
 \dot{m}_{i+1} = \dot{m}_{i},
$$

$$
 v_{l_{i}} = \left[\frac{\dot{m}_{i}}{\rho_{l_{i}}A} \right],
$$

$$
 v_{l_{i+1}} = \left[\frac{\dot{m}_{i+1}}{\rho_{l_{i+1}}A} \right].
$$

* Ecuación de cantidad de movimiento

$$
 p_{i+1} = p_{i} - \frac{\triangle z}{A} \left( \frac{\Phi \bar{f}\bar{\dot{m}} p}{8 \bar{\rho}A^{2}} + \bar{\rho} Ag\sin(\theta) + \left[ \frac{\dot{m}\left( x_{g}v_{g} + (1-x_{g})v_{l}\right)}{\triangle z} \right]_{i}^{i+1} \right).
$$

**Modelo analítico**. Es la representación matemática de un problema. Por ejemplo, la siguiente ecuación diferencial representa a un modelo para describir el crecimiento poblacional de ciertos organismos

$$
 \frac{\mathrm{d} N(t)}{\mathrm{d}t} = K \cdot N(t) \cdot \ln{\left( \frac{A}{N(t)} \right)}.
$$

