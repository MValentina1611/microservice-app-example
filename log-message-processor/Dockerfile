# Dockerfile para Log Message Processor
FROM python:3.6

WORKDIR /app

# Copiar los archivos del proyecto
COPY main.py .
COPY requirements.txt .

# Instalar las dependencias
RUN pip install --no-cache-dir -r requirements.txt

# Configuraciones de entorno
ENV REDIS_HOST=127.0.0.1
ENV REDIS_PORT=6379
ENV REDIS_CHANNEL=log_channel

# Comando para ejecutar la aplicación
CMD ["python3", "main.py"]

