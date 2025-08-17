
### **Taller Final: Análisis Exploratorio de un Catálogo de E-Commerce**

**Contexto de Negocio:**
Eres el nuevo analista de datos de "Fake Store". La gerencia necesita entender el catálogo de productos para tomar decisiones sobre precios, inventario y marketing. Tu misión es realizar un análisis exploratorio completo y presentar tus hallazgos.

**Objetivo:**
Usando la `Fake Store API`, realizarás un análisis en Google Colab para responder a preguntas de negocio clave, visualizando tus hallazgos y presentando un resumen con tus conclusiones.

**Entregable:**
Un notebook de Google Colab (`.ipynb`) con tu código, visualizaciones, análisis escritos y un resumen ejecutivo final.

---

#### **Parte 1: Adquisición y Preparación de los Datos**

1.  **Conexión a la API:**
    *   Importa `requests` y `pandas`.
    *   Realiza una petición `GET` al endpoint: `https://fakestoreapi.com/products`.
    *   Verifica que la petición fue exitosa (status code 200).

2.  **Creación y Limpieza del DataFrame:**
    *   Convierte la respuesta JSON en un DataFrame de Pandas.
    *   Inspecciona el DataFrame inicial con `.head()`, `.info()` y `.describe()`.
    *   **El Reto de los Datos Anidados:** La columna `rating` es un diccionario. Necesitamos separar la calificación (`rate`) y el número de votos (`count`) en sus propias columnas para poder analizarlas.

    **Pista / Ayuda:**
    ```python
    # Paso 1: Normalizar la columna 'rating' en un nuevo DataFrame
    rating_df = pd.json_normalize(df['rating'])

    # Paso 2: Renombrar las columnas para mayor claridad
    rating_df = rating_df.rename(columns={'rate': 'rating_rate', 'count': 'rating_count'})

    # Paso 3: Unir este nuevo DataFrame con el original
    df = pd.concat([df, rating_df], axis=1)

    # Paso 4: Eliminar la columna original 'rating' que ya no necesitamos
    df = df.drop(columns=['rating'])

    # ¡Ahora revisa tu DataFrame con df.head() para ver las nuevas columnas!
    ```

---

#### **Parte 2: Análisis Exploratorio de Datos (EDA)**

Para cada pregunta, presenta tu código, la visualización correspondiente y un párrafo corto explicando qué encontraste.

**Pregunta 1: Análisis de Precios**
*   ¿Cuál es la distribución de los precios de los productos? (Usa un **histograma**).
*   ¿Cuáles son los 5 productos más caros y los 5 más baratos? (Muestra una tabla).
*   **Insight de Negocio:** ¿Qué te dice esto sobre la tienda? ¿Vende principalmente productos de bajo, medio o alto costo?

**Pregunta 2: Análisis de Categorías**
*   ¿Cuántos productos hay en cada categoría? (Usa un **gráfico de barras**).
*   ¿Cuál es el precio promedio por categoría? (Usa otro **gráfico de barras**).
*   **Insight de Negocio:** ¿Qué categoría es la más cara en promedio? ¿Qué categoría tiene más variedad de productos?

**Pregunta 3: Análisis de la Calidad y Popularidad**
*   ¿Cuál es la distribución de las calificaciones de los productos (`rating_rate`)? (Usa un **histograma**).
*   ¿Existe alguna relación entre el precio de un producto y su calificación? (Usa un **diagrama de dispersión / scatter plot**).
*   **Insight de Negocio:** ¿Pagar más en esta tienda garantiza un producto mejor calificado por otros usuarios?

**Pregunta 4: Identificando los Productos Clave**
*   Identifica los 5 productos con el **mayor número de valoraciones** (`rating_count`). Estos son los más "populares" o "visibles".
*   Crea una nueva columna llamada `score`, calculada como: `score = rating_rate * rating_count`. Esta métrica combina calidad y popularidad.
*   ¿Cuáles son los 5 productos con el `score` más alto? Estos son probablemente los "productos estrella" de la tienda.
*   **Insight de Negocio:** Compara la lista de los productos más populares con la de los productos con mejor `score`. ¿Son los mismos? ¿Qué te dice esto?

