FROM node:18 AS build
WORKDIR /app
COPY . .

# Install dependencies
RUN npm install -g @angular/cli
RUN npm install -g angular-http-server
RUN npm install --force
RUN npm run build

# Deploy into NGINX
FROM nginx:alpine
COPY --from=build /app/dist/resumebuilder /usr/share/nginx/html
EXPOSE 80
CMD ["nginx","-g","daemon off;"]
