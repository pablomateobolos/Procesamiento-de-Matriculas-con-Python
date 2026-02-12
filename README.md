# Reconocimiento de Matrículas y Restricciones por Emisiones en Valencia
Sistema de detección y reconocimiento de matrículas utilizando OpenCV y OCR.
# Reconocimiento de Matrículas y Restricciones por Emisiones en Valencia

[cite_start]Este proyecto, desarrollado por **Iván Rodríguez Tello, Pablo Mateo Bolós y Sergio Ruiz Perelló**, utiliza técnicas de visión por computador y OCR para automatizar el control de acceso a los vehículos en zonas de bajas emisiones[cite: 3, 56].

## 📋 Descripción del Proyecto
[cite_start]El sistema procesa imágenes de vehículos para identificar su matrícula, estimar su antigüedad y determinar si pueden circular por el centro de Valencia basándose en su impacto ambiental y tipo de combustible[cite: 3, 56].

## 🛠️ Tecnologías y Librerías
* [cite_start]**OpenCV**: Procesamiento, redimensionado y transformación de imágenes[cite: 5, 58].
* [cite_start]**EasyOCR**: Motor de reconocimiento óptico de caracteres entrenado para español[cite: 5, 59].
* [cite_start]**Matplotlib & PIL**: Visualización y manipulación de archivos de imagen[cite: 5, 60].
* [cite_start]**NumPy & re**: Análisis de datos y filtrado mediante expresiones regulares[cite: 5, 64].

## ⚙️ Funcionamiento del Proyecto
1. [cite_start]**Carga y Preprocesamiento**: Las imágenes se redimensionan a $256 \times 256$ píxeles[cite: 8, 70]. [cite_start]Se aplica **umbralización adaptativa** para resaltar caracteres en condiciones de iluminación difícil[cite: 10, 75].
2. [cite_start]**Reconocimiento (OCR)**: Se detectan bloques de texto y su nivel de confianza[cite: 13, 83].
3. [cite_start]**Reconstrucción**: Se utiliza **Regex** para consolidar el formato estándar español (4 números y 3 letras)[cite: 16, 86].
4. [cite_start]**Estimación de Antigüedad**: Se analiza la primera letra de las tres finales (ej. 'K' indica matriculación entre 2017-2019)[cite: 19, 100].
5. [cite_start]**Clasificación**: Se cruza el año estimado con el combustible para asignar la etiqueta ambiental[cite: 23, 111].

## 🚦 Criterios de Restricción en Valencia
| Combustible | Año de Matriculación | Etiqueta | ¿Puede circular? |
| :--- | :--- | :--- | :--- |
| **Gasolina** | < 2001 | Sin etiqueta | [cite_start]❌ No [cite: 24, 105] |
| **Gasolina** | 2001 - 2006 | Etiqueta B | [cite_start]✅ Sí [cite: 24, 105] |
| **Gasolina** | > 2006 | Etiqueta C+ | [cite_start]✅ Sí [cite: 24, 106] |
| **Diésel** | < 2006 | Sin etiqueta | [cite_start]❌ No [cite: 25, 108] |
| **Diésel** | 2006 - 2014 | Etiqueta B | [cite_start]✅ Sí [cite: 25, 109] |
| **Diésel** | > 2014 | Etiqueta C+ | [cite_start]✅ Sí [cite: 25, 110] |

## 🚀 Conclusiones
* [cite_start]**Ventajas**: Proceso automatizado, aplicable en tiempo real y de bajo coste[cite: 38, 126].
* [cite_start]**Limitaciones**: Sensible a la calidad y ángulo de la imagen; limitado al formato de matrícula española[cite: 39, 129].

---
*Proyecto académico realizado para la evaluación de restricciones de tráfico inteligentes.*
