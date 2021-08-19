#Usare una imagen Docker existente como base
FROM node:14.14.0-alpine as builder
#Caso AWS no acepta etiqueta de renombre
#FROM node:alpine

#Asignar Directorio de Trabajo
WORKDIR '/app'

#Descargar e instalar dependencia
COPY ./package.json ./
RUN npm install
COPY . .

#Tareas del docker al iniciar
RUN npm run build

###Segundo contenedor donde se guardara todo lo compilido en el contenedor anterior
FROM nginx
EXPOSE 3000

#Adjuntar archivo de configuracion nginx
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

#Adjuntar compilacion de la imagen inicial.
COPY --from=builder /app/build /usr/share/nginx/html

#Caso AWS no acepta etiqueta de renombre
#COPY --from=0 /app/build /usr/share/nginx/html