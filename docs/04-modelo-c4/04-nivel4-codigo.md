# Nivel 4 · Diagrama de código

> **Proyecto:** Plataforma web para la búsqueda y contratación de servicios de construcción civil en Ayacucho.  
> **Componente detallado:** Contrataciones y acuerdos.  
> **Modelo:** C4 · Nivel 4 · Notación UML.  
> **Caso de uso:** AceptarPropuesta.

## 1. Objetivo

Detallar las clases e interfaces del componente Contrataciones y acuerdos y explicar cómo colaboran para aceptar una propuesta. Se utilizan los mismos diagramas aprobados en diseño interno, conservando una única imagen y un único archivo editable por diagrama.

| Aspecto | Descripción |
|---|---|
| Pregunta que responde | ¿Qué clases participan y cómo colaboran en una operación del módulo? |
| Audiencia | Equipo de desarrollo. |
| Notación | UML: clases para la estructura y secuencia como complemento dinámico del caso de uso. |
| Motivo del módulo elegido | Concentra aceptación, confirmación, versiones de acuerdos, concurrencia y coordinación entre módulos. |
| Alcance | Clases representativas de AceptarPropuesta; no se expanden todos los casos de uso de la plataforma. |
| Estado | Diseño propuesto con tipos lógicos, sin lenguaje, framework o motor seleccionado. |

Este nivel profundiza el componente mostrado en C3. El diseño interno explica la organización de carpetas y el pseudocódigo; aquí se presenta su relación con el modelo arquitectónico.

## 2. Diagrama de clases

![C4 · Clases de Contrataciones y acuerdos](../../img/clases-contrataciones.png)

[Editar en Draw.io](../../img/fuentes-svg/clases-contrataciones.drawio) · [Versión SVG](../../img/fuentes-svg/clases-contrataciones.svg)

### 2.1. Capas de Clean Architecture

| Capa | Elementos | Regla |
|---|---|---|
| Presentación | Controlador y traducción HTTP. | Invoca la aplicación sin acceder directamente a los datos. |
| Aplicación | Caso de uso, comandos, resultados y cinco puertos de salida. | Coordina el dominio y declara los contratos que necesita. No importa implementaciones concretas. |
| Dominio | Agregado Contratacion, valores, cambios y estados. | Conserva reglas y transiciones sin conocer HTTP, ORM o proveedores. |
| Infraestructura | Repositorios, unidad de trabajo y adaptadores. | Implementa los puertos de aplicación y conecta las tecnologías y operaciones públicas de otros módulos. |

Los puertos aparecen en una zona inferior de Aplicación para alinear cada contrato con su adaptador. Esa ubicación no los convierte en parte del dominio. La raíz de composición inyecta las implementaciones, como se explica en el diseño interno.

### 2.2. Clases del módulo de Contrataciones y acuerdos

| Clase o tipo | Tipo | Capa | Responsabilidad |
|---|---|---|---|
| ContratacionController | Controlador | Presentación | Recibir la petición y devolver una respuesta controlada. |
| AceptarPropuesta | Caso de uso | Aplicación | Validar la aceptación, crear la contratación y coordinar persistencia y avisos. |
| AceptarPropuestaCommand | Entrada | Aplicación | Transportar actor, propuesta, versión y clave de idempotencia. |
| ResultadoAceptacion | Resultado | Aplicación | Informar el identificador y el estado real alcanzado. |
| Contratacion | Entidad raíz del agregado | Dominio | Proteger participantes, estado, condiciones, versiones y cambios. |
| CondicionesAcordadas | Valor inmutable | Dominio | Conservar alcance, importe, moneda, plazo, materiales y exclusiones. |
| VersionDeAcuerdo | Valor inmutable | Dominio | Representar una versión aceptada sin sobrescribir la anterior. |
| CambioCondiciones | Entidad interna | Dominio | Conservar una propuesta de cambio y las aceptaciones de sus participantes. |
| EstadoContratacion | Enumeración | Dominio | Definir los estados permitidos del trabajo contratado. |
| EstadoCambio | Enumeración | Dominio | Definir PENDIENTE, ACEPTADO y RECHAZADO. |

