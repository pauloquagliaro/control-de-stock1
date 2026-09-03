## Caso de uso: Registrar ingreso de mercadería

**Actores:** Empleado o Empleador (primario) — Proveedor (secundario).

**Precondiciones:** el proveedor debe estar registrado en el sistema.

**Postcondiciones:** el stock de los productos ingresados aumenta según la cantidad recibida; si se realizó el pago en el momento, el egreso queda reflejado en el balance de caja del turno correspondiente.

**Camino básico:**

El usuario inicia el registro de un ingreso de mercadería, indicando el proveedor y el número de remito.<br>
El usuario carga cada producto recibido con su cantidad y costo unitario.<br>
El sistema actualiza el stock de cada producto y su precio de costo vigente.<br>
El usuario indica si el pago se realiza en el momento (efectivo o transferencia) o si queda pendiente.<br>
Si el pago es en el momento, el sistema registra la salida de dinero de caja correspondiente.<br>

**Caminos alternativos:**

4.a La caja no cuenta con dinero suficiente en efectivo.    4.a.1 El sistema sugiere realizar el pago por transferencia. Vuelve al paso 4.

4.b El pago queda pendiente.    4.b.1 El sistema registra el ingreso de mercadería sin asociarle un pago inmediato. Fin del caso de uso.

**Escenario de éxito:** el stock queda actualizado con la mercadería recibida, y el pago (si corresponde) queda reflejado en caja.

**Escenario de fracaso:** no aplica — el ingreso de mercadería se registra igual aunque el pago quede pendiente.