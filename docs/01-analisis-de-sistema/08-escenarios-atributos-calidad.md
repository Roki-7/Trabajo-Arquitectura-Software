# Escenarios de atributos de calidad

Los escenarios de calidad describen situaciones concretas que permiten comprobar cómo debe funcionar la plataforma.

Cada escenario identifica quién origina la situación, qué ocurre, qué parte del sistema se evalúa, en qué condiciones sucede, cómo debe responder y cómo se comprobará el resultado.

Las medidas son metas iniciales propuestas para el proyecto. No representan resultados obtenidos ni cifras confirmadas por un estudio de demanda. Se revisarán según las necesidades de los usuarios y los recursos disponibles.

Antes de ejecutar las pruebas se registrarán el equipo, la configuración, los datos y las herramientas utilizadas.

## EQ-01. Rendimiento en búsquedas y consultas

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC01 – Rendimiento. |
| **Fuente del estímulo** | Clientes que utilizan la plataforma al mismo tiempo. |
| **Estímulo** | Los usuarios buscan servicios, consultan perfiles y comparan cotizaciones. |
| **Artefacto** | API de búsqueda y consulta, y su acceso a la base de datos. |
| **Entorno** | Prueba de 15 minutos con 50 usuarios virtuales concurrentes y datos de referencia: 1 000 prestadores, 5 000 servicios y 10 000 solicitudes. Cada usuario realiza operaciones con pausas de entre 3 y 8 segundos. |
| **Respuesta esperada** | El sistema devuelve información correcta y permite continuar las consultas sin bloqueos. |
| **Medida propuesta** | Al menos el 95 % de las respuestas de la API tarda 2 segundos o menos, con menos del 1 % de errores técnicos. Se mide la búsqueda tradicional, sin incluir llamadas a proveedores externos. |
| **Verificación** | Ejecutar una prueba de carga y registrar tiempos, solicitudes por segundo y errores por operación. Comprobar también que los resultados sean correctos. |
| **Estado** | Meta propuesta, pendiente de validar en el entorno de prueba. |

## EQ-02. Disponibilidad de las funciones principales

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC02 – Disponibilidad. |
| **Fuente del estímulo** | Cliente o prestador que intenta utilizar la plataforma. |
| **Estímulo** | El usuario accede a búsqueda, solicitudes, cotizaciones o contrataciones. |
| **Artefacto** | Aplicación web, API y almacenamiento necesario para esas funciones. |
| **Entorno** | Sistema desplegado y supervisado durante un mes, con un calendario de servicio continuo. Las comprobaciones utilizan cuentas y datos de prueba identificados, sin afectar operaciones reales. |
| **Respuesta esperada** | Las funciones principales permanecen accesibles y permiten completar sus operaciones. |
| **Medida propuesta** | Estimar una disponibilidad mensual de al menos 99,5 % para cada función evaluada, mediante comprobaciones cada minuto. Un intervalo se considera disponible si su comprobación termina correctamente en un máximo de 10 segundos. Los intervalos fallidos y sin medición cuentan como no disponibles. Se incluye el mantenimiento dentro del cálculo. |
| **Verificación** | Dividir los intervalos disponibles entre todos los intervalos del periodo y multiplicar por 100. Registrar las fallas, los periodos sin medición y las interrupciones detectadas. |
| **Estado** | Meta propuesta. La medición por intervalos es una estimación y requiere un despliegue con monitoreo durante el periodo establecido. |

## EQ-03. Escalabilidad ante el aumento de usuarios

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC03 – Escalabilidad. |
| **Fuente del estímulo** | Incremento de usuarios concurrentes. |
| **Estímulo** | Aumenta la carga de búsquedas y consultas y se amplían los recursos del backend para atenderla. |
| **Artefacto** | Backend, base de datos y recursos del despliegue. |
| **Entorno** | Pruebas con los datos y el patrón de operaciones de EQ-01. Se compara una configuración inicial con otra que duplica la capacidad de CPU y memoria asignada al backend, manteniendo iguales el código y los recursos de la base de datos. |
| **Respuesta esperada** | La plataforma permite atender más usuarios mediante la ampliación de recursos, sin cambiar las reglas del negocio. |
| **Medida propuesta** | La configuración inicial debe atender 25 usuarios concurrentes y la ampliada debe atender 50, manteniendo al menos el 95 % de las respuestas en 2 segundos o menos y menos del 1 % de errores técnicos. Ambas configuraciones también se prueban con la misma carga de 50 usuarios para comparar el efecto de la ampliación. |
| **Verificación** | Ejecutar pruebas de 15 minutos por configuración y carga. Comparar tiempos, errores, solicitudes por segundo y consumo de recursos. Registrar si aparecen límites en la base de datos u otros componentes. |
| **Estado** | Meta propuesta. Si la infraestructura no permite modificar y medir los recursos, este escenario quedará pendiente y no se declarará comprobado. |

