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
