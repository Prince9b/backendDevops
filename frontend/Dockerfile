# Étape 1 : Build de l'application React
FROM node:20 AS build
WORKDIR /app

# On déclare qu'on accepte un argument venant de l'extérieur
ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Étape 2 : Diffusion via Nginx
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]