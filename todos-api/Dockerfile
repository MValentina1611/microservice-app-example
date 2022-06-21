FROM node:8.17.0

WORKDIR /app

# Copiar los archivos del proyecto
COPY . .

# Instalar las dependencias
RUN npm install

# Configuraciones de entorno
ENV TODO_API_PORT=8082
ENV JWT_SECRET=PRFT
ENV REDIS_HOST=127.0.0.1
ENV REDIS_PORT=6379
ENV REDIS_CHANNEL=log_channel

# Exponer el puerto
EXPOSE ${TODO_API_PORT}

# Comando para ejecutar la aplicación
CMD ["npm", "start"]

