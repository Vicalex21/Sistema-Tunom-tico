# Sistema-Tunomatico


## 📌 Descripción General del Sistema

**Tunomatico** es una solucion digital orientada a la gestion de turnos para usuarios que requieren atencion en servicios publicos o privados.
Su objetivo personal es **automatizar la asignacion de numeros de atencion**, asi facilitando la organizacion y eliminando tiempos de espera presenciales 

A traves de una interfaz, los usuarios pueden:
- Solicitar un numero de atencion
- Cancelar el numero 
- Consultar el estado de su solicitud

En segundo plano, el sistema administra la agenda disponible y **notifica a los usuarios sobre el estado de sus turnos mediante correo electronico o llamada**

Este sistema ha sido desarrollado aplicando buenas prácticas de diseño orientado a objetos y empleando patrones de diseño software como:
- Singleton
- Prototype
- Adapter 
- Bridge

Esto asegura una estructura escalable, mantenible y fácilmente integrable con otros sistemas.

---

aqui va la imagen

## 📌 Diagrama de Casos de Uso

> 📷 *[Aquí debe insertarse la imagen del diagrama de casos de uso]*

---

## 🧠 Descripción y Justificación del Diagrama de Casos de Uso

### 👥 Actores principales

    - Usuario: Interactúa con la plataforma para gestionar su atención.
    - Administrador: Mantiene la agenda de disponibilidad y gestiona los turnos existentes.
    - Sistema de Notificaciones: Un sistema externo encargado de enviar notificaciones automáticas a los usuarios.

--- 

### 🧑 Funcionalidades del Usuario

    - Solicitar un turno, que es la acción principal del sistema.
    - Ver el estado de su turno, para confirmar si sigue vigente o ha sido modificado.
    - Cancelar un turno, lo cual está modelado como una extensión (<<extend>>) del caso "Solicitar turno", ya que cancelar es una opción posterior o alternativa dentro del flujo de turnos.
    
📌 El caso **"Cancelar turno"** extiende a **"Notificar usuario"**, indicando que al cancelar un turno, se puede enviar automáticamente una notificación al usuario.

---

### 👨‍💼 Administrador

El administrador tiene acceso a:

    - Administrar disponibilidad, gestionando los horarios y cupos disponibles.
    - Este caso incluye (include) a "Ver todos los turnos", ya que para gestionar la agenda, el administrador necesita consultar los turnos previamente asignados.

---

### 🔔 Sistema de Notificaciones

- El sistema externo participa en el caso de uso **"Notificar usuario"**  
- Este caso está modelado como una **extensión** (`<<extend>>`) del proceso de cancelación, ya que solo se invoca en ciertos escenarios (por ejemplo, al anular un turno)

---

✅ **Conclusión**: Este modelo refleja de forma clara la lógica condicional y reutilizable del sistema, mediante relaciones `<<extend>>` para acciones opcionales y `<<include>>` para acciones obligatorias reutilizables.


## 🧩 Diagrama de Clases UML


🖼️ **Aquí debes insertar la imagen del diagrama de clases UML**  
 *(Nombre del archivo sugerido: `diagrama_clases_tunomatico.png`)*

---

### 🧠 Descripción General del Diagrama

El siguiente diagrama muestra la estructura interna del sistema Tunomático, detallando las clases principales, sus atributos, métodos y relaciones.

El sistema fue diseñado aplicando principios de **orientación a objetos** y empleando los siguientes **patrones de diseño**: `Singleton`, `Prototype`, `Adapter` y `Bridge`.

Las clases más importantes representadas son:

- **Usuario**: contiene los datos básicos del usuario que solicita un turno.
- **Turno**: representa un número de atención asociado a un usuario.
- **Agenda**: mantiene la disponibilidad horaria del sistema.
- **ControladorTurnos**: clase central que administra la creación y cancelación de turnos.
- **Notificación**: clase abstracta para el envío de notificaciones.
- **NotificaciónEmail / NotificaciónLlamada**: implementaciones concretas del sistema de notificación.
- **NotificaciónAdapter**: adapta servicios externos de notificación.

---

### 🔧 Justificación de Patrones Aplicados

#### 🔹 `Singleton` – Clase ControladorTurnos
Se aplica para garantizar que exista **una única instancia** que gestione toda la lógica de turnos del sistema.  
Esto evita duplicación de lógica y asegura consistencia global.

#### 🔹 `Prototype` – Clase Turno
El patrón Prototype permite **clonar turnos existentes**, útil si un usuario desea reprogramar o repetir un número previamente asignado.

#### 🔹 `Adapter` – Clase NotificaciónAdapter
Este adaptador sirve como **puente entre el sistema interno y un servicio externo** (como una API de llamadas o correos).  
Permite integrar funcionalidades externas sin acoplarse directamente a su implementación.

#### 🔹 `Bridge` – Clases Notificación / NotificaciónEmail / NotificaciónLlamada
Se utiliza para **desacoplar la abstracción de la notificación** (`Notificación`) de sus implementaciones (`Email`, `Llamada`).  
Esto permite agregar nuevos tipos de notificación sin modificar la lógica central del sistema.

---

> ✅ **Conclusión**: El diseño del sistema refleja una arquitectura profesional, reutilizable y mantenible, con uso efectivo de patrones de diseño clásicos.

