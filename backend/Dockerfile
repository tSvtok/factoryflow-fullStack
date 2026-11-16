FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./

# ---- development: nodemon + bind mount ----
FROM base AS dev
RUN npm install
COPY . .
EXPOSE 5000
CMD ["npm", "run", "dev"]

# ---- production ----
FROM base AS prod
ENV NODE_ENV=production
RUN npm ci --omit=dev
COPY . .
USER node
EXPOSE 5000
CMD ["node", "src/server.js"]
