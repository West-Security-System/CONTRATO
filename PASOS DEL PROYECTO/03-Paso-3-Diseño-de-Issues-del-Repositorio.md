# Paso 3 - Issues de los repositorios Frontend y Backend

## 3.1 Objetivo y organización

El proyecto se divide en dos repositorios de GitHub:

- `west-security-frontend`: interfaz web para administradores y guardias.
- `west-security-backend`: API, autenticación, reglas operativas y persistencia.

Se definen 14 issues para el repositorio frontend y se mantienen las 26 issues originales del repositorio backend. La numeración es independiente: cada issue frontend indica qué issues backend debe consumir o integrar. Una issue se cierra únicamente cuando su parte está implementada, probada y conectada con la issue complementaria.

El backend es la fuente de verdad para permisos, estados, fechas, distancia y persistencia. El frontend presenta estados y errores recibidos de la API; no reemplaza las validaciones del servidor. Todo endpoint debe documentar método, ruta, autenticación, payload, respuesta y errores.

## 3.2 Issues del repositorio `west-security-frontend`

Cada issue incluye objetivo, trabajo, aceptación, dependencias y evidencia. La issue backend del mismo número define el contrato que debe consumirse.

### Frontend Issue 1 - Inicializar la aplicación y el cliente HTTP
**Objetivo**: crear una base ejecutable y centralizar la comunicación con la API.

**Trabajo**: configurar HTML/CSS/JavaScript, scripts, carpetas, variables de entorno, URL única de API, `fetch`, cookies, JSON, timeout y manejo de errores 401/403/404/409/422/500 y de red.

**Criterios de aceptación**:
- inicia con un comando documentado,
- no duplica la URL ni el manejo de errores,
- separa vistas públicas y protegidas,
- convierte las respuestas en mensajes utilizables.

**Dependencias**: ninguna.

**Backend relacionado**: #1, #2 y #3.

**Evidencia**: ejecución local y pruebas de éxito, error y red.

### Frontend Issue 2 - Crear el sistema visual y la accesibilidad base
**Objetivo**: unificar la experiencia y hacer recuperables todos los flujos.

**Trabajo**: estilos globales, tipografía, colores, espaciado, botones, formularios, tablas, alertas, carga, error, responsive, labels, foco, teclado, confirmaciones y feedback no basado solo en color.

**Criterios de aceptación**:
- controles consistentes y con nombre accesible,
- foco visible y navegación por teclado,
- estados vacío, carga y error con una acción siguiente,
- funciona sin desbordamiento en móvil.

**Dependencias**: #1.

**Backend relacionado**: #2 y #25.

**Evidencia**: capturas desktop y móvil, checklist y pruebas de errores.

### Frontend Issue 3 - Implementar navegación, autenticación y sesión
**Objetivo**: separar y proteger los flujos de administrador y guardia.

**Trabajo**: rutas, redirección por rol, ruta inexistente, protección ante recarga, formulario de login con validación, estado de envío, `POST /api/login`, `GET /api/me`, `POST /api/logout`, limpieza y redirección.

**Criterios de aceptación**:
- sin sesión vuelve al login,
- no envía campos vacíos ni permite doble envío,
- redirige por rol y un guardia no ve admin,
- sesión inválida no muestra contenido y volver atrás no recupera acceso,
- presenta errores sin filtrar datos ni secretos.

**Dependencias**: #1.

**Backend relacionado**: #4, #5 y #6.

**Evidencia**: login admin, guardia e inválido, redirecciones y logout.

### Frontend Issue 4 - Crear el layout administrativo
**Objetivo**: dar una estructura común al panel de administración.

**Trabajo**: encabezado, menú, sección activa, usuario, carga, alertas y responsive.

**Criterios de aceptación**:
- todas las vistas comparten layout,
- las acciones admin no aparecen para guardias,
- funciona correctamente en escritorio y móvil.

**Dependencias**: #3.

**Backend relacionado**: #7.

**Evidencia**: capturas de escritorio y móvil.

### Frontend Issue 5 - Gestionar usuarios y bloqueos de guardias
**Objetivo**: administrar el personal y sus días no disponibles.

