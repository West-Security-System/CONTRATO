# Paso 2 - Límites, alcance y objetivos

## 2.1 Límites del sistema

### Dentro del sistema
- autenticación por sesión con roles de administrador y guardia,
- gestión de usuarios, servicios, horarios y asignaciones,
- registro de ingreso y egreso por parte del personal,
- validación de ubicación geográfica respecto del servicio,
- control de turnos activos, pendientes y completados,
- listado de registros y trazabilidad para administración,
- configuración básica del sistema para operar en un entorno web.

### Fuera del sistema
- app móvil nativa para Android o iOS,
- notificaciones push o SMS a dispositivos fuera del navegador,
- integración con ERPs, planillas de sueldos o sistemas de gestión externa,
- login con Google, OAuth corporativo o SSO institucional,
- dashboards analíticos avanzados, reportes de negocio complejos o inteligencia artificial,
- gestión de pagos, licencias, liquidaciones o administración de personal fuera del control operativo.

## 2.2 Alcance funcional

### Para guardias
- iniciar sesión con sus credenciales,
- consultar los servicios y turnos asignados,
- registrar su ingreso al servicio desde la web,
- registrar su egreso una vez finalizado el turno,
- validar su ubicación actual frente a la ubicación del servicio,
- verificar que el servicio activo y el horario sean válidos,
- consultar el historial básico de su actividad operativa.

### Para administradores
- crear, editar y eliminar usuarios del sistema,
- definir servicios o locales con nombre y coordenadas,
- crear y administrar horarios por servicio,
- asignar guardias a servicios y turnos,
- supervisar registros de ingreso y egreso,
- revisar servicios activos, registros históricos y posibles inconsistencias,
- mantener la configuración básica para el control operativo de la empresa.

## 2.3 Alcance no funcional

- Seguridad: manejo de sesiones, contraseñas protegidas con hash y control de acceso por roles.
- Performance: tiempos de respuesta razonables para login, carga de servicios y registro de turnos en carga normal.
- Disponibilidad: funcionamiento estable para uso operativo diario dentro del entorno web del proyecto.
- Usabilidad: interfaz simple, clara y adecuada para un uso rápido desde navegador.
- Mantenibilidad: estructura ordenada, lógica separada por responsabilidades y documentación básica del sistema.
- Persistencia: almacenamiento confiable de usuarios, servicios, horarios y registros.
- Escalabilidad: la solución está pensada para crecer de forma modular, sin depender de un backend totalmente acoplado.

## 2.4 Objetivos específicos y medibles

Los objetivos son concretos y se pueden comprobar al finalizar el desarrollo:

- Permitir el acceso de los dos perfiles definidos: administrador y guardia, con separación de rutas protegidas.
- Registrar el 100% de los ingresos y egresos aceptados con usuario, servicio, fecha, hora y estado del turno.
- Rechazar todo intento de ingreso que supere el radio máximo de 100 metros del servicio configurado.
- Impedir que un guardia mantenga más de un servicio activo sin registrar antes el egreso.
- Permitir al administrador gestionar usuarios, servicios, horarios y asignaciones desde el panel web.
- Mostrar al administrador el historial de registros y los servicios activos para supervisar la operación diaria.

## 2.5 Métricas de calidad

- Seguridad: 0 accesos exitosos a rutas administrativas con una sesión de guardia o sin autenticación.
- Geolocalización: 100% de los ingresos fuera de un radio de 100 metros rechazados.
- Integridad: 0 guardias con dos registros activos simultáneos durante las pruebas.
- Trazabilidad: 100% de los registros aceptados con usuario, servicio, ingreso y estado del egreso identificables.
- Rendimiento: login, carga de servicios y consulta del estado activo con respuesta menor a 2 segundos en uso normal.
- Usabilidad: todas las operaciones rechazadas muestran un mensaje comprensible y una acción siguiente.

## 2.6 Criterios de aceptación

- Un guardia solo puede registrar ingreso si se encuentra dentro del radio permitido del servicio.
- Un guardia no puede tener dos servicios activos al mismo tiempo.
- El administrador puede crear, modificar y supervisar usuarios, servicios, horarios y asignaciones.
- El sistema registra fecha, hora, servicio y estado del turno para auditoría.
- Los registros deben ser legibles y útiles para la supervisión operativa.
- El flujo principal debe funcionar sin depender de procesos manuales o de terceros externos.

## 2.7 Resumen del alcance

El proyecto está definido como un sistema web de control operativo de presencia para guardias. Su foco principal es la validación real de ingreso y egreso, la gestión de servicios y turnos, y la trazabilidad de la actividad para la administración. No incluye plataformas móviles ni módulos avanzados de negocio, pero sí cumple con la necesidad funcional central del negocio de seguridad.
