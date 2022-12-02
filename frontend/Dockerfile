FROM node:12.18.2 as build

ARG REACT_APP_SERVICES_HOST=/services/m

WORKDIR /app

COPY ./package.json /app/package.json
COPY ./package-lock.json /app/package-lock.json

RUN yarn install

COPY . .

RUN yarn build




FROM alpine:3.6

RUN apk add --no-cache nginx-mod-http-lua

# Delete default config
RUN rm -r /etc/nginx/conf.d && rm /etc/nginx/nginx.conf

# Create folder for PID file
RUN mkdir -p /run/nginx

# Add our nginx conf
# COPY ./nginx.conf /etc/nginx/nginx.conf

COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

COPY ./nginx/nginx_master_1.conf /etc/nginx/nginx.conf

COPY --from=build /app/build /usr/share/nginx/html

CMD ["nginx"]