**Trabajo**: tabla, alta, edición, baja, roles, validación, confirmación, error de username duplicado y carga, marcado, desmarcado, guardado, cancelación y confirmación de bloqueos.

**Criterios de aceptación**:
- el admin completa el CRUD y distingue roles,
- no puede eliminarse a sí mismo,
- los bloqueos persisten al recargar,
- los errores no dejan datos falsos.

**Dependencias**: #1 y #4.

**Backend relacionado**: #8 y #9.

**Evidencia**: alta, edición, error, baja, marcado, guardado, recarga y eliminación.

### Frontend Issue 6 - Gestionar servicios, coordenadas y horarios
**Objetivo**: configurar visualmente los lugares y turnos operativos.

**Trabajo**: CRUD de nombre, latitud y longitud, validación, confirmación, estados vacío/error, selector de servicio, días, hora inicial/final, capacidad y CRUD de horarios.

**Criterios de aceptación**:
- el admin crea, edita y elimina servicios y horarios,
- se muestran coordenadas,
- se informa duplicado o valor inválido,
- solo muestra horarios del servicio seleccionado,
- exige hora final posterior y evita duplicados visuales.

**Dependencias**: #1 y #4.

**Backend relacionado**: #10 y #11.

**Evidencia**: CRUD completo, alta, edición, rango inválido y baja.

### Frontend Issue 7 - Asignar guardias y mostrar el dashboard operativo
**Objetivo**: vincular personal con turnos y resumir la operación.

**Trabajo**: selector, asignación, desasignación, mensajes de bloqueo/conflicto, activos, registros recientes, alertas, enlaces, refresco y estados vacío/error.

**Criterios de aceptación**:
- lista solo guardias,
- refleja cambios al recargar y muestra rechazos del servidor,
- identifica guardia, servicio, fecha y estado,
- no muestra datos mientras cargan.

**Dependencias**: #5 y #6.

**Backend relacionado**: #12 y #13.

**Evidencia**: asignación válida, conflictos, dashboard con datos, sin datos y con error.

### Frontend Issue 8 - Preparar servicios asignados y geolocalización
**Objetivo**: permitir al guardia elegir un turno propio y obtener su ubicación real.

**Trabajo**: `GET /api/mis-servicios`, horarios, selector, estado sin asignaciones, permiso de geolocalización, coordenadas, precisión, espera, denegación y error de compatibilidad.

**Criterios de aceptación**:
- no muestra asignaciones ajenas,
- actualiza horarios y no permite continuar sin turno,
- no inventa coordenadas ni permite doble envío,
- explica cómo resolver el permiso.

**Dependencias**: #3 y #7.

**Backend relacionado**: #14 y #15.

**Evidencia**: guardia asignado y no asignado, permiso concedido, denegado y error.

### Frontend Issue 9 - Gestionar ingreso, turno activo y egreso
**Objetivo**: completar el ciclo operativo del guardia.

**Trabajo**: resumen de servicio/horario, ubicación, `POST /api/guardias`, carga, éxito, errores de radio/turno, consulta de activo, panel, deshabilitación, sincronización, confirmación de egreso, envío y error sin activo.

**Criterios de aceptación**:
- exige selección y ubicación, y conserva datos ante rechazo,
- muestra hora y servicio aceptados,
- muestra el turno activo, oculta el nuevo ingreso y maneja el 409 sin estado falso,
- el egreso aparece solo con activo, muestra la hora recibida y lo quita al cerrar.

**Dependencias**: #8.

**Backend relacionado**: #16, #17 y #18.

**Evidencia**: ingreso válido, fuera de 100 m e inválido, activo, recarga, segundo intento, egreso válido y sin turno.

### Frontend Issue 10 - Crear historial y notificaciones del guardia
**Objetivo**: mostrar la actividad propia y sus avisos internos.

**Trabajo**: `GET /api/mis-registros`, servicio, ingreso, egreso, estado, límite, vacío, contador de notificaciones, lista, fecha, leído/no leído y `POST /api/notificaciones/leidas`.

