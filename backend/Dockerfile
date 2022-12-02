FROM alpine:3.12


# install dependencies

RUN apk update

RUN apk add --no-cache nginx-mod-http-lua

#RUN apk add --update nodejs-npm 
#RUN apk add --update nodejs-current
RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.12/main/" >> /etc/apk/repositories \
    && apk add --update nodejs=12.22.12-r0 npm=12.22.12-r0


# Prepare backend
WORKDIR /app
COPY ./package.json /app/package.json
COPY ./package-lock.json /app/package-lock.json
RUN npm ci
COPY . .


# Delete default config
RUN rm -r /etc/nginx/conf.d && rm /etc/nginx/nginx.conf

# Create folder for PID file
RUN mkdir -p /run/nginx

# Add our nginx conf
#COPY ./nginx.conf /etc/nginx/nginx.conf

#COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

COPY ./nginx/nginx_master_1.conf /etc/nginx/nginx.conf

CMD ["node", "server.js"]