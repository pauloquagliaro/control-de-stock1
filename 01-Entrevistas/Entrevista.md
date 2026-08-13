# Entrevista

Participantes: Luca Valls, Alan Balzaretti, Paulo Quagliaro, Maximo Pistarino
Persona entrevistada: Mauro Valls (Dueño del negocio)
Objetivo: Relevamiento de requisitos para el sistema de control de stock

Contexto del lugar:
Es un almacén de venta de productos al público en general, no se apunta a un rubro puntual. Maneja bastante variedad: comestibles, productos de limpieza, electrónicos y también artículos para mascotas. Son cuatro empleados en total. Estos de dividen en turnos durante día en la atención al cliente y uno se encarga puntualmente del control del stock. El local es uno solo, no manejamos varios depósitos ni sucursales.

Preguntas y respuestas:

¿Cuentan con un sistema ya implementado?<br>
Rta: No, no se está utilizando ningun sistema actualmente

¿Cómo registran actualmente los movimientos de dinero y de mercadería?
Rta.: Los registros se hacen de forma manual. Cuando entra mercadería, no se anota nada, directamente se acomoda en las góndolas. Las salidas de dinero se anotan en una planilla de papel, dividida en turno mañana y turno tarde. Al empezar cada turno se anota el dinero que hay en caja, y durante el día se van anotando las ventas, separando lo que se cobra en efectivo de lo que se cobra por transferencia.

¿tienen alguna problematica acualmente?<br>
ta.: El problema más grande hoy es el control de caja. Al cerrar cada turno suelen aparecer diferencias entre lo que debería haber y lo que realmente hay, y es difícil saber de dónde sale el error porque no hay un registro detallado. 
Otro problema, este sí relacionado al sistema que vamos a hacer, es el control de stock y de ganancias. La mercadería que entra no siempre se registra, entonces no se sabe con exactitud cuánto hay de cada producto ni cuándo hace falta reponer. Además, con los productos que tienen fecha de vencimiento, al no hacerles seguimiento, a veces se vencen antes de venderse y se pierde plata. Hoy todo el tema de stock y ganancias se lleva a mano, es muy engorroso, y los números no quedan claros, ni el stock ni la ganancia por período.

¿Cuentan con computadora en el local? ¿Tienen conexión a internet? 
Rta.: Por ahora no hay ninguna computadora en el local. Sí hay conexión a internet.

¿Quiénes usarían el sistema y qué tareas debería poder hacer cada uno? 
Rta.: Lo usarían los empleados y yo. Los empleados deberían poder registrar ventas y consultar el stock disponible. Las tareas más delicadas, como modificar el stock, dar de alta o baja productos, eliminar registros y consultar balances o ganancias, las haría solo yo. También quiero poder imprimir reportes. El sistema tiene que permitir registrar proveedores, compras y ventas, y estaría bueno tener alertas cuando el stock de algún producto esté bajo.

¿hay alguna otra funcion que te gustaria que tenga el sistema?<br>
rta: Me gustaria poder ver los costos y beneficios de cada producto. Tambien ver un balance de lo que se factura y ver cuantas ventas se realizaron en “x” fechas

Análisis del equipo (no forma parte de las respuestas del entrevistado)
A partir de la respuesta sobre vencimientos, el equipo identificó que una de las causas de que se venza mercadería es que Mauro compra de más sin tener una noción clara de cuánto se vende realmente de cada producto, ya que el control de stock se hace a ojo.
Por eso se propone que el sistema muestre el promedio de ventas de cada producto en los últimos meses (por ejemplo, del último mes o de los últimos dos). Con ese dato a la vista, Mauro podría comparar antes de comprar y decidir con mejor criterio si le conviene o no aprovechar una oferta por cantidad. Esto ataca la causa del problema de vencimientos y se conecta con el pedido que ya había hecho de poder ver balances y ventas por fecha.
