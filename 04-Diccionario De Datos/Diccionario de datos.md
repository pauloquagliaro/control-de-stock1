# Diccionario de Datos - STOCKIFY

Listado organizado con las definiciones precisas y rigurosas de los datos del sistema de control de stock del almacén. Describe el significado de cada almacenamiento, de sus datos elementales y de las relaciones entre componentes, siguiendo la notación de la metodología estructurada.

---

## Notación

| Símbolo | Relación | Significado |
| :--- | :--- | :--- |
| `=` | Definición | "está compuesto de". |
| `+` | Secuencial | Componentes que siempre están presentes. |
| `[ \| ]` | Selección | Alternativas; solo se elige una. |
| `vi{ }vf` | Repetición | El componente se itera entre vi y vf veces. |
| `( )` | Opcional | El componente puede estar o no (repetición 0{ }1). |
| `@` | Identificador | Campo único que no se repite ni admite nulos (clave primaria). |

---

## Almacenamientos

Usuario = @nombreUsuario + contraseña + nombreCompleto + rol + estadoUsuario

Categoria = @nombreCategoria + (descripcionCategoria)

Proveedor = @cuit + razonSocial + (telefono) + (email) + (direccion) + estadoProveedor

Producto = @codigoBarras + nombreProducto + (descripcionProducto) + nombreCategoria + cuit + precioCosto + precioVenta + stockActual + stockMinimo + (fechaVencimiento) + estadoProducto

Cliente = @nombreCliente + apellidoCliente + (telefono) + saldoDeuda

Turno = @fechaTurno + tipoTurno + montoInicialCaja + 1{nombreUsuario}n + totalEfectivo + totalTransferencia + totalTurno

Venta = @numeroComprobante + fechaVenta + fechaTurno + tipoTurno + nombreUsuario + (nombreCliente + apellidoCliente) + 1{DetalleVenta}n + 1{DetallePago}n + totalVenta + estadoVenta

DetalleVenta = @numeroComprobante + codigoBarras + cantidad + precioUnitario + costoUnitario + subtotal

DetallePago = @numeroComprobante + medioPago + fechaPago + monto

IngresoMercaderia = @numeroRemito + cuit + fechaIngreso + nombreUsuario + 1{DetalleIngreso}n + medioPago + montoTotal

DetalleIngreso = @numeroRemito + codigoBarras + cantidad + costoUnitario

PagoProveedor = @cuit + fechaPago + monto + (concepto)
---

## Estructuras con relación de selección

Dato elemental cuyo valor se elige de un conjunto cerrado de alternativas:

    rol = [ Empleador | Empleado ]
    tipoTurno = [ mañana | tarde ]
    medioPago = [ efectivo | transferencia ]
    estado = [ activo | inactivo ]
    estadoVenta = [ confirmada | anulada ]

---

## Datos elementales

Mínimas unidades indivisibles de datos, con su nombre, descripción, longitud, tipo y dominio de valores admisibles.

