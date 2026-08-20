# Diccionario de Datos - STOCKIFY

## 1. Introducción

El Diccionario de Datos de **STOCKIFY** contiene las definiciones de los datos que intervienen en el sistema de gestión de stock del almacén.

Su objetivo es establecer una descripción precisa y organizada de los datos utilizados por el sistema, facilitando su comprensión tanto para el usuario como para el analista.

El diccionario define los **almacenamientos**, las **estructuras de datos** y los **datos elementales** que forman parte del sistema.

El sistema permite gestionar productos, ventas, proveedores, compras, pagos, empleados y turnos, además de consultar información relacionada con stock, ventas y balances.

---

## 2. Notación utilizada

|  Símbolo  | Relación      | Significado                                                                     |
| :-------: | :------------ | :------------------------------------------------------------------------------ |
|    `=`    | Definición    | Define de qué componentes está compuesto un elemento.                           |
|    `+`    | Secuencial    | Los componentes siempre están presentes en la estructura.                       |
|  `[ \| ]` | Selección     | Representa alternativas. Solo se selecciona una.                                |
| `vi{ }vf` | Repetición    | El componente puede repetirse entre un valor inicial y un valor final de veces. |
|   `( )`   | Opcional      | El componente puede estar presente o no.                                        |
|    `@`    | Identificador | Identifica un registro de manera única y no admite valores nulos.               |

---

# 3. Almacenamientos

Los almacenamientos representan los datos que permanecen almacenados en el sistema.

Cada almacenamiento se define mediante una estructura de datos compuesta por datos elementales y/o otras estructuras.

### 3.1 Usuario

```text
Usuario = @idUsuario + nombreUsuario + rolUsuario
```

Representa a una persona que utiliza el sistema. El sistema diferencia las funcionalidades disponibles según el rol del usuario.

### 3.2 Producto

```text
Producto = @codigoBarras + nombreProducto + precioVenta + costoProducto + (fechaVencimiento) + stockActual
```

Representa cada producto comercializado por el almacén.

### 3.3 Venta

```text
Venta = @idVenta + fechaVenta + turno + idUsuario + medioPago + 1{DetalleVenta}n + totalVenta
```

Representa una venta realizada en el negocio.

### 3.4 Detalle de venta

```text
DetalleVenta = codigoBarras + cantidad + precioVenta + subtotal
```

Representa un producto incluido dentro de una venta.

### 3.5 Proveedor

```text
Proveedor = @idProveedor + nombreProveedor + (telefono) + (email)
```

Representa a los proveedores que abastecen de mercadería al negocio.

### 3.6 Compra

```text
Compra = @idCompra + fechaCompra + idProveedor + 1{DetalleCompra}n + totalCompra
```

Representa una compra de mercadería realizada a un proveedor.

### 3.7 Detalle de compra

```text
DetalleCompra = codigoBarras + cantidad + costoProducto
```

Representa un producto incluido dentro de una compra.

### 3.8 Pago a proveedor

```text
PagoProveedor = @idPago + fechaPago + idProveedor + montoPago
```

Representa un pago realizado a un proveedor por mercadería adquirida.

### 3.9 Turno

```text
Turno = @idTurno + fechaTurno + tipoTurno + 1{empleado}n
```

Representa un turno de atención del negocio y los empleados que trabajaron durante el mismo.

---

# 4. Estructuras con relación de selección

Las estructuras de selección permiten establecer alternativas donde solamente una opción puede ser elegida.

### 4.1 Rol de usuario

```text
rolUsuario = [ empleador | empleado ]
```

El usuario puede tener el rol de empleador o empleado. Las funcionalidades disponibles dependen del rol.

### 4.2 Tipo de turno

```text
tipoTurno = [ mañana | tarde ]
```

El negocio se organiza en turno mañana y turno tarde.

### 4.3 Medio de pago

```text
medioPago = [ efectivo | transferencia ]
```

Una venta puede ser abonada mediante efectivo o transferencia.

---

# 5. Datos elementales

Los datos elementales representan las unidades mínimas e indivisibles de información utilizadas por el sistema.

Cada dato se describe mediante su nombre, descripción, longitud, tipo y dominio de valores admisibles.

