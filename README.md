# prac_git
Un repositorio creado para el Ejercicio Colaborativo de GitHub

1. **Introducción**

Este documento presenta la Especificación de Requerimientos de Software (ESRE) para el sistema de gestión de "El buen descanso", una empresa funeraria que busca ampliar sus servicios mediante la incorporación de un cementerio privado. El objetivo del sistema es brindar una solución que permita gestionar de forma organizada el proceso de afiliación de nuevos socios, la administración de los grupos familiares, la asignación de espacios funerarios y el registro de los pagos asociados al servicio.

**2. Alcance del producto**
El sistema de gestión de información de "El buen descanso" tiene como objetivo centralizar la administración de las operaciones relacionadas con el cementerio privado de la empresa. El proceso abarca desde que una persona completa la solicitud de afiliación mediante el formulario web hasta que se convierte en un socio activo, con un espacio funerario asignado y el registro de sus pagos mensuales.
Entre los principales beneficios del sistema se encuentra la sustitución del proceso manual de afiliación por un servicio web más seguro y organizado, reduciendo los tiempos de gestión. Además, permite centralizar el control de los espacios funerarios para evitar asignaciones duplicadas o inconsistentes y mejora la seguridad de la información mediante mecanismos como la autenticación de dos factores.

**3. Funcionalidades del producto** 

Las funcionalidades del sistema permitirán gestionar las principales actividades de la empresa relacionadas con los socios y el cementerio privado.
Entre ellas se incluyen:

- Registrar solicitudes de afiliación realizadas desde el sitio web.
- Permitir a los administradores aprobar o rechazar las solicitudes recibidas.
- Registrar y administrar la información de los socios.
- Gestionar los grupos o núcleos familiares asociados a cada socio.
- Asignar espacios funerarios disponibles según las preferencias del socio y la disponibilidad.
- Registrar y consultar los pagos mensuales de cada núcleo familiar.
- Permitir que los socios consulten su información personal, su grupo familiar y el espacio funerario asignado.
- Gestionar el acceso al sistema mediante autenticación de usuarios y, cuando corresponda, verificación en dos pasos (2FA).

**4. Clases y características del usuario**
El sistema identifica cuatro tipos de usuario, definidos a partir del modelo de datos de la Fase 1.

Interesado/Postulante
-Es una persona que todavía no es socia de “El buen descanso”, su única función dentro del sistema es completar el formulario de solicitud de afiliación.
-Su ùnico permiso es el de completar el formulario de afiliación.

Socio Titular
-Es el afiliado principal y el responsable de un núcleo familiar. 
-Tiene asignado un espacio funerario y puede gestionar la información de su núcleo familiar.
Sus permisos son:
-Consultar y modificar sus datos personales.
-Gestionar la información de su núcleo familiar.
-Consultar su espacio funerario asignado.
-Consultar el historial de pagos.

Socio Adjunto
-Es un integrante del núcleo familiar del socio titular.
Sus permisos son:
-Consultar los datos personales del núcleo.
-Consultar su espacio funerario asignado.

Administrador
-Es el funcionario de la empresa encargado de gestionar el sistema.
Sus permisos son: 
-Acceder a las solicitudes de afiliación.
-Aprobar o rechazar solicitudes.
-Dar de alta socios.
-Consultar y modificar información del sistema.
-Registrar pagos.
-Administrar espacios funerarios.



**5. Entorno Operativo**

    Plataforma de hardware:

        - Servidor de aplicaciones y base de datos alojado en infraestructura propia de la empresa o en un proveedor de hosting/cloud (a definir), con capacidad para soportar al menos 50 usuarios concurrentes según lo establecido en los requerimientos no funcionales de eficiencia.

        - Equipos cliente estándar (PC, notebook, tablet o smartphone) con acceso a internet, sin requerimientos de hardware específico más allá de un navegador web actualizado.

    Sistema operativo y software de base:

        - Servidor: sistema operativo Linux (distribución a definir por el equipo de infraestructura), compatible con el stack de desarrollo elegido (Python).

        - Motor de base de datos relacional (por ejemplo PostgreSQL o MySQL), acorde al modelo de datos normalizado en 3FN definido en la Fase I.

        - Servidor web / framework de aplicación en Python (por ejemplo Django o Flask) para exponer tanto el sitio público de afiliación como el portal de socios y el panel administrativo.

    Entorno cliente:

        - Acceso mediante navegador web estándar (Chrome, Firefox, Edge, Safari) en sus versiones actualizadas, sin necesidad de instalación de software adicional por parte de interesados o socios.

        - Diseño responsive para permitir el acceso desde dispositivos móviles, dado que la afiliación y consulta de estado se realizan de forma pública y remota.

    Interfaces con otros sistemas:

        - Pasarela de pago externa para el registro de pagos de afiliación y cuotas mensuales (según lo mencionado en RF3).

        - Servicio de correo electrónico (SMTP o API de terceros) para el envío de notificaciones automáticas de confirmación de solicitud y resultado de evaluación (RF1, RF2).

        - No se identifican Archivos de Interfaz Externa (EIF), en línea con lo definido en la Sección 2, ya que el sistema no consume datos mantenidos por otra aplicación externa.

    Condiciones de red:

        - Conexión a internet estable tanto del lado del servidor como del cliente, con comunicación cifrada (HTTPS) para proteger los datos personales y de pago transmitidos, en concordancia con el requerimiento no funcional de seguridad lógica y de datos.


