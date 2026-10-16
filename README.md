# Plataforma web para la búsqueda y contratación de servicios de construcción civil en Ayacucho

## Autor

Anderson Ochoa.

## Descripción

Proyecto académico de una plataforma que facilita la búsqueda y contratación de servicios de construcción civil. Clientes y prestadores podrán utilizarla desde celulares, tabletas y computadoras mediante una aplicación web responsive.

## Caso de estudio

Búsqueda y contratación de servicios del sector de construcción civil en Ayacucho, desde reparaciones e instalaciones hasta trabajos y obras de mayor alcance.

## Curso

Arquitectura de Software.

## Documentación de esta entrega

| Parte | Documento |
|---|---|
| Análisis | [Contexto y problemática](docs/01-analisis-de-sistema/00-contexto-y-problematica.md) |
| Análisis | [Actores](docs/01-analisis-de-sistema/01-actores.md) |
| Análisis | [Historias de usuario](docs/01-analisis-de-sistema/02-historias-de-usuario.md) |
| Análisis | [Requisitos funcionales y relación con historias](docs/01-analisis-de-sistema/03-requisitos-funcionales.md) |
| Análisis | [Atributos de calidad](docs/01-analisis-de-sistema/04-atributos-de-calidad.md) |
| Análisis | [Restricciones](docs/01-analisis-de-sistema/05-restricciones.md) |
| Análisis | [Drivers arquitectónicos](docs/01-analisis-de-sistema/06-drivers-arquitectonicos.md) |
| Análisis | [Decisiones arquitectónicas](docs/01-analisis-de-sistema/07-decisiones-arquitectonicas.md) |
| Análisis | [Escenarios de atributos de calidad](docs/01-analisis-de-sistema/08-escenarios-atributos-calidad.md) |
| Arquitectura | [Arquitectura inicial](docs/02-arquitectura-software/arquitectura-inicial.md) |
| Arquitectura | [Componentes arquitectónicos](docs/02-arquitectura-software/componentes-arquitectonicos.md) |
| Arquitectura | [Enfoque arquitectónico](docs/02-arquitectura-software/enfoque-arquitectonico.md) |
| Arquitectura | [Estilo arquitectónico](docs/02-arquitectura-software/estilo-arquitectonico.md) |
| Diseño | [Diseño interno de módulos](docs/03-diseño-de-software/diseño-interno/diseño-interno-de-modulos.md) |
| Diseño | [Patrones de diseño](docs/03-diseño-de-software/diseño-interno/patrones-de-diseño.md) |
| Diseño | [Principios de diseño — SOLID](docs/03-diseño-de-software/diseño-interno/principios-de-diseño.md) |
| Modelo C4 | [Nivel 1: contexto del sistema](docs/04-modelo-c4/01-nivel1-contexto.md) |
| Modelo C4 | [Nivel 2: contenedores](docs/04-modelo-c4/02-nivel2-contenedores.md) |
| Modelo C4 | [Nivel 3: componentes](docs/04-modelo-c4/03-nivel3-componentes.md) |
| Modelo C4 | [Nivel 4: código y secuencia](docs/04-modelo-c4/04-nivel4-codigo.md) |

## Imágenes y archivos editables

Las diez imágenes utilizadas en la documentación están en [img](img/). Sus fuentes [Draw.io y SVG](img/fuentes-svg/) permiten revisar los diagramas con zoom y editarlos.

| Diagrama | Documento donde se presenta |
|---|---|
| Componentes arquitectónicos | Componentes arquitectónicos. |
| Clean Architecture | Enfoque arquitectónico. |
| Monolito modular en capas | Estilo arquitectónico. |
| Capas del módulo y dependencias | Diseño interno, apartado 3. |
| Clases de Contrataciones y acuerdos | Diseño interno, apartado 4, y C4, nivel de código. |
| Secuencia de AceptarPropuesta | Diseño interno, apartado 5, y C4, nivel de código. |
| SOLID en Contrataciones y acuerdos | Principios de diseño. |
| Contexto del sistema | Modelo C4, nivel 1. |
| Contenedores de la plataforma | Modelo C4, nivel 2. |
| Componentes de la API | Modelo C4, nivel 3. |

## Organización del repositorio

| Carpeta | Contenido |
|---|---|
| `docs/01-analisis-de-sistema/` | Contexto, actores, historias, requisitos, calidad, restricciones, drivers, decisiones y escenarios. |
| `docs/02-arquitectura-software/` | Arquitectura inicial, componentes, enfoque y estilo. |
| `docs/03-diseño-de-software/diseño-interno/` | Diseño del módulo de referencia, patrones y principios. |
| `docs/04-modelo-c4/` | Contexto, contenedores, componentes y código con su secuencia. |
| `img/` | Diez imágenes utilizadas en la documentación. |
| `img/fuentes-svg/` | Diez archivos Draw.io editables y sus diez versiones SVG. |
| `tecnologia/` | Estructura reservada para el ejemplo tecnológico, pendiente de implementar. |

## Relación entre los documentos

La arquitectura inicial presenta la solución general. El modelo C4 desarrolla el contexto, las aplicaciones y almacenes y los componentes internos de la API. El diseño interno explica cómo se organiza el módulo de Contrataciones y acuerdos.

Los diagramas de clases y secuencia se utilizan tanto en diseño interno como en el nivel de código. Ambos documentos enlazan los mismos archivos para conservar un único modelo y evitar duplicar imágenes o editables.

## Alcance de esta entrega

La documentación de análisis, arquitectura, diseño y modelo C4 está desarrollada. Describe una solución propuesta; el código de referencia de diseño interno es pseudocódigo.

La [carpeta de tecnología](tecnologia/README.md) conserva el esqueleto preparado anteriormente. Sus archivos de implementación están vacíos: no hay todavía una aplicación ejecutable ni resultados de pruebas del software. Las extensiones de esos archivos no constituyen una selección definitiva del stack.

La pasarela de pagos se mantiene como ampliación futura para cobrar planes o servicios propios de la plataforma. Los trabajos de construcción se pagan directamente al prestador; el sistema conserva declaraciones y confirmaciones, sin procesar ni verificar transferencias bancarias.

## Consulta y edición

1. Comenzar por el análisis del sistema y continuar con arquitectura, diseño y modelo C4 en el orden del índice.
2. Consultar las imágenes desde cada documento; abrir los SVG para ampliar el detalle.
3. Abrir los archivos `.drawio` con Draw.io o diagrams.net para editar figuras, relaciones y textos.
4. Al actualizar clases o secuencia, conservar sus rutas para que el cambio se refleje en las dos secciones.

Los enlaces son relativos y están preparados para visualizar la documentación en GitHub. La publicación en un repositorio se realiza por separado; este paquete no implica que ya se haya subido.
