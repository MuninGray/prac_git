# prac_git
Un repositorio creado para el Ejercicio Colaborativo de GitHub

Entorno operativo:

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


Reglas de negocio:

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
