# Explicación Detallada del Código en main.numpy.ipynb

Este documento explica paso a paso cada celda de código en el notebook `main.numpy.ipynb`, detallando qué hace específicamente cada línea y por qué se utiliza.

## Celda 1: Importación de NumPy y Carga de Datos

```python
import numpy as np

data = np.genfromtxt(
    "data/pokemon_complete_2025.csv",
    delimiter=",",
    names=True,
    dtype=None,
    encoding="utf-8",
    invalid_raise=False  # 👈 ESTO ES LA CLAVE
)

print(data.dtype.names)
```

**¿Qué hace?**
- `import numpy as np`: Importa la librería NumPy con el alias `np` para facilitar su uso.
- `np.genfromtxt()`: Función de NumPy para cargar datos desde archivos de texto estructurado (como CSV).
  - `"data/pokemon_complete_2025.csv"`: Ruta al archivo CSV que contiene los datos de Pokémon.
  - `delimiter=","`: Especifica que los valores están separados por comas.
  - `names=True`: Indica que la primera fila contiene los nombres de las columnas.
  - `dtype=None`: Permite que NumPy infiera automáticamente los tipos de datos de cada columna.
  - `encoding="utf-8"`: Especifica la codificación de caracteres para manejar caracteres especiales.
  - `invalid_raise=False`: Evita que el programa se detenga si encuentra líneas con datos inválidos o mal formateados.
- `print(data.dtype.names)`: Imprime los nombres de todas las columnas del dataset cargado.

**Propósito**: Cargar el dataset completo de Pokémon en un array estructurado de NumPy para su posterior análisis.

## Celda 2: Extracción de la Columna 'generation'

```python
generaciones = data["generation"]

print(generaciones[:10])  # para ver ejemplos
```

**¿Qué hace?**
- `generaciones = data["generation"]`: Extrae la columna 'generation' del array estructurado `data`. Esta columna contiene los números de generación en formato romano (I, II, III, etc.).
- `print(generaciones[:10])`: Imprime los primeros 10 valores de la columna para verificar el contenido y formato.

**Propósito**: Obtener específicamente los datos de generación de Pokémon para analizar su distribución.

## Celda 3: Conversión de Números Romanos a Números

```python
# Diccionario para convertir números romanos a números
mapa = {
    "I": 1, "II": 2, "III": 3, "IV": 4,
    "V": 5, "VI": 6, "VII": 7, "VIII": 8, "IX": 9
}

# Convertir
generaciones_num = np.array([mapa.get(g, 0) for g in generaciones])

print(generaciones_num[:10])
```

**¿Qué hace?**
- `mapa = {...}`: Crea un diccionario que mapea números romanos (strings) a números enteros.
- `mapa.get(g, 0)`: Para cada valor `g` en `generaciones`, busca su equivalente numérico en el diccionario. Si no encuentra el valor, devuelve 0 como valor por defecto.
- `np.array([...])`: Convierte la lista resultante en un array de NumPy para operaciones eficientes.
- `print(generaciones_num[:10])`: Muestra los primeros 10 valores convertidos para verificar la transformación.

**Propósito**: Convertir los números romanos a formato numérico para poder realizar operaciones matemáticas y análisis estadísticos.

## Celda 4: Cálculo de Frecuencias por Generación

```python
valores, cantidades = np.unique(generaciones_num, return_counts=True)

print(valores)
print(cantidades)
```

**¿Qué hace?**
- `np.unique(generaciones_num, return_counts=True)`: Encuentra los valores únicos en el array `generaciones_num` y cuenta cuántas veces aparece cada uno.
  - `valores`: Array con los números de generación únicos (ordenados).
  - `cantidades`: Array con el conteo correspondiente para cada generación.
- `print(valores)` y `print(cantidades)`: Muestra los valores únicos y sus frecuencias respectivas.

**Propósito**: Obtener un resumen estadístico que muestra cuántos Pokémon hay en cada generación.

## Celda 5: Creación del Gráfico

```python
plt.plot(valores, cantidades, marker='o')
plt.xlabel("Generación")
plt.ylabel("Cantidad de Pokémon")
plt.title("Cantidad de Pokémon por Generación")

plt.savefig("grafico.png")  # 👈 guarda la imagen
plt.show()
```

