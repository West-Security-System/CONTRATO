# Paso 3 - Diseño de las Issues del Repositorio

## 1. Objetivo del paso

Este paso define cómo se va a construir el proyecto de forma incremental y controlada. La idea es dividir el desarrollo en tareas pequeñas, verificables y ordenadas por dependencias, para que cada bloque del sistema pueda completarse sin perder claridad de alcance ni generar trabajo duplicado.

---

## 2. Issues propuestas

### Issue 1 - Configuración inicial del repositorio
**Título y descripción**: Configuración inicial del repositorio. Preparar la estructura base del proyecto, con carpetas, archivos principales y la primera configuración del servidor.

**Objetivo**: dejar el proyecto listo para comenzar a desarrollarse sin errores de estructura ni configuración. El problema que se resuelve es la falta de una base técnica clara y ordenada.

**Alcance**:
- Incluido: estructura de carpetas, archivos base del backend, configuración mínima del servidor y organización de documentación.
- Excluido: lógica del negocio, pantallas funcionales, validaciones reales, conexión a base de datos.

**Criterios de aceptación**:
- el repositorio tiene una estructura clara y ordenada,
- el servidor puede levantarse con una configuración mínima,
- el proyecto queda listo para continuar con el desarrollo.

**Dependencias**: ninguna.

**Evidencias o pruebas**:
- captura del árbol del proyecto,
- ejecución exitosa del servidor base,
- verificación de respuesta del servicio en localhost.

---

### Issue 2 - Instalación de dependencias del backend
**Título y descripción**: Instalación de dependencias del backend. Instalar las librerías necesarias para ejecutar el servidor, manejar sesiones y proteger la aplicación de forma básica.

**Objetivo**: preparar el entorno técnico para que el proyecto pueda ejecutarse sin errores de módulos ni librerías faltantes. El problema que resuelve es la ausencia de una base funcional para el backend.

**Alcance**:
- Incluido: instalación de Express, express-session, bcrypt y base de datos local.
- Excluido: lógica funcional del sistema, autenticación completa, reportes y interfaces avanzadas.

**Criterios de aceptación**:
- todas las dependencias quedan instaladas,
- el proyecto puede iniciarse sin errores de importación,
- el entorno queda listo para continuar con el desarrollo backend.

**Dependencias**: Issue 1.

**Evidencias o pruebas**:
- salida de instalación exitosa,
- ejecución del servidor sin errores,
- comprobación de que los módulos se importan correctamente.

---

### Issue 3 - Crear la base de datos inicial
**Título y descripción**: Crear la base de datos inicial. Definir las tablas necesarias para usuarios, servicios, horarios y registros del sistema.

**Objetivo**: guardar la información del proyecto de forma persistente y confiable. El problema que resuelve es la falta de almacenamiento real y consistente de los datos del negocio.

**Alcance**:
- Incluido: creación de la base de datos, tablas principales, relaciones básicas y pruebas de lectura/escritura.
- Excluido: reportes complejos, integraciones externas y validaciones avanzadas.

**Criterios de aceptación**:
- existen las tablas esenciales del sistema,
- se pueden insertar y consultar datos de prueba,
- la aplicación puede operar con persistencia real.

**Dependencias**: Issue 2.

**Evidencias o pruebas**:
- captura de la estructura de la base,
- prueba de insert y select,
- log de funcionamiento correcto de la base.

---

### Issue 4 - Crear usuario administrador por defecto
**Título y descripción**: Crear usuario administrador por defecto. Dejar una cuenta inicial con permisos administrativos para que el sistema pueda empezar a utilizarse.

**Objetivo**: asegurar que el proyecto pueda arrancar con una primera cuenta válida. El problema que resuelve es la ausencia de un usuario principal para entrar al sistema desde el inicio.

**Alcance**:
- Incluido: usuario administrador inicial, contraseña encriptada y creación automática al iniciar la app.
- Excluido: gestión de usuarios desde la interfaz, roles complejos y permisos avanzados.

**Criterios de aceptación**:
- existe un administrador inicial al arrancar la aplicación,
- se puede iniciar sesión con credenciales válidas,
- la contraseña queda protegida con hash.

**Dependencias**: Issue 3.

**Evidencias o pruebas**:
- log de creación del administrador,
- prueba de login con credenciales iniciales,
- validación del hash guardado en la base.

---

