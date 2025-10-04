# Análisis de productos y puntuaciones de Amazon

**Objetivo**: Identificar las relaciones entre los productos disponibles y los datos de los clientes (puntuaciones, reseñas) para mejorar la estrategia de ventas y posicionamiento de productos en Amazon.

Se busca responder:

- [¿Qué tipos de productos se manejan en este dataset de amazon?](#categorías-principales)

- [¿Las marcas con más productos son también las mejor calificadas?](#top-15-marcas-y-sus-puntuaciones-promedio)

- [¿Qué categorías tienen los precios promedio más altos, más bajos y mayores descuentos?](#categorías-con-precios-promedio)

- [¿Existe relación entre porcentaje de descuento y calificación promedio?](#porcentaje-de-descuento-y-puntuaciones)

- [¿Existe relación entre cantidad de reseñas y puntuación?](#número-de-reseñas-y-puntuaciones)

# Validación de datos

- Puntuaciones 1-5 ✅
- Precio con descuento menor o igual a precio actual ✅
- Porcentajes de descuento entre 0 - 100% ✅
- Reseñas mayores a cero ✅
- Tipos de datos correctos ✅

# Creación de columnas

- **category_main**
- **brand**

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
