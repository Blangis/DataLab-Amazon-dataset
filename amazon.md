# Análisis de ventas Amazon

**Objetivo**: Identificar los factores que influyen en la satisfacción y compra de los clientes (precio, descuento, categoría, reseñas) para mejorar la estrategia de ventas y posicionamiento de productos en Amazon.

Se busca responder:

- ¿Qué productos o categorías generan mayor satisfacción? → Promedio de rating por producto o categoría.

- ¿Qué categorías tienen los precios promedio más altos, más bajos y mayores descuentos? → Agregando actual_price, discounted_price y discount_percentage.

- ¿Existe relación entre porcentaje de descuento y calificación promedio? → Comparando columnas numéricas ya agregadas por producto.

- ¿La diferencia entre precio real y precio con descuento está asociada a una mejor percepción del cliente? → Columna actual_price - discounted_price vs promedio rating.

- ¿Los productos más populares son también los mejor valorados? → Número de reseñas por producto vs promedio de rating.

- Patrones en reseñas positivas/negativas → Podrías hacer análisis de sentimiento concatenando todas las reseñas por producto y luego viendo tendencias por categoría.

# Productos

Se realizó la carga de los archivos, se identificaron valores nulos y se manejaron aquellos encontrados, con base en las preguntas a responder.

Se identificaron duplicados, se eliminaron aquellos que eran filas completas repetidas, y en los que se repetía el _product_id_ se optó por ordenar con base en el _discounted_price_ y quedarnos con la primer instancia de cada _product_id_ .

De esta manera de realizó la limpieza de esta tabla.

# Reviews

Se realizó la carga de los datos, se identificaron valores nulos, tenienddo las columnas **img_links** y **product_link** 466 valores nulos, sin embargo, considerando las preguntas a responder en este análisis, esas columnas no nos aportan información relevante, por lo que se eliminaron.
Para **rating_count** hubo 2 valores nulos, pero se decidieron imputar con 0.

Se identificaron duplicados