### Issue 5 - Implementar login y autenticación
**Título y descripción**: Implementar login y autenticación. Crear la lógica para validar usuario y contraseña y mantener la sesión activa del usuario autenticado.

**Objetivo**: permitir el ingreso seguro al sistema y controlar quién puede acceder a cada sección. El problema que resuelve es la ausencia de autenticación real y segura.

**Alcance**:
- Incluido: endpoint de login, validación de credenciales, creación de sesión y respuesta con datos básicos.
- Excluido: recuperación de contraseña, login con redes sociales y permisos complejos por acción.

**Criterios de aceptación**:
- un usuario válido puede iniciar sesión,
- un usuario inválido recibe error claro,
- la sesión queda activa para la navegación del sistema.

**Dependencias**: Issue 4.

**Evidencias o pruebas**:
- pruebas de login exitoso y fallido,
- captura de respuesta HTTP,
- comprobación de sesión activa.

---

### Issue 6 - Proteger rutas según el rol del usuario
**Título y descripción**: Proteger rutas según el rol del usuario. Restringir el acceso a zonas del sistema según si el usuario es administrador o guardia.

**Objetivo**: garantizar que cada perfil acceda solo a las partes que le corresponden. El problema que resuelve es el acceso no autorizado a funciones sensibles.

**Alcance**:
- Incluido: middleware de autenticación, middleware de administrador y validación de roles.
- Excluido: permisos granulares por tarea, SSO externo y roles muy complejos.

**Criterios de aceptación**:
- un usuario sin sesión no puede acceder a rutas protegidas,
- un guardia no puede ingresar al panel administrativo,
- un administrador sí puede entrar al panel de gestión.

**Dependencias**: Issue 5.

**Evidencias o pruebas**:
- pruebas de acceso con y sin sesión,
- prueba de acceso con usuario admin y guardia,
- captura de respuestas 401 y 403.

---

### Issue 7 - Crear pantalla de login
**Título y descripción**: Crear pantalla de login. Diseñar la primera vista del sistema para que el usuario ingrese usuario y contraseña.

**Objetivo**: dejar una interfaz simple y clara para autenticarse. El problema que resuelve es la ausencia de una vista de entrada al sistema.

**Alcance**:
- Incluido: formulario de ingreso, campos de usuario y contraseña, botón de acceso y diseño básico.
- Excluido: registro de usuarios, recuperación de contraseña y autenticación externa.

**Criterios de aceptación**:
- la pantalla se visualiza correctamente,
- el usuario puede completar los campos,
- el formulario se comunica con la API de login.

**Dependencias**: Issue 5.

**Evidencias o pruebas**:
- captura del formulario,
- prueba de envío del formulario,
- verificación de la respuesta del backend.

---

### Issue 8 - Crear pantalla principal del guardia
**Título y descripción**: Crear pantalla principal del guardia. Diseñar la vista inicial del perfil de seguridad con acceso a sus servicios y acciones principales.

**Objetivo**: permitir que el guardia vea su estado y registre su actividad desde una interfaz ordenada. El problema que resuelve es la ausencia de un punto de entrada claro para el flujo del personal de seguridad.

**Alcance**:
- Incluido: pantalla principal, información del usuario, servicios asignados y acceso a ingreso/egreso.
- Excluido: reportes avanzados, administración y vista con calendario complejo.

**Criterios de aceptación**:
- el guardia entra a su vista principal,
- puede ver los servicios asignados,
- tiene acceso directo a la operación principal del turno.

**Dependencias**: Issue 6, Issue 7.

**Evidencias o pruebas**:
- captura de la pantalla,
- prueba de carga con usuario autenticado,
- comprobación de que los datos visibles son correctos.

---

### Issue 9 - Crear panel de administración
**Título y descripción**: Crear panel de administración. Diseñar la vista principal del administrador con las secciones más importantes del sistema.

**Objetivo**: centralizar la administración para que el administrador gestione el sistema sin navegar en pantallas aisladas. El problema que resuelve es la falta de una vista general ordenada para administración.

**Alcance**:
- Incluido: panel principal, navegación entre módulos, acceso a usuarios, servicios y registros.
- Excluido: dashboards complejos, exportación avanzada y reportes visuales sofisticados.

**Criterios de aceptación**:
- el administrador entra al panel,
- ve las secciones principales,
- la navegación es clara y funcional.

