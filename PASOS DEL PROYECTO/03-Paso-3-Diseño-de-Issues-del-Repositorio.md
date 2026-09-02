# Paso 3 - Issues de los repositorios Frontend y Backend

## 3.1 Objetivo y organización

El proyecto se divide en dos repositorios de GitHub:

- `west-security-frontend`: interfaz web para administradores y guardias.
- `west-security-backend`: API, autenticación, reglas operativas y persistencia.

Se definen 26 issues para cada repositorio, 52 en total. El número es compartido: `frontend#N` y `backend#N` forman el mismo entregable coordinado. Una issue se cierra únicamente cuando su parte está implementada, probada y conectada con la issue complementaria.

El backend es la fuente de verdad para permisos, estados, fechas, distancia y persistencia. El frontend presenta estados y errores recibidos de la API; no reemplaza las validaciones del servidor. Todo endpoint debe documentar método, ruta, autenticación, payload, respuesta y errores.

## 3.2 Issues del repositorio `west-security-frontend`

Cada issue incluye objetivo, trabajo, aceptación, dependencias y evidencia. La issue backend del mismo número define el contrato que debe consumirse.

### Frontend Issue 1 - Inicializar la aplicación web
**Objetivo**: crear una base ejecutable y mantenible para el cliente.

**Trabajo**: configurar HTML/CSS/JavaScript, scripts, carpetas, variables de entorno y URL de API.

**Criterios de aceptación**:
- inicia con un comando documentado,
- separa vistas públicas y protegidas,
- no duplica la URL del backend.

**Dependencias**: ninguna.

**Backend relacionado**: #1.

**Evidencia**: ejecución local y captura inicial.

### Frontend Issue 2 - Crear el sistema visual base
**Objetivo**: unificar la experiencia.

**Trabajo**: estilos globales, tipografía, colores, espaciado, botones, formularios, tablas, alertas, carga, error y responsive.

**Criterios de aceptación**:
- controles consistentes,
- foco visible,
- estados vacío, carga y error,
- uso sin desbordamiento en móvil.

**Dependencias**: #1.

**Backend relacionado**: #2.

**Evidencia**: capturas desktop y móvil.

### Frontend Issue 3 - Implementar cliente HTTP común
**Objetivo**: centralizar la comunicación.

**Trabajo**: `fetch`, cookies, JSON, timeout, errores 401/403/404/409/422/500 y error de red.

**Criterios de aceptación**:
- ningún módulo repite URL o manejo de errores,
- las respuestas se convierten a mensajes utilizables.

**Dependencias**: #1.

**Backend relacionado**: #3.

**Evidencia**: pruebas de éxito, error y red.

### Frontend Issue 4 - Crear navegación y protección de vistas
**Objetivo**: separar login, panel guardia y panel admin.

**Trabajo**: rutas, redirección por rol, ruta inexistente y protección ante recarga.

**Criterios de aceptación**:
- sin sesión vuelve al login,
- un guardia no ve admin,
- cada rol llega a su panel.

**Dependencias**: #3.

**Backend relacionado**: #4 y #5.

**Evidencia**: recorrido de redirecciones.

### Frontend Issue 5 - Construir el formulario de login
**Objetivo**: permitir el acceso de ambos perfiles.

**Trabajo**: usuario, contraseña, validación, estado de envío, `POST /api/login`, redirección y error sin filtrar datos.

**Criterios de aceptación**:
- no envía campos vacíos,
- bloquea doble envío,
- redirige por rol,
- presenta credenciales inválidas.

**Dependencias**: #3 y #4.

**Backend relacionado**: #5.

**Evidencia**: login admin, guardia e inválido.

### Frontend Issue 6 - Implementar sesión actual y logout
**Objetivo**: mostrar la identidad y finalizar acceso.

**Trabajo**: `GET /api/me`, menú por rol, `POST /api/logout`, limpieza y redirección.

**Criterios de aceptación**:
- sesión inválida no muestra contenido,
- volver atrás no recupera acceso,
- no se muestran secretos.

**Dependencias**: #5.

**Backend relacionado**: #6.

**Evidencia**: flujo autenticado y posterior al logout.

### Frontend Issue 7 - Crear layout administrativo
**Objetivo**: dar una estructura común al panel admin.

**Trabajo**: encabezado, menú, sección activa, usuario, carga, alertas y responsive.

