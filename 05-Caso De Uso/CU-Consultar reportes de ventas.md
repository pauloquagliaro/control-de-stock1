## Caso de uso: Consultar reportes de ventas

**Actores:** Empleador (primario).

**Precondiciones:** el usuario debe estar logueado con rol Empleador.

**Postcondiciones:** ninguna (es una consulta), salvo que se solicite impresión.

**Camino básico:**

El empleador selecciona el tipo de reporte a consultar (productos más vendidos, ventas por fecha, o total vendido por turno).<br>
El empleador indica el filtro correspondiente (rango de fechas o turno).<br>
El sistema calcula y muestra el resultado solicitado.<br>
El empleador puede solicitar la impresión del reporte mostrado.<br>

**Caminos alternativos:**

3.a No hay ventas registradas para el filtro solicitado.
3.a.1 El sistema muestra el mensaje "no hay datos para el período seleccionado".

**Escenario de éxito:** el empleador obtiene el reporte solicitado, opcionalmente impreso.

**Escenario de fracaso:** no hay datos disponibles para el filtro solicitado.