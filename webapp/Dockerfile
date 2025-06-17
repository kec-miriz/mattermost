FROM node:22-alpine AS builder

WORKDIR /app

COPY package.json yarn.lock ./
COPY . .

RUN yarn install --frozen-lockfile \
  && yarn run build

FROM nginx:alpine

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]