## EQ-04. Seguridad en el acceso a información privada

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC04 – Seguridad. |
| **Fuente del estímulo** | Usuario sin sesión o con permisos insuficientes. |
| **Estímulo** | Intenta consultar o modificar solicitudes privadas, cotizaciones, contratos, documentos de verificación o funciones administrativas que no le corresponden. |
| **Artefacto** | Autenticación, autorización, API y acceso a archivos privados. |
| **Entorno** | Pruebas con cuentas de cliente, prestador y administrador, además de peticiones sin autenticación. |
| **Respuesta esperada** | El sistema rechaza el acceso, no modifica información y no devuelve datos privados. |
| **Medida propuesta** | Rechazar el 100 % de los intentos no autorizados incluidos en la matriz de pruebas. Ninguna respuesta revisada debe contener la información privada solicitada y ningún intento rechazado debe modificar los datos protegidos. |
| **Verificación** | Probar accesos directos a la API y archivos con identificadores de otros usuarios, sesiones inválidas y permisos insuficientes. Comprobar también que los accesos legítimos funcionen. |
| **Estado** | Meta propuesta. Su cumplimiento demuestra el resultado de los casos evaluados, no la ausencia de cualquier vulnerabilidad. |

## EQ-05. Mantenibilidad al sustituir el proveedor de IA

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC05 – Mantenibilidad. |
| **Fuente del estímulo** | Equipo de desarrollo. |
| **Estímulo** | Se necesita sustituir el servicio que interpreta las necesidades del cliente. |
| **Artefacto** | Contrato de asistencia de IA, adaptador y configuración que conecta sus implementaciones. |
| **Entorno** | Sistema con un contrato de integración definido y pruebas de búsqueda y contratación disponibles. |
| **Respuesta esperada** | Se incorpora la nueva implementación conservando las reglas del negocio y el funcionamiento de las demás capacidades. |
| **Medida propuesta** | El cambio no modifica las entidades ni los casos de uso de búsqueda y contratación. Las pruebas del contrato de IA y las pruebas de regresión definidas para esas funciones deben aprobarse. |
| **Verificación** | Sustituir el adaptador por una segunda implementación de prueba, revisar los archivos modificados y ejecutar las pruebas correspondientes. |
| **Estado** | Meta propuesta. Una implementación simulada permite comprobar la separación, pero no acredita una integración real con un segundo proveedor. |

## EQ-06. Usabilidad para solicitar un servicio rápido

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC06 – Usabilidad. |
| **Fuente del estímulo** | Cliente que utiliza la plataforma por primera vez. |
| **Estímulo** | Necesita buscar un gasfitero y enviar una solicitud para reparar una fuga de agua. |
| **Artefacto** | Interfaz de búsqueda, consulta de perfiles y registro de solicitudes. |
| **Entorno** | Prueba con cinco participantes que no hayan utilizado previamente el sistema, mediante cuentas de prueba y un dispositivo definido. |
| **Respuesta esperada** | Los participantes comprenden la navegación y envían la solicitud sin ayuda del evaluador ni campos propios de una obra grande. |
| **Medida propuesta** | Al menos cuatro de los cinco participantes completan la tarea sin ayuda y en un máximo de 5 minutos, desde el inicio de la búsqueda hasta la confirmación del envío. Se excluyen el registro de cuenta y la espera de respuesta del prestador. |
| **Verificación** | Observar la ejecución, medir el tiempo y registrar errores, abandonos y pasos que generen dudas. |
| **Estado** | Meta propuesta para una primera evaluación. Los resultados orientarán mejoras, sin considerarse representativos de todos los usuarios. |

## EQ-07. Adaptabilidad a distintos dispositivos

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC07 – Adaptabilidad. |
| **Fuente del estímulo** | Cliente o prestador que accede desde diferentes pantallas. |
| **Estímulo** | Utiliza la búsqueda, los perfiles, los formularios y la comparación de cotizaciones desde celular, tableta o computadora. |
| **Artefacto** | Interfaz web responsive. |
| **Entorno** | Pruebas con anchos de pantalla de 360, 768 y 1366 píxeles en los navegadores definidos para el proyecto. Se registran sus nombres y versiones. |
| **Respuesta esperada** | El contenido se reorganiza y las acciones principales permanecen visibles, legibles y utilizables. |
| **Medida propuesta** | Completar el 100 % de los recorridos de la matriz de pruebas sin controles superpuestos, textos cortados ni botones inaccesibles. No debe existir desplazamiento horizontal general; una comparación amplia puede utilizar desplazamiento dentro de su propio componente, claramente indicado. |
| **Verificación** | Ejecutar los recorridos en cada combinación de pantalla y navegador y comprobar al menos un celular y una computadora reales. |
| **Estado** | Meta propuesta. La matriz de dispositivos y navegadores se definirá antes de ejecutar la prueba. |

