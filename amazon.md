# Análisis de ventas Amazon

**Objetivo**: Identificar los factores que influyen en la satisfacción y compra de los clientes (precio, descuento, categoría, reseñas) para mejorar la estrategia de ventas y posicionamiento de productos en Amazon.

Se busca responder:

- [¿Qué tipos de productos se manejan en este dataset de amazon?](#categorías-principales)

- [¿Las marcas con más productos son también las mejor calificadas?](#top-15-marcas-y-sus-puntuaciones-promedio)

- [¿Qué categorías tienen los precios promedio más altos, más bajos y mayores descuentos?](#categorías-con-precios-promedio)

- [¿Existe relación entre porcentaje de descuento y calificación promedio?](#porcentaje-de-descuento-y-puntuaciones)

- [¿Existe relación entre cantidad de reseñas y puntuación?](#número-de-reseñas-y-puntuaciones)

# Productos

Se realizó la carga de los archivos, se identificaron valores nulos y se manejaron aquellos encontrados, con base en las preguntas a responder.

Se identificaron duplicados, se eliminaron aquellos que eran filas completas repetidas, y en los que se repetía el _product_id_ se optó por ordenar con base en el _discounted_price_ y quedarnos con la primer instancia de cada _product_id_ .

De esta manera de realizó la limpieza de nulos y duplicados de esta tabla, teniendo **1351** filas y **7** columnas.

# Reviews

Se realizó la carga de los datos, se identificaron valores nulos, teniendo las columnas **img_links** y **product_link** 466 valores nulos, sin embargo, considerando las preguntas a responder en este análisis, esas columnas no nos aportan información relevante, por lo que se eliminaron.

Para **rating_count** hubo 2 valores nulos, pero se decidieron dejar como NaN.

Se revisaron los identificadores en el dataset de reviews (reseñas) para identificar duplicados. En particular:

- **product_id** debería ser único para cada producto.

- **review_id** identifica cada reseña individual, pero para nuestro análisis agregado por producto, nos interesa una fila por producto, consolidando la información de todas sus reseñas.

Al revisar duplicados en review_id, identifiqué que había reseñas iguales asignados a diferentes product_id's, esto porque se trataba del mismo producto con ligeras diferencias (color, memoria, etc), sin embargo, al esperar agrupar por categoría y cantidad de productos, se decidió dejar solo a un review_id, eliminando los demás. De esta manera dejé un review_id único asignado a un product_id.

> Nota: Al mantener una fila por **product_id**, perdemos la granularidad de las reseñas individuales, pero simplifica el análisis de métricas por producto como promedio de rating, precio, descuento, etc.

Finalmente, posterior a la limpieza de nulos y duplicados en esta tabla, se obtuvieron **1186** filas y **8** columnas.

# **Detección y tratamiento de valores fuera de alcance**

Se revisaron columnas clave para detectar inconsistencias:

- rating:

  - Se esperaba rango de 1 a 5.
  - Se confirmó la existencia de un valor NaN.

- actual_price y discounted_price:

  - Se verificó que no existieran precios negativos o inconsistencias.
  - Se comprobó que el discounted_price siempre fuera menor o igual al actual_price.

- discount_percentage:

  - Se calcularon valores esperados y se revisó la distribución para evitar porcentajes mayores al 100% o negativos.

- rating_count:
  - Se identificó que representa la cantidad de usuarios que han puntuado un producto.
  - Los valores mínimos fueron 0 (productos sin reseñas) y el máximo quedó abierto (sin límite superior).
  - Se decidió filtrar productos con rating_count > 0 en análisis donde se requiera información confiable.

# 📊 Flujo de trabajo del análisis

1. Dataset de productos → limpieza → productos limpios (productos_limpios.csv).
2. Dataset de reseñas → limpieza → reseñas limpias (reseñas_limpias.csv).
3. Ambos se unen por `product_id`.
4. Resultado: dataset combinado (productos_reseñas.csv).

# Unión de tablas

Se unieron las tablas de productos y reseñas mediante la columna product_id, generando un dataset consolidado que permite responder directamente las preguntas planteadas.

Tabla de productos: 1351 filas × 7 columnas.

Tabla de reseñas: 1186 filas × 8 columnas.

Tabla final combinada: 1186 filas × 10 columnas (conservando únicamente variables relevantes para el análisis).

## Normalización de categorías y nombres de productos

Para facilitar el análisis por categorías y evitar excesiva granularidad:

Se creó una nueva columna **category_main**, que contiene solo el primer nivel de la categoría (antes del primer |). Esto permite agrupar productos de manera general sin perder la información completa, que se mantiene en la columna original category por si se desea un análisis más detallado en el futuro.

La columna product_name se mantuvo tal cual, conservando toda la descripción del producto. Esto permite identificar los productos de manera única y no perder información relevante de atributos que podrían aparecer en el nombre (como tamaño, color, modelo, etc.). Se intentó extraer la marca, y se creó una columna brand a partir de las primeras dos palabras de product_name, sin embargo, algunas marcas pueden no estar perfectamente capturadas si no están al inicio del nombre del producto.

Tabla limpia: 1186 filas x 12 columnas

> Nota: Esta normalización facilita el análisis exploratorio y la agregación por categorías principales, pero mantiene la posibilidad de análisis más específico si se requiere.

## Casteo y datos fuera de alcance

- rating y rating_count se convirtieron a números. ✅

- No hay nulos en los precios → ✅
- No hay precios <= 0 → ✅
- No hay casos absurdos (discounted_price > actual_price) → ✅
- Puntajes entre 1 a 5 → Un valor NaN, los demás (1185) correctos.
- rating_count mayores a cero. → ✅

Se decidió agrupar por categorías principales y marcas, para conocer diferentes hallazgos de nuestro dataset.

## Hallazgos

### Categorías principales

Contamos con 9 categorías únicas principales, de las cuales podemos identificar cuáles tienen más cantidad de productos.

<img src="./visualizaciones/categorias.png" alt="Texto alternativo"  style="display: block; margin: 0 auto;">

<br>

<img src="./visualizaciones/top3categoriasproductos.png" alt="Texto alternativo"  style="display: block; margin: 0 auto;">

### Categorías con precios promedio

<img src="./visualizaciones/categorias_precios.png" alt="Texto alternativo"  style="display: block; margin: 0 auto;">

- Precio promedio más alto → La categoría cuyos productos tienen el mayor valor en el mercado (lujo o alta gama).

- Precio promedio más bajo → La categoría más accesible en términos de costo.

- Mayor descuento promedio → La categoría donde las ofertas/promociones son más agresivas, lo que puede indicar alta competencia o estrategias de marketing.

### Conociendo las marcas que manejamos

<img src="./visualizaciones/marcas_satisfaccion.png" alt="Texto alternativo"  style="display: block; margin: 0 auto;">

<br>

<img src="./visualizaciones/top5_por_categoria.png" alt="Texto alternativo"  style="display: block; margin: 0 auto;">

### Top 15 marcas y sus puntuaciones promedio

<img src="./visualizaciones/productos_vs_rating.png" alt="Texto alternativo"  style="display: block; margin: 0 auto;">

El número de productos que ofrece una marca no muestra relación con la calificación promedio de sus productos. Algunas marcas con gran variedad no necesariamente son las mejor evaluadas.

### Porcentaje de descuento y puntuaciones

<img src="./visualizaciones/descuento_vs_rating.png" alt="Texto alternativo"  style="display: block; margin: 0 auto;">

### Número de reseñas y puntuaciones

<img src="./visualizaciones/resenas_vs_rating.png" alt="Texto alternativo"  style="display: block; margin: 0 auto;">

# Conclusiones

- `Diversificar productos en distintas categorías como Musical Instruments, Health&Personal Care, HomeImprovement.`

- `Diversificar productos con precios variados en categorías como Toys&Games, HomeImprovement, que pueden tener esa flexibilidad.`

- `Mayores descuentos no implican mejores puntuaciones en reseñas.`

- `El número de reseñas no se relaciona con las puntuaciones.`
