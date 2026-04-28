# Trabajo Práctico N°1 - Visualización de Datos con Python

## Tecnicatura Superior en Desarrollo de Software Multiplataforma
**Taller complementario - Big Data II**

Este proyecto presenta un análisis de distribución de Pokémon por generación utilizando un dataset completo de Pokémon y herramientas de procesamiento y visualización en Python.

## Grupo de Trabajo
- [Nombre del integrante 1]
- [Nombre del integrante 2]
- [Nombre del integrante 3]
- [Nombre del integrante 4]

## Descripción del Proyecto
El análisis se centra en la cantidad de Pokémon por generación. El flujo del proyecto incluye:
- Cargar datos desde un archivo CSV
- Limpiar y preprocesar atributos clave
- Convertir generaciones en valores numéricos
- Calcular conteos por generación
- Visualizar resultados con Matplotlib

## Dataset
Se utiliza el dataset `pokemon_complete_2025.csv`, que contiene atributos como nombre, tipo, generación y estadísticas base de cada Pokémon.

## Estructura del Proyecto
- `main.numpy.ipynb`: Notebook principal con el análisis y visualizaciones
- `data/pokemon_complete_2025.csv`: Dataset utilizado
- `README.md`: Documentación del proyecto

## Tecnologías y librerías
- Python 3.8+
- pandas
- NumPy
- Matplotlib

## Requisitos

- Python 3.8 o superior
- Jupyter Notebook o JupyterLab

## Instalación

```bash
pip install pandas numpy matplotlib jupyter
```

## Uso

1. Abrir `main.numpy.ipynb` en Jupyter Notebook o JupyterLab.
2. Ejecutar las celdas en orden.
3. Revisar los resultados y las visualizaciones generadas.

## Detalles de la implementación

- El notebook utiliza `pandas` para la carga y el preprocesamiento de datos.
- La columna `generation` se convierte a valores numéricos mediante un mapeo directo.
- Se calculan las frecuencias de generación con métodos vectorizados.
- La visualización se genera con Matplotlib y se guarda como imagen.

## Mejora realizada

Se reorganizó el flujo original para que sea más claro y modular, separando claramente:
- Carga de datos
- Limpieza y preprocesamiento
- Análisis estadístico
- Visualización

Esto facilita futuras ampliaciones y mantiene la lógica del análisis original.

## Notas

- Si el CSV tiene filas con formato inconsistente, `pandas.read_csv(..., on_bad_lines="skip")` evita errores de lectura.
- El uso de `pandas` permite un procesamiento más legible y elimina redundancias en el notebook.


