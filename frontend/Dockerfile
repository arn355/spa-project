# stage 1
FROM node:16 as builder

WORKDIR /app

COPY package*.json .

RUN npm i

COPY . .

RUN npm run build

# stage 2
FROM nginx:1.23.2

COPY --from=builder /app/build /usr/share/nginx/html

RUN rm /etc/nginx/conf.d/default.conf

COPY ./nginx.conf /etc/nginx/conf.d

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]