| Nombre             | Descripción                                                         | Longitud | Tipo             | Dominio                                         |
| :----------------- | :------------------------------------------------------------------ | :------: | :--------------- | :---------------------------------------------- |
| `idUsuario`        | Identificador único del usuario del sistema.                        |     —    | Numérico entero  | Continuo: `{vi: 1; vf: n}`                      |
| `nombreUsuario`    | Nombre utilizado para identificar al usuario.                       |    50    | Alfanumérico     | Texto libre                                     |
| `rolUsuario`       | Rol que determina las funcionalidades disponibles para el usuario.  |     —    | Alfanumérico     | Discreto: `{(E, empleador); (EM, empleado)}`    |
| `codigoBarras`     | Código utilizado para identificar un producto durante una venta.    |    50    | Alfanumérico     | Texto libre                                     |
| `nombreProducto`   | Nombre del producto comercializado.                                 |    100   | Alfanumérico     | Texto libre                                     |
| `precioVenta`      | Precio al que se comercializa el producto.                          |   12,2   | Numérico decimal | Continuo: `{vi: 0; vf: n}`                      |
| `costoProducto`    | Costo de adquisición del producto.                                  |   12,2   | Numérico decimal | Continuo: `{vi: 0; vf: n}`                      |
| `fechaVencimiento` | Fecha hasta la cual puede comercializarse el producto.              |     —    | Fecha            | Fecha válida                                    |
| `stockActual`      | Cantidad disponible del producto en el inventario.                  |     —    | Numérico entero  | Continuo: `{vi: 0; vf: n}`                      |
| `idVenta`          | Identificador único de una venta.                                   |     —    | Numérico entero  | Continuo: `{vi: 1; vf: n}`                      |
| `fechaVenta`       | Fecha en la que se realizó la venta.                                |     —    | Fecha/Hora       | Fecha y hora válidas                            |
| `turno`            | Turno en el que se realizó la venta.                                |     —    | Alfanumérico     | Discreto: `{(M, mañana); (T, tarde)}`           |
| `medioPago`        | Medio utilizado para abonar la venta.                               |     —    | Alfanumérico     | Discreto: `{(E, efectivo); (T, transferencia)}` |
| `cantidad`         | Cantidad de unidades de un producto involucradas en una operación.  |     —    | Numérico entero  | Continuo: `{vi: 1; vf: n}`                      |
| `subtotal`         | Importe correspondiente a un producto dentro de una venta o compra. |   12,2   | Numérico decimal | Continuo: `{vi: 0; vf: n}`                      |
| `totalVenta`       | Importe total correspondiente a una venta.                          |   12,2   | Numérico decimal | Continuo: `{vi: 0; vf: n}`                      |
| `idProveedor`      | Identificador único del proveedor.                                  |     —    | Numérico entero  | Continuo: `{vi: 1; vf: n}`                      |
| `nombreProveedor`  | Nombre o razón por la cual se identifica al proveedor.              |    100   | Alfanumérico     | Texto libre                                     |
| `telefono`         | Número telefónico de contacto del proveedor.                        |    30    | Alfanumérico     | Texto libre                                     |
| `email`            | Dirección de correo electrónico del proveedor.                      |    100   | Alfanumérico     | Texto libre                                     |
| `idCompra`         | Identificador único de una compra.                                  |     —    | Numérico entero  | Continuo: `{vi: 1; vf: n}`                      |
| `fechaCompra`      | Fecha en la que se realizó la compra al proveedor.                  |     —    | Fecha/Hora       | Fecha y hora válidas                            |
| `totalCompra`      | Importe total correspondiente a una compra.                         |   12,2   | Numérico decimal | Continuo: `{vi: 0; vf: n}`                      |
| `idPago`           | Identificador único de un pago realizado a un proveedor.            |     —    | Numérico entero  | Continuo: `{vi: 1; vf: n}`                      |
| `fechaPago`        | Fecha en la que se realizó el pago al proveedor.                    |     —    | Fecha/Hora       | Fecha y hora válidas                            |
| `montoPago`        | Importe abonado al proveedor.                                       |   12,2   | Numérico decimal | Continuo: `{vi: 0; vf: n}`                      |
| `idTurno`          | Identificador único de un turno.                                    |     —    | Numérico entero  | Continuo: `{vi: 1; vf: n}`                      |
| `fechaTurno`       | Fecha correspondiente al turno de atención.                         |     —    | Fecha            | Fecha válida                                    |
| `tipoTurno`        | Tipo de turno de atención.                                          |     —    | Alfanumérico     | Discreto: `{(M, mañana); (T, tarde)}`           |

---

# 6. Relaciones y reglas relevantes para los datos

Las siguientes relaciones se desprenden de los requerimientos y reglas de negocio del sistema.

### 6.1 Productos y ventas

Una venta está compuesta por uno o más detalles de venta:

```text
Venta = @idVenta + fechaVenta + turno + idUsuario + medioPago + 1{DetalleVenta}n + totalVenta
```

Cada detalle identifica el producto vendido, la cantidad, su precio de venta y el subtotal correspondiente.

### 6.2 Productos y compras

Una compra está compuesta por uno o más detalles de compra:

```text
Compra = @idCompra + fechaCompra + idProveedor + 1{DetalleCompra}n + totalCompra
```

Cada detalle identifica el producto adquirido, la cantidad y su costo.

### 6.3 Turnos y empleados

Cada turno debe quedar asociado al empleado o empleados que trabajaron durante el mismo.

```text
Turno = @idTurno + fechaTurno + tipoTurno + 1{empleado}n
```

### 6.4 Actualización del stock

Cuando se confirma una operación de entrada o salida de mercadería, se actualiza el stock correspondiente.

Las entradas de mercadería incrementan el stock y las salidas producidas por las ventas lo disminuyen.

### 6.5 Cálculo de ganancia

La ganancia de un producto se obtiene mediante la diferencia entre su precio de venta y su costo:

```text
gananciaProducto = precioVenta - costoProducto
```

### 6.6 Total de una venta

El total de una venta se obtiene a partir de los subtotales correspondientes a los productos vendidos:

```text
totalVenta = Σ subtotal
```

### 6.7 Total de ventas por período

El total facturado durante un período se obtiene a partir de las ventas registradas dentro de dicho período.

---

# 7. Observaciones

Este diccionario fue elaborado a partir del relevamiento de requisitos y las reglas de negocio disponibles para STOCKIFY.

Algunos elementos, como `idUsuario`, `idVenta`, `idCompra`, `idPago` e `idTurno`, se incorporan como identificadores necesarios para representar los almacenamientos siguiendo la notación de la materia.

La estructura deberá contrastarse con el **Diagrama de Flujo de Datos (DFD)** y el **Modelo Entidad-Relación (DER)** definitivo del proyecto para asegurar que los nombres, atributos y relaciones coincidan exactamente con dichos modelos.

No se incorpora la gestión de ventas fiadas ni información de clientes, ya que el relevamiento establece explícitamente que estas operaciones continuarán realizándose fuera del sistema.