**Dependencias**: Issue 6, Issue 7.

**Evidencias o pruebas**:
- captura del panel,
- validación de acceso con usuario admin,
- comprobación de bloqueo para usuarios sin permisos.

---

### Issue 10 - Gestionar usuarios y roles
**Título y descripción**: Gestionar usuarios y roles. Permitir crear, editar, listar y eliminar usuarios desde la administración.

**Objetivo**: controlar el personal del sistema y mantener sus datos actualizados. El problema que resuelve es la ausencia de administración del personal dentro del producto.

**Alcance**:
- Incluido: alta de usuarios, edición de datos y control de roles.
- Excluido: sueldos, permisos complejos e importación masiva.

**Criterios de aceptación**:
- el administrador puede crear usuarios,
- puede editar la información básica,
- no se permiten usuarios duplicados,
- la eliminación y edición funcionan correctamente.

**Dependencias**: Issue 3, Issue 9.

**Evidencias o pruebas**:
- pruebas de creación, edición y eliminación,
- validación de usuarios duplicados,
- comprobación de persistencia en la base de datos.

---

### Issue 11 - Gestionar servicios o locales
**Título y descripción**: Gestionar servicios o locales. Crear y administrar los servicios donde trabajan los guardias.

**Objetivo**: definir los puntos de trabajo del sistema y evitar que el control se quede sin una estructura real de servicios. El problema que resuelve es la falta de registro de los lugares de trabajo.

**Alcance**:
- Incluido: alta de servicios, edición de nombre y datos básicos, eliminación y listado.
- Excluido: geolocalización avanzada, mapas externos y reglas complejas de asignación.

**Criterios de aceptación**:
- un servicio puede crearse y guardarse,
- puede modificarse o eliminarse,
- la lista se actualiza correctamente en la interfaz.

**Dependencias**: Issue 3, Issue 9.

**Evidencias o pruebas**:
- prueba CRUD del servicio,
- comprobación de persistencia,
- captura del listado actualizado.

---

### Issue 12 - Agregar coordenadas geográficas a los servicios
**Título y descripción**: Agregar coordenadas geográficas a los servicios. Guardar la ubicación del servicio con latitud y longitud.

**Objetivo**: permitir validar si el guardia está en el lugar correcto al registrar su presencia. El problema que resuelve es la falta de referencia geográfica del servicio.

**Alcance**:
- Incluido: latitud, longitud, almacenamiento y edición desde administración.
- Excluido: mapas interactivos, geocodificación externa y rastreo continuo.

**Criterios de aceptación**:
- cada servicio tiene una ubicación válida,
- la información queda guardada,
- el administrador puede editar la ubicación cuando lo necesite.

**Dependencias**: Issue 11.

**Evidencias o pruebas**:
- prueba de guardado de coordenadas,
- consulta del backend para confirmar persistencia,
- validación de edición desde la interfaz.

---

### Issue 13 - Crear horarios por servicio
**Título y descripción**: Crear horarios por servicio. Definir los horarios de ingreso, salida y disponibilidad para cada servicio.

**Objetivo**: controlar el trabajo del guardia dentro del turno y organizar la disponibilidad del servicio. El problema que resuelve es la falta de definición temporal del servicio.

**Alcance**:
- Incluido: horario de inicio, horario de fin, relación con el servicio y listado/edición.
- Excluido: carga masiva de turnos, automatización avanzada y reportes complejos.

**Criterios de aceptación**:
- se pueden crear horarios para un servicio,
- se pueden modificar y consultar,
- la información queda persistida.

**Dependencias**: Issue 11.

**Evidencias o pruebas**:
- prueba de creación de horario,
- captura del listado de horarios,
- validación de los datos guardados.

---

### Issue 14 - Asignar guardias a servicios y turnos
**Título y descripción**: Asignar guardias a servicios y turnos. Vincular el personal con servicios específicos y horarios de trabajo.

**Objetivo**: asegurar que cada persona esté asociada al servicio correcto y que el sistema conozca el turno asignado. El problema que resuelve es la ausencia de organización del personal por servicio.

**Alcance**:
- Incluido: asociación de guardias a servicios, relación con horarios y actualización de asignaciones.
- Excluido: carga masiva automática, optimización compleja y sistemas externos.

**Criterios de aceptación**:
- un guardia puede asignarse a un servicio,
- un servicio puede tener varios guardias,
- las asignaciones quedan visibles y persistidas.

