# Paso 1 - Objetivo principal del proyecto

## 1.1 Problema que resuelve
Las empresas de seguridad privada necesitan controlar de forma confiable si cada guardia llega a tiempo, permanece en el servicio asignado y registra correctamente su ingreso y egreso. En la práctica, este control suele hacerse manualmente mediante llamadas, planillas o reportes verbales, lo que genera errores, ausencias no detectadas, falta de trazabilidad y dificultad para supervisar la operación diaria.

El proyecto busca resolver esta problemática con un sistema web centralizado que permita registrar y auditar la presencia de cada guardia sin depender de procesos manuales o poco fiables.

## 1.2 Objetivo general del sistema
**West Security Company** es una aplicación web para gestionar la presencia de guardias en servicios o locales asignados. El sistema permite a los administradores definir servicios, horarios y asignaciones, mientras que los guardias registran su ingreso y egreso desde un navegador, validando su ubicación actual frente a la ubicación del servicio.

La aplicación está pensada para ser un control operativo básico, claro y usable, orientado a la seguridad del turno y a la trazabilidad de las tareas realizadas por cada persona.

## 1.3 Usuarios y perfiles
El sistema contempla dos perfiles principales:

- Administrador: configura usuarios, servicios, horarios, asignaciones y revisa los historiales de registros.
- Guardia: consulta sus servicios asignados, valida su ubicación y registra su ingreso/egreso del turno.

## 1.4 Funcionalidad principal
La funcionalidad central del proyecto es la siguiente:

- el administrador crea y mantiene los servicios y sus ubicaciones,
- asigna guardias y turnos a cada servicio,
- el guardia inicia sesión y selecciona el servicio correspondiente,
- la app solicita su ubicación actual para validar que se encuentra en el lugar correcto,
- el sistema registra la entrada o salida con fecha, hora, servicio y datos del turno,
- el administrador puede consultar el historial y supervisar la actividad operativa.

## 1.5 Alcance realista del proyecto
Este proyecto contempla una solución web de gestión operativa para control de presencia, no una app móvil nativa ni un sistema de analytics avanzados o de pagos. La prioridad es la confiabilidad del registro, la seguridad de la sesión y la claridad del proceso para administradores y guardias.

En este sentido, el sistema se enfoca en:

- controlar la presencia del personal en el servicio asignado,
- evitar turnos duplicados o inconsistentes,
- registrar evidencia operativa en cada ingreso/egreso,
- facilitar la administración del personal y sus horarios.

## 1.6 Resultado esperado
El proyecto tiene como objetivo dejar un sistema funcional para la gestión de ingreso y egreso de guardias, con una base web simple, segura y mantenible, que permita reducir errores manuales, mejorar la trazabilidad y apoyar la supervisión operativa del servicio.
