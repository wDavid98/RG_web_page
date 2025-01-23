FROM node:22.13.1 as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY ./ /app
RUN npm run build

FROM nginx:stable as production-stage
RUN mkdir /app
COPY --from=build-stage /app/dist /app
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
