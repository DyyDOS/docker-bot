# FROM alpine
# EXPOSE 80
# COPY ./BOT-FB-UI/* /var/www/localhost/htdocs
# RUN apk add nginx && \
#     mkdir /run/nginx && \
#     apk add nodejs && \
#     apk add npm && \
#     cd /var/www/localhost/htdocs && \
#     npm install && \
#     npm run build && \
#     apk del nodejs && \
#     apk del npm && \
#     mv /var/www/localhost/htdocs/build /var/www/localhost && \
#     cd /var/www/localhost/htdocs && \
#     rm -rf * && \
#     mv /var/www/localhost/build /var/www/localhost/htdocs;
# CMD ["/bin/sh", "-c", "exec nginx -g 'daemon off;';"]
# WORKDIR /var/www/localhost/htdocs

# 1. For build React app
FROM node:lts AS development

# Set working directory
WORKDIR /app

# 
COPY ./Bot-FB-UI/package.json /app/package.json
COPY ./Bot-FB-UI/package-lock.json /app/package-lock.json

# Same as npm install
RUN npm ci

COPY ./Bot-FB-UI/. /app
COPY ./conf/. /app/conf
ENV CI=true 
ENV PORT=3000

CMD [ "npm", "start" ]
FROM development AS build

RUN npm run build

CMD [ "npm", "start" ]

# 2. For Nginx setup
FROM nginx:alpine

# Copy config nginx
COPY --from=build /app/conf/app.conf /etc/nginx/conf.d/app.conf
COPY --from=build /app/conf/api.conf /etc/nginx/conf.d/api.conf

WORKDIR /usr/share/nginx/html

# Remove default nginx static assets
RUN rm -rf ./*

# Copy static assets from builder stage
COPY --from=build /app/build .

# Containers run nginx with global directives and daemon off
ENTRYPOINT ["nginx", "-g", "daemon off;"]

