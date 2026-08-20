# Casos de Uso - STOCKIFY

Documentación de los requerimientos funcionales del sistema de control de stock del almacén desde el punto de vista de los usuarios.

---

## Actores

**Primarios** (utilizan las funciones principales del sistema):

- **Empleador (dueño del negocio):** acceso total. Gestiona productos, proveedores, usuarios y turnos; registra pagos a proveedores; consulta balances, ganancias y reportes; puede anular ventas. También puede registrar ventas.
- **Empleado:** funciones limitadas. Registra ventas y consulta el stock disponible; no puede modificar precios, stock, dar de alta/baja registros, ni acceder a balances o ganancias.

**Secundarios:**

- No se identifican actores secundarios. El sistema no integra con otros sistemas externos según el relevamiento realizado.

---

## CU-01 - Iniciar sesión

**Actores:** Empleador, Empleado (primario).

**Precondiciones:** El usuario debe estar dado de alta en el sistema con un nombre de usuario y una contraseña, y encontrarse activo.

**Camino básico:**
1. El usuario ingresa su nombre de usuario y su contraseña.
2. El sistema valida las credenciales.
3. El sistema identifica el rol del usuario (Empleador o Empleado).
4. El sistema habilita las funciones correspondientes a ese rol.

**Caminos alternativos:**
2.a El usuario o la contraseña son incorrectos.
2.a.1 El sistema muestra el mensaje "usuario o contraseña incorrectos" y vuelve al paso 1.
2.b El usuario está dado de baja (inactivo).
2.b.1 El sistema muestra el mensaje "usuario inactivo" y no permite el ingreso.

**Postcondiciones:** El usuario queda autenticado con los permisos de su rol.

**Escenario de éxito:** el usuario ingresó al sistema con los permisos de su rol.
**Escenario de fracaso:** el usuario no pudo ingresar por credenciales inválidas o por estar inactivo.

---

## CU-02 - Registrar venta

**Actores:** Empleado (primario), Empleador.

**Precondiciones:** El usuario debe estar logueado. Debe haber un turno abierto. Deben existir productos cargados con stock disponible.

**Camino básico:**
1. El usuario selecciona la opción de registrar una nueva venta dentro del turno abierto.
2. El usuario identifica un producto mediante su código de barras (o lo busca por nombre) e ingresa la cantidad.
3. El sistema verifica que haya stock suficiente y calcula el subtotal (cantidad x precio de venta vigente).
4. El usuario repite el paso 2 por cada producto que se lleva el cliente.
5. El sistema calcula el total sumando todos los subtotales.
6. El usuario indica el medio de pago (efectivo o transferencia).
7. El usuario confirma la venta.
8. El sistema registra la venta con fecha, turno y usuario; descuenta el stock de cada producto vendido y suma el importe al total del medio de pago correspondiente del turno.

**Caminos alternativos:**
2.a El código de barras no corresponde a ningún producto.
2.a.1 El sistema muestra el mensaje "producto no encontrado". Vuelve al paso 2.
3.a El stock del producto es insuficiente.
3.a.1 El sistema avisa que no hay stock suficiente y no agrega el producto. Vuelve al paso 2.
7.a El usuario cancela la venta.
7.a.1 El sistema descarta la venta sin registrar cambios. Fin.

**A tener en cuenta:** los caminos alternativos del punto 7 se pueden dar en cualquier momento de la carga, pero se ubican en ese paso por ser el punto natural donde el usuario decide confirmar o no la operación.

**Postcondiciones:** La venta queda registrada, el stock de los productos vendidos queda actualizado y el total del turno se actualiza según el medio de pago.

**Escenario de éxito:** la venta se registró y el stock y los totales del turno se actualizaron correctamente.
**Escenario de fracaso:** la venta no se registró por falta de stock o por cancelación del usuario.

---

## CU-03 - Anular venta

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado. La venta debe existir y no haber sido anulada previamente. (El Empleado no tiene este permiso.)

**Camino básico:**
1. El Empleador busca la venta que quiere anular.
2. El sistema muestra el detalle de la venta.
3. El Empleador confirma la anulación.
4. El sistema marca la venta como anulada, repone al stock las cantidades de cada producto vendido y descuenta el importe del total del turno correspondiente.

**Caminos alternativos:**
1.a La venta no existe.
1.a.1 El sistema avisa "venta no encontrada" y vuelve al paso 1.
3.a La venta ya estaba anulada.
3.a.1 El sistema avisa que la venta ya fue anulada y no realiza cambios. Fin.

**Postcondiciones:** La venta queda anulada, el stock de esos productos vuelve a estar disponible y los totales del turno quedan ajustados.

**Escenario de éxito:** la venta se anuló y el stock y los totales se repusieron correctamente.
**Escenario de fracaso:** no se anuló porque la venta no existía o ya estaba anulada.

---

## CU-04 - Consultar stock disponible

**Actores:** Empleado, Empleador (primario ambos).

