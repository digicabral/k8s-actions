FROM node:18-alpine AS builder

WORKDIR /app

COPY ["./package.json", "./package-lock.json", "./tsconfig.json", "/app/"]
COPY ["./src","/app/src/"]

RUN npm install
RUN npm run build

FROM node:18-alpine
WORKDIR /app

COPY --from=builder ["/app/package.json", "/app/package-lock.json", "/app/"]
COPY --from=builder ["/app/dist", "/app/dist/"]

RUN npm i --omit=dev

ENTRYPOINT [ "npm", "start" ]