**6. Reglas de Negocio**

    - Las siguientes reglas de negocio expresan políticas operativas, comerciales y de control que la empresa aplica y que el software debe respetar de forma transversal, independientemente del módulo o funcionalidad que se esté ejecutando:

    - Toda persona debe ser mayor de edad (18 años o más, calculado a partir de fec_nac) para poder constituirse como Socio Titular (RNE2).

    - No puede generarse un alta en la tabla SOCIOS si la SOLICITUD asociada no se encuentra en estado "Aprobado" por un Administrador (RNE7).

    - El estado de una solicitud solo puede tomar uno de los siguientes valores: Pendiente, Aprobado o Rechazado (RNE6).

    - El tipo de espacio funerario sólo puede ser Parcela, Panteón o Nicho (RNE9); no se admiten otros valores.

    - La fecha de ingreso de un socio (fec_ing) debe ser siempre menor o igual a la fecha del sistema al momento del alta (RNE8).

    - La fecha de pago (fec_ap) de un núcleo familiar no puede ser anterior a la fecha de ingreso del socio titular (RNE1) y debe ser mayor o igual a la fecha del último pago registrado (RNE3).

    - El monto de todo pago registrado debe ser estrictamente mayor a 0 (RNE4).

    - El pago mensual es obligatorio por grupo familiar (núcleo), independientemente de la cantidad de integrantes que lo compongan.

    - Si el campo 2FA está habilitado para un usuario en SYS_LOG, no se permitirá iniciar sesión sin validar el segundo factor de autenticación (RNE5).

    - Un espacio funerario sólo puede asignarse a un socio si se encuentra disponible; no se permite la doble asignación simultánea de un mismo espacio.
    
**7. Requerimientos de interfaces externas**
7.1 Interfaz de Usuario (UI)
Formularios Web Públicos: El sistema dispondrá de un formulario web de acceso público y optimizado para el perfil Interesado, permitiendo la carga ágil de datos de la entidad SOLICITUD. Contará con validaciones en tiempo real para evitar envíos con campos obligatorios vacíos o tasas de error altas.  
Portal de Socios: Interfaz privada y autenticada mediante contraseña (login_us) para los perfiles de Socio Titular y Adjunto. Permitirá una navegación intuitiva para la consulta del estado de cuenta (SOCIOS, PAGOS) y la edición autogestionada del núcleo familiar (NUCLEAN, INTEGRAN).  
Panel de Administración (Backoffice): Interfaz avanzada y de alta seguridad exclusiva para el perfil Administrador. Diseñada mediante tablas dinámicas y paneles operativos dedicados a la evaluación de solicitudes, asignación de espacios funerarios en el cementerio y registro manual de pagos.  

7.2 Interfaz de HardwareDispositivos de Entrada/Salida: El sistema operará a través de periféricos estándar (teclado, mouse, monitores o pantallas móviles) para la interacción con los formularios y paneles de gestión.  Dispositivos de Impresión: Compatibilidad con impresoras estándar de oficina y de dispositivos móviles para la salida física del comprobante único generado tras el registro de cada pago mensual (comp).  
Soporte de Hardware Especializado: No se requiere interacción con hardware crítico o especializado en el cementerio ni en la sede administrativa. Toda la operación se gestionará mediante terminales de cómputo convencionales.  

