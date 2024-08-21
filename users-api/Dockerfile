# Utiliza la imagen base de Alpine Linux con JDK 8
FROM openjdk:8-jdk-alpine

# Establece el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copia todos los archivos de la aplicación al contenedor
COPY . .

# Construye la aplicación usando Maven Wrapper para crear el archivo .jar
RUN ./mvnw clean install

# Define variables de entorno necesarias para la aplicación
ENV JWT_SECRET=PRFT
ENV SERVER_PORT=8083

# Expone el puerto definido para el servicio
EXPOSE ${SERVER_PORT}

# Comando que se ejecuta cuando se inicia el contenedor
CMD ["java", "-jar", "target/users-api-0.0.1-SNAPSHOT.jar"]
