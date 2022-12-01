FROM node:12.18.2 as build

ARG REACT_APP_SERVICES_HOST=/services/m

WORKDIR /app

COPY ./package.json /app/package.json
COPY ./package-lock.json /app/package-lock.json

RUN yarn install

COPY . .

RUN yarn build




FROM ubuntu/nginx:1.18-21.04_edge

# Create folder for PID file
RUN mkdir -p /run/nginx

COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

COPY ./nginx/nginx_master_1.conf /etc/nginx/nginx.conf

#COPY ./nginx/nginx_master_1.conf /usr/local/openresty/nginx/conf/nginx.conf

COPY --from=build /app/build /usr/share/nginx/html