La contratación puede quedar EN_CONFIRMACION o crearse CONFIRMADA si la propuesta es firme, vigente y tiene disponibilidad confirmada. El historial admite cero versiones antes de la confirmación. Un cambio de condiciones genera otra versión únicamente cuando ambas partes lo aceptan; las condiciones aceptadas anteriores siguen vigentes hasta entonces.

El diagrama conserva métodos de confirmación y cambios para explicar el agregado. Los casos de uso correspondientes se desarrollarán por separado. Los tipos auxiliares de identificadores, fechas y avisos no se expanden en otras clases.

### 2.3. Puertos y adaptadores

| Puerto de Aplicación | Implementación de Infraestructura | Colaboración |
|---|---|---|
| RepositorioContrataciones | RepositorioContratacionesBD | Buscar la contratación y guardarla con control de versión. |
| UnidadDeTrabajo | UnidadDeTrabajoBD | Coordinar el contexto transaccional y su confirmación o reversión. |
| AvisosPendientes | RegistroDeAvisosBD | Registrar el aviso en el outbox dentro de la operación principal. |
| ConsultaPropuestas | ConsultaPropuestasAdapter | Consultar la API pública de Cotizaciones para obtener la propuesta vigente. |
| GestionSolicitudes | GestionSolicitudesAdapter | Validar al cliente y la disponibilidad y registrar el vínculo mediante la API pública de Solicitudes. |

APIPublicaCotizaciones y APIPublicaSolicitudes representan operaciones internas del monolito, no servicios HTTP independientes. Los adaptadores no importan repositorios privados ni modifican tablas del otro módulo.

La unidad de trabajo exige que las operaciones públicas que actualizan Solicitudes utilicen el mismo contexto transaccional. Su firma se muestra resumida; el pseudocódigo de diseño interno explica la clave idempotente y el resultado persistido.

### 2.4. Notación UML utilizada

| Símbolo | Significado | Ejemplo |
|---|---|---|
| Línea continua con punta abierta | Asociación: conserva una referencia. | AceptarPropuesta → RepositorioContrataciones. |
| Línea discontinua con punta abierta | Dependencia: usa un tipo o crea una instancia. | AceptarPropuesta → Contratacion. |
| Línea discontinua con triángulo vacío | Realización: implementa una interfaz. | RepositorioContratacionesBD → RepositorioContrataciones. |
| Rombo relleno junto al todo | Composición: las partes pertenecen al agregado. | Contratacion → VersionDeAcuerdo. |
| «interface» | Contrato sin implementación concreta. | ConsultaPropuestas. |
| `-` / `+` | Miembro privado / público. | `- estado` / `+ confirmar()`. |
| `1`, `0..1`, `0..*` | Una instancia, opcional o colección de cero o más elementos. | Historial de versiones antes de la confirmación. |
| `{static}` | Método de creación estático. | `crearConfirmada(datos)`. |

## 3. Diagrama de secuencia: aceptar una propuesta

![Secuencia UML · Aceptar una propuesta](../../img/flujo-aceptar-propuesta.png)

[Editar en Draw.io](../../img/fuentes-svg/flujo-aceptar-propuesta.drawio) · [Versión SVG](../../img/fuentes-svg/flujo-aceptar-propuesta.svg)

El flujo comienza cuando un cliente autenticado acepta una propuesta. La identidad se obtiene de la sesión validada, no de un identificador que el navegador pueda elegir libremente. El punto de entrada propuesto es `POST /api/v1/contrataciones/aceptaciones`.

