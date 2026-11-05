## 1. Propósito del proyecto

El propósito de este proyecto es realizar la preparación y consolidación de diferentes archivos de información relacionados con las ventas de productos. Mediante Python y la biblioteca Pandas, se cargan cinco tablas de datos, se revisa su estructura y calidad, se identifican valores nulos y registros duplicados, y posteriormente se integran mediante operaciones de unión.

Como resultado, se obtiene un solo DataFrame con información relacionada con las ventas, productos, categorías, segmentos y calendario. Finalmente, se genera un archivo de los principales indicadores de ventas y se exporta la información en formatos Excel o CSV para facilitar su consulta y utilización en etapas posteriores.

## 2. Datos utilizados

Para realizar el proyecto se utilizaron cinco archivos:

| Archivo | Descripción |
|---|---|
| `DIM_CALENDAR` | Información relacionada con el calendario y las fechas. |
| `DIM_CATEGORY` | Información de las categorías de productos. |
| `DIM_PRODUCT` | Información y características de los productos. |
| `DIM_SEGMENT` | Información de los segmentos y atributos de los productos. |
| `FACT_SALES` | Información de las ventas de los productos. |

Los archivos se encontraban en formatos Excel (`.xlsx`) y CSV (`.csv`).

## 3. Herramientas y tecnologías

- **Python:** lenguaje de programación utilizado para el procesamiento de los datos.
- **Pandas:** biblioteca utilizada para cargar, explorar, limpiar, unir y exportar los DataFrames.
- **Jupyter Notebook:** entorno de trabajo para ejecutar y documentar el código.

## 4. Técnicas y procedimientos aplicados

### 4.1. Carga de archivos

Se utilizó Pandas para cargar los cinco archivos en DataFrames, mediante las funciones `read_excel()` y `read_csv()`, dependiendo del formato de cada archivo.

### 4.2. Exploración y comprensión de los datos

Se utilizaron diferentes métodos para conocer la estructura y el contenido de cada tabla:

- `head()`: permite visualizar los primeros registros.
- `info()`: muestra información sobre las columnas, los tipos de datos y los registros.
- `describe()`: proporciona estadísticas descriptivas de las columnas numéricas.
- `isnull().sum()`: identifica la cantidad de valores nulos por columna.
- `duplicated().sum()`: permite identificar registros duplicados.

Durante esta revisión se identificó que no había registros duplicados, por lo que no fue necesario aplicar `drop_duplicates()`.

### 4.3. Integración de las tablas

Se realizaron uniones entre los DataFrames utilizando el método `merge()` de Pandas y el tipo de unión `left`, con el propósito de conservar los registros de la tabla principal de ventas.

Las uniones se realizaron en el siguiente orden:

1. **Ventas y productos:** se relacionó `FACT_SALES` con `DIM_PRODUCT`, utilizando `ITEM_CODE` e `ITEM` como campos de correspondencia.
2. **Productos y categorías:** se integró `DIM_CATEGORY` utilizando las columnas `CATEGORY` e `ID_CATEGORY`.
3. **Categorías y segmentos:** se incorporó `DIM_SEGMENT` mediante las columnas `CATEGORY`, `ATTR1`, `ATTR2`, `ATTR3` y `FORMAT`.
4. **Información de calendario:** se integró `DIM_CALENDAR` utilizando la columna `WEEK`.

El resultado fue un DataFrame consolidado denominado `df_union4`.

### 4.4. Limpieza y revisión de los datos

Después de integrar las tablas, se realizaron las siguientes actividades:

- Se revisaron nuevamente los valores nulos mediante `isnull().sum()`.
- Se convirtió la columna `DATE` al tipo de dato fecha utilizando `pd.to_datetime()`.
- Se verificaron los nombres de las columnas mediante `columns.tolist()`.
- Se eliminaron espacios innecesarios al inicio y al final de los valores de las columnas de tipo texto mediante `str.strip()`.
- Se revisaron los valores únicos de la columna `CATEGORY_y` para comprobar su contenido.

Estas actividades permitieron verificar la estructura y mejorar la consistencia de la información consolidada.

### 4.5. Generación del resumen 

Se creó una copia del DataFrame consolidado mediante `copy()`, con el objetivo de conservar la información original y realizar los cálculos sobre una copia.

Posteriormente, se agregó una fila denominada `RESUMEN`, en la cual se calcularon los siguientes indicadores:

- **`TOTAL_UNIT_SALES`:** suma del total de unidades vendidas.
- **`TOTAL_VALUE_SALES`:** suma del valor total de las ventas.
- **`TOTAL_UNIT_AVG_WEEKLY_SALES`:** promedio de las ventas semanales promedio.

Los resultados se incorporaron en la fila de resumen del DataFrame `df_union4_resumen`.

### 4.6. Exportación de los resultados

Finalmente, se exportó el DataFrame consolidado con su fila de resumen en dos formatos:

- **Excel:** `Productos.xlsx`
- **CSV:** `Productos.csv`

Para ello se utilizaron los métodos `to_excel()` y `to_csv()` de Pandas.

## 5. Resultados obtenidos

Como resultado del procesamiento se obtuvo un archivo consolidado que integra la información de las cinco tablas originales.

El resultado incluye:

- Información de ventas.
- Datos y características de los productos.
- Categorías de productos.
- Atributos y segmentos.
- Información de calendario y fechas.
- Una fila adicional con el resumen de los indicadores de ventas.

Además, se generaron dos archivos de salida, uno en formato Excel y otro en CSV, que permiten consultar y reutilizar la información procesada.

## 6. Conclusiones

El proyecto permitió integrar diferentes fuentes de información en una sola estructura, facilitando la consulta de los datos relacionados con las ventas y sus características.

La exploración inicial permitió conocer la estructura de los archivos, revisar los tipos de datos, identificar valores nulos y comprobar la existencia de registros duplicados. Posteriormente, las uniones que se permitio relacionar la información de las tablas de ventas, productos, categorías, segmentos y calendario.

También se realizaron ajustes en los tipos de datos y en los valores de texto para mejorar la consistencia de la información. Finalmente, se calcularon indicadores generales de ventas y se exportó el resultado en formatos CSV y Excel.


## 7. Estructura general del proyecto

```text
Proyecto/
├── DIM_CALENDAR (2).xlsx
├── DIM_CATEGORY (2).csv
├── DIM_PRODUCT (1).xlsx
├── DIM_SEGMENT (1).xlsx
├── FACT_SALES (1).csv
├── Codigo.ipynb
├── Productos.xlsx
└── Productos.csv
```

**Nota:** Los archivos de salida se generan al ejecutar el código y se guardan en el directorio de trabajo de Python.
