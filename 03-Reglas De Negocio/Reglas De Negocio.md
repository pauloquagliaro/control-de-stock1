# Reglas De Negocio

1. Hechos<br>
● Estructura del negocio: El almacén cuenta con una única sucursal física y se dedica a la venta de productos de diversos rubros (comestibles, limpieza, electrónicos y mascotas) a todo público.<br>
● Equipo de trabajo: El personal está compuesto por 4 empleados en total (3 destinados a la atención al cliente en turnos rotativos de mañana y tarde, y 1 exclusivo para el control de stock).<br>
● Modelo de datos simplificado: El negocio requiere registrar proveedores , compras y ventas , pero explícitamente no realiza ni necesita un registro de datos de clientes.

---

2. Restricciones<br>
● Seguridad de datos: Solo el usuario con rol de Empleador tiene permisos para modificar los niveles de stock manualmente , eliminar registros y visualizar los balances económicos diarios y mensuales.<br>
● Congelamiento de precios: Cuando se registra una compra con un costo mayor al proveedor, el sistema tiene prohibido modificar el precio de venta automáticamente. El precio de venta al público se mantiene viejo hasta que el empleador lo autorice y cambie manualmente.<br>
● Políticas de Turnos: Cada turno debe registrar obligatoriamente con cuánto dinero en efectivo inicia la caja.

---

3. Acciones Disparadores<br>
● Inicio de Sesión Registro de Auditoría: Cuando un empleado se loguea con su usuario individual, el sistema dispara un registro automático e inalterable de asistencia visible para el empleador.<br>
● Venta/Compra de Producto Actualización de Stock: Al confirmar una transacción de salida o entrada, se dispara la actualización del inventario en tiempo real.<br>
● Cruce de Umbral Alerta de Stock Mínimo: Cuando las existencias físicas de un producto caen por debajo del límite configurado para su categoría, el sistema dispara una alerta visual de reposición.<br>
● Modificación de Ítem en Venta Registro de Anulación: Cuando el empleado cancela un producto durante la carga de la venta, se dispara un estado de "Ítem Anulado" asociado a su usuario para auditoría.<br>
● Cierre de Turno Arqueo Parcial: Al finalizar el turno mañana, se realiza la extracción del efectivo acumulado dejando una base de cambio, obligando a iniciar un nuevo ciclo de caja en el siguiente turno.

---

4. Cálculos<br>
● Cálculo de Ganancia Neta por Producto: Se abandona el estimativo general del 28% diario. Para ello, el empleador ingresa manualmente el precio de costo y el precio de venta final en el sistema, y luego el software calcula la ganancia real mediante la fórmula:<br>
Ganancia = Precio de Venta - Precio de Costo<br>
● Arqueo Teórico de Caja: Para reducir los errores de faltantes y sobrantes, el sistema calculará al final del día cuánto dinero debería haber físicamente usando la siguiente ecuación:<br>
Caja teorica = Caja Inicial + Ventas en Efectivo - Pagos a Proveedores<br>
● Balances Periódicos: Sumatoria automatizada de las ganancias netas de todas las ventas concretadas en el día o en el mes seleccionado, detallando de forma visible todos los gastos también.

---

5. Inferencias<br>
● Insuficiencia de Efectivo en Caja: Si se debe pagar a un proveedor un monto superior al dinero disponible en la caja física, el sistema permitirá registrar la transacción bajo la modalidad de transferencia bancaria.<br>
● Discrepancia en Arqueo (Sobrante/Faltante): Si el dinero físico real al cierre del turno no coincide con el cálculo del sistema, este no bloqueará la operación. Permitirá cerrar la jornada registrando la diferencia como "desajuste coherente por redondeo" para la posterior revisión del empleador.<br>
● Productos Vencidos o Perdidos (Mermas): Ante la pérdida o vencimiento de mercadería, el sistema debe permitir una salida de stock excepcional sin contrapartida de dinero (venta $0), restando las unidades del inventario y registrándose como pérdida directa, permitiendo esta acción exclusivamente al usuario con rol de empleador.<br>
● Devolución de Producto: Si un cliente regresa un artículo, el sistema debe gestionar la excepción de reingresar la unidad al stock físico y restar el dinero correspondiente de la caja del turno actual.<br>
● Notificación de Diferencias: En los días y turnos donde el balance final presente una diferencia o desajuste de caja, el sistema debe emitir un mensaje de aviso que muestre explícitamente el monto de la discrepancia y el nombre del empleado que trabajó en ese turno.
