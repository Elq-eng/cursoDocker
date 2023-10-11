FROM node:19.2-alpine3.16 as deps

#cd app
WORKDIR /app

#Dest /app
COPY package.json ./

#sinstalr librerias
RUN npm install



#stage Two build y tests
FROM node:19.2-alpine3.16 as builder
#cd app
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run test


#stage Three
#deoendencias de produccion 
FROM node:19.2-alpine3.16 as prod-deps
#cd app
WORKDIR /app
COPY package.json ./
RUN npm install --prod




#runner stage four 
FROM node:19.2-alpine3.16 as runner 
#cd app
WORKDIR /app
COPY --from=prod-deps /app/node_modules ./node_modules
COPY app.js ./
COPY tasks/ ./tasks
CMD [ "node","app.js" ]
