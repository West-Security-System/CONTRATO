# Paso 3 - Diseño de las Issues del Repositorio

## 3.1 Objetivo del paso

Las issues representan cambios concretos para construir West Security Company. Están ordenadas según sus dependencias y prioridades, desde la persistencia y el acceso hasta la operación diaria del guardia y la supervisión administrativa. Cada issue se limita a una parte verificable del sistema y no incorpora funcionalidades fuera del alcance definido en el Paso 2.

Las issues 1 a 7 tienen prioridad alta porque habilitan la base, la persistencia y el acceso seguro. Las issues 8 a 20 tienen prioridad alta porque construyen el flujo operativo de usuarios, servicios, turnos e ingreso/egreso. Las issues 21 a 24 tienen prioridad media porque agregan supervisión, correcciones administrativas y consulta mensual sobre un flujo ya funcional.

## 3.2 Issues del proyecto

### Issue 1 - Inicializar la base SQLite del sistema
**Título y descripción**: Crear la base local `west_control.db` y habilitar su carga al iniciar el servidor.

**Objetivo y problema que resuelve**: establecer la persistencia necesaria para no perder usuarios, servicios, horarios y registros cuando se reinicia la aplicación.

**Alcance**:
- Incluido: inicialización de SQLite/sql.js, creación de la carpeta `data` y activación de claves foráneas.
- Excluido: datos de prueba, pantallas y consultas específicas de cada módulo.

**Criterios de aceptación**:
- la base se crea automáticamente si no existe,
- el servidor inicia sin error cuando la base ya existe,
- las claves foráneas quedan activas.

**Dependencias**: ninguna.

**Evidencias o pruebas**:
- ejecución del servidor con base nueva,
- ejecución posterior usando la misma base,
- captura de la estructura creada.

---

### Issue 2 - Crear tablas de usuarios y roles
**Título y descripción**: Crear la tabla `usuarios` con credenciales, datos personales, rol y bloqueos.

**Objetivo y problema que resuelve**: almacenar los dos perfiles del sistema y sus datos operativos sin usar información fija en el código.

**Alcance**:
- Incluido: campos `username`, `password`, `nombre`, `dni`, `rol`, `bloqueos` y fecha de creación.
- Excluido: formulario de administración y permisos distintos de `admin` y `guardia`.

**Criterios de aceptación**:
- el nombre de usuario es único,
- el rol por defecto es `guardia`,
- los datos obligatorios no aceptan valores vacíos.

**Dependencias**: Issue 1.

**Evidencias o pruebas**:
- consulta de la tabla `usuarios`,
- inserción de un admin y un guardia,
- prueba de rechazo de un usuario duplicado.

---

### Issue 3 - Crear tablas de servicios, horarios y registros
**Título y descripción**: Crear las tablas `locales`, `horarios` y `registros` con las relaciones necesarias para controlar turnos.

**Objetivo y problema que resuelve**: representar en la base el servicio, el horario asignado y el ciclo completo de ingreso/egreso.

**Alcance**:
- Incluido: coordenadas del local, relación horario-local, usuario asignado, timestamps, datos de ubicación y estado de egreso.
- Excluido: consultas del panel, métricas y notificaciones.

**Criterios de aceptación**:
- un horario pertenece a un servicio existente,
- un registro pertenece a un usuario existente,
- un registro permite guardar ingreso y egreso en la misma fila.

**Dependencias**: Issue 1, Issue 2.

**Evidencias o pruebas**:
- consulta de las tres tablas,
- inserción de un servicio con horario,
- inserción y lectura de un registro de prueba.

---

### Issue 4 - Sembrar el administrador inicial
**Título y descripción**: Crear automáticamente el usuario administrador `westcompany` cuando no exista.

**Objetivo y problema que resuelve**: permitir el primer acceso administrativo sin editar manualmente la base de datos.

