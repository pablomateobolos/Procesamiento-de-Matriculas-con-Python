# Reconocimiento de Matrículas y Restricciones por Emisiones en Valencia

Este proyecto ha sido desarrollado por **Iván Rodríguez Tello, Pablo Mateo Bolós y Sergio Ruiz Perelló**. El principal objetivo es integrar técnicas avanzadas de visión por computador y reconocimiento óptico de caracteres (OCR) para gestionar de forma automatizada el cumplimiento de las normativas de las Zonas de Bajas Emisiones (ZBE) en la ciudad de Valencia.

## 📋 Descripción del Proyecto
El sistema actúa como un pipeline completo que recibe imágenes de vehículos, localiza y lee sus matrículas, estima la antigüedad del coche mediante datos de la DGT y, cruzando esta información con el tipo de combustible, determina la etiqueta ambiental correspondiente. Finalmente, el programa toma una decisión mediante la lectura de una matrícula sobre si el vehículo está autorizado para circular por una zona de bajas emisiones, como puede ser este caso, en el centro urbano de Valencia.

## 🛠️ Tecnologías y Librerías Utilizadas
El desarrollo se apoya en un stack tecnológico robusto diseñado para el procesamiento de imágenes y análisis de datos:
* **OpenCV**: Utiliza la carga de imágenes, redimensionado a 256x256 píxeles y transformaciones morfológicas que facilitan la detección.
* **EasyOCR**: Actúa como el motor principal de reconocimiento. Está configurado específicamente para extraer texto con altos niveles de confianza (reconocimiento de conjunto de pixeles que forma una letra).
* **Matplotlib & PIL**: Empleadas para la visualización de los resultados intermedios, como la cuadrícula de imágenes procesadas y la superposición de cuadros delimitadores.
* **NumPy & re**: Fundamentales para la manipulación de matrices de píxeles y el uso de expresiones regulares que validan que el texto detectado cumple con el patrón `NNNNLLL` de las matrículas españolas.

## ⚙️ Metodología y Pipeline
El proceso se divide en cinco etapas críticas:
1.  **Preprocesamiento y Umbralización**: Para combatir problemas de iluminación, sombras o reflejos, se aplica un método de **umbralización adaptativa**. A diferencia de un umbral fijo, este ajusta el valor de binarización según la media local de los píxeles circundantes, resaltando los caracteres de la matrícula incluso en condiciones adversas.
2.  **Detección de Texto**: EasyOCR escanea la imagen preprocesada. El sistema no solo extrae el texto, sino que analiza las coordenadas de ubicación y la probabilidad de acierto del modelo.
3.  **Reconstrucción de Matrícula**: Es común que el OCR detecte los números y las letras como bloques separados. Mediante expresiones regulares, el sistema concatena y limpia los caracteres para asegurar que la matrícula analizada y tomada como resultado es válida.
4.  **Estimación del Año**: Utilizando la primera letra del bloque final (por ejemplo, una matrícula que empieza por 'K'), el sistema consulta una tabla de rangos temporales basada en registros de la DGT (ej: serie 'K' corresponde a fecha de matriculación entre 2017-2019).
5.  **Lógica de Restricción**: Con el año estimado y el tipo de combustible del vehículo que se le pide indicar al usuario (gasolina o diésel), se aplica un motor de reglas que simula las restricciones reales de tráfico en Valencia.

## 🚦 Clasificación Ambiental y Acceso a Valencia
El sistema decide la capacidad de circulación basándose en el siguiente esquema de etiquetas:

| Combustible | Año Estimado | Clasificación | Acceso al Centro |
| :--- | :--- | :--- | :--- |
| **Gasolina** | Previo a 2001 | Sin Etiqueta (A) | ❌ Prohibido |
| **Gasolina** | 2001 - 2006 | Etiqueta B | ✅ Permitido |
| **Gasolina** | Posterior a 2006| Etiqueta C o superior | ✅ Permitido |
| **Diésel** | Previo a 2006 | Sin Etiqueta (A) | ❌ Prohibido |
| **Diésel** | 2006 - 2014 | Etiqueta B | ✅ Permitido |
| **Diésel** | Posterior a 2014| Etiqueta C o superior | ✅ Permitido |

## 🚀 Conclusiones y Futuro del Proyecto
Este proyecto demuestra la viabilidad de utilizar herramientas de código abierto para resolver problemas urbanos complejos.
* **Ventajas**: Es una solución escalable, automatizable y de bajo coste que no requiere la instalación de sensores físicos complejos en los vehículos.
* **Limitaciones**: La precisión actual depende de la calidad de la imagen y del ángulo de la cámara. Como mejora futura, se podría plantear la integración de modelos de Deep Learning específicos para la detección de objetos para localizar la matrícula antes de aplicar el OCR.

