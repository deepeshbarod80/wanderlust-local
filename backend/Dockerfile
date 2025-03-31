FROM node:21
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
COPY .env.argocd .env
EXPOSE 8080
CMD ["npm", "start"]