**Alcance**:
- Incluido: función `seedAdmin`, hash de contraseña y creación condicional del usuario admin.
- Excluido: recuperación de contraseña y creación automática de guardias.

**Criterios de aceptación**:
- el usuario admin se crea una sola vez,
- la contraseña almacenada no está en texto plano,
- el reinicio del servidor no duplica la cuenta.

**Dependencias**: Issue 2.

**Evidencias o pruebas**:
- consulta de la cuenta inicial,
- comparación de login correcto e incorrecto,
- segundo arranque sin duplicación.

---

### Issue 5 - Implementar inicio y cierre de sesión
**Título y descripción**: Implementar `POST /api/login`, `POST /api/logout` y `GET /api/me`.

**Objetivo y problema que resuelve**: autenticar a administradores y guardias y permitir que la interfaz conozca la sesión actual.

**Alcance**:
- Incluido: comparación con bcrypt, creación/destrucción de sesión y devolución de datos básicos del usuario.
- Excluido: OAuth, Google, SSO y recuperación de contraseña.

**Criterios de aceptación**:
- credenciales válidas crean una sesión,
- credenciales inválidas responden con error 401,
- logout destruye la sesión,
- `/api/me` devuelve el usuario autenticado.

**Dependencias**: Issue 4.

**Evidencias o pruebas**:
- pruebas HTTP de login válido e inválido,
- consulta de `/api/me` antes y después del logout,
- verificación de contraseña hasheada.

---

### Issue 6 - Aplicar límite de intentos de login
**Título y descripción**: Configurar el límite de 30 intentos de autenticación en una ventana de 15 minutos.

**Objetivo y problema que resuelve**: reducir intentos automatizados de acceso sobre `/api/login`.

**Alcance**:
- Incluido: `express-rate-limit` aplicado al endpoint de login y respuesta de bloqueo.
- Excluido: captcha, autenticación multifactor y bloqueo permanente de cuentas.

**Criterios de aceptación**:
- los primeros 30 intentos permitidos procesan normalmente,
- los intentos posteriores dentro de la ventana responden con error,
- el límite se aplica al login y no bloquea las consultas operativas normales.

**Dependencias**: Issue 5.

**Evidencias o pruebas**:
- prueba automatizada o manual de múltiples intentos,
- respuesta del límite alcanzado,
- verificación de acceso posterior a la ventana.

---

### Issue 7 - Proteger rutas autenticadas y administrativas
**Título y descripción**: Aplicar `requiereAuth` y `requiereAdmin` a las rutas del sistema.

**Objetivo y problema que resuelve**: impedir que usuarios sin sesión o guardias ejecuten operaciones administrativas.

**Alcance**:
- Incluido: protección de rutas `/api/mis-servicios`, `/api/guardias` y `/api/admin/*`.
- Excluido: permisos por botón, nuevos roles y SSO.

**Criterios de aceptación**:
- una petición sin sesión recibe 401,
- una sesión de guardia en `/api/admin/*` recibe 403,
- una sesión admin puede acceder a sus endpoints.

**Dependencias**: Issue 5.

**Evidencias o pruebas**:
- pruebas con cookie ausente,
- pruebas con sesión de guardia,
- pruebas con sesión de administrador.

---

### Issue 8 - Implementar la pantalla de login
**Título y descripción**: Conectar `public/login.html` y `public/js/login.js` con `POST /api/login`.

**Objetivo y problema que resuelve**: permitir que ambos perfiles ingresen desde el navegador sin usar llamadas manuales a la API.

**Alcance**:
- Incluido: campos de usuario y contraseña, envío del formulario, redirección por rol y mensaje de error.
- Excluido: registro público y recuperación de contraseña.

**Criterios de aceptación**:
- el login válido redirige al panel correspondiente,
- el login inválido muestra el error del servidor,
- los campos obligatorios se validan antes de enviar.

**Dependencias**: Issue 5, Issue 7.

