# Sistema-Tunomatico


## 📌 Descripción General del Sistema

**Tunomatico** es una solucion digital orientada a la gestion de turnos para usuarios que requieren atencion en servicios publicos o privados.
Su objetivo personal es **automatizar la asignacion de numeros de atencion**, asi facilitando la organizacion y eliminando tiempos de espera presenciales.

A traves de una interfaz, los usuarios pueden:
- Solicitar un numero de atencion
- Cancelar el numero 
- Consultar el estado de su solicitud

En segundo plano, el sistema administra la agenda disponible y **notifica a los usuarios sobre el estado de sus turnos mediante correo electronico o llamada**

Este sistema ha sido desarrollado aplicando diseño orientado a objetos y empleando patrones de diseño software como:
- Singleton
- Prototype
- Adapter 
- Bridge

Esto asegura una estructura escalable, mantenible y fácilmente integrable con otros sistemas.

---


## 🎯 Diagrama de Casos de Uso

![Caso de uso (1) drawio](https://github.com/user-attachments/assets/2a734186-e9d4-430f-ba85-976ac52151a7)


---

## 🧠 Descripción y Justificación del Diagrama de Casos de Uso

### 👥 Actores principales

    - Usuario: Interactúa con la plataforma para gestionar su atención.
    - Administrador: Mantiene la disponibilidad y gestiona los turnos existentes.
    - Sistema de Notificaciones: Un sistema externo encargado de enviar notificaciones a los usuarios.

--- 

### 🧑 Funcionalidades del Usuario

    - Solicitar un turno, que es la acción principal del sistema.
    - Ver el estado de su turno, para confirmar si sigue vigente o ha sido modificado.
    - Cancelar un turno, lo cual está modelado como una extensión (<<extend>>) del caso "Solicitar turno", ya que cancelar es una opción posterior dentro del flujo de turnos.
    
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


---


## 🧩 Diagrama de Clases UML

![diagrama de clases drawio (2)](https://github.com/user-attachments/assets/01a77d5e-4da8-42f3-8ab7-b87b9d0183db)


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
Esto evita duplicación de lógica.

#### 🔹 `Prototype` – Clase Turno
El patrón Prototype permite **clonar turnos existentes**, útil si un usuario desea reprogramar o repetir un número previamente asignado.

#### 🔹 `Adapter` – Clase NotificaciónAdapter
Este adaptador sirve como **puente entre el sistema interno y un servicio externo** (como una API de llamadas o correos).  
Permite integrar funcionalidades externas.

#### 🔹 `Bridge` – Clases Notificación / NotificaciónEmail / NotificaciónLlamada
Se utiliza para **desacoplar la abstracción de la notificación** (`Notificación`) de sus implementaciones (`Email`, `Llamada`).  

---

> ✅ **Conclusión**: El diseño del sistema refleja una arquitectura profesional y mantenible, con uso efectivo de patrones de diseño clásicos.


---


## 🏗️ Diagrama de Implementación UML

![Diagrama de implementacion drawio](https://github.com/user-attachments/assets/c889d3c5-3327-430e-98a1-e605d00e3f25)

---

### 🧱 Arquitectura Física del Sistema

El sistema **Tunomático** está desplegado en una arquitectura de múltiples nodos conectados entre si. Cada nodo contiene los componentes que le corresponden para garantizar un funcionamiento modular, escalable y mantenible.

---

### 🔹 <<nodo>> Cliente Web

- **Componentes**:
  - `interfaz.html` – estructura visual del sitio
  - `app.js` – lógica en el navegador
  - `styles.css` – estilos y diseño

---

### 🔹 <<nodo>> Servidor de Aplicaciones

- **Componentes**:
  - `ControladorTurnos` → `<<Singleton>>`: centraliza la gestión de turnos.
  - `Turno` → `<<Prototype>>`: permite clonar turnos fácilmente.
  - `Agenda` → gestiona disponibilidad horaria.
  - `Notificación` / `NotificaciónAdapter` → `<<Bridge>>` y `<<Adapter>>`: separan canal de envío e integran APIs externas.

  ---

### 🔹 <<nodo>> Base de Datos

- **Componentes**:
  - `turnos.db` – turnos registrados
  - `usuarios.db` – datos de los usuarios
  - `agenda.db` – horarios disponibles

---

### 🔹 <<nodo>> Servidor REST

- **Componentes expuestos**:
  - `/API/turnos`
  - `/API/disponibilidad`

---

### 🔹 <<nodo>> Servidor de Notificaciones

- **Conexión**: vía REST API desde el `NotificaciónAdapter`
- Sistema externo encargado de enviar notificaciones al usuario, ya sea por correo o llamada.

---

### 🧠 Patrones de Diseño Representados

| Patrón       | Ubicación                         | Propósito                                                                 |
|--------------|-----------------------------------|--------------------------------------------------------------------------|
| Singleton    | `ControladorTurnos`               | Una única instancia para controlar lógica de turnos                      |
| Prototype    | `Turno`                           | Clonación de objetos turno                                               |
| Adapter      | `NotificaciónAdapter`             | Adaptación con servicios externos de notificación                        |
| Bridge       | `Notificación`, `Email`, `Llamada`| Separar lógica del tipo de canal utilizado                               |

---

> ✅ **Conclusión**: Este diagrama refleja una arquitectura alineada con buenas prácticas de ingeniería de software. La distribución de responsabilidades y el uso correcto de patrones aseguran que el sistema sea robusto, mantenible y fácilmente extensible.