**Criterios de aceptación**:
- todas las vistas comparten layout,
- las acciones admin no aparecen para guardias.

**Dependencias**: #6.

**Backend relacionado**: #7.

**Evidencia**: capturas de escritorio y móvil.

### Frontend Issue 8 - Gestionar usuarios
**Objetivo**: ofrecer CRUD de personal.

**Trabajo**: tabla, alta, edición, baja, rol, validación, confirmación y error de username duplicado.

**Criterios de aceptación**:
- admin completa CRUD,
- distingue roles,
- no puede eliminarse a sí mismo.

**Dependencias**: #3 y #7.

**Backend relacionado**: #8.

**Evidencia**: alta, edición, error y baja.

### Frontend Issue 9 - Gestionar bloqueos de guardias
**Objetivo**: editar días no disponibles.

**Trabajo**: cargar, marcar, desmarcar, guardar, cancelar y confirmar bloqueos.

**Criterios de aceptación**:
- persisten al recargar,
- los errores no dejan datos falsos.

**Dependencias**: #8.

**Backend relacionado**: #9.

**Evidencia**: marcar, guardar, recargar y quitar.

### Frontend Issue 10 - Diseñar administración de servicios y coordenadas
**Objetivo**: hacer toda la parte gráfica de locales/servicios.

**Trabajo**: CRUD de nombre, latitud y longitud, validación, confirmación y estados vacío/error.

**Criterios de aceptación**:
- admin crea, edita y elimina,
- se muestran coordenadas,
- se informa duplicado o valor inválido.

**Dependencias**: #3 y #7.

**Backend relacionado**: #10.

**Evidencia**: CRUD completo y validaciones.

### Frontend Issue 11 - Gestionar horarios por servicio
**Objetivo**: administrar turnos visualmente.

**Trabajo**: selector de servicio, días, hora inicial/final, capacidad y CRUD.

**Criterios de aceptación**:
- solo muestra horarios del servicio,
- exige hora final posterior,
- evita duplicados visuales.

**Dependencias**: #10.

**Backend relacionado**: #11.

**Evidencia**: alta, edición, rango inválido y baja.

### Frontend Issue 12 - Asignar guardias a horarios
**Objetivo**: vincular personal y turnos.

**Trabajo**: selector, asignación, desasignación y mensajes de bloqueo/conflicto.

**Criterios de aceptación**:
- lista solo guardias,
- refleja el cambio al recargar,
- muestra rechazos del servidor.

**Dependencias**: #9 y #11.

**Backend relacionado**: #12.

**Evidencia**: asignación válida y conflictos.

### Frontend Issue 13 - Crear dashboard operativo admin
**Objetivo**: resumir la operación.

**Trabajo**: activos, registros recientes, alertas, enlaces, refresco y estados vacío/error.

**Criterios de aceptación**:
- identifica guardia, servicio, fecha y estado,
- no muestra datos mientras cargan.

**Dependencias**: #7 y #12.

**Backend relacionado**: #13.

**Evidencia**: con datos, sin datos y error.

### Frontend Issue 14 - Mostrar servicios asignados al guardia
**Objetivo**: permitir seleccionar un turno propio.

**Trabajo**: `GET /api/mis-servicios`, horarios, selector y estado sin asignaciones.

**Criterios de aceptación**:
- no muestra asignaciones ajenas,
- actualiza horarios,
- no permite continuar sin turno.

**Dependencias**: #6 y #12.

**Backend relacionado**: #14.

**Evidencia**: guardia asignado y no asignado.

### Frontend Issue 15 - Integrar geolocalización del navegador
**Objetivo**: obtener ubicación real antes de operar.

**Trabajo**: permiso, coordenadas, precisión, espera, denegación y error de compatibilidad.

**Criterios de aceptación**:
- no inventa coordenadas,
- evita doble envío,
- indica cómo resolver el permiso.

**Dependencias**: #14.

**Backend relacionado**: #15.

**Evidencia**: permiso concedido, denegado y error.

### Frontend Issue 16 - Implementar formulario de ingreso
**Objetivo**: enviar visualmente el ingreso.

**Trabajo**: resumen de servicio/horario, ubicación, `POST /api/guardias`, carga, éxito y errores de radio/turno.

**Criterios de aceptación**:
- exige selección y ubicación,
- muestra hora y servicio aceptados,
- conserva datos ante rechazo.

