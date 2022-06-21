# Dockerfile para el Frontend
FROM node:8.17.0

WORKDIR /app

# Copiar los archivos del proyecto
COPY . .

# Instalar las dependencias y construir la aplicación
RUN npm install
RUN npm run build

# Configuraciones de entorno
ENV PORT=8080
ENV AUTH_API_ADDRESS=http://127.0.0.1:8000
ENV TODOS_API_ADDRESS=http://127.0.0.1:8082

# Exponer el puerto
EXPOSE ${PORT}

# Comando para ejecutar la aplicación
CMD ["npm", "start"]

