# Requerimientos del Sistema (Almacén)

---

## 1. Requerimientos Funcionales (RF)

RF-01 (Registro de ventas): El sistema me tiene que dejar cargar cada venta indicando si se pagó en efectivo o por transferencia.
RF-02 (Apertura de caja): Permitir registrar la cantidad de plata con la que se arranca la caja a la mañana.
RF-03 (Registro de gastos): Poder registrar los pagos a proveedores que se hacen en efectivo directo desde la caja durante el día.
RF-04 (Cierre de caja): El sistema calcula solo el saldo teórico final del día para comparar con la plata física y ver si falta o sobra caja.
RF-05 (Control de stock automatizado): Descontar o sumar stock en tiempo real automáticamente con cada venta, compra o devolución.
RF-06 (Registro de mermas y vencimientos): Dar de baja productos rotos, perdidos o vencidos para ajustar el inventario real. Esta opción la puede usar únicamente el dueño/empleador.
RF-07 (Alertas de stock mínimo): Tirar una alerta cuando un producto esté con pocas unidades para saber que hay que reponer y no quedarse sin mercadería.
RF-08 (Registro de proveedores): Guardar los datos de contacto y nombres de los proveedores para dar de alta y consultar cuando haga falta.
RF-09 (Registro de compras): Cargar las compras hechas a proveedores con sus cantidades y el total invertido.
RF-10 (Balance diario y mensual): Generar los balances de ganancias y gastos al cerrar el día y al final del mes.
RF-11 (Reportes por fecha): Filtrar y consultar el total de ventas filtrando por un rango de fechas a elección.
RF-12 (Impresión de reportes): Opción para imprimir o guardar en PDF/digital los reportes y balances.
RF-13 (Cálculo de costos y beneficios): Ver el costo real y la ganancia neta por producto metiendo a mano el costo y precio de venta (sin usar porcentajes fijos globales).

---

## 2. Requerimientos No Funcionales (RNF)

RNF-01 (Control de accesos por rol): Manejar dos perfiles de usuario: *Empleado* y *Empleador*. Cada empleado va a entrar con su propia cuenta individual.
RNF-02 (Restricción de visualización): Los balances diarios y mensuales solo los puede ver el rol de Empleador.
RNF-03 (Restricción de modificaciones críticas): Solamente el Empleador tiene permisos para corregir stock a mano o borrar registros del sistema.
RNF-04 (Interfaz intuitiva para múltiples operadores): La pantalla de ventas tiene que ser re simple y rápida porque la van a usar varios empleados en distintos turnos (mañana/tarde).

---

## 3. Requerimientos de Dominio (RD)

RD-01 (Exclusión de registro de clientes): Se le vende a público general, así que no se guarda ningún dato de clientes en la base de datos.
RD-02 (Operación centralizada): El sistema está pensado para manejar la caja, stock y ventas de un solo local/almacén físico.
RD-03 (Validación de turno mediante inicio de sesión): El turno de atención se valida cuando el empleado inicia sesión. Si vuelve a iniciar sesión el mismo día, el sistema detecta que es la misma persona y no crea un turno de caja nuevo.
  
