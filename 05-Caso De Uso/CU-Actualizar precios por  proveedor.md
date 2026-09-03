## Caso de uso: Actualizar precios por proveedor

**Actores:** Empleador (primario).

**Precondiciones:** debe existir al menos un proveedor con productos asociados.

**Postcondiciones:** los productos del proveedor seleccionado quedan con su precio de venta actualizado.

**Camino básico:**

El empleador selecciona un proveedor.<br>
El sistema muestra los productos asociados a ese proveedor con su precio de venta vigente.<br>
El empleador ingresa el porcentaje de aumento a aplicar.<br>
El sistema calcula el nuevo precio de venta de cada producto y solicita confirmación.<br>
El empleador confirma.<br>
El sistema actualiza el precio de venta de todos los productos del proveedor.<br>

**Caminos alternativos:**

1.a El proveedor seleccionado no tiene productos asociados.    1.a.1 El sistema muestra el mensaje "el proveedor no tiene productos asociados". Vuelve al paso 1.

3.a El empleador ingresa un porcentaje inválido (negativo o no numérico).    3.a.1 El sistema muestra el mensaje "porcentaje inválido". Vuelve al paso 3.

**Escenario de éxito:** los productos del proveedor quedan con el precio actualizado.

**Escenario de fracaso:** no se aplica el aumento por no haber productos asociados o por un porcentaje inválido.