**Evidencias o pruebas**:
- captura del formulario,
- prueba de redirección admin/guardia,
- prueba visual de credenciales inválidas.

---

### Issue 9 - Implementar CRUD de usuarios del administrador
**Título y descripción**: Conectar el panel con `GET/POST/PUT/DELETE /api/admin/usuarios`.

**Objetivo y problema que resuelve**: permitir que el administrador mantenga actualizado el personal que puede operar en el sistema.

**Alcance**:
- Incluido: listado, creación, edición, eliminación, validación de username y hash de contraseña.
- Excluido: sueldos, legajos, licencias e importación masiva.

**Criterios de aceptación**:
- el administrador puede crear, editar y eliminar un usuario,
- un username duplicado responde 409,
- un admin no puede eliminarse a sí mismo,
- la contraseña nueva se guarda hasheada.

**Dependencias**: Issue 7.

**Evidencias o pruebas**:
- capturas de alta, edición y baja,
- prueba de duplicado,
- consulta de persistencia en `usuarios`.

---

### Issue 10 - Implementar bloqueos de días por guardia
**Título y descripción**: Conectar `PUT /api/admin/usuarios/:id/bloqueos` para guardar días en los que un guardia no puede ser asignado.

**Objetivo y problema que resuelve**: registrar restricciones operativas individuales antes de crear o modificar horarios.

**Alcance**:
- Incluido: edición de bloqueos, serialización en el campo `bloqueos` y visualización en el panel.
- Excluido: licencias laborales, cálculo de vacaciones y notificaciones externas.

**Criterios de aceptación**:
- el administrador puede marcar y desmarcar días,
- los bloqueos sobreviven al reinicio,
- la API devuelve el estado actualizado.

**Dependencias**: Issue 9.

**Evidencias o pruebas**:
- captura del formulario de bloqueos,
- consulta antes y después del reinicio,
- prueba de guardado y lectura del JSON.

---

### Issue 11 - Implementar CRUD de servicios con coordenadas
**Título y descripción**: Conectar el panel con `GET/POST/PUT/DELETE /api/admin/locales` para administrar servicios o locales.

**Objetivo y problema que resuelve**: permitir definir los lugares donde se controlará la presencia de los guardias.

**Alcance**:
- Incluido: nombre único, latitud, longitud, edición, eliminación y listado de servicios.
- Excluido: mapas externos, geocodificación automática y seguimiento en vivo.

**Criterios de aceptación**:
- el administrador puede crear, modificar y eliminar un servicio,
- el nombre duplicado se rechaza,
- latitud y longitud quedan guardadas,
- un servicio eliminado no deja horarios huérfanos.

**Dependencias**: Issue 3, Issue 7.

**Evidencias o pruebas**:
- prueba CRUD completa,
- consulta de coordenadas guardadas,
- comprobación de eliminación de relaciones por cascada.

---

### Issue 12 - Implementar horarios por servicio
**Título y descripción**: Conectar la creación, edición, eliminación y consulta de horarios asociados a cada local.

**Objetivo y problema que resuelve**: definir cuándo puede registrarse un turno y qué guardias están asociados a cada servicio.

**Alcance**:
- Incluido: `GET/POST/PUT/DELETE` de horarios, hora inicial/final y rango de días.
- Excluido: planificación automática y sincronización con calendarios externos.

**Criterios de aceptación**:
- un horario queda asociado al servicio elegido,
- se pueden editar horas y días,
- se puede eliminar un horario,
- la consulta devuelve solo horarios del servicio indicado.

**Dependencias**: Issue 11.

**Evidencias o pruebas**:
- captura del formulario de horario,
- pruebas de alta, edición y baja,
- consulta del endpoint por servicio.

---

### Issue 13 - Asignar guardias a horarios
**Título y descripción**: Permitir asociar un `guardia_id` a cada horario desde el panel administrativo.