**Dependencias**: Issue 10, Issue 11, Issue 13.

**Evidencias o pruebas**:
- prueba de asignación,
- validación de la relación en base de datos,
- comprobación del listado asociado.

---

### Issue 15 - Obtener ubicación del dispositivo del guardia
**Título y descripción**: Obtener ubicación del dispositivo del guardia. Capturar la geolocalización actual del navegador para compararla con la ubicación del servicio.

**Objetivo**: validar que el guardia se encuentra físicamente en el lugar correcto al registrar su ingreso o salida. El problema que resuelve es la falta de verificación física real de la presencia del guardia.

**Alcance**:
- Incluido: acceso a geolocalización, permiso del navegador, obtención de latitud/longitud y envío al backend.
- Excluido: mapas, seguimiento continuo y geofencing avanzado.

**Criterios de aceptación**:
- el navegador solicita permiso de ubicación,
- se obtiene la coordenada actual,
- la app puede enviar esos datos para validación.

**Dependencias**: Issue 12, Issue 8.

**Evidencias o pruebas**:
- captura del permiso del navegador,
- datos de latitud y longitud obtenidos,
- verificación del envío al backend.

---

### Issue 16 - Registrar ingreso del guardia
**Título y descripción**: Registrar ingreso del guardia. Crear la lógica para registrar la entrada a un servicio validando ubicación, horario y disponibilidad.

**Objetivo**: asegurar que el ingreso quede documentado y solo pueda realizarse bajo condiciones correctas. El problema que resuelve es la falta de control del ingreso al servicio.

**Alcance**:
- Incluido: validación de servicio, cálculo de distancia, comprobación de turno y registro de ingreso con timestamp.
- Excluido: foto obligatoria, análisis de desempeño y validaciones externas complejas.

**Criterios de aceptación**:
- un ingreso válido queda guardado,
- un ingreso fuera de lugar se rechaza,
- la marca de tiempo y el servicio quedan registrados.

**Dependencias**: Issue 13, Issue 14, Issue 15.

**Evidencias o pruebas**:
- pruebas de ingreso correcto e incorrecto,
- captura del registro generado,
- validación de distancia y horario.

---

### Issue 17 - Registrar egreso del guardia
**Título y descripción**: Registrar egreso del guardia. Permitir cerrar el servicio activo con la hora de salida y las validaciones necesarias.

**Objetivo**: completar el ciclo del turno y evitar dejar servicios activos sin cierre. El problema que resuelve es la falta de cierre correcto del servicio.

**Alcance**:
- Incluido: validación de servicio activo, registro de egreso, actualización del estado del turno y timestamp de salida.
- Excluido: cierre forzado por administrador, reportes complejos y notificaciones avanzadas.

**Criterios de aceptación**:
- un guardia con servicio activo puede registrar egreso,
- un guardia sin servicio activo recibe error,
- el registro queda completo con fecha y hora de salida.

**Dependencias**: Issue 16.

**Evidencias o pruebas**:
- prueba de egreso válido e inválido,
- captura del registro completado,
- comprobación del estado final del servicio.

---

### Issue 18 - Validar servicios activos y evitar duplicados
**Título y descripción**: Validar servicios activos y evitar duplicados. Impedir que un guardia tenga más de un servicio activo al mismo tiempo.

**Objetivo**: evitar inconsistencias operativas y garantizar que cada guardia esté involucrado en un único turno activo válido. El problema que resuelve es la posibilidad de tener dos turnos simultáneos.

**Alcance**:
- Incluido: búsqueda de servicio activo, validación de duplicados y bloqueo del ingreso si ya existe uno activo.
- Excluido: prioridad entre servicios, excepciones complejas y reglas de negocio avanzadas.

**Criterios de aceptación**:
- si ya existe un servicio activo, el nuevo ingreso se bloquea,
- el sistema responde con un mensaje claro,
- no se genera un segundo registro activo para el mismo guardia.

**Dependencias**: Issue 16.

**Evidencias o pruebas**:
- prueba de doble ingreso activo,
- captura del mensaje de error,
- comprobación de que no se guarda una segunda entrada.

---

### Issue 19 - Validar horario y tolerancia del turno
**Título y descripción**: Validar horario y tolerancia del turno. Comparar la hora real del registro con el horario definido para el servicio.

