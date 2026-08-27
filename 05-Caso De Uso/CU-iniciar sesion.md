## Caso de uso: Iniciar sesión

**Actores:** Empleado o Empleador (primario).

**Precondiciones:**
- El usuario debe tener un nombre de usuario y contraseña registrados en el sistema.
- El usuario debe estar en estado activo (no dado de baja).

**Postcondiciones:**
- El usuario queda autenticado en el sistema, con acceso a las funcionalidades habilitadas según su rol (Empleado o Empleador).

**Camino básico:**
1. El usuario ingresa su nombre de usuario y contraseña.
2. El sistema valida las credenciales ingresadas.
3. El sistema identifica el rol del usuario y habilita las funcionalidades correspondientes.
4. El sistema muestra la pantalla principal.

**Caminos alternativos:**

2.a El nombre de usuario no existe o la contraseña es incorrecta.
2.a.1 El sistema muestra el mensaje "usuario o contraseña incorrectos". Vuelve al paso 1.

2.b El usuario existe pero está dado de baja (inactivo).
2.b.1 El sistema muestra el mensaje "usuario inactivo, contacte al empleador". No permite continuar.

**Escenario de éxito:** el usuario accede al sistema con las funcionalidades habilitadas según su rol.

**Escenario de fracaso:** el usuario no puede acceder por ingresar credenciales incorrectas o por tener su cuenta dada de baja.
