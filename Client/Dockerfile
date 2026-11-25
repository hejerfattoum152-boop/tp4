FROM node:lts-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM node:lts-alpine

WORKDIR /app

RUN npm install -g serve

# On copie le dossier 'dist' généré par Vite
COPY --from=build /app/dist ./dist

EXPOSE 3000

# On sert le dossier 'dist'
CMD ["serve", "-s", "dist", "-l", "3000"]
