# Utiliza la imagen de Node.js para construir y servir la aplicación Vue.js
FROM node:8.17.0

# Establece el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copia los archivos fuente de la aplicación al contenedor
COPY . .

# Instala las dependencias de Node.js y construye la aplicación
RUN npm install
RUN npm run build

# Define variables de entorno necesarias para la aplicación
ENV PORT=8080
ENV AUTH_API_ADDRESS=http://127.0.0.1:8000
ENV TODOS_API_ADDRESS=http://127.0.0.1:8082

# Expone el puerto definido para el servicio
EXPOSE ${PORT}

# Comando que se ejecuta cuando se inicia el contenedor
CMD ["npm", "start"]

