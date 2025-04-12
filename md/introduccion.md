# Anexo - Introducción al Diseño Orientado a Objetos

La Programación Orientada a Objetos (POO) es un paradigma de programación que organiza el código en torno a "objetos", que son instancias de "clases" que encapsulan datos y comportamientos relacionados. Es importante porque permite modularidad, reutilización de código, escalabilidad y mantenimiento eficiente de software.

## Los cuatro fundamentos de POO

* **Encapsulamiento**:  
Protege la información sensible y permite el acceso solo a usuarios autorizados a travez de metodos específicos.

    * **Ejemplo**  
    Los datos de contacto de pacientes y médicos deben ser accesibles unicamente por el personal autorizado.
    
        | Paciente | Medico | Administrativo |
        |:--------------------------------:|:--------------------------:|:-------------------------:|
        | **Nombre** _publico_             | **Nombre** _publico_       | _verObraSocial_ (Paciente) |
        | **Datos Obra Social** _privado_  | **Especialidad** _publico_ | _contactarMedico_(Medico) |
        | **Contacto** _privado_           | **Contacto** _privado_     |

* **Herencia**:  
Permite que una clase (subclase) adquiera las propiedades y comportamientos de otra (superclase).

    * **Ejemplo**  
     Se puede tener una clase base "Persona" de la que derivan "Paciente" y "Médico" con atributos específicos.

        | Persona | Medico | Paciente |
        |:---------:|:-----------:|:-----------------:|
        | Nombre   | Matricula    | Obra Social       |
        | Apellido | Especialidad | Historial Clinico |
        | Contacto | Pacientes    | 

* **Polimorfismo**:  
Permite que diferentes objetos respondan a la misma acción de manera distinta.

    * **Ejemplo**  
    Una notificación puede enviarse tanto aun medico com a un paciente pero que pueden tener distinta informacion.

        | Notificacion | Medico _subclase_ | Paciente _subclase_ |
        |:----------------------:|:----------------------:|:----------------------:|
        | _enviarNotificacion()_ | _enviarNotificacion()_ | _enviarNotificacion()_ |

* **Abstracción**:  
Oculta detalles complejos y solo expone lo necesario para el uso de un objeto.

    * **Ejemplo**  
     Un turno se confirma sin necesidad de saber como es el proceso por detras.

        | Turno |
        |:-------------:|
        | _confirmar()_ |
        | _cancelar()_  |
        | _modificar()_ |

## Requisitos iniciales del sistema

1. Los pacientes y profesionales de la salud deben poder registrarse en el sistema.
2. El sistema debe permitir crear turnos médicos.
3. El sistema debe proteger los datos de los usuarios.
4. Se debe mantener un historial de turnos para cada paciente y profesional.
5. El sistema debe enviar notificaciones automáticas sobre cambios en los turnos a pacientes y profesionales.

## Casos de uso

* **Registro de Usuarios**
    - Actores: Pacientes, Medicos, Administradores
    - Descripción breve: Permite a los usuarios registrarse en el sistema proporcionando sus datos personales.
    - Flujo principal de eventos:
        1. El usuario accede a la opción "Registrarse" desde la pantalla de inicio.
        2. Selecciona su rol (paciente, médico o administrador).
        3. Se despliega el formulario correspondiente al rol elegido.
        4. El usuario completa todos los campos requeridos (nombre, DNI, correo, teléfono, etc.).
        5. En caso de ser médico, también se solicita especialidad, matrícula y horarios disponibles.
        6. El sistema valida que el correo electrónico no esté registrado previamente.
        7. Se validan los formatos de correo, teléfono y otros campos obligatorios.
        8. Si todo está correcto, se genera un nuevo registro en la base de datos.
        9. Se crean las credenciales de acceso.
        10. El sistema muestra un mensaje de confirmación y redirige al inicio de sesión.

    **PRECONDICIONES**: El usuario no debe estar registrado previamente.  
    **POSTCONDICIONES**: El usuario queda registrado en el sistema.