**Nota**: Esta celda asume que `import matplotlib.pyplot as plt` ya fue ejecutado anteriormente.

**¿Qué hace?**
- `plt.plot(valores, cantidades, marker='o')`: Crea un gráfico de líneas conectando los puntos (valores, cantidades), con marcadores circulares en cada punto de datos.
- `plt.xlabel("Generación")`: Etiqueta el eje X con "Generación".
- `plt.ylabel("Cantidad de Pokémon")`: Etiqueta el eje Y con "Cantidad de Pokémon".
- `plt.title("Cantidad de Pokémon por Generación")`: Agrega un título descriptivo al gráfico.
- `plt.savefig("grafico.png")`: Guarda el gráfico como un archivo de imagen PNG en el directorio actual.
- `plt.show()`: Muestra el gráfico en la interfaz del notebook.

**Propósito**: Visualizar gráficamente la distribución de Pokémon por generación, facilitando la identificación de patrones y tendencias.

## Celda 6: Importación de Pandas y Carga Alternativa

```python
import pandas as pd

df = pd.read_csv("data/pokemon_complete_2025.csv", on_bad_lines="skip")

print(df.columns)
```

**¿Qué hace?**
- `import pandas as pd`: Importa la librería Pandas con el alias `pd`.
- `pd.read_csv()`: Función de Pandas para leer archivos CSV.
  - `"data/pokemon_complete_2025.csv"`: Ruta al mismo archivo CSV.
  - `on_bad_lines="skip"`: Indica que se omitan las líneas que no se puedan parsear correctamente.
- `print(df.columns)`: Imprime los nombres de todas las columnas del DataFrame creado.

**Propósito**: Demostrar una alternativa de carga de datos usando Pandas en lugar de NumPy puro, obteniendo un DataFrame más flexible.

## Celda 7: Exploración de la Columna 'generation' con Pandas

```python
print(df["generation"].head())
```

**¿Qué hace?**
- `df["generation"]`: Selecciona la columna 'generation' del DataFrame.
- `.head()`: Muestra las primeras 5 filas de la columna (comportamiento por defecto de Pandas).
- `print()`: Imprime el resultado.

**Propósito**: Explorar rápidamente el contenido de la columna de generaciones usando Pandas.

## Celda 8: Conversión de Serie de Pandas a Array de NumPy

```python
import numpy as np

generaciones = df["generation"].values
```

**¿Qué hace?**
- `df["generation"].values`: Convierte la columna 'generation' del DataFrame de Pandas a un array de NumPy.
- `generaciones = ...`: Asigna este array a la variable `generaciones`.

**Propósito**: Preparar los datos de generación para procesamiento con NumPy, aprovechando la flexibilidad de Pandas para la carga inicial.

## Celda 9: Conversión de Números Romanos (Repetida)

```python
mapa = {
    "I": 1, "II": 2, "III": 3, "IV": 4,
    "V": 5, "VI": 6, "VII": 7, "VIII": 8, "IX": 9
}

generaciones_num = np.array([mapa.get(g, 0) for g in generaciones])
```

**¿Qué hace?**
- Identico a la Celda 3: Crea el diccionario de mapeo y convierte los números romanos a numéricos.

**Propósito**: Aplicar la misma transformación de datos, posiblemente para comparación o como alternativa al método anterior.

## Celda 10: Cálculo de Frecuencias (Repetido)

```python
valores, cantidades = np.unique(generaciones_num, return_counts=True)

print(valores)
print(cantidades)
```

**¿Qué hace?**
- Identico a la Celda 4: Calcula los valores únicos y sus conteos.

**Propósito**: Obtener el mismo resumen estadístico, demostrando consistencia entre diferentes métodos de procesamiento.

## Notas Generales

- **Duplicación de código**: Las celdas 3-4 y 9-10 realizan operaciones similares, mostrando dos enfoques diferentes (NumPy puro vs. combinación Pandas-NumPy).
- **Flujo de trabajo**: El notebook demuestra un flujo completo de análisis de datos: carga → exploración → transformación → análisis → visualización.
- **Manejo de errores**: Se utilizan parámetros como `invalid_raise=False` y `on_bad_lines="skip"` para robustecer el código ante datos imperfectos.
- **Visualización**: El gráfico final combina los resultados del análisis para una presentación clara y efectiva de los datos.