---

#### **Parte 3: Resumen Ejecutivo y Recomendaciones**

Escribe un resumen (máximo 3 párrafos) para la gerencia de "Fake Store":
*   Resume tus 3 hallazgos más importantes.
*   Proporciona 2 recomendaciones de negocio claras y accionables basadas en tu análisis.

---

### Análisis de Catálogo de "Fake Store"**

**Confirmación y Puntos Clave del Taller:**

En esta actividad los datos permiten:
*   **Manejo de Datos Numéricos:** Análisis de precios (`price`).
*   **Análisis Categórico:** Agrupación por `category`.
*   **Pre-procesamiento de Datos:** La necesidad de separar la columna `rating` en `rate` y `count` es un ejercicio práctico fundamental.
*   **Creación de Métricas:** La creación de la columna `score` les enseña a ir más allá de los datos brutos.
*   **Enfoque de Negocio:** Las preguntas están orientadas a generar insights y recomendaciones, que es el objetivo final de la analítica.

---

### **Diccionario de Términos Clave (Inglés - Español)**

Este diccionario les ayudará a entender los términos técnicos en inglés que encontrarán en el código y en la documentación.

| Término en Inglés | Traducción al Español | Explicación en Contexto de Análisis de Datos |
| :--- | :--- | :--- |
| **API** | API (Interfaz de Programación de Aplicaciones) | Un "mesero" que nos permite pedir datos de un servidor en internet. |
| **DataFrame** | DataFrame (Marco de Datos) | La estructura principal de Pandas, similar a una tabla de Excel con filas y columnas. |
| **JSON** | JSON | Un formato de texto muy común para intercambiar datos en la web. Es fácil de leer para humanos y máquinas. |
| **Endpoint** | Punto de Conexión / URL | La dirección web (URL) específica a la que le pedimos los datos a la API. |
| **Request** | Petición / Solicitud | La acción de pedirle datos a la API. |
| **Response** | Respuesta | Los datos que la API nos devuelve después de nuestra petición. |
| **Head** (`.head()`) | Cabeza | Un comando de Pandas para ver las primeras 5 filas de un DataFrame. |
| **Info** (`.info()`) | Información | Un comando para ver un resumen del DataFrame: número de filas, columnas y tipo de dato de cada una. |
| **Describe** (`.describe()`) | Describir | Un comando que muestra estadísticas básicas (media, desviación estándar, etc.) de las columnas numéricas. |
| **Value Counts** (`.value_counts()`) | Conteo de Valores | Un comando para contar cuántas veces aparece cada valor único en una columna (ideal para categorías). |
| **Sort Values** (`.sort_values()`) | Ordenar Valores | Un comando para ordenar las filas de un DataFrame basándose en los valores de una o más columnas. |
| **Category** | Categoría | Columna que indica el tipo de producto (ropa de hombre, joyería, etc.). |
| **Price** | Precio | El costo del producto. |
| **Rating** | Calificación / Valoración | El objeto que contiene la puntuación y el número de votos de un producto. |
| **Rate** | Tasa / Puntuación | La calificación promedio del producto (ej: 4.1 de 5). |
| **Count** | Conteo / Número | El número total de personas que han calificado el producto. |
| **Histogram** | Histograma | Un gráfico que muestra la distribución de una variable numérica (ej: cuántos productos cuestan entre 0-50, 50-100, etc.). |
| **Bar Chart** | Gráfico de Barras | Un gráfico para comparar cantidades entre diferentes categorías (ej: número de productos por categoría). |
| **Scatter Plot** | Diagrama de Dispersión | Un gráfico para ver la relación entre dos variables numéricas (ej: precio vs. calificación). |