* **Creacion de Turnos**
    - Actores: Paciente, Administrador
    - Descripción breve: Se asigna un turno a un paciente con un médico según disponibilidad.
    - Flujo principal de eventos:
        1. El paciente o administrador inicia sesión en el sistema.
        2. Accede a la sección "Solicitar turno".
        3. Selecciona una especialidad médica.
        4. El sistema muestra los médicos disponibles según la especialidad.
        5. El usuario elige un médico.
        6. El sistema muestra las fechas y horarios disponibles del médico.
        7. El usuario selecciona fecha y hora deseada.
        8. El sistema verifica si ya existe otro turno en ese horario.
        9. Si está libre, guarda el turno en la agenda con estado "pendiente" o "confirmado".
        10. Se envían notificaciones automáticas al paciente y al médico.
    
    **PRECONDICIONES**: El paciente y el médico deben estar registrados y el medico debe tener el horario disponible.  
    **POSTCONDICIONES**: Se crea el turno en la base de datos y se notifica a los involucrados.

* **Cancelación de turno**
    - Actores: Paciente, Administrador
    - Descripción breve: Un turno es cancelado.
    - Flujo principal de eventos:
        1. El usuario inicia sesión en el sistema.
        2. Accede a la sección "Mis turnos" sie s Paciente o "Agenda" si es Administrativo.
        3. Visualiza la lista de turnos pendientes o confirmados.
        4. Selecciona el turno que desea cancelar.
        5. Hace clic en "Cancelar turno".
        6. El sistema solicita confirmación de la acción.
        7. El usuario confirma la cancelación.
        8. El sistema cambia el estado del turno a “cancelado”.
        9. Se libera el horario en la agenda del médico.
        10. Se envían notificaciones al paciente, médico y/o administrador.
    
    **PRECONDICIONES**: El turno debe existir y no haber ocurrido.  
    **POSTCONDICIONES**: El turno es marcado como cancelado y notificado a los involucrados.

* **Notificaciones automáticas**
    - Actores: Sistema
    - Descripción breve: El sistema envía notificaciones sobre cambios en los turnos.
    - Flujo principal de eventos:
        1. El sistema detecta un cambio en un turno (alta, modificación, cancelación o confirmación).
        2. Identifica los usuarios involucrados (paciente, médico).
        3. Verifica los datos de contacto disponibles (correo o teléfono).
        4. Genera un mensaje personalizado según el tipo de cambio.
        5. Elige el canal de envío (correo o mensaje de texto).
        6. Envía la notificación al paciente.
        7. Envía la notificación al médico.
        8. Registra en el sistema que la notificación fue enviada.
        9. Si hay error de entrega, se reintenta o se guarda como pendiente.
        10. Se registra la acción en el historial de actividad del sistema.

    **PRECONDICIONES**: El turno debe existir en el sistema.  
    **POSTCONDICIONES**: Se notifican los cambios a los usuarios involucrados.

* **Confirmacion de turno**
    - Actores: Paciente
    - Descripcion breve: El paciente debe confirmar un turno.
    - Flujo principal de eventos:
        1. El paciente inicia sesión en el sistema.
        2. Accede a la sección "Mis turnos".
        3. El sistema muestra los turnos en estado "a confirmar".
        4. El paciente selecciona un turno de la lista.
        5. Hace clic en la opción "Confirmar turno".
        6. El sistema solicita confirmación final de la acción.
        7. El paciente acepta la confirmación.
        8. El sistema actualiza el estado del turno a “confirmado”.
        9. Se envía una notificación automática al médico.
        10. Se registra el cambio en el historial del turno y del paciente.

    **PRECONDICIONES**: El paciente debe tener aunque sea un turno asignado.  
    **POSTCONDICIONES**: La fecha o el horario de un turno es modificada.

## Boceto inicial del diseño de clases
La clase _Usuario_ es una clase padre que se divide en 3 subclases, _Medico_, _Paciente_ y _Administrador_. De estas tres, cada una tiene distintos atributos y metodos que son tareas que puede desempeñar cada usuario.  
La clase principal o con "mas protagonismo" es la clase _Turno_ que es la que tiene todos los metodos para que los usuarios gestionen los turnos correspondientes dependiendo los permisos, esta clase es la ecargada de registrar, confirmar, cancelar, modificar un turno y tiene todos los datos del mismo, el medico y el paciente asociados, la fecha y hora del turno y la duracion de forma que no se superpongan turnos, tambien esta el estado (cancelado, confirmado, modificado). De esta clase, depende tambien la clase _Agenda_ que tiene una lista de turnos historicos y turnos futuros agendados, y el metodo cambiarDia, que lo que haria seria agarrar todos los turnos que pasaron en un dia y pasarlos de futuros a historicos. Por ultimo esta la clase _Notificaciones_ que guarda los datos de una notificacion (a quien enviarsela, la razon de la notificacion, etc. ) y lo que hace es notificar al paciente.
![](imagenes/image.png)

