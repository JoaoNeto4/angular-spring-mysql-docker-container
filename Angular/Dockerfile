FROM node:18.17.1-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm install

RUN npx ngcc --properties es2023 browser module main --first-only --create-ivy-entry-points

COPY . .

RUN npm run build

FROM nginx:stable

#helpdesk-front name is from package.json "name"
COPY --from=build /app/dist/helpdesk-front/ /usr/share/nginx/html

EXPOSE 80
