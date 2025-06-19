FROM node:22-alpine AS builder

RUN apk add --no-cache \
    bash \
    git \
    autoconf \
    automake \
    libtool \
    build-base \
    make \
    g++ \
    nasm \
    pkgconf \
    pkgconfig \
    zlib-dev \
    python3

WORKDIR /app

COPY . .

RUN npm install --save-dev imagemin-optipng

RUN npm install
RUN npm run build

FROM nginx:alpine

COPY --from=builder /app/channels/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]