**Objetivo y problema que resuelve**: asegurar que el sistema conozca qué persona está habilitada para cubrir cada turno.

**Alcance**:
- Incluido: selector de guardia, asociación horario-usuario y visualización de asignaciones.
- Excluido: asignación automática, optimización de dotación y recursos humanos.

**Criterios de aceptación**:
- el administrador puede asignar un guardia a un horario,
- el guardia ve el servicio en `/api/mis-servicios`,
- la asignación queda persistida,
- un guardia bloqueado no se asigna al día bloqueado.

**Dependencias**: Issue 10, Issue 12.

**Evidencias o pruebas**:
- captura de la asignación,
- consulta de `guardia_id`,
- comprobación del servicio visible para el guardia.

---

### Issue 14 - Mostrar servicios asignados al guardia
**Título y descripción**: Conectar la pantalla del guardia con `GET /api/mis-servicios` y `GET /api/servicio/:nombre/horarios`.

**Objetivo y problema que resuelve**: mostrar al usuario únicamente los servicios y turnos que puede seleccionar.

**Alcance**:
- Incluido: carga de servicios asignados, consulta de horarios del servicio y selección del turno.
- Excluido: visualización de servicios de otros guardias y asignación desde el perfil guardia.

**Criterios de aceptación**:
- la lista muestra los servicios asignados al usuario autenticado,
- al elegir un servicio se cargan sus horarios,
- un guardia sin asignaciones recibe una lista vacía clara.

**Dependencias**: Issue 13.

**Evidencias o pruebas**:
- captura de la pantalla con servicios,
- prueba con guardia asignado,
- prueba con guardia sin asignaciones.

---

### Issue 15 - Obtener y enviar la geolocalización actual
**Título y descripción**: Usar `navigator.geolocation` en `public/js/app.js` para enviar latitud y longitud al registrar el turno.

**Objetivo y problema que resuelve**: aportar la ubicación real del dispositivo para validar la presencia en el servicio.

**Alcance**:
- Incluido: solicitud de permiso, lectura de coordenadas, manejo de error y envío al endpoint de guardias.
- Excluido: mapa, rastreo continuo, historial de recorridos y geofencing avanzado.

**Criterios de aceptación**:
- el navegador solicita permiso,
- la app obtiene latitud y longitud cuando el permiso es concedido,
- se informa claramente si el permiso es denegado,
- las coordenadas se envían junto con el servicio y horario.

**Dependencias**: Issue 11, Issue 14.

**Evidencias o pruebas**:
- captura del permiso,
- prueba con ubicación válida,
- prueba con permiso denegado.

---

### Issue 16 - Validar distancia máxima del servicio
**Título y descripción**: Aplicar el cálculo de distancia entre la posición del guardia y las coordenadas del local, rechazando distancias mayores a 100 metros.

**Objetivo y problema que resuelve**: evitar ingresos registrados desde ubicaciones que no corresponden al servicio seleccionado.

**Alcance**:
- Incluido: función `calcularDistanciaMetros`, comparación con 100 m y respuesta de rechazo con distancia informada.
- Excluido: radio configurable por usuario, seguimiento en vivo y mapas.

**Criterios de aceptación**:
- una ubicación dentro del radio puede continuar,
- una ubicación mayor a 100 m recibe 403,
- el mensaje incluye la distancia aproximada,
- no se crea registro cuando la validación falla.

**Dependencias**: Issue 15.

**Evidencias o pruebas**:
- prueba con coordenadas dentro del radio,
- prueba con coordenadas fuera del radio,
- consulta de registros para confirmar que no se guardó el rechazo.

---

### Issue 17 - Validar horario, capacidad y selección del turno
**Título y descripción**: Validar en `POST /api/guardias` que el horario elegido corresponda al día, no esté completo y no comience más de 90 minutos después del intento.

**Objetivo y problema que resuelve**: impedir ingresos en turnos inválidos, llenos o demasiado alejados de su horario.

