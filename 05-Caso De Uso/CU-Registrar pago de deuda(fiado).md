## Caso de uso: Registrar pago de deuda (fiado)

**Actores:** Empleado o Empleador (primario).

**Precondiciones:** el cliente debe tener una factura de fiado impaga o pagada parcialmente.

**Postcondiciones:** el saldo adeudado por el cliente se reduce según el monto pagado; si el pago cubre el total, la factura pasa a estado "pagada" y el importe se incorpora al balance de caja del turno.

**Camino básico:**

El usuario busca al cliente y selecciona la factura de fiado a saldar.<br>
El sistema muestra el saldo pendiente de la factura.<br>
El usuario ingresa el monto a abonar y el medio de pago (o una combinación de medios).<br>
El sistema valida que el monto no supere el saldo pendiente.<br>
El sistema registra el pago, actualiza el saldo de la factura e incorpora el importe abonado al balance de caja del turno.<br>

**Caminos alternativos:**

4.a El monto ingresado supera el saldo pendiente.    4.a.1 El sistema muestra el mensaje "el monto supera la deuda pendiente". Vuelve al paso 3.

5.a El monto abonado cubre el total de la deuda de la factura.    5.a.1 El sistema marca la factura como "pagada". Fin del caso de uso.

5.b El monto abonado es menor al total adeudado.    5.b.1 El sistema marca la factura como "pagada parcial" y mantiene el saldo restante. Fin del caso de uso.

**Escenario de éxito:** el pago queda registrado y el saldo del cliente se actualiza correctamente.

**Escenario de fracaso:** el pago no se registra porque el monto ingresado supera la deuda pendiente.