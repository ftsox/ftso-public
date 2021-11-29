FROM node:14-alpine3.10 as ts-compiler
WORKDIR /usr/app
COPY ./package*.json ./
COPY ./tsconfig*.json ./
RUN npm install
COPY . ./
RUN npm run build

FROM node:14-alpine3.10 as ts-remover
WORKDIR /usr/app
RUN apk update && apk add bash
COPY --from=ts-compiler /usr/app/package*.json ./
COPY --from=ts-compiler /usr/app/dist ./
RUN npm install --only=production