**Dependencias**: #14 y #15.

**Backend relacionado**: #16.

**Evidencia**: válido, fuera de 100 m e inválido.

### Frontend Issue 17 - Mostrar turno activo y bloquear segundo ingreso
**Objetivo**: representar el estado real del guardia.

**Trabajo**: consulta de activo, panel, deshabilitación y sincronización después de ingreso/recarga.

**Criterios de aceptación**:
- muestra servicio y hora,
- oculta nuevo ingreso,
- maneja el 409 sin estado falso.

**Dependencias**: #16.

**Backend relacionado**: #17.

**Evidencia**: activo, recarga y segundo intento.

### Frontend Issue 18 - Implementar formulario de egreso
**Objetivo**: cerrar el turno activo.

**Trabajo**: confirmación, ubicación, envío, espera, éxito y error sin activo.

**Criterios de aceptación**:
- aparece solo con activo,
- muestra hora recibida,
- lo quita del estado activo al cerrar.

**Dependencias**: #17.

**Backend relacionado**: #18.

**Evidencia**: egreso válido y sin turno.

### Frontend Issue 19 - Crear historial del guardia
**Objetivo**: mostrar actividad propia.

**Trabajo**: `GET /api/mis-registros`, servicio, ingreso, egreso, estado, límite y vacío.

**Criterios de aceptación**:
- nunca muestra otro usuario,
- diferencia abiertos y cerrados.

**Dependencias**: #18.

**Backend relacionado**: #19.

**Evidencia**: activo, cerrado y vacío.

### Frontend Issue 20 - Crear bandeja de notificaciones
**Objetivo**: mostrar avisos internos.

**Trabajo**: contador, lista, fecha, leído/no leído y `POST /api/notificaciones/leidas`.

**Criterios de aceptación**:
- contador coincide,
- solo muestra avisos propios,
- marcar leído actualiza la lista.

**Dependencias**: #6.

**Backend relacionado**: #20.

**Evidencia**: pendiente, leído y vacío.

### Frontend Issue 21 - Listar registros para administración
**Objetivo**: supervisar activos e historial.

**Trabajo**: tablas, detalle, filtros por guardia/servicio/estado/período y orden temporal.

**Criterios de aceptación**:
- filtros no mezclan consultas,
- distingue activo y cerrado,
- muestra vacío.

**Dependencias**: #13.

**Backend relacionado**: #21.

**Evidencia**: filtros, detalle y 404.

### Frontend Issue 22 - Completar o eliminar registros
**Objetivo**: ejecutar correcciones administrativas.

**Trabajo**: selección múltiple, confirmaciones, completar, borrar, refresco y mensajes.

**Criterios de aceptación**:
- no permite acción sin selección,
- refleja el resultado real del servidor.

**Dependencias**: #21.

**Backend relacionado**: #22.

**Evidencia**: acción exitosa y rechazada.

### Frontend Issue 23 - Crear calendario mensual
**Objetivo**: visualizar registros por servicio y mes.

**Trabajo**: selectores, tabla/calendario, detalle diario y estados sin actividad.

**Criterios de aceptación**:
- cambiar mes consulta de nuevo,
- diferencia ingreso y egreso,
- no mezcla datos antiguos durante carga.

**Dependencias**: #21.

**Backend relacionado**: #23.

**Evidencia**: dos meses y período vacío.

### Frontend Issue 24 - Editar valores mensuales del servicio
**Objetivo**: editar valores operativos, sin liquidación.

**Trabajo**: campos numéricos, guardar, cancelar, validación y recarga.

**Criterios de aceptación**:
- persiste valores válidos,
- rechaza formato inválido,
- aclara el alcance.

**Dependencias**: #23.

**Backend relacionado**: #24.

**Evidencia**: lectura, edición y persistencia.

### Frontend Issue 25 - Revisar accesibilidad y errores
**Objetivo**: hacer recuperables todos los flujos.

**Trabajo**: labels, foco, teclado, mensajes, reintentos, confirmaciones y feedback no basado solo en color.

**Criterios de aceptación**:
- cada control tiene nombre,
- cada error indica la siguiente acción,
- funciona en móvil.

**Dependencias**: #1 a #24.

**Backend relacionado**: #25.

**Evidencia**: checklist y pruebas de errores.

### Frontend Issue 26 - Integración, pruebas y documentación del cliente
**Objetivo**: cerrar el frontend contra API real.