**Criterios de aceptación**:
- nunca muestra otro usuario,
- diferencia registros abiertos y cerrados,
- el contador coincide y marcar leído actualiza la lista,
- solo muestra avisos propios.

**Dependencias**: #3 y #9.

**Backend relacionado**: #19 y #20.

**Evidencia**: historial activo, cerrado y vacío; notificaciones pendientes, leídas y vacías.

### Frontend Issue 11 - Supervisar y corregir registros desde administración
**Objetivo**: consultar activos e historial y ejecutar correcciones administrativas.

**Trabajo**: tablas, detalle, filtros por guardia/servicio/estado/período, orden temporal, selección múltiple, confirmaciones, completar, borrar, refresco y mensajes.

**Criterios de aceptación**:
- los filtros no mezclan consultas y distinguen activo de cerrado,
- muestra estados vacíos y errores 404,
- no permite acciones sin selección,
- refleja el resultado real del servidor.

**Dependencias**: #4 y #7.

**Backend relacionado**: #21 y #22.

**Evidencia**: filtros, detalle, 404, acción exitosa y rechazada.

### Frontend Issue 12 - Crear calendario mensual
**Objetivo**: visualizar registros por servicio y mes.

**Trabajo**: selectores, tabla/calendario, detalle diario y estados sin actividad.

**Criterios de aceptación**:
- cambiar el mes consulta de nuevo,
- diferencia ingreso y egreso,
- no mezcla datos antiguos durante la carga.

**Dependencias**: #11.

**Backend relacionado**: #23.

**Evidencia**: dos meses y período vacío.

### Frontend Issue 13 - Editar valores mensuales del servicio
**Objetivo**: editar valores operativos sin convertirlos en liquidación.

**Trabajo**: lectura, campos numéricos, guardar, cancelar, validación y recarga.

**Criterios de aceptación**:
- persiste valores válidos,
- rechaza formato inválido,
- aclara el alcance de la funcionalidad.

**Dependencias**: #12.

**Backend relacionado**: #24.

**Evidencia**: lectura, edición y persistencia.

### Frontend Issue 14 - Integrar, probar y documentar el cliente
**Objetivo**: cerrar el frontend contra la API real con un flujo reproducible.

**Trabajo**: pruebas de login, CRUD, asignación, radio de 100 m, segundo activo, egreso, historial y administración; validación de contratos, README y despliegue.

**Criterios de aceptación**:
- los comandos son reproducibles,
- el contrato coincide con la API,
- el flujo completo funciona con los estados de éxito, error, carga y vacío.

**Dependencias**: #1 a #13.

**Backend relacionado**: #1 a #26.

**Evidencia**: reporte, capturas y README.



## 3.3 Issues del repositorio `west-security-backend`

### Backend Issue 1 - Inicializar servidor y configuración
**Objetivo**: crear API ejecutable.

**Trabajo**: servidor, scripts, puerto, origen permitido, estructura por responsabilidades y `GET /api/health`.

**Criterios de aceptación**:
- inicia documentadamente,
- salud responde estado y versión,
- secretos vienen de entorno.

**Dependencias**: ninguna.

**Frontend relacionado**: #1.

**Evidencia**: arranque y respuesta.

### Backend Issue 2 - Definir contrato de respuestas y errores
**Objetivo**: hacer predecible la API.

**Trabajo**: formato JSON común, middleware, validación y códigos 400/401/403/404/409/422/500.

**Criterios de aceptación**:
- errores sin stack trace productivo,
- campos inválidos identificables.

**Dependencias**: #1.

**Frontend relacionado**: #1 y #2.

**Evidencia**: colección de casos.

### Backend Issue 3 - Implementar SQLite y migraciones
**Objetivo**: persistir sin perder datos.

**Trabajo**: crear/cargar `west_control.db`, carpeta data, esquema idempotente y claves foráneas.

**Criterios de aceptación**:
- base nueva y existente arrancan,
- migrar dos veces no duplica,
- error de persistencia detiene explícitamente.

**Dependencias**: #1.

**Frontend relacionado**: #1.

**Evidencia**: dos arranques y esquema.

### Backend Issue 4 - Crear usuarios y roles
**Objetivo**: almacenar admin/guardia con integridad.

