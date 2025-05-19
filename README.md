# Sistema-Tunomatico


📌 Descripción General del Sistema

El sistema Tunomatico es una solucion digital orientada a la gestion de turnos para usuarios que requieren atencion en servicios publicos o privados.
Su objetivo personal es automatizar la asignacion de numeros de atencion, asi facilitando la organizacion y eliminando tiempos de espera presenciales 

A traves de una interfaz, los usuarios podran solicitar un numero de atencion, cancelar el numero y consultar el estado de su solicitud. En segundo plano, el sistema administra la agenda disponible
y notifica a los usuarios sobre el estado de sus turnos mediante correo electronico o llamada

Este sistema ha sido desarrollado aplicando buenas prácticas de diseño orientado a objetos y empleando patrones de diseño software como Singleton, Prototype, Adapter y Bridge, lo que asegura una estructura escalable, mantenible y fácilmente integrable con otros sistemas.

aqui va la imagen

Diagrama de caso de uso
Descripción y Justificación del Diagrama
El sistema Tunomático contempla tres actores principales:
    - Usuario: Interactúa con la plataforma para gestionar su atención.
    - Administrador: Mantiene la agenda de disponibilidad y gestiona los turnos existentes.
    - Sistema de Notificaciones: Un sistema externo encargado de enviar notificaciones automáticas a los usuarios.

El usuario puede:
    - Solicitar un turno, que es la acción principal del sistema.
    - Ver el estado de su turno, para confirmar si sigue vigente o ha sido modificado.
    - Cancelar un turno, lo cual está modelado como una extensión (<<extend>>) del caso "Solicitar turno", ya que cancelar es una opción posterior o alternativa dentro del flujo de turnos.
    
A su vez, el caso "Cancelar turno" extiende a "Notificar usuario", lo que implica que cuando se cancela un turno, opcionalmente se activa la acción de enviar una notificación al usuario.

El administrador tiene acceso a:
    - Administrar disponibilidad, gestionando los horarios y cupos disponibles.
    - Este caso incluye (include) a "Ver todos los turnos", ya que para gestionar la agenda, el administrador necesita consultar los turnos previamente asignados.

El sistema de notificaciones interactúa mediante el caso de uso "Notificar usuario", el cual también está modelado como una extensión (extend) del proceso de cancelación, ya que se invoca solo en ciertos escenarios, como al anular un turno.

Este modelo permite reflejar la lógica condicional y reutilizable del sistema, empleando correctamente relaciones extend para acciones opcionales y include para acciones obligatorias compartidas por múltiples casos de uso.
