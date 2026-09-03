## Caso de uso: Consultar balance de caja

**Actores:** Empleado o Empleador (primario).

**Precondiciones:** debe existir al menos un turno registrado en el período consultado.

**Postcondiciones:** ninguna (es una consulta), salvo que se solicite impresión.

**Camino básico:**

El usuario indica el turno, día, mes o lapso de tiempo a consultar.<br>
El sistema muestra el monto inicial de caja, el total de ventas y el detalle de cada operación realizada en el período.<br>

**Caminos alternativos:**

1.a No existen operaciones registradas para el período indicado.    1.a.1 El sistema muestra el mensaje "no hay movimientos registrados en el período seleccionado".

2.a El usuario tiene rol Empleador.    2.a.1 El sistema muestra además el costo de la mercadería vendida y la ganancia bruta del período.

2.b El usuario, con rol Empleador, solicita imprimir el balance.    2.b.1 El sistema genera el documento imprimible. Fin del caso de uso.

**Escenario de éxito:** el usuario visualiza el balance con el nivel de detalle habilitado para su rol.

**Escenario de fracaso:** no hay movimientos registrados para el período consultado.