**Objetivo**: controlar la puntualidad y evitar registros que se hagan fuera de la ventana esperada. El problema que resuelve es la ausencia de validación del cumplimiento del horario.

**Alcance**:
- Incluido: comparación entre hora actual y horario del servicio, validación según horario y mensajes de temprano o tardío.
- Excluido: penalizaciones complejas, análisis de cumplimiento a largo plazo y lógica de planilla.

**Criterios de aceptación**:
- se acepta un ingreso dentro del horario permitido,
- se reconoce si llegó temprano o tarde,
- el sistema rechaza o acepta según la regla definida.

**Dependencias**: Issue 13, Issue 16.

**Evidencias o pruebas**:
- pruebas de ingreso temprano, puntual y tardío,
- validación del mensaje devuelto,
- comprobación del registro generado o rechazado.

---

### Issue 20 - Crear listado de registros para administración
**Título y descripción**: Crear listado de registros para administración. Mostrar los ingresos y egresos registrados para supervisar la actividad del personal.

**Objetivo**: permitir que el administrador revise el historial sin consultar la base manualmente. El problema que resuelve es la falta de trazabilidad y control operativo.

**Alcance**:
- Incluido: listado de registros, información de servicio y usuario, estado de ingreso y egreso y acceso desde la administración.
- Excluido: exportación a Excel, reportes complejos y filtros avanzados.

**Criterios de aceptación**:
- el administrador puede ver los registros,
- la información incluye guardia, servicio y fechas,
- cada registro presenta su estado de forma legible.

**Dependencias**: Issue 17, Issue 9.

**Evidencias o pruebas**:
- captura del listado de registros,
- validación de la información mostrada,
- comprobación de acceso desde el panel administrativo.

---

### Issue 21 - Crear notificaciones de asignación y cambios
**Título y descripción**: Crear notificaciones de asignación y cambios. Avisar al guardia cuando se le asigna o retira un servicio.

**Objetivo**: mejorar la comunicación operativa y mantener informado al personal. El problema que resuelve es la falta de avisos sobre cambios relevantes.

**Alcance**:
- Incluido: creación de notificaciones, asociación con el usuario, visualización en la interfaz y marcado como leídas.
- Excluido: SMS, correo electrónico y push para dispositivos móviles.

**Criterios de aceptación**:
- se genera una notificación al cambiar la asignación,
- el usuario puede verla desde su panel,
- la notificación queda asociada al guardia correspondiente.

**Dependencias**: Issue 14.

**Evidencias o pruebas**:
- prueba de creación de notificación,
- captura de la vista de notificaciones,
- validación de lectura y almacenamiento.

---

### Issue 22 - Crear calendario mensual por servicio
**Título y descripción**: Crear calendario mensual por servicio. Mostrar los registros agrupados por fecha en una vista mensual.

**Objetivo**: facilitar la supervisión por período y dar una lectura visual clara de la actividad del servicio. El problema que resuelve es la falta de visualización temporal del trabajo por servicio.

**Alcance**:
- Incluido: calendario mensual, agrupación por fecha, registros por servicio y vista general del mes.
- Excluido: reportes complejos, exportación PDF y gráficos avanzados.

**Criterios de aceptación**:
- el administrador puede ver la actividad por día,
- las fechas muestran los registros relevantes,
- la vista ayuda a controlar el servicio en el mes.

**Dependencias**: Issue 20, Issue 9.

**Evidencias o pruebas**:
- captura del calendario mensual,
- comprobación de registros por fecha,
- validación de navegación del mes.

---

### Issue 23 - Agregar métricas básicas de cumplimiento
**Título y descripción**: Agregar métricas básicas de cumplimiento. Calcular indicadores simples sobre registros y rendimiento del servicio.

**Objetivo**: aportar medición de calidad y facilitar la evaluación del desempeño del sistema. El problema que resuelve es la ausencia de indicadores claros de cumplimiento.

**Alcance**:
- Incluido: conteo de registros, indicadores de cumplimiento, métricas básicas por servicio y visualización simple.
- Excluido: dashboards avanzados, análisis predictivo e inteligencia artificial.

**Criterios de aceptación**:
- los indicadores se calculan con datos reales,
- el administrador puede visualizarlos,
- reflejan claramente la actividad del sistema.

**Dependencias**: Issue 20, Issue 22.