**Precondiciones:** El usuario debe estar logueado.

**Camino básico:**
1. El usuario busca un producto por nombre o código de barras.
2. El sistema muestra la cantidad disponible en inventario del producto.

**Caminos alternativos:**
1.a El producto no existe.
1.a.1 El sistema muestra el mensaje "producto no encontrado".

**Postcondiciones:** El usuario visualiza la cantidad disponible del producto consultado.

**Escenario de éxito:** el usuario obtuvo la cantidad disponible del producto.
**Escenario de fracaso:** no se pudo consultar porque el producto no existe.

---

## CU-05 - Gestionar producto (alta, baja y modificación)

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado.

**Camino básico (alta):**
1. El Empleador selecciona la opción de alta de producto.
2. Ingresa el código de barras, nombre, descripción, categoría, proveedor, costo, precio de venta, stock inicial, stock mínimo y fecha de vencimiento (si corresponde).
3. El sistema valida que el código de barras no esté repetido.
4. El sistema guarda el producto.

**Caminos alternativos:**
3.a El código de barras ya está registrado.
3.a.1 El sistema muestra el mensaje "código ya registrado" y vuelve al paso 2.
b. Modificación: el Empleador busca un producto, edita sus datos (incluido el precio de venta y el costo) y guarda los cambios.
c. Baja: el Empleador busca un producto y lo da de baja (queda inactivo, no se elimina).

**Postcondiciones:** El producto queda dado de alta, modificado o inactivo según la operación.

**Escenario de éxito:** el producto se registró o se actualizó correctamente.
**Escenario de fracaso:** el alta no se completó por un código repetido.

---

## CU-06 - Registrar ingreso de mercadería

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado. El producto y el proveedor deben existir en el sistema.

**Camino básico:**
1. El Empleador selecciona la opción de ingreso de mercadería.
2. Selecciona el producto y el proveedor.
3. Ingresa la cantidad recibida y, si cambió, el nuevo costo del producto.
4. El sistema suma esa cantidad al stock actual del producto.
5. El sistema confirma la actualización del stock.

**Caminos alternativos:**
2.a El producto o el proveedor no existen todavía.
2.a.1 El sistema ofrece dar de alta el producto (CU-05) o el proveedor (CU-07), o cancelar la operación.

**Postcondiciones:** El stock del producto queda incrementado con la cantidad ingresada.

**Escenario de éxito:** el stock del producto se actualizó con la mercadería recibida.
**Escenario de fracaso:** no se registró el ingreso porque el producto o el proveedor no existían y se canceló.

---

## CU-07 - Gestionar proveedor (alta, baja y modificación)

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado.

**Camino básico (alta):**
1. El Empleador selecciona la opción de alta de proveedor.
2. Ingresa la razón social, el CUIT y los datos de contacto (teléfono, email, dirección).
3. El sistema valida que el CUIT no esté repetido.
4. El sistema guarda el proveedor.

**Caminos alternativos:**
3.a El CUIT ya está registrado.
3.a.1 El sistema muestra el mensaje "proveedor ya registrado" y vuelve al paso 2.
b. Modificación: el Empleador busca un proveedor, edita sus datos y guarda.
c. Baja: el Empleador da de baja un proveedor (queda inactivo).

**Postcondiciones:** El proveedor queda dado de alta, modificado o inactivo según la operación.

**Escenario de éxito:** el proveedor se registró o se actualizó correctamente.
**Escenario de fracaso:** el alta no se completó por un CUIT repetido.

---

## CU-08 - Registrar pago a proveedor

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado. El proveedor debe existir en el sistema.

**Camino básico:**
1. El Empleador selecciona el proveedor al que le va a registrar un pago.
2. Ingresa el monto, la fecha y el concepto del pago (por ejemplo, a qué mercadería corresponde).
3. El sistema guarda el registro del pago asociado a ese proveedor.

**Caminos alternativos:**
2.a El monto ingresado no es válido (vacío o negativo).
2.a.1 El sistema avisa que el monto no es válido y vuelve al paso 2.

**Postcondiciones:** El pago queda registrado y asociado al proveedor correspondiente.

**Escenario de éxito:** el pago se registró correctamente.
**Escenario de fracaso:** el pago no se registró por un monto inválido.

---

## CU-09 - Gestionar usuario (alta, baja y modificación)

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado.

**Camino básico (alta):**
1. El Empleador selecciona la opción de alta de usuario.
2. Ingresa el nombre de usuario, la contraseña, el nombre completo y el rol (Empleador o Empleado).
3. El sistema valida que el nombre de usuario no esté repetido.
4. El sistema guarda el usuario con la contraseña cifrada.

**Caminos alternativos:**
3.a El nombre de usuario ya existe.
3.a.1 El sistema muestra el mensaje "nombre de usuario no disponible" y vuelve al paso 2.
b. Modificación: el Empleador edita los datos o el rol de un usuario y guarda.
c. Baja: el Empleador da de baja un usuario (queda inactivo).

