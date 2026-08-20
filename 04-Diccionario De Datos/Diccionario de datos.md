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

Los almacenamientos son los flujos de datos en reposo del sistema. Cada uno se define como una estructura de datos:

    Usuario = @idUsuario + nombreUsuario + contraseña + nombreCompleto + rol + estadoUsuario

    Categoria = @idCategoria + nombreCategoria + (descripcionCategoria)

    Proveedor = @idProveedor + razonSocial + cuit + (telefono) + (email) + (direccion) + estadoProveedor

    Producto = @idProducto + codigoBarras + nombreProducto + (descripcionProducto) + idCategoria + idProveedor + precioCosto + precioVenta + stockActual + stockMinimo + (fechaVencimiento) + estadoProducto

    Turno = @idTurno + fechaTurno + tipoTurno + montoInicialCaja + 1{idUsuario}n + totalEfectivo + totalTransferencia + totalTurno

    Venta = @idVenta + fechaVenta + idTurno + idUsuario + medioPago + 1{DetalleVenta}n + totalVenta + estadoVenta

    DetalleVenta = @idDetalle + idVenta + idProducto + cantidad + precioUnitario + subtotal

    PagoProveedor = @idPago + idProveedor + fechaPago + monto + (concepto)

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
| idUsuario | Identificador único del usuario. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| nombreUsuario | Nombre de acceso al sistema (único). | 30 | Alfanumérico | Texto libre |
| contraseña | Contraseña almacenada cifrada (hash). | 255 | Alfanumérico | Texto libre |
| nombreCompleto | Nombre y apellido del usuario. | 80 | Alfanumérico | Texto libre |
| rol | Rol del usuario dentro del sistema, determina las funcionalidades habilitadas. | 15 | Alfanumérico | Discreto: {(D, Empleador); (E, Empleado)} |
| idCategoria | Identificador único de la categoría. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| nombreCategoria | Nombre del rubro/categoría del producto (ej.: comestibles, limpieza). | 50 | Alfanumérico | Texto libre |
| descripcionCategoria | Descripción de la categoría. | 150 | Alfanumérico | Texto libre |
| idProveedor | Identificador único del proveedor. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| razonSocial | Razón social del proveedor. | 100 | Alfanumérico | Texto libre |
| cuit | CUIT del proveedor. | 13 | Numérico | Formato XX-XXXXXXXX-X |
| telefono | Teléfono de contacto del proveedor. | 30 | Numérico | Texto libre |
| email | Correo electrónico de contacto del proveedor. | 80 | Alfanumérico | Texto libre |
| direccion | Domicilio del proveedor. | 120 | Alfanumérico | Texto libre |
| idProducto | Identificador único del producto. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| codigoBarras | Código de barras del producto, utilizado para identificarlo al momento de la venta. Es único, no admite repetición. | 13 | Numérico | Continuo: {vi: 0; vf: n} |
| nombreProducto | Nombre del producto. | 100 | Alfanumérico | Texto libre |
| descripcionProducto | Descripción del producto. | 200 | Alfanumérico | Texto libre |
| precioCosto | Costo de adquisición vigente del producto. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| precioVenta | Precio de venta vigente del producto al público. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| stockActual | Cantidad disponible en inventario. | — | Numérico (entero) | Continuo: {vi: 0; vf: n} |
| stockMinimo | Umbral mínimo que dispara la alerta de reposición. | — | Numérico (entero) | Continuo: {vi: 0; vf: n} |
| fechaVencimiento | Fecha de vencimiento del producto, cuando corresponda. | — | Fecha | Continuo: {vi: fecha actual; vf: n} |
| idTurno | Identificador único del turno. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| fechaTurno | Fecha en la que se desarrolla el turno. | — | Fecha | Continuo: {vi: 14/05/2026; vf: fecha actual} |
| tipoTurno | Franja horaria del turno. | 10 | Alfanumérico | Discreto: {(M, mañana); (T, tarde)} |
| montoInicialCaja | Monto de dinero en caja al iniciar el turno. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| totalEfectivo | Total vendido en efectivo durante el turno. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| totalTransferencia | Total vendido por transferencia durante el turno. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| totalTurno | Importe total vendido durante el turno (efectivo + transferencia). | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| idVenta | Identificador único de la venta. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| fechaVenta | Fecha y hora de la venta. | — | Fecha/Hora | Continuo: {vi: 14/05/2026; vf: fecha actual} |
| medioPago | Medio de pago utilizado para abonar la venta. | 15 | Alfanumérico | Discreto: {(E, efectivo); (T, transferencia)} |
| totalVenta | Importe total de la venta. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| idDetalle | Identificador único del detalle de venta. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| cantidad | Cantidad de unidades vendidas del producto. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| precioUnitario | Precio unitario del producto al momento de la venta. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| subtotal | Subtotal de la línea (cantidad x precioUnitario). | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| idPago | Identificador único del pago realizado a un proveedor. | — | Numérico (entero) | Continuo: {vi: 1; vf: n} |
| fechaPago | Fecha en la que se realizó el pago al proveedor. | — | Fecha | Continuo: {vi: 14/05/2026; vf: fecha actual} |
| monto | Importe abonado al proveedor. | 12,2 | Numérico (decimal) | Continuo: {vi: 0; vf: n} |
| concepto | Detalle o motivo del pago realizado al proveedor. | 150 | Alfanumérico | Texto libre |
| estadoUsuario | Estado del usuario. | — | Booleano | Dominio {(1, activo); (0, inactivo)} |
| estadoProveedor | Estado del proveedor. | — | Booleano | Dominio {(1, activo); (0, inactivo)} |
| estadoProducto | Estado del producto. | — | Booleano | Dominio {(1, activo); (0, inactivo)} |
| estadoVenta | Estado de la venta. | — | Alfanumérico | Dominio {(C, confirmada); (A, anulada)} |
