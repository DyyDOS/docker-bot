#1. For app
FROM node:alpine
WORKDIR /usr/src/app

COPY ./backend-bot/package.json /usr/src/app/package.json
COPY ./backend-bot/package-lock.json /usr/src/app/package-lock.json
RUN npm i
RUN npm ci

COPY ./backend-bot/. /usr/src/app/

ENV CI=true
ENV PORT=3001

CMD [ "npm", "start" ]


