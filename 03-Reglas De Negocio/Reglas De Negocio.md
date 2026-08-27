# Reglas De Negocio

### 1. Hechos<br>
### 01 — Turnos de atención
El negocio se organiza en turno mañana y turno tarde.

### 02 — Medio de pago
Una venta puede ser abonada mediante efectivo o transferencia, o mediante una combinación de ambos dentro de una misma operación.

### 03 — Margen de ganancia
El margen de ganancia aplicado al precio de venta puede variar según el producto.
---

### 2. Restricciones<br>
### 01 — Acceso según rol
Los empleados no podrán realizar las operaciones que sean exclusivas del empleador.

### 02 — Gestión de fiado fuera del sistema
El sistema no deberá gestionar las ventas fiadas ni la información de clientes que adeudan, ya que esta información continuará registrándose fuera del sistema.

---

### 3. Acciones Disparadores<br>
### 01 Actualización de Stock 
Al confirmar una transacción de salida o entrada, se dispara la actualización del inventario en tiempo real.

---

### 4. Cálculos<br>
### 01 — Ganancia por producto
La ganancia bruta obtenida por un producto se determinará a partir de la diferencia entre su precio de venta y su costo.

### 02 — Total de ventas por turno
El total vendido de un turno se calculará a partir de las ventas registradas durante dicho turno.

### 03 — Total de ventas de un período
El total facturado durante un período se calculará a partir de las ventas registradas dentro de dicho período.