**Trabajo**: pruebas de login, CRUD, asignación, radio de 100 m, segundo activo, egreso, historial y administración; README y despliegue.

**Criterios de aceptación**:
- comandos reproducibles,
- contrato coincidente,
- flujo completo funcional.

**Dependencias**: #1 a #25.

**Backend relacionado**: #26.

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

**Frontend relacionado**: #2 y #3.

**Evidencia**: colección de casos.

### Backend Issue 3 - Implementar SQLite y migraciones
**Objetivo**: persistir sin perder datos.

**Trabajo**: crear/cargar `west_control.db`, carpeta data, esquema idempotente y claves foráneas.

**Criterios de aceptación**:
- base nueva y existente arrancan,
- migrar dos veces no duplica,
- error de persistencia detiene explícitamente.

**Dependencias**: #1.

**Frontend relacionado**: #3.

**Evidencia**: dos arranques y esquema.

### Backend Issue 4 - Crear usuarios y roles
**Objetivo**: almacenar admin/guardia con integridad.

**Trabajo**: tabla `usuarios`, username único, campos obligatorios, roles restringidos, hash, bloqueos y timestamps.

**Criterios de aceptación**:
- duplicados y roles inválidos se rechazan,
- nunca se guarda password plano.

**Dependencias**: #3.

**Frontend relacionado**: #4.

**Evidencia**: inserciones y rechazos.

### Backend Issue 5 - Implementar login, sesión y token
**Objetivo**: verificar credenciales y crear acceso seguro.

**Trabajo**: `POST /api/login`, bcrypt, cookie HttpOnly con sesión/token, expiración y respuesta mínima.

**Criterios de aceptación**:
- válido crea sesión,
- inválido responde 401 sin revelar usuarios,
- cookie usa SameSite adecuado.

**Dependencias**: #2 y #4.

**Frontend relacionado**: #5.

**Evidencia**: ambos roles y error.

### Backend Issue 6 - Implementar logout y usuario actual
**Objetivo**: invalidar acceso y consultar identidad.

**Trabajo**: `POST /api/logout`, `GET /api/me`, invalidación y 401 sin sesión.

**Criterios de aceptación**:
- logout es inmediato e idempotente,
- nunca devuelve hashes.

**Dependencias**: #5.

**Frontend relacionado**: #6.

**Evidencia**: antes y después del logout.

### Backend Issue 7 - Proteger rutas por rol
**Objetivo**: impedir accesos indebidos.

**Trabajo**: `requiereAuth`, `requiereAdmin`, rutas, 401/403 y CORS restringido.

**Criterios de aceptación**:
- sin sesión responde 401,
- guardia en admin responde 403,
- admin autorizado puede acceder.

**Dependencias**: #6.

**Frontend relacionado**: #7.

**Evidencia**: matriz de permisos.

### Backend Issue 8 - CRUD administrativo de usuarios
**Objetivo**: exponer gestión de personal.

**Trabajo**: `GET/POST/PUT/DELETE /api/admin/usuarios`, validación, hash, ocultamiento de secretos y autoeliminación prohibida.

**Criterios de aceptación**:
- CRUD admin completo,
- duplicado responde 409,
- guardia no tiene permisos.

**Dependencias**: #4 y #7.

**Frontend relacionado**: #8.

**Evidencia**: pruebas CRUD.

### Backend Issue 9 - Persistir bloqueos de guardias
**Objetivo**: guardar días no disponibles.

**Trabajo**: `PUT /api/admin/usuarios/:id/bloqueos`, formato, validación, lectura y conflicto de asignación.

**Criterios de aceptación**:
- persiste,
- un valor inválido responde 422,
- una asignación incompatible se rechaza.

**Dependencias**: #8.

**Frontend relacionado**: #9.

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

**Frontend relacionado**: #10.

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

**Frontend relacionado**: #11.

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

**Frontend relacionado**: #12.

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

**Frontend relacionado**: #13.

**Evidencia**: con/sin actividad y filtros.

### Backend Issue 14 - Exponer servicios del guardia
**Objetivo**: devolver únicamente asignaciones propias.

**Trabajo**: `GET /api/mis-servicios` y `GET /api/servicio/:nombre/horarios`, autorización y ids estables.

**Criterios de aceptación**:
- no revela asignaciones ajenas,
- sin asignaciones devuelve lista vacía,
- servicio no asignado no devuelve horarios.

