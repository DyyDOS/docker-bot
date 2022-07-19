#1. For app
FROM node:alpine
WORKDIR /usr/src/app

COPY package.json /usr/src/app/package.json
COPY package-lock.json /usr/src/app/package-lock.json
RUN npm i
RUN npm ci

COPY . /usr/src/app

ENV CI=true
ENV PORT=3001

CMD [ "npm", "start" ]