**Trabajo**: tabla `usuarios`, username único, campos obligatorios, roles restringidos, hash, bloqueos y timestamps.

**Criterios de aceptación**:
- duplicados y roles inválidos se rechazan,
- nunca se guarda password plano.

**Dependencias**: #3.

**Frontend relacionado**: #3.

**Evidencia**: inserciones y rechazos.

### Backend Issue 5 - Implementar login, sesión y token
**Objetivo**: verificar credenciales y crear acceso seguro.

**Trabajo**: `POST /api/login`, bcrypt, cookie HttpOnly con sesión/token, expiración y respuesta mínima.

**Criterios de aceptación**:
- válido crea sesión,
- inválido responde 401 sin revelar usuarios,
- cookie usa SameSite adecuado.

**Dependencias**: #2 y #4.

**Frontend relacionado**: #3.

**Evidencia**: ambos roles y error.

### Backend Issue 6 - Implementar logout y usuario actual
**Objetivo**: invalidar acceso y consultar identidad.

**Trabajo**: `POST /api/logout`, `GET /api/me`, invalidación y 401 sin sesión.

**Criterios de aceptación**:
- logout es inmediato e idempotente,
- nunca devuelve hashes.

**Dependencias**: #5.

**Frontend relacionado**: #3.

**Evidencia**: antes y después del logout.

### Backend Issue 7 - Proteger rutas por rol
**Objetivo**: impedir accesos indebidos.

**Trabajo**: `requiereAuth`, `requiereAdmin`, rutas, 401/403 y CORS restringido.

**Criterios de aceptación**:
- sin sesión responde 401,
- guardia en admin responde 403,
- admin autorizado puede acceder.

**Dependencias**: #6.

**Frontend relacionado**: #4.

**Evidencia**: matriz de permisos.

### Backend Issue 8 - CRUD administrativo de usuarios
**Objetivo**: exponer gestión de personal.

**Trabajo**: `GET/POST/PUT/DELETE /api/admin/usuarios`, validación, hash, ocultamiento de secretos y autoeliminación prohibida.

**Criterios de aceptación**:
- CRUD admin completo,
- duplicado responde 409,
- guardia no tiene permisos.

**Dependencias**: #4 y #7.

**Frontend relacionado**: #5.

**Evidencia**: pruebas CRUD.

### Backend Issue 9 - Persistir bloqueos de guardias
**Objetivo**: guardar días no disponibles.

**Trabajo**: `PUT /api/admin/usuarios/:id/bloqueos`, formato, validación, lectura y conflicto de asignación.

**Criterios de aceptación**:
- persiste,
- un valor inválido responde 422,
- una asignación incompatible se rechaza.

**Dependencias**: #8.

**Frontend relacionado**: #5.

**Evidencia**: escritura, lectura y conflicto.

### Backend Issue 10 - CRUD de servicios y coordenadas
**Objetivo**: proveer el contrato de la pantalla de servicios.

**Trabajo**: `GET/POST/PUT/DELETE /api/admin/locales`, nombre único, latitud/longitud y relaciones.

**Criterios de aceptación**:
- CRUD admin,
- duplicado responde 409,
- coordenadas fuera de rango responden 422,
- política de huérfanos definida.

**Dependencias**: #3 y #7.

**Frontend relacionado**: #6.

**Evidencia**: CRUD y eliminación relacionada.

### Backend Issue 11 - CRUD de horarios
**Objetivo**: administrar turnos consistentes.

**Trabajo**: endpoints, días, horas, capacidad y servicio asociado.

**Criterios de aceptación**:
- exige servicio existente,
- hora final posterior,
- respeta permisos admin,
- consulta filtrada por servicio.

**Dependencias**: #10.

**Frontend relacionado**: #6.

**Evidencia**: válidos e inválidos.

### Backend Issue 12 - Asignar guardias a horarios
**Objetivo**: vincular persona y turno.

**Trabajo**: asignar/desasignar, validar rol, bloqueos, duplicidad y disponibilidad.

**Criterios de aceptación**:
- solo acepta guardias válidos,
- bloqueo 409/422 documentado,
- persiste la asignación,
- la consulta personal la devuelve.