**Dependencias**: #12.

**Frontend relacionado**: #14.

**Evidencia**: dos usuarios aislados.

### Backend Issue 15 - Validar coordenadas
**Objetivo**: aceptar ubicación válida y segura.

**Trabajo**: tipos, latitud [-90,90], longitud [-180,180], ausencia, precisión y payload inválido.

**Criterios de aceptación**:
- los inválidos responden 422,
- no se procesa ingreso/egreso sin ubicación.

**Dependencias**: #14.

**Frontend relacionado**: #15.

**Evidencia**: válidas, ausentes y fuera de rango.

### Backend Issue 16 - Registrar ingreso y radio de 100 metros
**Objetivo**: aceptar ingreso solo en el servicio correcto.

**Trabajo**: `POST /api/guardias`, distancia, límite 100 m, usuario, servicio, horario, timestamp y coordenadas.

**Criterios de aceptación**:
- dentro de 100 m continúa,
- mayor a 100 m responde 403 sin insertar,
- el registro aceptado queda abierto.

**Dependencias**: #11, #14 y #15.

**Frontend relacionado**: #16.

**Evidencia**: límite, dentro y fuera.

### Backend Issue 17 - Validar turno y evitar segundo servicio activo
**Objetivo**: impedir turnos inválidos o simultáneos.

**Trabajo**: día, horario, capacidad, anticipación máxima de 90 minutos, búsqueda sin egreso y transacción.

**Criterios de aceptación**:
- inválido, completo o anticipado se rechaza,
- activo devuelve 409 con servicio,
- peticiones simultáneas no duplican.

**Dependencias**: #16.

**Frontend relacionado**: #17.

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

**Frontend relacionado**: #18.

**Evidencia**: válido, ajeno y ausente.

### Backend Issue 19 - Exponer historial propio
**Objetivo**: entregar trazabilidad al guardia.

**Trabajo**: `GET /api/mis-registros`, orden, límite/paginación y aislamiento por usuario.

**Criterios de aceptación**:
- incluye abiertos y cerrados,
- nunca mezcla usuarios,
- vacío devuelve colección 200.

**Dependencias**: #18.

**Frontend relacionado**: #19.

**Evidencia**: dos usuarios y vacío.

### Backend Issue 20 - Implementar notificaciones pendientes
**Objetivo**: proveer avisos internos.

**Trabajo**: estructura, `GET /api/notificaciones`, `POST /api/notificaciones/leidas`, aislamiento y marcado idempotente.

**Criterios de aceptación**:
- solo devuelve notificaciones propias,
- repetir el marcado es seguro,
- el límite está documentado.

**Dependencias**: #5 y #14.

**Frontend relacionado**: #20.

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

**Frontend relacionado**: #21.

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

**Frontend relacionado**: #22.

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

**Frontend relacionado**: #23.

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

**Frontend relacionado**: #24.

**Evidencia**: alta, lectura y actualización.

### Backend Issue 25 - Seguridad y validación transversal
**Objetivo**: endurecer la API.

**Trabajo**: rate limit de login de 30 intentos/15 minutos, headers, sanitización, logs sin secretos, transacciones y payloads validados.

**Criterios de aceptación**:
- intento 31 responde 429,
- no se registran tokens ni passwords,
- los errores mantienen formato común.

**Dependencias**: #2 y #5 a #24.

**Frontend relacionado**: #25.

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

**Frontend relacionado**: #26.

**Evidencia**: reporte, contrato y README.

## 3.4 Orden recomendado

1. Completar issues 1 a 7 en ambos repositorios: base, contrato, sesión y permisos.
2. Completar 8 a 12: usuarios, bloqueos, servicios, horarios y asignaciones.
3. Completar 13 a 20: dashboard, operación del guardia, ingreso, egreso e historial.
4. Completar 21 a 24: supervisión, calendario y valores mensuales.
5. Completar 25 y 26: seguridad, accesibilidad, integración, pruebas y documentación.

## 3.5 Criterio de cierre

El paso queda completo cuando existen los dos repositorios, cada uno tiene sus 26 issues copiadas o vinculadas, y cada par comparte un contrato probado. El flujo final debe cubrir login por rol, asignación, consulta, validación dentro de 100 metros, ingreso, bloqueo de un segundo servicio activo, egreso, historial y supervisión administrativa.