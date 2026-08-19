# Paso 2 - Límites, alcance y objetivos

## 2.1 Límites del sistema

**Dentro del sistema:**
- login con roles de administrador y guardia.
- gestion de usuarios, servicios, horarios y registros.
- registro de ingreso y egreso con validacion por ubicacion, horario y servicio activo.
- control de turnos activos, pendientes y completados.
- visualizacion de historial para administracion.
- gestion de asignaciones, notificaciones y configuraciones basicas del negocio.

**Fuera del sistema:**
- integracion con sistemas externos, ERPs o planillas de sueldos.
- autenticacion con Google o SSO corporativo.
- app movil nativa o push notifications a dispositivos.
- gestion de personal, liquidaciones, pagos.

## 2.2 Alcance funcional

**Para guardias:**
- iniciar sesion y consultar sus servicios asignados.
- registrar ingreso y egreso del servicio correspondiente.
- validar su ubicacion para confirmar presencia en el lugar.
- consultar el estado del servicio activo y datos del turno.

**Para administradores:**
- crear, editar y eliminar usuarios, servicios y horarios.
- asignar guardias a servicios y turnos.
- supervisar ingresos, egresos, servicios activos y registros historicos.
- administrar configuraciones basicas para el control operativo.

## 2.3 Alcance no funcional

- seguridad en sesiones y almacenamiento de contraseñas.
- interfaz simple, clara y usable para ambos perfiles.
- respuesta eficiente para operaciones de control diarias.
- persistencia confiable de registros y configuraciones del sistema.
- mantenibilidad del codigo para futuras modificaciones.

## 2.4 Objetivos específicos

- controlar la presencia de los guardias en cada servicio asignado.
- reducir errores manuales en el registro de entrada y salida.
- evitar duplicados, turnos activos inconsistentes o registros fuera de horario.
- dejar una trazabilidad clara de cada servicio y cada guardia.
- facilitar la administracion y supervision del personal de seguridad.

## 2.5 Métricas de calidad

- porcentaje de registros validos sobre total de intentos: idealmente alto y estable.
- cantidad de registros duplicados o rechazados por validacion incorrecta: debe mantenerse baja.
- tiempo de respuesta en operaciones basicas como login, carga de servicios y registro: debe ser rapido y consistente.
- nivel de cumplimiento de guardias respecto a horario de ingreso y egreso: indicador clave del funcionamiento del sistema.
- claridad y legibilidad de la informacion para administradores al revisar registros y supervisar servicios.

## 2.6 Criterios de aceptacion

- Un guardia solo puede registrar ingreso si se encuentra dentro del radio permitido del servicio.
- Un guardia no puede tener dos servicios activos al mismo tiempo.
- El administrador puede crear, modificar y supervisar usuarios, servicios y horarios.
- El sistema debe registrar fecha, hora y estado del turno para auditoria.
- La informacion de registros debe ser legible y util para la toma de decisiones del administrador.
- Recoleccion y analisis de datos para facilitar la lectura de los administradores.
