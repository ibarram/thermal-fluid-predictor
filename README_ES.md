[![version](https://img.shields.io/badge/version-1.0.0-blue)](https://github.com/ibarram/thermal-fluid-predictor/)
[![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/w/ibarram/thermal-fluid-predictor)](https://github.com/ibarram/thermal-fluid-predictor/)
[![GitHub discussions](https://img.shields.io/github/discussions/ibarram/thermal-fluid-predictor)](https://github.com/ibarram/thermal-fluid-predictor/discussions)
[![GitHub issues](https://img.shields.io/github/issues/ibarram/thermal-fluid-predictor)](https://github.com/ibarram/thermal-fluid-predictor/issues)
[![Readme-EN](https://img.shields.io/badge/README-English-green.svg)](README.md)
[![Datos: CC BY 4.0](https://img.shields.io/badge/Datos-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/deed.es)
[![Código: MIT](https://img.shields.io/badge/C%C3%B3digo-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

<br />
<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/escudo-png.png" alt="Logo" width="120" height="120">
  </a>

  <h3 align="center">thermal-fluid-predictor</h3>

  <p align="center">
    Conjunto de datos experimental e implementación multilenguaje para la predicción en tiempo real de la temperatura del fluido en calentadores de agua a gas mediante sistemas embebidos.
    <br />
    <a href="https://github.com/ibarram/thermal-fluid-predictor"><strong>Explorar la documentación »</strong></a>
    <br />
    <br />
    <a href="https://github.com/ibarram/thermal-fluid-predictor/issues">Reportar un error</a>
    ·
    <a href="https://github.com/ibarram/thermal-fluid-predictor/issues">Solicitar una función</a>
  </p>
</div>

<details><summary>Contenido</summary><p>

 * [Resumen](#resumen)

 * [Banco de pruebas](#banco-de-pruebas)

 * [Obtener los datos](#obtener-los-datos)

 * [Base de datos](#base-de-datos)

 * [Carga de datos](#carga-de-datos)

 * [Implementaciones](#implementaciones)

 * [Comparativa](#comparativa)

 * [Publicaciones](#publicaciones)

 * [Contacto](#contacto)

 * [Cómo citar la base de datos thermal-fluid-predictor](#cómo-citar-la-base-de-datos-thermal-fluid-predictor)

 * [Licencia](#licencia)

</p></details><p></p>

## Resumen

Thermal Fluid Predictor es un proyecto multiplataforma para el modelado y la predicción del comportamiento térmico de un fluido en tiempo real. El repositorio incluye implementaciones en Python, MATLAB, C y R, orientadas a su integración en sistemas embebidos con recursos limitados, como los calentadores de agua a gas. Proporciona conjuntos de datos curados, modelos entrenados y diagramas del sistema para facilitar el desarrollo, la simulación y el despliegue reproducibles.

El conjunto de datos contiene mediciones de cinco variables obtenidas de un calentador de agua de recuperación rápida. La metodología de muestreo se basa en el concepto de **«estado del proceso del agua»**.

Cada proceso tiene una duración total de muestreo de 4 minutos.

Las muestras se registran cada 200 *ms*, es decir, a una frecuencia de muestreo de 5 *Hz*, lo que significa que en cada fase de 4 minutos se obtienen 1 200 muestras.

La construcción de los archivos de datos se basó en la tabla 1, que incluye 12 combinaciones únicas y no repetidas.

| # | Nombre de archivo | Rep. | Estado del agua | Flujo de agua | Flujo de gas | Temp. entrada (°C) | Temp. consigna (°C) |
|:-:|:-|:-:|:-|:-|:-|:-:|:-:|
| 1 | `C01_R01_SH_FZ_GL` | 1 | Heating | Zero | Low | 27 | — |
| 2 | `C02_R01_SH_FZ_GH` | 1 | Heating | Zero | High | 32 | — |
| 3 | `C03_R01_SH_FL_GL` | 1 | Heating | Low | Low | 26 | — |
| 4 | `C04_R01_SH_FL_GH` | 1 | Heating | Low | High | 28 | — |
| 5 | `C05_R01_SH_FH_GL` | 1 | Heating | High | Low | 25 | — |
| 6 | `C06_R01_SH_FH_GH` | 1 | Heating | High | High | 25 | — |
| 7 | `C07_R01_SS_FL_GL` | 1 | Steady | Low | Low | — | 41 |
| 8 | `C08_R01_SS_FL_GH` | 1 | Steady | Low | High | — | 40 |
| 9 | `C09_R01_SS_FH_GL` | 1 | Steady | High | Low | — | 38 |
| 10 | `C10_R01_SS_FH_GH` | 1 | Steady | High | High | — | 35 |
| 11 | `C11_R01_SC_FL_GZ` | 1 | Cooling | Low | Zero | — | — |
| 12 | `C12_R01_SC_FH_GZ` | 1 | Cooling | High | Zero | — | — |

**Tabla 1.** *Combinaciones utilizadas para generar los archivos de datos. Cada
combinación se repitió 10 veces, con un total de 120 registros. La temperatura
de entrada aplica solo al estado Heating; la de consigna, solo al estado Steady.*

Por lo tanto, el número total de archivos de datos únicos es 12. No obstante, se generaron repeticiones para ampliar la información del conjunto de datos: 10 archivos por combinación, lo que resulta en un total de 120 archivos.

## Banco de pruebas

El conjunto de datos se adquirió en el Laboratorio de Ingeniería Eléctrica de la División de Ingenierías del Campus Irapuato-Salamanca de la Universidad de Guanajuato, México.

El banco de pruebas consiste en un sistema calentador de agua de recuperación rápida que opera con gas LP y suministra 13 litros de agua por minuto. Se alimenta con dos pilas de 1.5 V tipo D conectadas en serie (3 V en total) e incluye una servoválvula para controlar el suministro de gas LP.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/testbench_fullview.png" alt="testbenchfullview1" width="800" height="400">
  </a>

**Figura 2.** *Fotografía del banco de pruebas utilizado para generar la base de datos. **Vista izquierda** | **Vista frontal** | **Vista derecha**.*
</div>

Las señales eléctricas de los sensores montados en el sistema de calentamiento se procesan mediante dos dispositivos. El primero es el microcontrolador STM32L476RGT6, integrado en una tarjeta Nucleo, que recibe las señales de dos sensores de temperatura (termistor NTC 3950 MF52 de 100 kΩ, ±1 %) para medir las variaciones de voltaje producidas por los cambios de resistencia del sensor ante la temperatura. Cada uno de estos sensores está montado externamente sobre las tuberías de entrada y de salida de agua, respectivamente.

También adquiere los datos de flujo de agua mediante un sensor de efecto Hall (sensor de flujo YF-B1), que mide los pulsos por segundo (Hz) generados por el paso del agua a través de la tubería.

El segundo dispositivo es el módulo NI USB-TC01, que permite medir la temperatura de salida mediante una sonda termopar tipo K de precisión.

Como se mencionó, la adquisición de datos se estructura a partir del concepto de «proceso del agua» para generar los archivos correspondientes. La convención de nombres sigue la estructura **C«XX»_R«ZZ»_S«W»_F«Y»_G«V»**, que se explica en detalle en las siguientes imágenes.

Como se muestra inicialmente en la `Figura 3`, la primera parte del nombre del archivo indica el número de archivo y su repetición (**C«XX»_R«ZZ»**). En total hay 12 archivos únicos, cada uno replicado 10 veces en este conjunto de datos. Pueden generarse repeticiones adicionales si se requiere.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/Interface2_last.png" alt="Interface2_last" width="600" height="600">
  </a>

**Figura 3.** *Obtención del número de combinación y del número de repetición.*
</div>

En el segundo paso, como se muestra en la `Figura 4`, se asigna el «proceso del agua» (**S«W»**):

- El agua se está calentando (**SH – State Heating**).
- La temperatura del agua se mantiene en un valor de consigna (**SS – State Steady**).
- El agua se está enfriando (**SC – State Cooling**).

En cada caso, la duración del muestreo es de 4 minutos con una muestra cada 200 *ms*, lo que corresponde a una frecuencia de muestreo de 5 *Hz* y un total de 1 200 muestras por ciclo completo.

En el primer caso (SH) el agua se calienta activamente, por lo que se activan tanto la salida de gas LP como la chispa de ignición para producir la flama.
En el segundo caso (SS) se define una temperatura de consigna y se aplica un método de control básico que simplemente enciende y apaga la fuente de gas para mantener una temperatura relativamente estable, aunque no controlada con precisión, únicamente con fines experimentales.
En el último caso (SC) el sistema entra en la fase de enfriamiento: se apagan tanto la salida de gas LP como la chispa de ignición, de modo que la flama deja de producirse.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/Interface3_last.png" alt="Interface3_last" width="600" height="600">
  </a>

**Figura 4.** *Obtención del estado de temperatura del agua.*
</div>

En el tercer paso, mostrado en la `Figura 5`, se asigna el caudal de agua que circula por la tubería (**F«Y»**).
Esta variable no tiene un valor fijo, pues depende por completo del consumo o la demanda de agua del usuario. Por ello, el equipo de investigación definió únicamente valores estimados:

- Flujo de agua «Cero» (**FZ**): el caudal debe ser nulo, es decir, la válvula de salida del calentador está completamente cerrada mientras la de entrada permanece abierta.
- Flujo de agua «Bajo» (**FL**): el caudal está entre 4 y 7 *L/min*. Ambas válvulas están abiertas; en este experimento la válvula de salida se fijó en posición intermedia.
- Flujo de agua «Alto» (**FH**): el caudal está entre 12 y 15 *L/min*. Ambas válvulas están abiertas; en este experimento la válvula de salida se abrió por completo.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/Interface4_last.png" alt="Interface4_last" width="600" height="600">
  </a>

**Figura 5.** *Obtención del flujo de agua.*
</div>

En el paso final, mostrado en la `Figura 6`, se asigna el valor de salida para la apertura de la válvula de gas LP (**G«V»**).
Esta variable no se mide en términos de presión, sino por la cantidad de corriente eléctrica suministrada a la electroválvula para controlar su apertura. Este comportamiento se ilustra en la `Figura 7`, que muestra la curva característica de funcionamiento. La operación de la válvula se define como sigue:

- Flujo de gas «Cero» (**GZ**): corriente aplicada = 0 *mA*; la válvula permanece completamente cerrada.
- Flujo de gas «Bajo» (**GL**): corriente aplicada = 10 *mA*; la válvula se abre a una posición mínima.
- Flujo de gas «Alto» (**GH**): corriente aplicada = 25 *mA*; la válvula se abre al máximo. Aplicar más corriente no produce cambios adicionales.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/Interface5_last.png" alt="Interface5_last" width="600" height="600">
  </a>

**Figura 6.** *Obtención del flujo de gas.*
</div>


<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/GraphGas.png" alt="GraphGas" width="500" height="500">
  </a>

**Figura 7.** *Características de la electroválvula.*
</div>

Por ejemplo, para generar un archivo se deben asignar los siguientes parámetros tomando como referencia la tabla de la `Figura 1`:

- **C01_R01**: primera combinación, entonces *C01*, y primera repetición, entonces *R01*.
- **SH**: el agua comenzará a calentarse, por lo que se selecciona la opción Heating en el campo State de la interfaz.
- **FZ**: el flujo de agua será nulo en este primer caso; por tanto, la válvula de salida permanecerá cerrada y se ajusta Water Flow a Zero en la interfaz.
- **GL**: el flujo de gas LP será bajo, por lo que se selecciona la opción Low en Gas Flow de la interfaz.

El nombre final del archivo será: **`C01_R01_SH_FZ_GL`**

***Nota:*** deben tenerse en cuenta ciertas consideraciones en algunos casos. Por ejemplo, como se muestra en la `Figura 8`, algunos elementos de la sección «Gas Flow» —como la condición Zero— aparecen tachados, ya que el agua no puede calentarse si no hay flujo de gas; por lo tanto, no tiene sentido considerar esa opción.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/Diagram1Combination2.png" alt="Diagram1Combination2" width="600" height="600">
  </a>

**Figura 8.** *Ejemplo de cómo seleccionar las variables de cada parte del archivo.*
</div>

De este modo se generan los 12 archivos esenciales del proceso. Cada archivo contiene 1 200 muestras, es decir, 12 archivos CSV con dimensiones [1200x5], lo que da un total de [12x1200x5]. Si se consideran las 10 repeticiones por archivo, se obtienen [12x10] archivos CSV. Combinando esto con el número de muestras por archivo resulta [12x10x1200x5] = [144 000x5] muestras en total.

Si necesita utilizar la interfaz de LabVIEW junto con el código cargado en la tarjeta STM32, se adjuntan los enlaces de descarga.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/labviewinterface.png" alt="labviewinterface" width="600" height="600">
  </a>

**Figura 9.** *Vista de ejemplo de la interfaz de LabVIEW.*
</div>

Puede descargar la interfaz de LabVIEW con el siguiente enlace.

|Nombre|Descripción|Tamaño|Enlace|
|:-|:-|:-|:-|
| `Data_HeaterSystem.zip` | Interfaz de LabVIEW para generar la base de datos | 288 KBytes | [Descargar](src/Data_HeaterSystem.zip) |

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/STM32IDE.png" alt="STM32IDE" width="600" height="600">
  </a>

**Figura 10.** *Plataforma [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html#overview).*
</div>


|Nombre|Descripción|Tamaño|Enlace|
|:-|:-|:-|:-|
| `STM32_Code_tfp.zip` | Código para STM32 | 14.7 MBytes | [Descargar](src/STM32_Code_tfp.zip) |

## Obtener los datos

Puede utilizar los enlaces directos para descargar el conjunto de datos, almacenado en formatos CSV y MAT.

|Nombre|Descripción|Muestras|Tamaño|Enlace|Suma MD5|
|:-|:-|:-|:-|:-|:-|
| `Raw_Signals_tfp.zip` | Datos crudos en formato CSV | [144,000x5] | 1.2 MBytes | [Descargar](Dataset/Raw_Signals_tfp.zip) | *(pendiente)* |
| `Raw_Signals_tfp_Folders.zip` | Datos crudos en formato CSV organizados en carpetas | [144,000x5] | 1.21 MBytes | [Descargar](Dataset/Raw_Signals_tfp_Folders.zip) | *(pendiente)* |
| `data_tfp.mat` | Datos crudos en formato MAT | [144,000x5] | 1.94 MBytes | [Descargar](Dataset/data_tfp.mat) | *(pendiente)* |

> Las sumas de verificación pueden comprobarse con `md5sum <archivo>` en Linux/macOS o `CertUtil -hashfile <archivo> MD5` en Windows.

De forma alternativa, puede clonar este repositorio de GitHub; el conjunto de datos se encuentra en `Dataset/`. El repositorio también contiene scripts de carga y visualización.

### Variables registradas

| Columna | Variable | Unidad | Descripción |
|:-|:-|:-|:-|
| 1 | `Time` | s | Tiempo transcurrido desde el inicio del registro |
| 2 | `TempIn` | °C | Temperatura del agua a la entrada (termistor NTC, no invasivo) |
| 3 | `TempOut` | °C | Temperatura del agua a la salida (termistor NTC, no invasivo) |
| 4 | `WaterFlow` | L/min | Caudal de agua a la salida (sensor de efecto Hall) |
| 5 | `TempReal` | °C | Temperatura de salida de referencia (termopar tipo K de inmersión) |

## Base de datos

La base de datos se presenta en dos formatos. El primero utiliza MATLAB y proporciona un archivo `.mat` correspondiente al thermal-fluid-predictor. La organización del archivo `.mat` se ilustra en la `Figura 11`, donde los valores y el número de muestras cambian según el archivo seleccionado.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/matfile.png" alt="matfile" width="600" height="600">
  </a>

**Figura 11.** *Representación esquemática de los datos organizados para el archivo de MATLAB.*
</div>

El segundo formato es un conjunto de archivos CSV organizados en carpetas, una por cada estado de operación, disponible en `Raw_Signals_tfp_Folders.zip`. Cada carpeta incluye las mediciones adquiridas en archivos individuales que siguen la convención de nombres descrita anteriormente.

Además del conjunto de datos, se proporcionan scripts de carga y lectura para MATLAB, Python, R y C.

## Carga de datos

Se crearon varios scripts para cargar el conjunto de datos de forma eficiente. Estos scripts facilitan la carga tanto de datos crudos como procesados, permitiendo trabajar en distintas etapas del análisis. Están desarrollados en MATLAB, Python, R y C.

#### MATLAB

```matlab
% Cargar el conjunto de datos completo
load('Dataset/data_tfp.mat');

% Cargar un registro individual
T = readtable('Dataset/Raw_Signals_tfp/C01_R01_SH_FZ_GL.csv');

plot(T.Time, [T.TempIn, T.TempOut, T.TempReal]);
xlabel('Tiempo (s)'); ylabel('Temperatura (\circC)');
legend('TempIn','TempOut','TempReal');
```

#### Python

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('Dataset/Raw_Signals_tfp/C01_R01_SH_FZ_GL.csv')

df.plot(x='Time', y=['TempIn', 'TempOut', 'TempReal'])
plt.xlabel('Tiempo (s)')
plt.ylabel('Temperatura (°C)')
plt.show()
```

#### R

```r
df <- read.csv("Dataset/Raw_Signals_tfp/C01_R01_SH_FZ_GL.csv")

matplot(df$Time, df[, c("TempIn", "TempOut", "TempReal")],
        type = "l", lty = 1,
        xlab = "Tiempo (s)", ylab = "Temperatura (C)")
legend("topleft", c("TempIn", "TempOut", "TempReal"),
       lty = 1, col = 1:3)
```

#### C

```c
#include <stdio.h>

int main(void) {
    FILE *f = fopen("Dataset/Raw_Signals_tfp/C01_R01_SH_FZ_GL.csv", "r");
    char line[256];
    float t, tin, tout, flow, treal;

    fgets(line, sizeof(line), f);            /* omitir encabezado */
    while (fgets(line, sizeof(line), f)) {
        sscanf(line, "%f,%f,%f,%f,%f", &t, &tin, &tout, &flow, &treal);
        printf("%6.2f  %6.2f\n", t, treal);
    }
    fclose(f);
    return 0;
}
```

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/HeatingSampleGif.gif" alt="Heating" width="300" height="400">
  </a>

  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/SteadySampleGif.gif" alt="Steady" width="300" height="400">
  </a>

  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/CoolingSampleGif.gif" alt="Cooling" width="300" height="400">
  </a>

**Figura 12.** *Muestras de calentamiento | estado estable | enfriamiento del agua.*
</div>

## Implementaciones

El directorio `models/` contiene los scripts utilizados para entrenar y evaluar los modelos de sensor virtual reportados en la publicación asociada.

| Ruta | Descripción |
|:-|:-|
| `models/train_knn.m` | Regresión KNN ponderada por distancia, un modelo por estado de operación |
| `models/train_dl.m` | Modelos de referencia LSTM, GRU y Bi-LSTM |
| `models/group_kfold.m` | Partición en 5 pliegues a nivel de archivo |
| `models/ema_filter.m` | Filtro de media móvil exponencial de primer orden |

> **Protocolo de validación.** Los pliegues de la validación cruzada se forman **a nivel de archivo**, no a nivel de muestra: los 120 archivos de adquisición se reparten en cinco grupos disjuntos, de modo que las 1 200 muestras de un registro pertenecen exclusivamente a la partición de entrenamiento o a la de validación. Esto evita que muestras temporalmente contiguas (separadas 200 ms y, por tanto, fuertemente correlacionadas) aparezcan en ambas particiones, lo que sesgaría a estimadores locales como KNN. Todas las métricas reportadas se calculan sobre registros de validación no vistos durante el entrenamiento.

## Comparativa

Puede enviar su propia evaluación creando un nuevo *issue* y la mostraremos aquí. Antes de proceder, verifique que su resultado no esté ya en esta lista. Para más información, consulte nuestras pautas de contribución.

| Modelo | Estado | MAE (°C) | RMSE (°C) | R² | Dentro de ±1 °C (%) | Fuente |
|:-|:-|:-|:-|:-|:-|:-|
| KNN (ponderado) | Heating | 0.231 | 0.752 | 0.947 | 93.70 | Este trabajo |
| KNN (ponderado) | Steady | 0.093 | 0.233 | 0.994 | 99.10 | Este trabajo |
| KNN (ponderado) | Cooling | 0.144 | 0.321 | 0.996 | 97.14 | Este trabajo |
| KNN (ponderado) | All States | 0.273 | 0.842 | 0.970 | 92.65 | Este trabajo |

## Publicaciones

Publicaciones de la comunidad científica que utilizan el conjunto de datos TFP:

*Un artículo de revista que describe este conjunto de datos se encuentra actualmente en revisión. Esta lista se actualizará tras su aceptación.*

## Contacto

[Dr. M.-A. Ibarra-Manzano](mailto:ibarram@ugto.mx?subject=[GitHub]%20TFP%20dataset) - [ORCID: 0000-0003-4317-0248](https://orcid.org/0000-0003-4317-0248) - [SCOPUS: 15837259000](https://www.scopus.com/authid/detail.uri?authorId=15837259000)

[M.I. M.-A. Armenta-Loredo](mailto:ma.armentaloredo@ugto.mx?subject=[GitHub]%20TFP%20dataset) - [ORCID: 0009-0006-7338-6065](https://orcid.org/0009-0006-7338-6065)

Enlace del proyecto: [thermal-fluid-predictor (TFP)](https://github.com/ibarram/thermal-fluid-predictor)

## Cómo citar la base de datos thermal-fluid-predictor

Si utiliza la base de datos TFP en una publicación científica, agradeceremos que haga referencia al siguiente trabajo. Actualmente hay un artículo de revista en revisión; los datos de la cita se añadirán tras su aceptación. Mientras tanto, cite el repositorio:

Entrada BibTeX:

```bibtex
@misc{tfp2026,
  author    = {Ibarra-Manzano, Mario-Alberto and
               Armenta-Loredo, Miguel-Angel and
               Almanza-Ojeda, Dora-Luz},
  title     = {Thermal Fluid Predictor {(TFP)} Dataset},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.XXXXXXX},
  url       = {https://github.com/ibarram/thermal-fluid-predictor}
}
```

Entrada Biblatex:

```bibtex
@dataset{tfp2026,
  author    = {Ibarra-Manzano, Mario-Alberto and
               Armenta-Loredo, Miguel-Angel and
               Almanza-Ojeda, Dora-Luz},
  title     = {Thermal Fluid Predictor {(TFP)} Dataset},
  date      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.XXXXXXX},
  url       = {https://github.com/ibarram/thermal-fluid-predictor},
  version   = {1.0.0}
}
```

## Licencia

Este repositorio emplea dos licencias:

- **Conjunto de datos** (`Dataset/`): [Creative Commons Atribución 4.0 Internacional (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.es). Puede compartir y adaptar los datos para cualquier finalidad, siempre que se otorgue el crédito correspondiente.
- **Código fuente** (`src/`, `models/`, scripts de carga): [Licencia MIT](https://opensource.org/licenses/MIT).

Consulte [`LICENSE`](LICENSE) y [`LICENSE-DATA`](LICENSE-DATA) para los términos completos.
