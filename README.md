# Modelo predictivo para estimar el riesgo de diabetes en el Perú mediante selección metaheurística de variables (ABC binario) — ENDES 2025

**Curso:** Inteligencia Artificial (`1INF24`) — Pontificia Universidad Católica del Perú (PUCP)  
**Grupo 8:**
- Jose A. Chisun Fajardo
- Renato S. Yallahui Quevedo
- Alexandro Atencia Esteban
- Gabriel A. Quispe Cerrón
- Harumi A. Mochizuki Flores

---

## Descripción del proyecto

Este repositorio contiene el código fuente reproducible, los conjuntos de datos y los resultados experimentales de la Tarea Académica del Grupo 8. El estudio desarrolla y evalúa una adaptación binaria del algoritmo **Artificial Bee Colony (ABC)** para seleccionar variables clínicas y sociodemográficas no invasivas asociadas al diagnóstico autorreportado de diabetes mellitus en personas de 15 años a más en el Perú, a partir de la **Encuesta Demográfica y de Salud Familiar (ENDES) 2025** del INEI (29 598 registros válidos, 1 126 casos positivos, 22 predictores).

Los subconjuntos seleccionados por ABC binario se comparan frente al uso de las 22 variables originales y frente al método de filtro `SelectKBest` (información mutua con igual `k`) empleando tres clasificadores supervisados (**KNN**, **Árbol de decisión** y **Regresión logística**) dentro de tuberías sin fuga de información (*data leakage*).

---

## Estructura del repositorio

| Archivo / Carpeta | Descripción |
| :--- | :--- |
| `Grupo8_TA.ipynb` | Cuaderno principal en Python (preprocesamiento, implementación de ABC binario, experimentos `E0`–`E4` y generación de figuras). Incluye todas las celdas ejecutadas. |
| `endes2025_diabetes.csv` | Dataset de entrada del proyecto (33 569 × 27), resultante de unir por `HHID` las columnas requeridas de los módulos `CSALUD01` (1640), `RECH0` (1629) y `RECH23` (1630) de la ENDES 2025 sin alterar los códigos originales del INEI. |
| `dataset_limpio.csv` | Dataset depurado generado por la Parte 1 del cuaderno (29 598 × 26: 22 predictores no invasivos, 3 variables auxiliares y la etiqueta binaria `diabetes`). |
| `resultados/` | Tablas `.csv`, registros `.json` y figuras `.png` (300 DPI) generadas por los experimentos `E0`–`E4` y reportadas en el informe final. |
| `Grupo8-TA-Final.pdf` | Informe final en formato IEEE / plantilla oficial PUCP. |
| `Grupo8-TA-Final.docx` | Versión editable del informe final en Microsoft Word. |

---

## Instrucciones de ejecución

### Opción 1: Google Colab (recomendado)
1. Abrir `Grupo8_TA.ipynb` en Google Colab.
2. En el panel izquierdo (**Archivos**), subir el archivo `endes2025_diabetes.csv` a la raíz del entorno.
3. Ejecutar todas las celdas (`Entorno de ejecución > Ejecutar todas`).
   - La ejecución completa toma aproximadamente **30 minutos** (22 corridas de ABC binario con validación cruzada de 5 pliegues).
   - Para una verificación rápida de funcionamiento (~1 minuto), cambiar `EJECUCION_RAPIDA = True` en la celda de **Parámetros**.

### Opción 2: Entorno local (Python 3.10+)
```bash
pip install numpy pandas matplotlib scikit-learn imbalanced-learn jupyter
jupyter notebook Grupo8_TA.ipynb
```