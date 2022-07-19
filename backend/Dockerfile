#1. For app
FROM node:alpine
WORKDIR /backend-bot
COPY package.json ./
COPY package-lock.json ./
COPY ./ ./
RUN npm i
RUN npm ci

COPY . /app

ENV CI=true
ENV PORT=3001

CMD [ "npm", "start" ]


