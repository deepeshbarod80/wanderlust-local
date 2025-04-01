FROM node:21
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

# Only copy .env.argocd if it exists
RUN if [ -f .env.argocd ]; then \
      cp .env.argocd .env; \
    else \
      echo "WARNING: .env.argocd not found, using default .env"; \
    fi

EXPOSE 8080
CMD ["npm", "start"]
