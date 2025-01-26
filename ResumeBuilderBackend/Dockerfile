FROM node:18 AS build
WORKDIR /app
COPY . . 

# Install dependencies
RUN npm install
RUN npm install -g typescript

RUN tsc --build

EXPOSE 4292
CMD ["npm","run","start"]