**Evidencias o pruebas**:
- captura de métricas,
- validación de los valores calculados,
- comprobación de consistencia con los registros reales.

---

### Issue 24 - Mejorar mensajes de validación y errores
**Título y descripción**: Mejorar mensajes de validación y errores. Ajustar los mensajes del sistema para que sean claros cuando una acción es rechazada.

**Objetivo**: mejorar la experiencia del usuario y reducir la confusión frente a errores de negocio o validación. El problema que resuelve es la falta de feedback claro y comprensible.

**Alcance**:
- Incluido: mensajes de error claros, mensajes de éxito, validación visible en pantallas y mensajes críticos.
- Excluido: internacionalización, mensajes multilenguaje y librerías visuales complejas.

**Criterios de aceptación**:
- cada error relevante muestra un mensaje entendible,
- el usuario sabe qué acción debe seguir,
- los mensajes son consistentes en toda la aplicación.

**Dependencias**: Issue 16, Issue 17, Issue 19.

**Evidencias o pruebas**:
- captura de mensajes de error,
- validación del contenido con casos reales,
- prueba de flujo completo con errores esperados.

---

### Issue 25 - Realizar pruebas del flujo principal
**Título y descripción**: Realizar pruebas del flujo principal. Validar el funcionamiento completo del sistema desde login hasta registro y administración.

**Objetivo**: comprobar que el proyecto cumple con su función principal y que el flujo central funciona de forma integrada. El problema que resuelve es la falta de validación final del sistema completo.

**Alcance**:
- Incluido: login, gestión básica, servicios y horarios, ingreso y egreso, administración y seguimiento.
- Excluido: pruebas de carga extrema, seguridad avanzada y nuevas funcionalidades no contempladas.

**Criterios de aceptación**:
- se prueba el flujo principal completo,
- no quedan errores críticos en la ruta principal,
- los resultados se documentan para cierre del proyecto.

**Dependencias**: todas las issues anteriores.

**Evidencias o pruebas**:
- checklist de validación,
- capturas del flujo principal,
- resultados de pruebas funcionales.

---

### Issue 26 - Corregir errores y dejar la versión estable
**Título y descripción**: Corregir errores y dejar la versión estable. Resolver defectos detectados en pruebas y estabilizar la aplicación para uso real.

**Objetivo**: evitar que el sistema quede con fallas funcionales que afecten la operación diaria. El problema que resuelve es la presencia de errores que pueden interrumpir el flujo principal.

**Alcance**:
- Incluido: corrección de errores críticos, ajuste de validaciones, mejoras de flujo y estabilización del sistema.
- Excluido: nuevas funcionalidades, refactors grandes no necesarios y cambios ajenos al alcance del proyecto.

**Criterios de aceptación**:
- los errores críticos se corrigen,
- la aplicación funciona de forma estable,
- el flujo principal queda consistente y usable.

**Dependencias**: Issue 25.

**Evidencias o pruebas**:
- listado de errores corregidos,
- validación final del funcionamiento,
- captura de pruebas repetidas exitosas.

---

### Issue 27 - Documentar la versión final del proyecto
**Título y descripción**: Documentar la versión final del proyecto. Dejar la documentación del sistema para que pueda mantenerse y evolucionar.

**Objetivo**: cerrar el proyecto con una referencia clara para mantenimiento y futuras mejoras. El problema que resuelve es la ausencia de documentación útil para continuar o entregar el sistema.

**Alcance**:
- Incluido: README final, explicación del flujo general, referencia a la estructura del repositorio y documentación básica de uso.
- Excluido: manual técnico avanzado, documentación legal y despliegue profesional en producción.

**Criterios de aceptación**:
- la documentación final queda disponible dentro del repositorio,
- cualquier persona puede entender el objetivo del sistema,
- la información es clara y útil para futuras mejoras.

**Dependencias**: Issue 26.

**Evidencias o pruebas**:
- archivo README final,
- revisión del contenido,
- comprobación de que explica los pasos principales del proyecto.

---

## 3. Conclusión

Estas issues están pensadas para construir el proyecto de forma incremental, priorizando primero la base técnica y luego la lógica funcional. Cada tarea cuenta con objetivo claro, alcance definido, dependencias, criterios de aceptación y evidencias de validación, por lo que el sistema puede desarrollarse sin perder control del alcance ni de la calidad.
