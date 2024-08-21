# 📝 Microservice TODO Application

## 🌟 Resumen del Proyecto
Esta aplicación es un ejemplo de arquitectura de microservicios diseñada para enseñar los fundamentos de sistemas distribuidos. La aplicación, aunque es una simple lista de tareas (TODO), está compuesta por múltiples microservicios escritos en diferentes lenguajes y frameworks, lo que permite experimentar con diversas herramientas y entornos.

### 🚀 Dockerización del Proyecto
La aplicación está completamente dockerizada, lo que significa que cada microservicio se ejecuta en un contenedor independiente. Esto asegura que el entorno de desarrollo sea consistente y reproducible, sin importar dónde se ejecute.

---

## 📦 Componentes

- **Users API:** Aplicación Spring Boot para gestionar perfiles de usuario.
- **Auth API:** Aplicación Go que proporciona funcionalidad de autenticación mediante JWT.
- **TODOs API:** Aplicación Node.js que maneja operaciones CRUD para las tareas.
- **Log Message Processor:** Procesador de mensajes en cola, escrito en Python, que lee y procesa logs desde Redis.
- **Frontend:** Aplicación Vue.js que sirve como interfaz de usuario.

---

## 🐳 Dockerfiles y Docker Compose

### 🏗️ Dockerfiles

Cada microservicio tiene su propio Dockerfile, que define cómo se construirá la imagen del contenedor:

1. **Users API:** 
   - **Base:** `openjdk:8-jdk-alpine`.
   - **Comando clave:** `./mvnw clean install` para construir la aplicación Java.

2. **Auth API:** 
   - **Base:** `golang:1.18.2` (etapa de construcción) y `gcr.io/distroless/base-debian10` (imagen final).
   - **Comando clave:** `go build -o auth-api` para compilar la aplicación Go.

3. **Frontend:** 
   - **Base:** `node:8.17.0`.
   - **Comando clave:** `npm run build` para construir la aplicación Vue.js.

4. **TODOs API:** 
   - **Base:** `node:8.17.0`.
   - **Comando clave:** `npm install` para instalar dependencias.

5. **Log Message Processor:** 
   - **Base:** `python:3.6`.
   - **Comando clave:** `pip install -r requirements.txt` para instalar dependencias Python.

### 🛠️ Docker Compose

Docker Compose simplifica la ejecución de la aplicación al orquestar todos los contenedores desde un solo archivo (`docker-compose.yml`). Esto incluye:

- **Definición de servicios:** Cada microservicio se define como un servicio en el archivo Compose.
- **Mapeo de puertos:** Permite el acceso a los servicios desde el host.
- **Variables de entorno:** Configura los parámetros necesarios para cada servicio.
- **Redes:** Todos los servicios están conectados a una red interna (`app-network`), que permite la comunicación entre ellos de forma aislada del resto del sistema.


---
## 🔧 Comandos Útiles

Aquí algunos comandos básicos para trabajar con Docker en este proyecto:

- **Construir imágenes:**
  ```bash
  docker-compose build

- **Levantar todos los servicios:**
  ```bash
  docker-compose up

- **Detener y eliminar contenedores:**
  ```bash
  docker-compose down
---

## 🕸️ Arquitectura de Red

Los microservicios se comunican entre sí mediante HTTP a través de una red interna (bridge network) definida en Docker Compose. Redis actúa como un broker de mensajes para la comunicación entre el servicio de TODOs API y el Log Message Processor.

---

## 🌐 Servicios y Puertos Expuestos

* **👤 Users API:** Puerto `8083` - Proporciona la funcionalidad de gestión de usuarios.
* **🔐 Auth API:** Puerto `8000` - Responsable de la autenticación y autorización.
* **📝 TODOs API:** Puerto `8082` - Gestiona las operaciones sobre las tareas.
* **📄 Log Message Processor:** No expone un puerto ya que su función es procesar mensajes internamente.
* **🖥️ Frontend:** Puerto `8080` - Interfaz gráfica que interactúa con los microservicios.
  
Take a look at the components diagram that describes them and their interactions.

![microservice-app-example](/arch-img/Microservices.png)

*Tomado del repositorio origen [https://github.com/bortizf/microservice-app-example]()*

---
## 🛠️ Dependencias Tecnológicas

* **☕ Java (openJDK8)**
* **🐹 Go (1.18.2)**
* **🟩 Node (8.17.0) & NPM (6.13.4)**
* **📝 Redis (7.0)**
* **🐍 Python (3.6) & Pip**
