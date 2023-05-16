ARG NODE_IMAGE=node:16-bullseye
FROM ${NODE_IMAGE} as node-build

WORKDIR /app
COPY package.json .
COPY package-lock.json .
RUN npm install -g npm@9.5.1
RUN npm install
COPY . .
RUN npm run build:prod