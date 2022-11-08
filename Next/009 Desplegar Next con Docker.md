### 1. Creamos `.dockerignore`

Con lo siguiente:

```
Dockerfile
.dockerignore
node_modules
npm-debug.log
README.md
.next
```

### 2. Creamos `Dockerfile`

Este es un ejemplo de los comandos que podria llevar

```
# Fuente: https://github.com/vercel/next.js/blob/canary/examples/with-docker/README.md

# Install dependencies only when needed

FROM node:16-alpine AS deps

# Check https://github.com/nodejs/docker-node/tree/b4117f9333da4138b03a546ec926ef50a31506c3#nodealpine to understand why libc6-compat might be needed.

RUN apk add --no-cache libc6-compat

WORKDIR /app

COPY package.json yarn.lock ./

RUN yarn install --frozen-lockfile

# Rebuild the source code only when needed

FROM node:16-alpine AS builder

WORKDIR /app

COPY --from=deps /app/node_modules ./node_modules

COPY . .

RUN yarn build

# Production image, copy all the files and run next

FROM node:16-alpine AS runner

WORKDIR /app

ENV NODE_ENV production

RUN addgroup -g 1001 -S nodejs

RUN adduser -S nextjs -u 1001

# You only need to copy next.config.js if you are NOT using the default configuration

# COPY --from=builder /app/next.config.js ./

COPY --from=builder /app/public ./public

COPY --from=builder /app/package.json ./package.json

# Automatically leverage output traces to reduce image size

# https://nextjs.org/docs/advanced-features/output-file-tracing

COPY --from=builder --chown=nextjs:nodejs /app/.next/standalone ./

COPY --from=builder --chown=nextjs:nodejs /app/.next/static ./.next/static

USER nextjs

EXPOSE 3000

ENV PORT 3000

# Next.js collects completely anonymous telemetry data about general usage.

# Learn more here: https://nextjs.org/telemetry

# Uncomment the following line in case you want to disable telemetry.

# ENV NEXT_TELEMETRY_DISABLED 1

CMD ["node", "server.js"]

# entre 50 a 150 MB
```

#### Instalamos Docker en nuestra maquina

Se recomienda seguir los pasos en la sección de Docker para instalar todo lo necesario
***[Docker](../Docker/000%20Docker.md)***

### 3. Generando y levantando el contenedor

1. `rm -rf yarn.lock`
2. `yarn -i`
3. `docker build -t [nombre-de-la-imagen]:[tag] .` => Generando la imagen
4. `docker run --name=[nombre-del-contenedor] -p 3030:3000 [nombre-de-la-imagen]` => Levanta el contenedor