**Alcance**:
- Incluido: horario del día, `horario_id`, capacidad de guardias y tolerancia de 90 minutos.
- Excluido: sanciones por tardanza, liquidación de horas y planificación automática.

**Criterios de aceptación**:
- un horario inexistente para el día se rechaza,
- un horario completo se rechaza,
- un ingreso con más de 90 minutos de anticipación se rechaza,
- un horario válido puede continuar hacia el registro.

**Dependencias**: Issue 12, Issue 14.

**Evidencias o pruebas**:
- pruebas de turno válido, inválido y completo,
- prueba de anticipación mayor a 90 minutos,
- respuestas de error documentadas.

---

### Issue 18 - Registrar el ingreso del guardia
**Título y descripción**: Crear el registro de ingreso mediante `guardarRegistro` con usuario, servicio, horario, coordenadas, foto opcional y estado horario.

**Objetivo y problema que resuelve**: dejar evidencia persistente de que un guardia inició un turno bajo las validaciones definidas.

**Alcance**:
- Incluido: inserción del registro tipo `ingreso`, timestamp, horario seleccionado, coordenadas y diferencia horaria.
- Excluido: edición directa por el guardia y cierre automático del turno.

**Criterios de aceptación**:
- el ingreso válido responde con un id,
- la fila guarda usuario, servicio, hora y horario,
- el registro comienza sin `egreso_timestamp`,
- la interfaz informa que el ingreso fue registrado.

**Dependencias**: Issue 16, Issue 17.

**Evidencias o pruebas**:
- prueba de ingreso exitoso,
- consulta de la fila creada,
- captura del mensaje de confirmación.

---

### Issue 19 - Impedir dos servicios activos
**Título y descripción**: Aplicar `tieneServicioActivo` y `tieneServicioActivoPorNombreDni` antes de aceptar un nuevo ingreso.

**Objetivo y problema que resuelve**: evitar que un guardia figure simultáneamente en dos servicios sin haber cerrado el primero.

**Alcance**:
- Incluido: búsqueda de registros sin egreso y rechazo del segundo ingreso.
- Excluido: reasignación automática y cierre administrativo en esta validación.

**Criterios de aceptación**:
- un guardia con registro activo recibe error 400,
- el mensaje informa el servicio activo,
- no se inserta un segundo registro abierto.

**Dependencias**: Issue 18.

**Evidencias o pruebas**:
- dos intentos consecutivos de ingreso,
- respuesta del segundo intento,
- conteo de registros abiertos antes y después.

---

### Issue 20 - Registrar el egreso del guardia
**Título y descripción**: Completar el registro activo con `completarRegistro` al recibir un egreso válido.

**Objetivo y problema que resuelve**: cerrar el turno y guardar la hora y ubicación de salida para completar la trazabilidad.

**Alcance**:
- Incluido: búsqueda del activo, timestamp de egreso, coordenadas, foto opcional y diferencia frente al horario final.
- Excluido: egreso sin autenticación y cierre de servicios ajenos al usuario.

**Criterios de aceptación**:
- un guardia con servicio activo puede registrar egreso,
- un guardia sin servicio activo recibe error 400,
- `egreso_timestamp` queda guardado,
- el registro deja de aparecer como activo.

**Dependencias**: Issue 18, Issue 19.

**Evidencias o pruebas**:
- prueba de egreso válido,
- prueba sin servicio activo,
- consulta del registro antes y después del egreso.

---

### Issue 21 - Mostrar servicios activos y registros al administrador
**Título y descripción**: Conectar el panel con `GET /api/admin/activos`, `GET /api/admin/registros` y `GET /api/admin/registros/:id`.

**Objetivo y problema que resuelve**: permitir supervisar quién está trabajando, qué turnos ya terminaron y qué datos tiene cada registro.

