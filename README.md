# 📝 Microservice TODO Application

## 🌟 Project Summary
This application is an example of a microservice architecture designed to teach the fundamentals of distributed systems. The application, although a simple TODO list, consists of multiple microservices written in different languages and frameworks, allowing experimentation with various tools and environments.

### 🚀 Dockerization of the Project
The application is fully dockerized, meaning each microservice runs in its own container. This ensures that the development environment is consistent and reproducible, no matter where it is run.

---

## 📦 Components

- **Users API:** Spring Boot application for managing user profiles.
- **Auth API:** Go application that provides authentication functionality using JWT.
- **TODOs API:** Node.js application that handles CRUD operations for tasks.
- **Log Message Processor:** Message processor written in Python that reads and processes logs from Redis.
- **Frontend:** Vue.js application that serves as the user interface.

---

## 🐳 Dockerfiles and Docker Compose

### 🏗️ Dockerfiles

Each microservice has its own Dockerfile that defines how the container image will be built:

1. **Users API:** 
   - **Base:** `openjdk:8-jdk-alpine`.
   - **Key Command:** `./mvnw clean install` to build the Java application.

2. **Auth API:** 
   - **Base:** `golang:1.18.2` (build stage) and `gcr.io/distroless/base-debian10` (final image).
   - **Key Command:** `go build -o auth-api` to compile the Go application.

3. **Frontend:** 
   - **Base:** `node:8.17.0`.
   - **Key Command:** `npm run build` to build the Vue.js application.

4. **TODOs API:** 
   - **Base:** `node:8.17.0`.
   - **Key Command:** `npm install` to install dependencies.

5. **Log Message Processor:** 
   - **Base:** `python:3.6`.
   - **Key Command:** `pip install -r requirements.txt` to install Python dependencies.

### 🛠️ Docker Compose

Docker Compose simplifies the execution of the application by orchestrating all containers from a single file (`docker-compose.yml`). This includes:

- **Service Definitions:** Each microservice is defined as a service in the Compose file.
- **Port Mapping:** Allows access to services from the host.
- **Environment Variables:** Configures necessary parameters for each service.
- **Networks:** All services are connected to an internal network (`app-network`), allowing communication between them in isolation from the rest of the system.

---
## 🔧 Useful Commands

- **Build Images:**
  ```bash
  docker-compose build

- **Start all services:**
  ```bash
  docker-compose up

- **Stop and remove containers:**
  ```bash
  docker-compose down
---

## 🕸️ Network Architecture

Microservices communicate with each other over HTTP through an internal network (bridge network) defined in Docker Compose. Redis acts as a message broker for communication between the TODOs API service and the Log Message Processor.

---

## 🌐 Services and Exposed Ports

* **👤 Users API:** Port `8083` - Provides user management functionality.
* **🔐 Auth API:** Port `8000` - Responsible for authentication and authorization.
* **📝 TODOs API:** Port `8082` - Manages CRUD operations for tasks.
* **📄 Log Message Processor:** Does not expose a port as its function is to process messages internally.
* **🖥️ Frontend:** Port `8080` - User interface interacting with the microservices.

Take a look at the components diagram that describes them and their interactions.

![microservice-app-example](/arch-img/Microservices.png)

*Source: [https://github.com/bortizf/microservice-app-example]()*

This the deploy diagram of the application

![deploydiagram](/arch-img/Msa-Depd.drawio.png) 

---

## 📊 Monitoring

For monitoring the application, three main tools are used: **Prometheus**, **Grafana**, and **cAdvisor**. Here’s how these tools interact to provide a comprehensive view of container status and performance.

**:owl: cAdvisor:**
- **Role:** cAdvisor is responsible for collecting performance and resource metrics from Docker containers. These metrics include CPU, memory, network, and disk usage, among others.
- **Functioning:** cAdvisor exposes an API with these metrics that Prometheus can scrape.

**:trident: Prometheus:**
- **Role:** Prometheus acts as a metric storage and querying system. It collects the metrics exposed by cAdvisor and stores them in a time-series database.
- **Functioning:** Prometheus performs periodic scraping of metrics exposed by cAdvisor and stores this data. Grafana then queries Prometheus to visualize this data.

**:flying_disc: Grafana:**
- **Role:** Grafana is a visualization platform that allows creating dashboards and graphs from metrics stored in Prometheus.
- **Functioning:** Grafana connects to Prometheus as a data source and uses PromQL queries to retrieve and display information in charts and tables.

**:electric_plug: Exposed Ports:**
- **cAdvisor:** Exposes metrics on port `8081`.
- **Prometheus:** Exposes its web interface on port `9090`.
- **Grafana:** Exposes its web interface on port `3000`.

*Examples of Prometheus Queries:*
- **CPU Usage per Container:**
  ```promql
  rate(container_cpu_usage_seconds_total{image!="", container_label_com_docker_swarm_service_name!="", container_label_com_docker_swarm_task_name=""}[5m])

**:chart_with_downwards_trend:	Grafana's dashboard:** 
![Cache](/arch-img/cpu-containers.png)

![Memory](/arch-img/memory-usage.png)

![Cache](/arch-img/cpu-containers.png)

![Network-traffic](/arch-img/network-traffic.png)

*Source: [http://localhost:3000/d/4dMaCsRZz/docker-container-and-host-metrics?orgId=1&from=now-6h&to=now-4h&viewPanel=19&editPanel=19]()*

As shown in the Grafana charts, the application was up but inactive for an extended period, until before 17:40. After that, I started making requests by logging in with each user and editing the to-do list, which is when a significant change in the metrics is observed. For example, in the CPU usage per container, there is a noticeable increase in CPU usage by the `users_api` and `todos_api` containers due to the dynamic nature of the requests being made. In the rest of the charts, we see a similar behavior, with an increase in metrics when more requests are made. Another interesting chart is the network traffic across the entire node, where we see a significant rise in the sending and receiving of information.



---
## :bookmark_tabs: Conclusion
This project has been a valuable learning experience, providing practical insights into designing and managing microservices, containerizing applications with Docker, and setting up effective monitoring with Prometheus, Grafana, and cAdvisor. We’ve gained hands-on skills in application deployment, internal networking, and performance monitoring, which are essential for modern software development. Overall, this project has enhanced our understanding of how to build and maintain scalable, distributed systems and highlighted the importance of thorough documentation and monitoring.

---

## 🛠️ Technological Dependencies

* **☕ Java (openJDK8)**
* **🐹 Go (1.18.2)**
* **🟩 Node (8.17.0) & NPM (6.13.4)**
* **📝 Redis (7.0)**
* **🐍 Python (3.6) & Pip**
  

