# Sistema-Tunomatico


## 📌 Descripción General del Sistema

**Tunomático** es una solución digital que permite a personas sacar turnos fácilmente en lugares donde se necesita atención, como centros médicos o instituciones públicas, asi facilitando la organizacion y eliminando tiempos de espera presenciales.


A traves de una interfaz, los usuarios pueden:
- Solicitar un numero de atencion
- Cancelar el numero 
- Consultar el estado de su solicitud

Mientras tanto, el sistema se encarga de mantener actualizada la agenda y de **enviar notificaciones al usuario**, ya sea por correo o por llamada, cuando algo cambia.

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

### 👥 Actores del sistema:
    - Usuario: usa la plataforma para pedir y revisar turnos.
    - Administrador: se encarga de mantener actualizada la agenda de turnos.
    - Sistema de Notificaciones: servicio externo que envía mensajes automáticos.

--- 

### 🧑 Funcionalidades del Usuario

    - Pedir un turno, que es la función principal.
    - Ver el estado de su turno (si sigue agendado, si fue cancelado, etc.).
    - Cancelar un turno, acción que puede llevar a enviar una notificación automática al usuario. Por eso está conectada con “Notificar usuario”.

    
📌 El caso **"Cancelar turno"** extiende a **"Notificar usuario"**, indicando que al cancelar un turno, se puede enviar automáticamente una notificación al usuario.

---

### 👨‍💼 Administrador

El administrador tiene acceso a:

    - Administrar disponibilidad, gestionando los horarios y cupos disponibles.
    - Este caso incluye (include) a "Ver todos los turnos", ya que para gestionar la agenda, el administrador necesita consultar los turnos previamente asignados.

---


### 🔔 Sistema de Notificaciones

    - Solo entra en acción si se **cancela un turno**, para **avisar automáticamente** al usuario por correo o llamada.

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
- **Agenda**: gestiona la disponibilidad de horarios.
- **ControladorTurnos**: clase central que administra la creación y cancelación de turnos.
- **Notificación**: define cómo se debe notificar a un usuario.
- **NotificaciónEmail / NotificaciónLlamada**: formas específicas de enviar notificaciones.
- **NotificaciónAdapter**: se usa para conectar con servicios externos (como una API).

---

### 🔧 Justificación de Patrones Aplicados

#### 🔹 `Singleton` – Clase ControladorTurnos
asegura que solo exista una única instancia que controle los turnos.

#### 🔹 `Prototype` – Clase Turno
El patrón Prototype permite **clonar turnos existentes**, útil si un usuario desea reprogramar o repetir un número previamente asignado.

#### 🔹 `Adapter` – Clase NotificaciónAdapter
adapta el sistema a servicios externos, como el envío de correos o llamadas.

#### 🔹 `Bridge` – Clases Notificación / NotificaciónEmail / NotificaciónLlamada
permite cambiar o agregar tipos de notificación sin afectar el resto del sistema.

---

✅ **Conclusión**: Esta estructura hace que el sistema sea claro, bien dividido en funciones, y fácil de mantener o ampliar más adelante.


---


## 🏗️ Diagrama de Implementación UML

![Diagrama de implementacion drawio](https://github.com/user-attachments/assets/c889d3c5-3327-430e-98a1-e605d00e3f25)

---

### 🧱 Arquitectura Física del Sistema

El sistema **Tunomático** está desplegado en una arquitectura de múltiples nodos conectados entre si. Cada nodo contiene los componentes que le corresponden para garantizar un funcionamiento modular, escalable y mantenible.

---

### 🔹 nodo Cliente Web

- **Componentes**:
  - `interfaz.html` – estructura visual del sitio
  - `app.js` – lógica en el navegador
  - `styles.css` – estilos y diseño

---

### 🔹 nodo Servidor de Aplicaciones

- **Componentes**:
  - `ControladorTurnos` → `<<Singleton>>`: centraliza la gestión de turnos.
  - `Turno` → `<<Prototype>>`: permite clonar turnos fácilmente.
  - `Agenda` → gestiona disponibilidad horaria.
  - `Notificación` / `NotificaciónAdapter` → `<<Bridge>>` y `<<Adapter>>`: separan canal de envío e integran APIs externas.

  ---

### 🔹 nodo Base de Datos

- **Componentes**:
  - `turnos.db` – turnos registrados
  - `usuarios.db` – datos de los usuarios
  - `agenda.db` – horarios disponibles

---

### 🔹 nodo Servidor REST

- **Componentes**:
  - `API/turnos`
  - `API/disponibilidad`

---

### 🔹 nodo Servidor de Notificaciones

- **Conexión**: vía REST API desde el `NotificaciónAdapter`
- Sistema externo encargado de enviar notificaciones al usuario, ya sea por correo o llamada.

---

### 🧠 Patrones de Diseño Representados

| Patrón       | Ubicación                         | Propósito                                                                |
|--------------|-----------------------------------|--------------------------------------------------------------------------|
| Singleton    | `ControladorTurnos`               | Asegura un único controlador global de turnos                            |
| Prototype    | `Turno`                           | Permite clonar turnos fácilmente                                         |
| Adapter      | `NotificaciónAdapter`             | Conecta el sistema con APIs externas de notificación                     |
| Bridge       | `Notificación`, `Email`, `Llamada`| Separar lógica del tipo de canal utilizado                               |

---

✅ **Conclusión**: Este diagrama muestra una estructura bien pensada y organizada. Cada parte del sistema cumple un rol claro, y el uso de patrones de diseño ayuda a que el sistema sea más fácil de entender, mantener y mejorar en el futuro.

---

## 💡 Reflexiones Finales

El desarrollo del sistema **Tunomático** permitió aplicar de manera práctica los principios de diseño orientado a objetos, junto con la integración de patrones de diseño clásicos como `Singleton`, `Prototype`, `Adapter` y `Bridge`.

Durante el proceso de modelado se vio distintas etapas fundamentales del sistema:

    - Se identificaron claramente los actores y funciones del sistema mediante el diagrama de casos de uso.
    - Se diseñaron clases bien estructuradas y con responsabilidades definidas en el diagrama de clases.
    - Se representó cómo el sistema se instala y se comunica en la vida real con el diagrama de implementación.

Aplicar patrones como `Singleton`, `Prototype`, `Adapter` y `Bridge` no solo ayudó a mejorar el diseño, sino también a pensar en cómo hacer que el sistema sea fácil de mantener, escalar y entender por otros desarrolladores.


Además, el uso de herramientas UML para representar gráficamente las decisiones permitió visualizar mejor las conexiones entre capas del sistema y evaluar de forma anticipada la calidad del diseño.


