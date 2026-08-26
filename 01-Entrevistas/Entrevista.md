### Entrevista
### Participantes:  Luca Valls, Alan Balzaretti, Paulo Quagliaro, Maximo Pistarino
### Persona entrevistada: Mauro Valls (Dueño del negocio)
### Objetivo: Relevamiento de requisitos para el sistema de control de stock

**Contexto del lugar:** Es un almacén de venta de productos al público en general, no se apunta a un rubro puntual. Maneja bastante variedad: comestibles, productos de limpieza, electrónicos y también artículos para mascotas. Son cuatro empleados y el dueño. Estos se dividen en turnos durante el día en la atención al cliente. El local es uno solo, no manejamos varios depósitos ni sucursales.

**Preguntas y respuestas:**

**1) ¿Cómo es un día normal de trabajo?**
*   **Rta:** Lo primero que se hace en el inicio de la jornada es anotar el turno correspondiente (Turno mañana o Turno tarde), con cuánto dinero inició la caja, la firma del empleado que ha trabajado, el total que se vende en efectivo por un lado y por otro en transferencia, los cigarros vendidos y el importe de la mercadería comprada en el día (si es en efectivo E, si es transferencia T).

**2) ¿Cuántas personas están trabajando? ¿Cuáles son sus roles?**
*   **Rta:** Hay 5 personas trabajando, una es el empleador que se encarga de ir a buscar la mercadería, tres personas se encargan de atender al cliente y reponer mercadería, la restante se encarga de comprar la mercadería.

**3) ¿Cuentan con un sistema ya implementado? ¿Tienen alguna computadora en el local o conexión a internet?**
*   **Rta:** No, no se está utilizando un sistema actualmente. No se cuenta con computadoras en el local, si hay conexión a internet.

**4) ¿Cómo se organizan a la hora de comprar productos?**
*   **Rta:** Eso depende de los productos que van faltando, por lo general se compra en grandes cantidades cuando sale una buena oferta que tenga una fecha de vencimiento prolongada.

**5) ¿Cómo llevan el control de stock?**
*   **Rta:** No hay un control de stock preciso, el control de los productos es a ojo, no se anota en ningún lado la cantidad de productos que hay.

**6) ¿Cuál es la problemática a la que se enfrenta el negocio actualmente?**
*   **Rta:** Las problemáticas son que a la hora pico (11:00 hasta las 14:30 en el turno mañana y 20:30 hasta las 00:30 en el turno tarde), se acumulan demasiados clientes y en algunos casos no se puede anotar el importe de la venta lo que al final de la jornada te termina dando un faltante de caja, también aparecen sobrantes en diversos casos. Otro problema es que no hay un stock preciso lo que me genera pérdida de tiempo ya que necesito ir al depósito a ver qué mercadería necesito comprar.

**7) ¿Cuál crees que es la solución a todo esto?**
*   **Rta:** La solución que pienso es tener un sistema en el que pueda ver la cantidad de stock que tengo , ver el precio lista y costo de cada uno, poder ver cuál es el producto más vendido, poder imprimir la cantidad de stock y los balances de caja de cada turno. Por otro lado quiero que el sistema cuente con un código de barras a la hora de vender cada producto, ver la totalidad vendida en cada turno y la suma de ambas. También ver un balance de las ganancias y ver cuántas ventas se realizaron en “x” fechas.

**8) ¿Respecto al balance de cajas que informacion esperas ver?**<br>
*   **Rta:** En el balance de caja quiero que me aparezca con cuanta plata empezo la caja, el total de ventas, el costo de la mercadería vendida y la ganancia bruta resultante. Además, quiero poder ver el detalle de cada operación realizada en ese período.

**9) ¿Quiénes usarían el sistema y qué tareas debería poder hacer cada uno?**<br>
*   **Rta:** Lo usarían los empleados y yo. Los empleados deberían poder registrar ventas y consultar el stock disponible. Las tareas más delicadas, como modificar el stock, dar de alta o baja productos y eliminar registros, las haría solo yo (empleador). También quiero poder imprimir reportes.

**10) ¿Venden fiado?**
*   **Rta:** Se vende solo fiado a clientes del barrio y se anotan en un cuadernillo el importe y el nombre y apellido. Si un cliente viene a comprar pero tiene una deuda muy vieja o excedida, no se le fía en esos casos.

**11) entendemos, en ese caso Para poder llevar correctamente el control del stock y del balance de caja, proponemos que estas ventas se registren mediante una factura, detallando los productos vendidos, cantidades y precios. La factura quedaría registrada como impaga hasta que el cliente realice el pago. De esta manera, los productos se descuentan del stock al momento de realizar la venta, pero el importe no se incorpora al balance de caja hasta que sea abonado. ¿Está de acuerdo con manejarlo de esta manera?**
*   **Rta:** Dale, me parece bien

**12) ¿Cómo se manejan con los pedidos a los proveedores y los pagos?**
*   **Rta:** En algunos casos los proveedores van hasta el negocio y ofrecen los productos que tienen en oferta, si hay algún producto que se necesite y sea buena la oferta se pide.Cuando llega mercadería al negocio, la persona que se encuentra atendiendo en ese momento puede retirar dinero de la caja para realizar el pago al proveedor.En  caso de no contar con dinero suficiente en la caja se avisa al empleador y se paga mediante transferencia. Este movimiento se registra actualmente en el cuaderno junto con las demás operaciones del negocio.

**13) Teniendo en cuenta que estos pagos representan una salida de dinero de la caja, te proponemos registrar estos movimientos en el sistema para que puedan ser contemplados en los balances de caja. ¿Está de acuerdo con esta propuesta?**
*   **Rta:** Sí, estoy de acuerdo.

**14) ¿Cómo se calcula el precio de venta de cada producto?**
*   **Rta:** El precio de venta depende de cada producto y del margen de ganancia que se desea obtener. El porcentaje no es igual para todos los productos, sino que puede variar según el caso.

**15) ¿Cómo se calcula la ganancia de las ventas hechas en cada turno?**
*   **Rta:** Se calcula el 28% del total como ganancia, por ejemplo: si ese día se vendió un total de $200.000, el 28% ($56.000) se toma como ganancia. Eso hace que podamos ver un aproximado de la ganancia del día, pero no se sabe el monto específico de ganancia por producto.

**16) Entendemos que ese es el sistema de cálculo actual para tener un aproximado de las ganancias pero cuando tengas el sistema y este te permita ver a detalle la ganancia de cada producto este 28% para calcular la ganancia quedaría obsoleto y pasarías a tenerla más detallada y precisa.**
*   **Rta:** Claro, lo que yo hago es un aproximado; si tuviera el sistema sabría cuánto ganó con más precisión en cada producto.