**Dependencias**: #9 y #11.

**Frontend relacionado**: #7.

**Evidencia**: asignación, bloqueo y lectura.

### Backend Issue 13 - Exponer resumen operativo admin
**Objetivo**: entregar datos del dashboard.

**Trabajo**: activos, recientes, filtros y límites en `GET /api/admin/activos` y `/api/admin/registros`.

**Criterios de aceptación**:
- solo admin accede,
- activos son registros sin egreso,
- fechas consistentes,
- respuestas limitadas.

**Dependencias**: #7 y #12.

**Frontend relacionado**: #7.

**Evidencia**: con/sin actividad y filtros.

### Backend Issue 14 - Exponer servicios del guardia
**Objetivo**: devolver únicamente asignaciones propias.

**Trabajo**: `GET /api/mis-servicios` y `GET /api/servicio/:nombre/horarios`, autorización y ids estables.

**Criterios de aceptación**:
- no revela asignaciones ajenas,
- sin asignaciones devuelve lista vacía,
- servicio no asignado no devuelve horarios.

**Dependencias**: #12.

**Frontend relacionado**: #8.

**Evidencia**: dos usuarios aislados.

### Backend Issue 15 - Validar coordenadas
**Objetivo**: aceptar ubicación válida y segura.

**Trabajo**: tipos, latitud [-90,90], longitud [-180,180], ausencia, precisión y payload inválido.

**Criterios de aceptación**:
- los inválidos responden 422,
- no se procesa ingreso/egreso sin ubicación.

**Dependencias**: #14.

**Frontend relacionado**: #8.

**Evidencia**: válidas, ausentes y fuera de rango.

### Backend Issue 16 - Registrar ingreso y radio de 100 metros
**Objetivo**: aceptar ingreso solo en el servicio correcto.

**Trabajo**: `POST /api/guardias`, distancia, límite 100 m, usuario, servicio, horario, timestamp y coordenadas.

**Criterios de aceptación**:
- dentro de 100 m continúa,
- mayor a 100 m responde 403 sin insertar,
- el registro aceptado queda abierto.

**Dependencias**: #11, #14 y #15.

**Frontend relacionado**: #9.

**Evidencia**: límite, dentro y fuera.

### Backend Issue 17 - Validar turno y evitar segundo servicio activo
**Objetivo**: impedir turnos inválidos o simultáneos.

**Trabajo**: día, horario, capacidad, anticipación máxima de 90 minutos, búsqueda sin egreso y transacción.

**Criterios de aceptación**:
- inválido, completo o anticipado se rechaza,
- activo devuelve 409 con servicio,
- peticiones simultáneas no duplican.

**Dependencias**: #16.

**Frontend relacionado**: #9.

**Evidencia**: casos inválidos y doble petición.

### Backend Issue 18 - Registrar egreso
**Objetivo**: cerrar el registro activo.

**Trabajo**: `POST /api/guardias/:id/egreso`, propietario, coordenadas, timestamp y transición cerrada.

**Criterios de aceptación**:
- solo dueño o admin autorizado,
- sin activo responde error,
- la misma fila recibe egreso,
- repetirlo no modifica silenciosamente.

**Dependencias**: #15 y #17.

**Frontend relacionado**: #9.

**Evidencia**: válido, ajeno y ausente.

### Backend Issue 19 - Exponer historial propio
**Objetivo**: entregar trazabilidad al guardia.

**Trabajo**: `GET /api/mis-registros`, orden, límite/paginación y aislamiento por usuario.

**Criterios de aceptación**:
- incluye abiertos y cerrados,
- nunca mezcla usuarios,
- vacío devuelve colección 200.

**Dependencias**: #18.

**Frontend relacionado**: #10.

**Evidencia**: dos usuarios y vacío.

### Backend Issue 20 - Implementar notificaciones pendientes
**Objetivo**: proveer avisos internos.

**Trabajo**: estructura, `GET /api/notificaciones`, `POST /api/notificaciones/leidas`, aislamiento y marcado idempotente.

