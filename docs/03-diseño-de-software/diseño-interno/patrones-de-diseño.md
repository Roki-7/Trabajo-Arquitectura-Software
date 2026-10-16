# Patrones de diseño

## Objetivo

Documentar los patrones previstos en el backend, indicando dónde se utilizan, qué problema resuelven y con qué piezas del diseño se relacionan. Las descripciones corresponden al diseño propuesto y se comprobarán durante la implementación.

## Contexto

- **Estilo:** monolito modular organizado en capas.
- **Enfoque interno:** Clean Architecture.
- **Módulo de referencia:** Contrataciones y acuerdos.
- **Base:** diagramas de componentes, paquetes, clases y secuencia ya elaborados.
- **Tecnología:** framework, motor y proveedores por seleccionar.

## Patrones aplicados

| Patrón | Dónde se usa | Problema que resuelve | Se implementa con | Piezas de referencia |
|---|---|---|---|---|
| Adapter | Contrataciones → Cotizaciones y Solicitudes. | Colaborar sin conocer detalles privados de los otros módulos. | Contratos internos y llamadas a sus APIs públicas. | ConsultaPropuestasAdapter, GestionSolicitudesAdapter. |
| Adapter | IA, archivos, mapas y envío de avisos. | Traducir formatos y errores de proveedores distintos. | Clientes técnicos dentro de infraestructura. | Adaptadores de servicios externos y archivos del diseño arquitectónico. |
| Repository | Contrataciones → base de datos. | Mantener los casos de uso independientes de SQL y del motor. | Implementación del puerto de persistencia. | RepositorioContrataciones, RepositorioContratacionesBD. |
| Unit of Work | Guardado coordinado de la aceptación. | Evitar que queden cambios parciales en la contratación, la solicitud y el aviso. | Un contexto transaccional compartido por operación. | UnidadDeTrabajo, UnidadDeTrabajoBD. |
| Transactional Outbox | Contratación → avisos pendientes. | Conservar la intención de envío aunque falle el proveedor después de guardar el acuerdo. | Aviso almacenado con la operación y envío posterior al commit. | AvisosPendientes, RegistroDeAvisosBD y proceso de avisos pendientes. |

Transactional Outbox es un patrón de integración y consistencia; no pertenece al catálogo clásico GoF. Se incluye porque forma parte del flujo documentado. Los puertos del backend se ubican en Aplicación y sus implementaciones en Infraestructura.

## Cómo funciona cada patrón

| Patrón | En pocas palabras |
|---|---|
| Adapter | El caso de uso pide una propuesta vigente; el adaptador utiliza la API pública de Cotizaciones. |
| Repository | El negocio pide guardar la contratación; el repositorio resuelve la persistencia y sus conflictos conocidos. |
| Unit of Work | Los cambios relacionados se confirman juntos o se revierten antes de confirmar. |
| Transactional Outbox | Se guarda el aviso con el acuerdo y se envía después; no se mantiene la transacción abierta esperando al proveedor. |

La consulta previa no reemplaza los controles de unicidad y versión en persistencia. Los reintentos de aceptación utilizan idempotencia. Los avisos también necesitan identificar y controlar entregas repetidas: Outbox por sí solo no garantiza una entrega exactamente una vez.

## Beneficio

- Los casos de uso y las reglas quedan separados de herramientas y proveedores.
- Otra implementación compatible se conecta desde la composición sin reescribir el caso de uso.
- Los dobles controlados facilitan las pruebas; la persistencia y las transacciones requieren pruebas de integración.
- La contratación se conserva aunque un proveedor de notificaciones no esté disponible después del commit.

## Patrones previstos para siguientes iteraciones

| Patrón | Dónde se aplicaría | Cuándo |
|---|---|---|
| Adapter para pagos | Cobro de planes o servicios de la plataforma. | Al implementar ese servicio y seleccionar el proveedor; no cobra el trabajo al prestador en el alcance actual. |
| Decorator | Consultas frecuentes de catálogo o perfiles. | Si las mediciones justifican caché u otra función adicional. No se incorpora Redis por anticipado. |
| Factory | Construcción de variantes de acuerdos. | Si la complejidad justifica una fábrica específica. Los métodos estáticos actuales no demuestran que ya exista Factory Method de GoF. |
| Facade | Operaciones públicas de módulos que crezcan. | Si se necesita simplificar varias colaboraciones detrás de una interfaz. Una API pública no implica por sí sola el patrón. |
