# Restricciones

Las restricciones son condiciones y límites que deben respetarse durante el desarrollo del proyecto. Pueden estar relacionados con la tecnología, el funcionamiento del negocio o las indicaciones del curso.

| ID | Restricción | Descripción |
|---|---|---|
| RC01 | **Aplicación web responsive** | La plataforma debe utilizarse desde un navegador y adaptar su interfaz a celulares, tabletas, computadoras y laptops. El desarrollo de aplicaciones nativas para Android o iOS queda fuera de esta versión. |
| RC02 | **Servicios de construcción civil** | La plataforma debe admitir servicios del sector de construcción civil, desde estudios y diseño hasta ejecución, instalaciones, acabados, mantenimiento y supervisión. La incorporación de otros sectores queda para futuras ampliaciones. |
| RC03 | **Cobertura inicial en Ayacucho** | La primera versión atenderá las zonas de Ayacucho que se definan para el proyecto. La expansión a otras regiones se realizará posteriormente. |
| RC04 | **Uso de Git y GitHub** | Los documentos y el código deben gestionarse con Git y mantenerse en un repositorio de GitHub para conservar el historial de cambios. |
| RC05 | **Documentación académica** | La documentación debe elaborarse en Markdown y organizarse según las guías del curso, incluyendo análisis del sistema, arquitectura, diseño y modelo C4. |
| RC06 | **Comunicación mediante API REST** | La comunicación entre la aplicación web y el backend debe realizarse mediante una API REST. |
| RC07 | **Conexión a internet** | Las funciones que consultan o actualizan información compartida requieren conexión a internet. Esta versión no permitirá completar contrataciones sin conexión. |
| RC08 | **Condiciones de servicios externos** | Las integraciones de IA, notificaciones y mapas que se incorporen deben respetar las condiciones de acceso y los límites de uso de sus proveedores. |
| RC09 | **Protección de credenciales** | Las claves privadas de los servicios externos deben mantenerse en el servidor. No deben incluirse en el código público ni exponerse en el navegador. |
| RC10 | **Pagos directos al prestador** | El cliente pagará directamente al prestador. La plataforma registrará el pago declarado y la respuesta del receptor, sin procesar, retener ni distribuir dinero. |
| RC11 | **Cobro de la plataforma en una etapa futura** | El cobro por servicios o planes de la plataforma y la integración necesaria para recibir esos pagos quedan fuera de esta versión. |
| RC12 | **Responsabilidad sobre la ejecución** | La plataforma facilitará la búsqueda, contratación y seguimiento. La realización del trabajo y las evaluaciones técnicas corresponderán al prestador contratado. |
| RC13 | **Comunicación por llamada o WhatsApp** | Estos medios se utilizarán como canales de contacto. La plataforma no accederá a sus conversaciones ni registrará automáticamente lo acordado fuera del sistema. |
| RC14 | **Tratamiento de datos personales** | La recopilación, uso y conservación de datos personales deben ajustarse a las obligaciones aplicables de protección de datos. Los documentos privados y las direcciones exactas solo estarán disponibles para usuarios autorizados. |
| RC15 | **Documentos de contratación** | Los documentos se prepararán a partir de las condiciones acordadas por las partes. Antes de utilizarlos con clientes reales deberán definirse y revisarse las plantillas y el mecanismo de aceptación o firma. |

La base de datos y los proveedores de IA, notificaciones y mapas todavía no están seleccionados. Su elección se justificará en las decisiones arquitectónicas.