6. Requerimientos de Interfaces Externas
6.1 Interfaz de Usuario (UI)
Formularios Web Públicos: El sistema dispondrá de un formulario web de acceso público y optimizado para el perfil Interesado, permitiendo la carga ágil de datos de la entidad SOLICITUD. Contará con validaciones en tiempo real para evitar envíos con campos obligatorios vacíos o tasas de error altas.  
Portal de Socios: Interfaz privada y autenticada mediante contraseña (login_us) para los perfiles de Socio Titular y Adjunto. Permitirá una navegación intuitiva para la consulta del estado de cuenta (SOCIOS, PAGOS) y la edición autogestionada del núcleo familiar (NUCLEAN, INTEGRAN).  
Panel de Administración (Backoffice): Interfaz avanzada y de alta seguridad exclusiva para el perfil Administrador. Diseñada mediante tablas dinámicas y paneles operativos dedicados a la evaluación de solicitudes, asignación de espacios funerarios en el cementerio y registro manual de pagos.  

6.2 Interfaz de HardwareDispositivos de Entrada/Salida: El sistema operará a través de periféricos estándar (teclado, mouse, monitores o pantallas móviles) para la interacción con los formularios y paneles de gestión.  Dispositivos de Impresión: Compatibilidad con impresoras estándar de oficina y de dispositivos móviles para la salida física del comprobante único generado tras el registro de cada pago mensual (comp).  
Soporte de Hardware Especializado: No se requiere interacción con hardware crítico o especializado en el cementerio ni en la sede administrativa. Toda la operación se gestionará mediante terminales de cómputo convencionales.  

6.3 Interfaz de Software
Entorno de Ejecución: El núcleo del sistema estará desarrollado y se ejecutará sobre el intérprete de Python.  Gestor de Base de Datos (DBMS): Interfaz de comunicación directa con el motor de base de datos relacional para dar soporte al modelo de datos definido en el DER (organizado bajo las reglas de la Tercera Forma Normal). El software interactuará con las 8 tablas lógicas identificadas (ESPACIO_FUNERARIA, PERSONAS, SOCIOS, NUCLEAN, ADMINISTRADORES, SOLICITUDES, PAGOS, SYS_LOG).  
Servicio de Correo Electrónico (SMTP): Conexión con un servidor externo de mensajería (o API de correo) para el disparo automático de correos electrónicos de confirmación a los interesados tras registrar exitosamente una solicitud en estado "Pendiente".  

6.4 Interfaz de Comunicaciones
Protocolo de Red Seguro: Toda transferencia de datos entre los clientes (interesados, socios y administradores) y el servidor centralizado se realizará obligatoriamente bajo el protocolo seguro HTTPS/TLS, garantizando el cifrado de datos en tránsito.  
Protocolo de Autenticación de Doble Factor (2FA): Interfaz de comunicación con módulos de seguridad encargados de exigir, registrar y validar el segundo factor de autenticación previo al inicio de sesión. Ningún inicio de sesión prosperará en el sistema sin la respuesta exitosa de esta interfaz.  
Bitácora del Sistema: Interfaz interna de comunicación con la tabla SYS_LOG para almacenar en tiempo real las marcas temporales de éxito o fallo de autenticación de los usuarios (fec_hor_ent, fec_hor_sal).  

Glosario
ESRE
Especificación de Requerimientos de Software, documento que describe formalmente las funciones, restricciones y características que debe cumplir el sistema.

RF
Requerimiento Funcional: describe una acción o comportamiento específico que el sistema debe realizar.

RN
Regla de Negocio: política o principio que rige el comportamiento global del sistema, independientemente de una funcionalidad puntual.

RNF
Requerimiento No Funcional: criterio de calidad (rendimiento, seguridad, usabilidad) que debe cumplir el sistema, medible y cuantificable.

DER
Diagrama de Entidad-Relación: representación gráfica de las entidades del sistema y sus relaciones.

RNE
Restricción No Estructural: regla de integridad de negocio que no puede expresarse mediante la sola estructura de tablas de la base de datos.

3FN
Tercera Forma Normal: nivel de normalización de una base de datos relacional que elimina dependencias transitivas entre atributos.

Socio Titular
Socio responsable principal de un núcleo familiar, encargado del pago mensual de la cuota.

Socio Adjunto
Socio asociado a un núcleo familiar con derecho de uso sobre los espacios funerarios, sin responsabilidad directa de pago.

Núcleo familiar
Conjunto de personas declaradas por un Socio Titular que tienen derecho a utilizar los espacios funerarios asignados.

Interesado
Persona externa al sistema que inicia una solicitud de afiliación sin ser aún socio.

Espacio funerario
Unidad física del cementerio destinada al servicio fúnebre, clasificada como Parcela, Panteón o Nicho.

2FA
Doble Factor de Autenticación (Two-Factor Authentication): mecanismo de seguridad que exige una validación adicional a la contraseña para iniciar sesión.

UPF
Unidad de Puntos de Función No Ajustados, resultado del conteo de funciones de datos y transaccionales antes de aplicar el factor de ajuste.

VAF
Factor de Ajuste de Valor (Value Adjustment Factor), calculado a partir de las 14 Características Generales del Sistema (GSC).

APF
Análisis por Puntos de Función: técnica de estimación del tamaño funcional de un software desde la perspectiva del usuario.

ILF
Archivo Lógico Interno (Internal Logical File): grupo de datos mantenido dentro del sistema.

ELF
Archivo de Interfaz Externa (External Interface File): grupo de datos referenciado por el sistema pero mantenido por otro sistema.

EI
Entrada Externa (External Input): transacción que procesa datos que ingresan al sistema.

EQ
Consulta Externa (External Query): transacción que recupera datos sin modificarlos.

EO
Salida Externa (External Output): transacción que genera datos de salida con lógica de procesamiento adicional.

