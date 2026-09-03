## Caso de uso:Registrar venta

**Actores:** Empleado o Empleador (primario) — Lector de código de barras (secundario, hardware).

**Precondiciones:**

El usuario debe estar logueado en el sistema con rol Empleado o Empleador.<br>
Debe existir un turno de caja abierto.<br>
Si la venta es fiada, el cliente debe estar registrado en el sistema.<br>

**Postcondiciones:**

El stock de los productos vendidos queda descontado.<br>
Se genera un registro de venta (comprobante) asociado al turno correspondiente.<br>
Si la venta fue abonada (total o parcialmente) al momento, el importe correspondiente se incorpora al balance de caja del turno. Si quedó impaga (fiado), el importe no se incorpora hasta que se registre su pago.<br>

**Camino básico** (venta de contado, un solo medio de pago):

1.El usuario inicia el registro de una nueva venta.<br>
2.El usuario escanea el código de barras de un producto.<br>
3.El sistema busca el producto, valida que haya stock disponible y agrega la línea a la venta con su precio unitario vigente.<br>
4.El usuario repite los pasos 2 y 3 hasta terminar de cargar los productos.<br>
5.El sistema calcula el total de la venta.<br>
6.El usuario selecciona el medio de pago (efectivo o transferencia) e ingresa el monto.<br>
7.El sistema valida que el monto cubra el total, descuenta el stock de cada producto vendido, genera el comprobante y actualiza los totales del turno.<br>

**Caminos alternativos:**

2.a El código de barras no corresponde a ningún producto registrado.    2.a.1 El sistema muestra el mensaje "producto no encontrado". Vuelve al paso 2.

3.a El producto no tiene stock suficiente para la cantidad solicitada.    3.a.1 El sistema muestra el mensaje "stock insuficiente" y no agrega la línea. Vuelve al paso 2.

6.a El usuario indica que la venta es fiada.    6.a.1 El sistema solicita seleccionar al cliente.    6.a.2 El sistema valida que el cliente no tenga una deuda vieja o excedida.    6.a.3 El sistema genera la venta como factura impaga, descuenta el stock, y no incorpora el importe al balance de caja. Fin del caso de uso.

6.b El usuario indica que el pago se realiza combinando más de un medio de pago.    6.b.1 El sistema permite ingresar más de una línea de pago (medio + monto).    6.b.2 El sistema valida que la suma de los montos ingresados sea igual al total de la venta. Continúa en el paso 7.

6.a.2.a El cliente tiene una deuda vieja o excedida.    6.a.2.a.1 El sistema muestra el mensaje "no se puede fiar a este cliente" y no permite continuar la venta como fiada. Vuelve al paso 6.

**Escenario de éxito:** la venta queda registrada, el stock se actualiza y el importe se refleja en el balance de caja del turno (o queda pendiente de cobro si fue fiada).

**Escenario de fracaso:** la venta no se concreta porque el producto no existe, no hay stock suficiente, o el cliente no puede acceder a fiado por tener una deuda vieja o excedida.