**Criterios de aceptación**:
- solo devuelve notificaciones propias,
- repetir el marcado es seguro,
- el límite está documentado.

**Dependencias**: #5 y #14.

**Frontend relacionado**: #10.

**Evidencia**: pendientes, leído y aislamiento.

### Backend Issue 21 - Consultas admin de registros y detalle
**Objetivo**: proveer supervisión completa.

**Trabajo**: activos, historial, `GET /api/admin/registros/:id`, filtros, límites y datos relacionados.

**Criterios de aceptación**:
- solo admin accede,
- detalle válido,
- id inexistente responde 404,
- filtros seguros.

**Dependencias**: #18.

**Frontend relacionado**: #11.

**Evidencia**: activos, historial y 404.

### Backend Issue 22 - Completar o eliminar registros admin
**Objetivo**: resolver incompletos y borrar seleccionados autorizadamente.

**Trabajo**: completar, borrar ids, transacciones y resultados parciales.

**Criterios de aceptación**:
- solo admin accede,
- el cierre es válido,
- ids inexistentes no borran otros,
- el resultado es explícito.

**Dependencias**: #21.

**Frontend relacionado**: #11.

**Evidencia**: completar, borrar y permisos.

### Backend Issue 23 - Consulta de calendario mensual
**Objetivo**: agrupar registros por servicio y mes.

**Trabajo**: `GET /api/admin/calendario/:servicioId`, mes/año, validación, zona horaria y orden.

**Criterios de aceptación**:
- solo devuelve el período solicitado,
- mes inválido responde 422,
- cambio de año correcto,
- período vacío devuelve una colección.

**Dependencias**: #21.

**Frontend relacionado**: #12.

**Evidencia**: dos meses y vacío.

### Backend Issue 24 - Persistir valores mensuales
**Objetivo**: guardar valores básicos del servicio sin liquidación.

**Trabajo**: consulta/actualización por servicio y mes, unicidad y validación numérica.

**Criterios de aceptación**:
- admin autorizado,
- inválido responde 422,
- el valor actualizado persiste,
- no se implementan pagos.

**Dependencias**: #23.

**Frontend relacionado**: #13.

**Evidencia**: alta, lectura y actualización.

### Backend Issue 25 - Seguridad y validación transversal
**Objetivo**: endurecer la API.

**Trabajo**: rate limit de login de 30 intentos/15 minutos, headers, sanitización, logs sin secretos, transacciones y payloads validados.

**Criterios de aceptación**:
- intento 31 responde 429,
- no se registran tokens ni passwords,
- los errores mantienen formato común.

**Dependencias**: #2 y #5 a #24.

**Frontend relacionado**: #2.

**Evidencia**: rate limit, logs y matriz de errores.

### Backend Issue 26 - Integración, pruebas y documentación de API
**Objetivo**: cerrar el contrato consumible por frontend.

**Trabajo**: pruebas E2E de login, CRUD, asignación, radio 100 m, segundo activo, egreso, historial, notificaciones y calendario; README, entorno, esquema y endpoints.

**Criterios de aceptación**:
- instalación limpia inicia,
- comandos reproducibles,
- contrato coincide,
- casos válidos y rechazados cubiertos.

**Dependencias**: #1 a #25.

**Frontend relacionado**: #14.

**Evidencia**: reporte, contrato y README.

## 3.4 Orden recomendado

1. Completar issues 1 a 7 en ambos repositorios: base, contrato, sesión y permisos.
2. Completar 8 a 12: usuarios, bloqueos, servicios, horarios y asignaciones.
3. Completar 13 a 20: dashboard, operación del guardia, ingreso, egreso e historial.
4. Completar 21 a 24: supervisión, calendario y valores mensuales.
5. Completar 25 y 26: seguridad, accesibilidad, integración, pruebas y documentación.

## 3.5 Criterio de cierre

El paso queda completo cuando existen los dos repositorios, cada uno tiene sus 26 issues copiadas o vinculadas, y cada par comparte un contrato probado. El flujo final debe cubrir login por rol, asignación, consulta, validación dentro de 100 metros, ingreso, bloqueo de un segundo servicio activo, egreso, historial y supervisión administrativa.