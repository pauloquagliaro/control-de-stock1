## Caso de uso: Gestionar proveedores

**Actores:** Empleador (primario).

**Precondiciones:** el usuario debe estar logueado con rol Empleador.

**Postcondiciones:** el registro de proveedores queda actualizado.

**Camino básico** (alta de proveedor):

1.El empleador inicia el alta de un nuevo proveedor.<br>
2.El sistema solicita CUIT y razón social, y opcionalmente teléfono, email y dirección.<br>
3.El empleador completa los datos y confirma.<br>
4.El sistema valida que el CUIT no esté registrado previamente.<br>
5.El sistema da de alta el proveedor.<br>

**Caminos alternativos:**

1.a El empleador elige modificar un proveedor existente.    1.a.1 El sistema muestra los datos actuales del proveedor.    1.a.2 El empleador edita los campos y confirma.    1.a.3 El sistema actualiza el proveedor. Fin del caso de uso.

1.b El empleador elige dar de baja un proveedor.    1.b.1 El sistema verifica si el proveedor tiene productos activos asociados.    1.b.2 El sistema marca al proveedor como inactivo. Fin del caso de uso.

4.a El CUIT ya está registrado en otro proveedor.    4.a.1 El sistema muestra el mensaje "CUIT ya registrado". Vuelve al paso 2.

1.b.1.a El proveedor tiene productos activos asociados.    1.b.1.a.1 El sistema advierte que el proveedor tiene productos activos y solicita confirmación antes de continuar.

**Escenario de éxito:** el proveedor queda dado de alta, modificado o dado de baja.

**Escenario de fracaso:** el alta no se concreta por un CUIT duplicado.