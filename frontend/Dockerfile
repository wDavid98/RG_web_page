# Etapa 1: Construcción de la aplicación Vue.js
FROM node:22.13.1 as build-stage

# Configurar el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar los archivos de dependencias (mejora caché de Docker)
COPY package*.json ./

# Instalar las dependencias
RUN npm install

# Copiar todo el código fuente de la aplicación al contenedor
COPY . .

# Construir la aplicación Vue.js
RUN npm run build

# Etapa 2: Servir los archivos con NGINX
FROM nginx:stable as production-stage

# Copiar los archivos estáticos de la etapa de construcción
COPY --from=build-stage /app/dist /app

# Copiar la configuración personalizada de Nginx
COPY nginx.conf /etc/nginx/nginx.conf

# Expose the port 80
EXPOSE 80

# Start Nginx to serve the application
CMD ["nginx", "-g", "daemon off;"]
