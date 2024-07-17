FROM node:18 AS build

WORKDIR /app

COPY . .

RUN npm install

RUN npm run build && rm -rf node_modules

FROM node:18-alpine

ENV NODE_ENV=production

USER node

RUN mkdir /home/node/app

WORKDIR /home/node/app

COPY --chown=node:node --from=build /app/dist ./dist

COPY --chown=node:node --from=build /app/package*.json .

RUN npm ci 

EXPOSE 3000

CMD ["npm", "run", "serve"]