| Nombre | Descripción | Longitud | Tipo | Dominio |
| :--- | :--- | :---: | :--- | :--- |
| nombreUsuario | Nombre de acceso al sistema (único). | 30 | Alfanumérico | Texto libre |
| contraseña | Contraseña almacenada cifrada (hash). | 255 | Alfanumérico | Texto libre |
| nombreCompleto | Nombre y apellido del usuario. | 80 | Alfanumérico | Texto libre |
| rol | Rol del usuario dentro del sistema, determina las funcionalidades habilitadas. | 15 | Alfanumérico | Discreto: {(D, Empleador); (E, Empleado)} |
| nombreCategoria | Nombre del rubro/categoría del producto (ej.: comestibles, limpieza). | 50 | Alfanumérico | Texto libre |
| descripcionCategoria | Descripción de la categoría. | 150 | Alfanumérico | Texto libre |
| cuit | CUIT del proveedor, utilizado como identificador del mismo. | 13 | Numérico | Formato XX-XXXXXXXX-X |
| razonSocial | Razón social del proveedor. | 100 | Alfanumérico | Texto libre |
| telefono | Teléfono de contacto (proveedor o cliente). | 30 | Numérico | Texto libre |
| email | Correo electrónico de contacto del proveedor. | 80 | Alfanumérico | Texto libre |
| direccion | Domicilio del proveedor. | 120 | Alfanumérico | Texto libre |
| codigoBarras | Código de barras del producto, utilizado como identificador del mismo. Identifica una combinación específica de marca y presentación. | 13 | Numérico | Continuo: {vi: 0; vf: n} |
| nombreProducto | Nombre del producto. | 100 | Alfanumérico | Texto libre |
| descripcionProducto | Descripción del producto. | 200 | Alfanumérico | Texto libre |
| precioCosto | Costo de adquisición vigente del producto. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| precioVenta | Precio de venta vigente del producto al público. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| stockActual | Cantidad disponible en inventario. | — | Numérico (entero) | Continuo: {vi: 0; vf: n} |
| stockMinimo | Umbral mínimo que dispara la alerta de reposición. | — | Numérico (entero) | Continuo: {vi: 0; vf: n} |
| fechaVencimiento | Fecha de vencimiento del producto, cuando corresponda. | — | Fecha | Fecha válida, posterior a la fecha de ingreso del producto |
| nombreCliente | Nombre del cliente con cuenta de fiado. | 50 | Alfanumérico | Texto libre |
| apellidoCliente | Apellido del cliente con cuenta de fiado. | 50 | Alfanumérico | Texto libre |
| saldoDeuda | Saldo actual adeudado por el cliente. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| fechaTurno | Fecha en la que se desarrolla el turno. | — | Fecha | Fecha válida, no posterior a la fecha actual |
| tipoTurno | Franja horaria del turno. | 10 | Alfanumérico | Discreto: {(M, mañana); (T, tarde)} |
| montoInicialCaja | Monto de dinero en caja al iniciar el turno. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| totalEfectivo | Total vendido en efectivo durante el turno. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| totalTransferencia | Total vendido por transferencia durante el turno. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| totalTurno | Importe total vendido durante el turno (efectivo + transferencia). | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| numeroComprobante | Número de comprobante/ticket asociado a una venta. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| fechaVenta | Fecha y hora de la venta. | — | Fecha/Hora | Fecha y hora válida, no posterior al momento actual |
| totalVenta | Importe total de la venta. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| cantidad | Cantidad de unidades vendidas o ingresadas del producto. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| precioUnitario | Precio unitario de venta del producto al momento de la operación. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| costoUnitario | Costo unitario del producto al momento de la operación (venta o ingreso). | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| subtotal | Subtotal de la línea (cantidad x precioUnitario). | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| medioPago | Medio de pago utilizado para abonar una venta o un ingreso de mercadería. | 15 | Alfanumérico | Discreto: {(E, efectivo); (T, transferencia)} |
| fechaPago | Fecha en la que se realizó un pago (a un proveedor o de una venta). | — | Fecha | Fecha válida, no posterior a la fecha actual |
| numeroRemito | Número de remito entregado por el proveedor junto con la mercadería. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| fechaIngreso | Fecha en la que se recibió la mercadería. | — | Fecha | Fecha válida, no posterior a la fecha actual |
| montoTotal | Importe total abonado por un ingreso de mercadería. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| monto | Importe abonado a un proveedor o correspondiente a una línea de pago de una venta. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| concepto | Detalle o motivo del pago realizado al proveedor. | 150 | Alfanumérico | Texto libre |
| estadoUsuario | Estado del usuario. | — | Booleano | Dominio {(1, activo); (0, inactivo)} |
| estadoProveedor | Estado del proveedor. | — | Booleano | Dominio {(1, activo); (0, inactivo)} |
| estadoProducto | Estado del producto. | — | Booleano | Dominio {(1, activo); (0, inactivo)} |
| estadoVenta | Estado de la venta, determinado por la comparación entre la suma de sus pagos y el total. | — | Alfanumérico | Dominio {(I, impaga); (P, pagada parcial); (C, pagada); (A, anulada)} |
