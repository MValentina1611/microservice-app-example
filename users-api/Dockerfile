# Dockerfile para Users API
FROM openjdk:8-jdk-alpine

WORKDIR /app

# Copiar los archivos del proyecto
COPY . .

# Construir la aplicación usando Maven Wrapper
RUN ./mvnw clean install

# Configuraciones de entorno
ENV JWT_SECRET=PRFT
ENV SERVER_PORT=8083

# Exponer el puerto
EXPOSE ${SERVER_PORT}

# Comando para ejecutar la aplicación
CMD ["java", "-jar", "target/users-api-0.0.1-SNAPSHOT.jar"]

