## Caso de uso: Consultar stock y precios

**Actores:** Empleado o Empleador (primario).

**Precondiciones:** el usuario debe estar logueado.

**Postcondiciones:** ninguna (es una consulta de solo lectura).

**Camino básico:**

1.El usuario ingresa a la consulta de productos, opcionalmente buscando por nombre o código de barras.<br>
2.El sistema muestra el listado de productos con código de barras, nombre, precio de venta y cantidad disponible en stock.<br>
3.Si el usuario tiene rol Empleador, el sistema muestra además el precio de costo de cada producto.<br>

**Caminos alternativos:**

1.a La búsqueda no encuentra productos coincidentes.    1.a.1 El sistema muestra el mensaje "no se encontraron productos". Vuelve al paso 1.

**Escenario de éxito:** el usuario visualiza el stock y los precios habilitados para su rol.

**Escenario de fracaso:** no aplica (una búsqueda sin resultados no es un fracaso del caso de uso).