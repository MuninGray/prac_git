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


Requerimientos funcionales
Funcionalidad: Solicitud de Afiliación Web
RF1
Descripción: El sistema debe permitir que un Interesado complete un formulario web con sus datos personales (cédula, nombre, apellidos, dirección, email) y no debe permitir su envío si falta algún campo obligatorio.
Prioridad: Alta.
Acciones iniciadoras / Estímulos: El Interesado accede a la página pública de la empresa y selecciona "Solicitar afiliación".
Comportamiento esperado del sistema: El sistema valida en tiempo real los campos obligatorios y bloquea el envío mostrando un mensaje indicando los campos faltantes, hasta que el formulario esté completo.
RF2
Descripción: El sistema debe enviar un correo electrónico de confirmación al Interesado una vez registrada su solicitud.
Prioridad: Media.
Acciones iniciadoras / Estímulos: Se registra exitosamente una nueva solicitud en estado "Pendiente".
Comportamiento esperado del sistema: El sistema dispara automáticamente un correo de confirmación al email declarado por el Interesado, indicando que la solicitud fue recibida.
RF3
Descripción: El sistema no debe permitir la creación de un registro de Socio si la solicitud asociada no está en estado "Aprobado".
Prioridad: Alta.
Acciones iniciadoras / Estímulos: Un Administrador intenta dar de alta a un socio a partir de una solicitud.
Comportamiento esperado del sistema: El sistema verifica el estado de la solicitud; si no es "Aprobado", bloquea el alta y muestra un mensaje de error explicando el motivo.
RF4
Descripción: El sistema debe registrar la fecha de evaluación y el Administrador responsable cada vez que se evalúa una solicitud.
Prioridad: Media.
Acciones iniciadoras / Estímulos: Un Administrador aprueba o rechaza una solicitud desde el módulo correspondiente.
Comportamiento esperado del sistema: El sistema guarda automáticamente la fecha/hora de evaluación y el identificador del Administrador que tomó la decisión.

Funcionalidad: Gestión de Miembros del Núcleo Familiar
RF5
Descripción: El sistema debe permitir al Socio Titular registrar múltiples integrantes en su núcleo familiar, indicando el vínculo de cada uno.
Prioridad: Alta.
Acciones iniciadoras / Estímulos: El Socio Titular selecciona "Agregar integrante" en la sección "Mi núcleo familiar".
Comportamiento esperado del sistema: El sistema solicita los datos personales y el vínculo, valida que estén completos y agrega el nuevo integrante al núcleo familiar del socio.
RF6
Descripción: El sistema no debe permitir registrar un integrante con una cédula ya existente dentro del mismo núcleo familiar.
Prioridad: Media.
Acciones iniciadoras / Estímulos: El Socio Titular intenta agregar un integrante cuya cédula ya figura en el núcleo.
Comportamiento esperado del sistema: El sistema detecta la duplicación y muestra un mensaje de error indicando que la persona ya se encuentra registrada.
RF7
Descripción: El sistema debe permitir al Socio Titular modificar o dar de baja a un integrante de su núcleo familiar.
Prioridad: Media.
Acciones iniciadoras / Estímulos: El Socio Titular selecciona un integrante existente y elige "Editar" o "Eliminar".
Comportamiento esperado del sistema: El sistema actualiza o elimina el registro del integrante, conservando el historial de cambios sobre el núcleo familiar.
RF8
Descripción: El sistema no debe permitir registrar un integrante sin especificar el vínculo familiar.
Prioridad: Baja.
Acciones iniciadoras / Estímulos: El Socio Titular intenta guardar un integrante sin completar el campo "vínculo".
Comportamiento esperado del sistema: El sistema bloquea el guardado y muestra un mensaje de error claro solicitando completar el vínculo.

