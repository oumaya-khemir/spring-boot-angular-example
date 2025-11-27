# Dockerfile frontend
FROM node:18 as build

# Créer le répertoire de travail
WORKDIR /app

# Copier package.json et package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm install -g npm@11.6.4


# Copier le reste des fichiers
COPY . .

# Compiler l'application Angular
RUN npm run build --prod

# Étape finale : serveur Nginx
FROM nginx:alpine

# Copier les fichiers compilés dans Nginx
COPY --from=build /app/dist/* /usr/share/nginx/html/

# Exposer le port
EXPOSE 80

# Lancer Nginx
CMD ["nginx", "-g", "daemon off;"]