7.3 Interfaz de Software
Entorno de Ejecución: El núcleo del sistema estará desarrollado y se ejecutará sobre el intérprete de Python.  Gestor de Base de Datos (DBMS): Interfaz de comunicación directa con el motor de base de datos relacional para dar soporte al modelo de datos definido en el DER (organizado bajo las reglas de la Tercera Forma Normal). El software interactuará con las 8 tablas lógicas identificadas (ESPACIO_FUNERARIA, PERSONAS, SOCIOS, NUCLEAN, ADMINISTRADORES, SOLICITUDES, PAGOS, SYS_LOG).  
Servicio de Correo Electrónico (SMTP): Conexión con un servidor externo de mensajería (o API de correo) para el disparo automático de correos electrónicos de confirmación a los interesados tras registrar exitosamente una solicitud en estado "Pendiente".  

7.4 Interfaz de Comunicaciones
Protocolo de Red Seguro: Toda transferencia de datos entre los clientes (interesados, socios y administradores) y el servidor centralizado se realizará obligatoriamente bajo el protocolo seguro HTTPS/TLS, garantizando el cifrado de datos en tránsito.  
Protocolo de Autenticación de Doble Factor (2FA): Interfaz de comunicación con módulos de seguridad encargados de exigir, registrar y validar el segundo factor de autenticación previo al inicio de sesión. Ningún inicio de sesión prosperará en el sistema sin la respuesta exitosa de esta interfaz.  
Bitácora del Sistema: Interfaz interna de comunicación con la tabla SYS_LOG para almacenar en tiempo real las marcas temporales de éxito o fallo de autenticación de los usuarios (fec_hor_ent, fec_hor_sal).  

**Glosario**
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

**8. Requerimientos Funcionales**
- RF1 – Solicitud de afiliación web. El sistema deberá permitir que un interesado complete y envíe un formulario de solicitud de afiliación.

 - RF1.1: El sistema debe permitir que cualquier interesado complete el formulario de solicitud sin necesidad de autenticarse previamente.
 - RF1.2: Al recibirse el formulario, el sistema debe crear un registro en la tabla SOLICITUDES con estado inicial "Pendiente".
 - RF1.3: El sistema debe validar que los campos obligatorios estén completos antes de permitir el envío y, en caso de error, mostrar un mensaje claro indicando el campo a corregir.

- RF2 – Gestión del núcleo familiar. El sistema deberá permitir al socio titular administrar los integrantes de su núcleo familiar.
 - RF2.1: El sistema debe permitir asociar personas al núcleo familiar indicando el vínculo correspondiente.
 - RF2.2: El sistema debe permitir vincular un socio adjunto con un socio titular dentro del mismo núcleo.
 - RF2.3: El sistema no debe exigir mayoría de edad a los integrantes del núcleo familiar.
 - RF2.4: El sistema debe impedir guardar registros con datos incompletos e indicar qué información falta.

- RF3 – Asignación de espacios funerarios. El sistema deberá permitir asignar un espacio funerario disponible a un socio aprobado.
 - RF3.1: El sistema debe permitir al administrador asignar un espacio funerario a un socio aprobado.
 - RF3.2: El sistema solo debe permitir asignar espacios de tipo parcela, panteón o nicho.
 - RF3.3: El sistema debe registrar la fecha de asignación del espacio.
 - RF3.4: El sistema no debe permitir asignar un mismo espacio funerario a más de un socio.

- RF4 – Registro de pagos mensuales. El sistema deberá permitir registrar los pagos correspondientes a cada núcleo familiar.
 - RF4.1: El sistema debe permitir registrar el núcleo familiar, el monto abonado y el comprobante del pago.
 - RF4.2: El monto del pago debe ser mayor que cero.
 - RF4.3: La fecha del pago no puede ser anterior a la fecha de ingreso del socio ni posterior a la fecha actual.
 - RF4.4: El sistema debe asociar cada pago al administrador que lo registró y almacenar el comprobante correspondiente.

**9. Requerimientos No Funcionales**

A continuación se detallan los requerimientos no funcionales del sistema:

**RNF-01 – Rendimiento** 

Las operaciones principales del sistema deberán responder en menos de 5 segundos en condiciones normales de uso.

**RNF-02 – Concurrencia** 
El sistema deberá soportar al menos 50 usuarios conectados al mismo tiempo sin degradar significativamente su rendimiento.

**RNF-03 – Seguridad** 
El sistema deberá implementar autenticación de doble factor para los usuarios que tengan esta opción habilitada.

**RNF-04 – Respaldo de información** 
El sistema deberá realizar una copia de seguridad de la información cada 24 horas.

**RNF-05 – Usabilidad** 
Un usuario sin capacitación previa deberá poder aprender a utilizar el formulario de afiliación en un tiempo menor a 10 minutos.

**RNF-06 – Manejo de errores** 
El sistema deberá mostrar mensajes de error claros y entendibles para el usuario, evitando mensajes técnicos o provenientes de la base de datos.