Funcionalidad: Registro de Pagos Mensuales
RF9
Descripción: El sistema no debe permitir registrar un pago con un monto igual o menor a cero.
Prioridad: Alta.
Acciones iniciadoras / Estímulos: Un Administrador ingresa un monto de pago inválido en el módulo de pagos.
Comportamiento esperado del sistema: El sistema rechaza el ingreso y muestra un mensaje de error indicando que el monto debe ser mayor a cero.
RF10
Descripción: El sistema no debe permitir registrar un pago cuya fecha sea anterior a la fecha de ingreso del socio titular del núcleo.
Prioridad: Alta.
Acciones iniciadoras / Estímulos: Un Administrador ingresa una fecha de pago incompatible con la fecha de alta del socio.
Comportamiento esperado del sistema: El sistema valida la fecha ingresada contra la fecha de ingreso del socio y bloquea el registro si es incorrecta, mostrando el motivo del error.
RF11
Descripción: El sistema debe generar un número de comprobante único para cada pago registrado.
Prioridad: Media.
Acciones iniciadoras / Estímulos: Se confirma el registro de un nuevo pago.
Comportamiento esperado del sistema: El sistema asigna automáticamente un identificador de comprobante único, utilizado luego para consultas y auditorías.
RF12
Descripción: El sistema debe informar el motivo específico cuando un pago no pueda registrarse por datos inválidos.
Prioridad: Baja.
Acciones iniciadoras / Estímulos: Un Administrador intenta registrar un pago con datos incorrectos o incompletos.
Comportamiento esperado del sistema: El sistema muestra un mensaje de error específico (por ejemplo, "monto inválido" o "fecha incorrecta") en lugar de un error genérico.

Funcionalidad: Autenticación y Control de Accesos
RF13
Descripción: El sistema no debe permitir el inicio de sesión de un usuario con 2FA habilitado si no completó la validación del segundo factor.
Prioridad: Alta.
Acciones iniciadoras / Estímulos: Un usuario con 2FA activo ingresa usuario y contraseña correctos, pero no valida el segundo factor.
Comportamiento esperado del sistema: El sistema bloquea el acceso hasta recibir la validación del segundo factor, informando al usuario que debe completarla.
RF14
Descripción: El sistema debe registrar todo intento de inicio de sesión, exitoso o fallido, junto con la fecha y hora correspondiente.
Prioridad: Media.
Acciones iniciadoras / Estímulos: Un usuario intenta iniciar sesión (con éxito o no).
Comportamiento esperado del sistema: El sistema guarda un registro en la bitácora de accesos (SYS_LOG) con el resultado del intento y su marca temporal.
RF15
Descripción: El sistema debe cerrar automáticamente la sesión de un usuario tras un período de inactividad prolongado.
Prioridad: Media.
Acciones iniciadoras / Estímulos: Un usuario permanece inactivo dentro del sistema durante un tiempo determinado.
Comportamiento esperado del sistema: El sistema finaliza la sesión automáticamente y solicita reautenticación para continuar.


Requerimientos no funcionales
Eficiencia
RNF1: El sistema debe responder a toda consulta o transacción de negocio (registro de solicitud, registro de pago, consulta de núcleo familiar) en menos de 3 segundos.
RNF2: El sistema debe ser capaz de operar adecuadamente con hasta 50 sesiones concurrentes de socios en el portal web, sin degradación perceptible del tiempo de respuesta.
RNF3: Los datos actualizados en la base de datos (por ejemplo, el estado de una solicitud o el estado de cuenta de un núcleo familiar) deben reflejarse para todos los usuarios que acceden en menos de 2 segundos.

Seguridad lógica y de datos
RNF4: Los permisos de acceso al sistema solo podrán ser modificados por un Administrador con rol de administrador de accesos.
RNF5: El sistema debe respaldarse (backup) cada 24 horas, almacenando la copia en una ubicación distinta al servidor donde reside el sistema en producción.
RNF6: Todas las comunicaciones entre el cliente web y el servidor del sistema deben estar encriptadas mediante protocolo HTTPS/TLS.
RNF7: El sistema no permitirá el inicio de sesión de un usuario con doble factor de autenticación (2FA) habilitado sin validar dicho factor.

Usabilidad
RNF8: El tiempo de aprendizaje del sistema por parte de un Interesado sin conocimientos técnicos previos deberá ser menor a 10 minutos para completar el formulario de afiliación.
RNF9: La tasa de errores cometidos por el usuario al completar el formulario de solicitud deberá ser menor al 5% de los intentos totales.
RNF10: El sistema debe proporcionar mensajes de error informativos y orientados al usuario final, indicando claramente el motivo del error y cómo corregirlo (por ejemplo, "el monto debe ser mayor a cero" en lugar de un error genérico).