| Paso | Origen → destino | Acción |
|---|---|---|
| 1 | ClienteWeb → ContratacionController | Enviar propuesta, versión y clave de idempotencia. |
| 2 | ContratacionController → AceptarPropuesta | Ejecutar el caso de uso con la entrada validada. |
| 3–6 | AceptarPropuesta → UnidadDeTrabajo → BD | Abrir la transacción, reservar la clave y ejecutar la operación en el contexto compartido. |
| 7 | AceptarPropuesta → ConsultaPropuestas | Obtener la versión vigente y las condiciones registradas. |
| 8 | AceptarPropuesta → GestionSolicitudes | Validar al cliente y la disponibilidad de la solicitud. |
| 9 | AceptarPropuesta → RepositorioContrataciones | Comprobar que no existe otra contratación activa. |
| 10a–10b | AceptarPropuesta → Contratacion | Crear CONFIRMADA o EN_CONFIRMACION según las condiciones verificadas. |
| 11 | AceptarPropuesta → RepositorioContrataciones | Guardar con controles de versión y unicidad. |
| 12 | AceptarPropuesta → GestionSolicitudes | Registrar el vínculo mediante la operación pública del propietario. |
| 13 | AceptarPropuesta → AvisosPendientes | Guardar el aviso sin enviarlo todavía. |
| 14–16 | Operación → UnidadDeTrabajo → BD | Persistir el resultado idempotente y confirmar todos los cambios. |
| 17 | ContratacionController → ClienteWeb | Responder 201 con el identificador y el estado, después del commit. |
| Alternativa | Error de validación o persistencia | Interrumpir las llamadas restantes y revertir cambios no confirmados. |

**Condiciones de la operación:**

- La primera validación fallida interrumpe la operación. Los bloques break agrupan el manejo de errores de cada fase para facilitar la lectura.
- La consulta previa de una contratación activa no basta para resolver la concurrencia: la persistencia también protege la unicidad y la versión.
- La misma clave con los mismos datos devuelve el resultado confirmado. Reutilizarla con datos diferentes se rechaza como conflicto.
- La propuesta conserva su información y estado para el historial. Las propuestas no seleccionadas no generan una penalización reputacional.
- Una respuesta 201 indica que se creó el registro; EN_CONFIRMACION requiere otra petición del prestador mediante ConfirmarContratacion.
- El envío de avisos ocurre después del commit. Si el proveedor falla, el aviso se reintenta y la contratación no se deshace.
- Si una desconexión deja incierto el resultado del commit, el reintento usa la misma clave; no se presume que hubo rollback.

El controlador traduce errores a respuestas controladas: 400 para entrada inválida, 401 sin autenticación, 403 sin permiso, 404 si no existe el recurso, 409 por conflictos, 422 por reglas de validación y 500 ante un fallo técnico inesperado. La implementación concretará el contrato de errores.

## 4. Patrones y principios que se ven en este nivel

| Elemento | Patrón o principio | Aplicación |
|---|---|---|
| RepositorioContrataciones y su implementación | Repository | Separar reglas y persistencia. |
| ConsultaPropuestasAdapter y GestionSolicitudesAdapter | Adapter | Traducir las necesidades del caso de uso a operaciones públicas de otros módulos. |
| UnidadDeTrabajo | Unidad de trabajo | Confirmar o revertir cambios coordinados. |
| AvisosPendientes y RegistroDeAvisosBD | Outbox transaccional | Persistir el aviso junto con los cambios antes del envío externo. |
| Caso de uso que recibe interfaces | Inversión de dependencias | Conocer los contratos y no las implementaciones concretas. |
| Controlador, caso de uso, agregado y adaptadores separados | Responsabilidad única | Mantener una responsabilidad clara por pieza. |
| Puertos específicos | Segregación de interfaces | Solicitar solo las operaciones necesarias. |
| Contrataciones usa APIs públicas de otros módulos | Límite del monolito modular | Conservar encapsulación y propiedad de los datos. |

La aceptación no cobra el trabajo. La pasarela futura se reserva para servicios o planes propios de la plataforma y no se incorpora a este caso de uso.

El detalle de carpetas, composición y pseudocódigo se encuentra en [diseño interno de módulos](../03-diseño-de-software/diseño-interno/diseño-interno-de-modulos.md). Los [patrones](../03-diseño-de-software/diseño-interno/patrones-de-diseño.md) y [principios SOLID](../03-diseño-de-software/diseño-interno/principios-de-diseño.md) explican sus motivos y límites. Son decisiones de diseño, no afirmaciones de pruebas o código ya ejecutados.

---

[Índice del proyecto](../../README.md) · [Nivel anterior](03-nivel3-componentes.md)