## EQ-08. Resiliencia ante fallas de servicios externos

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC08 – Resiliencia. |
| **Fuente del estímulo** | Falla o demora del proveedor de IA, notificaciones o mapas. |
| **Estímulo** | El proveedor deja de responder o devuelve errores durante una operación. |
| **Artefacto** | Adaptadores externos, búsqueda y proceso de envío de notificaciones. |
| **Entorno** | Pruebas controladas con interrupciones simuladas de cada integración por separado. |
| **Respuesta esperada** | La plataforma comunica el problema, conserva las operaciones confirmadas y mantiene disponibles las funciones independientes. |
| **Medida propuesta** | Si la IA o los mapas no responden, presentar una alternativa en un máximo de 8 segundos: filtros de búsqueda o selección manual de zona. Si falla una notificación, conservar la contratación y la tarea de envío. Tras restablecer el servicio, registrar un nuevo intento en un máximo de 5 minutos, sin duplicar la contratación ni otros efectos del negocio. |
| **Verificación** | Simular errores, tiempos de espera y respuestas perdidas. Revisar las alternativas, las operaciones guardadas y los intentos de notificación. |
| **Estado** | Meta propuesta. Los reintentos pueden producir avisos externos duplicados si el proveedor recibió el envío pero no confirmó su resultado. La entrega única solo se comprobará si el proveedor ofrece un mecanismo que permita garantizarla. |

## EQ-09. Integridad en contrataciones y acuerdos

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | AC09 – Integridad de la información. |
| **Fuente del estímulo** | Usuarios que actúan simultáneamente, solicitudes repetidas o una falla durante el guardado. |
| **Estímulo** | Se intenta confirmar más de una propuesta para una solicitud, repetir una confirmación o guardar parcialmente un cambio de acuerdo. |
| **Artefacto** | Casos de uso de contratación y modificación de acuerdos, transacciones y restricciones de la base de datos. |
| **Entorno** | Pruebas con solicitudes abiertas y cotizaciones válidas, incluyendo peticiones concurrentes y fallas simuladas durante el guardado. |
| **Respuesta esperada** | Se conserva una sola contratación activa por solicitud, no se repiten los efectos de una operación y no quedan acuerdos parcialmente actualizados. |
| **Medida propuesta** | En 100 repeticiones de una prueba con 10 intentos concurrentes sobre la misma solicitud, crear exactamente una contratación activa por prueba y responder de forma controlada a los demás intentos. Repetir una confirmación con el mismo identificador no debe crear otra contratación. Un cambio sin aceptación de ambas partes no debe modificar el acuerdo vigente. Ante una falla de guardado, debe conservarse completo el acuerdo anterior o guardarse completo el nuevo acuerdo aceptado, nunca una combinación parcial. |
| **Verificación** | Ejecutar pruebas concurrentes, repetir peticiones, intentar aplicar cambios no aceptados y provocar fallas antes de completar la transacción. Revisar contrataciones, versiones y confirmaciones guardadas. |
| **Estado** | Meta propuesta, pendiente de ejecutar sobre la implementación. |

## Resumen de escenarios

| Código | Atributo de calidad | Qué se busca comprobar |
|---|---|---|
| EQ-01 | Rendimiento | Que las búsquedas y consultas respondan dentro del tiempo propuesto. |
| EQ-02 | Disponibilidad | Que las funciones principales estén accesibles durante el periodo de servicio. |
| EQ-03 | Escalabilidad | Que la ampliación de recursos permita atender una carga mayor sin cambiar las reglas del negocio. |
| EQ-04 | Seguridad | Que se rechacen los accesos no autorizados evaluados, sin exponer ni modificar información privada. |
| EQ-05 | Mantenibilidad | Que pueda sustituirse una integración sin modificar las reglas principales. |
| EQ-06 | Usabilidad | Que los clientes puedan solicitar un servicio rápido sin ayuda. |
| EQ-07 | Adaptabilidad | Que las tareas principales puedan completarse desde distintas pantallas y navegadores. |
| EQ-08 | Resiliencia | Que las fallas externas no detengan funciones independientes ni deshagan operaciones confirmadas. |
| EQ-09 | Integridad de la información | Que no existan contrataciones duplicadas, cambios no aceptados ni acuerdos guardados parcialmente. |