**Alcance**:
- Incluido: listado de activos, historial, detalle por registro y búsqueda visual básica.
- Excluido: exportación a Excel/PDF y analítica avanzada.

**Criterios de aceptación**:
- el admin visualiza los servicios sin egreso,
- el historial muestra guardia, servicio, ingreso y egreso,
- el detalle permite revisar un registro específico,
- un guardia no puede consultar estos endpoints.

**Dependencias**: Issue 20, Issue 7.

**Evidencias o pruebas**:
- captura de activos e historial,
- prueba de detalle,
- prueba de acceso con rol guardia.

---

### Issue 22 - Completar o eliminar registros desde administración
**Título y descripción**: Implementar las acciones administrativas `POST /api/admin/registros/:id/completar` y `POST /api/admin/registros/delete`.

**Objetivo y problema que resuelve**: corregir registros operativos incompletos o eliminar datos seleccionados cuando el administrador lo justifica.

**Alcance**:
- Incluido: completar un registro, eliminar registros seleccionados y actualizar el listado.
- Excluido: auditoría avanzada de quién borró, recuperación de eliminados y edición libre de timestamps.

**Criterios de aceptación**:
- el admin puede completar un registro pendiente,
- puede eliminar solo los ids seleccionados,
- el historial se actualiza después de cada operación,
- un guardia no puede ejecutar estas acciones.

**Dependencias**: Issue 21.

**Evidencias o pruebas**:
- prueba de completar registro,
- prueba de eliminación seleccionada,
- consulta antes y después de cada acción.

---

### Issue 23 - Implementar notificaciones pendientes
**Título y descripción**: Conectar `GET /api/notificaciones` y `POST /api/notificaciones/leidas` para mostrar y marcar avisos del guardia.

**Objetivo y problema que resuelve**: informar cambios operativos al usuario dentro de la aplicación y evitar que los avisos pendientes se pierdan.

**Alcance**:
- Incluido: consulta de hasta 50 notificaciones pendientes y marcado por usuario autenticado.
- Excluido: SMS, correo, push móvil y notificaciones de terceros.

**Criterios de aceptación**:
- el guardia ve solo sus notificaciones no leídas,
- puede marcarlas como leídas,
- una notificación leída no vuelve a aparecer como pendiente.

**Dependencias**: Issue 5, Issue 14.

**Evidencias o pruebas**:
- creación de una notificación de prueba,
- captura de la bandeja,
- consulta antes y después de marcar como leída.

---

### Issue 24 - Visualizar calendario mensual y valores del servicio
**Título y descripción**: Conectar el panel con `GET /api/admin/calendario/:servicioId` y la actualización de valores mensuales del servicio.

**Objetivo y problema que resuelve**: consultar los registros agrupados por mes y mantener los valores básicos asociados a cada servicio para la supervisión administrativa.

**Alcance**:
- Incluido: selector de servicio y mes, registros del período, valores de horas de sueldo/servicio y actualización administrativa.
- Excluido: liquidación de sueldos, pagos, reportes externos y dashboard predictivo.

**Criterios de aceptación**:
- el admin puede seleccionar un servicio y mes,
- el calendario muestra ingresos y egresos del período,
- los valores mensuales se guardan y vuelven a cargarse,
- la información corresponde al servicio elegido.

**Dependencias**: Issue 21.

**Evidencias o pruebas**:
- captura del calendario mensual,
- prueba con dos meses distintos,
- comprobación de persistencia de valores.

---

## 3.3 Validación final de las issues

La issue final de cada bloque debe presentar evidencias verificables en el repositorio: capturas de las pantallas, respuestas de los endpoints, consultas de persistencia y resultados de los casos válidos e inválidos. La aceptación general del Paso 3 se alcanza cuando las 24 issues están documentadas, cada una tiene sus dependencias identificadas y el flujo completo de autenticación, asignación, ingreso, egreso y supervisión puede probarse sin salir del alcance del sistema.