**Postcondiciones:** El usuario queda dado de alta, modificado o inactivo según la operación.

**Escenario de éxito:** el usuario se registró o se actualizó correctamente.
**Escenario de fracaso:** el alta no se completó por un nombre de usuario repetido.

---

## CU-10 - Registrar turno (apertura y cierre)

**Actores:** Empleado, Empleador (ambos pueden abrir o cerrar su turno).

**Precondiciones:** El usuario debe estar logueado.

**Camino básico (apertura):**
1. El usuario selecciona abrir un turno (mañana o tarde).
2. Ingresa el monto inicial de caja.
3. El sistema asocia al usuario (o a los usuarios) que trabajan durante ese turno.
4. El sistema deja el turno abierto, disponible para registrar ventas.

**Camino básico (cierre):**
5. El usuario selecciona cerrar el turno.
6. El sistema muestra el resumen del turno: total en efectivo, total por transferencia y total general.
7. El usuario confirma el cierre.

**Caminos alternativos:**
1.a Ya existe un turno abierto de esa franja horaria en el día.
1.a.1 El sistema avisa que el turno ya está abierto y no permite abrir otro.

**Postcondiciones:** El turno queda abierto o cerrado, con los empleados asociados y los totales correspondientes disponibles para el balance.

**Escenario de éxito:** el turno se abrió o se cerró correctamente con sus totales.
**Escenario de fracaso:** no se pudo abrir el turno porque ya había uno abierto para esa franja.

---

## CU-11 - Consultar balance por turno y por período

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado. Deben existir turnos y/o ventas registradas.

**Camino básico:**
1. El Empleador selecciona consultar balance.
2. Elige un turno puntual o un rango de fechas.
3. El sistema calcula y muestra el total facturado, discriminado por medio de pago (efectivo/transferencia) y, si es por turno, los empleados que trabajaron.

**Caminos alternativos:**
2.a No hay ventas registradas en el turno o rango elegido.
2.a.1 El sistema informa que no hay datos para ese período. Fin.

**Postcondiciones:** El Empleador visualiza el balance solicitado.

**Escenario de éxito:** el balance se generó con los totales correctos.
**Escenario de fracaso:** no se pudo generar el balance por falta de datos en el período.

---

## CU-12 - Consultar productos más vendidos

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado.

**Camino básico:**
1. El Empleador selecciona consultar productos más vendidos.
2. Opcionalmente filtra por un rango de fechas (por ejemplo, el último mes o los últimos dos).
3. El sistema muestra el ranking de productos según la cantidad vendida, junto con el promedio de ventas del período consultado.

**Caminos alternativos:**
2.a No hay ventas registradas en el período elegido.
2.a.1 El sistema informa que no hay datos para mostrar.

**A tener en cuenta:** el promedio de ventas por producto surge del análisis del equipo (no fue un pedido explícito del entrevistado) y busca darle al Empleador un criterio objetivo antes de decidir una compra por cantidad, para reducir el vencimiento de mercadería por sobre-stockeo.

**Postcondiciones:** El Empleador visualiza el ranking de productos más vendidos y su promedio de ventas.

**Escenario de éxito:** el ranking se generó correctamente.
**Escenario de fracaso:** no se pudo generar por falta de ventas registradas en el período.

---

## CU-13 - Consultar ganancia por producto

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado. El producto debe tener cargado su costo y su precio de venta.

**Camino básico:**
1. El Empleador selecciona consultar ganancia por producto.
2. El sistema calcula la diferencia entre el precio de venta y el costo de cada producto y la muestra.

**Caminos alternativos:**
1.a El producto no tiene costo cargado.
1.a.1 El sistema no puede calcular la ganancia y avisa que falta cargar el costo del producto.

**Postcondiciones:** El Empleador visualiza el costo, el precio de venta y la ganancia de cada producto.

**Escenario de éxito:** la ganancia se calculó y se mostró correctamente.
**Escenario de fracaso:** no se pudo calcular por falta del costo del producto.

---

## CU-14 - Generar e imprimir reportes

**Actores:** Empleador (primario).

**Precondiciones:** El Empleador debe estar logueado. Debe existir información registrada para el período o tipo de reporte elegido.

**Camino básico:**
1. El Empleador selecciona el tipo de reporte (ventas, balance, stock, proveedores, ganancias, etc.) y el rango de fechas si corresponde.
2. El sistema arma el reporte con la información registrada.
3. El sistema lo muestra en pantalla.
4. El Empleador lo exporta o lo imprime.

**Caminos alternativos:**
2.a No hay datos para el período o tipo de reporte elegido.
2.a.1 El sistema avisa que no hay información para generar el reporte. Fin.

**Postcondiciones:** El reporte queda generado y disponible para exportar o imprimir.

**Escenario de éxito:** el reporte se generó con la información correspondiente.
**Escenario de fracaso:** no se generó el reporte por falta de datos en el período elegido.
