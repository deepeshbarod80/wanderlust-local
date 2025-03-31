# ------------------- Stage 1: Build Stage ------------------------------
FROM node:21 AS frontend-builder

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

# ------------------- Stage 2: Final Stage ------------------------------
FROM node:21-slim
WORKDIR /app
COPY --from=frontend-builder /app .

# Environment configuration
ARG ENV=production
COPY .env.${ENV} .env.local

# Dynamic host configuration
RUN if [ "$ENV" = "development" ]; then \
      echo "VITE_API_BASE_URL=http://172.28.39.56:31100" >> .env.local; \
    else \
      echo "VITE_API_BASE_URL=http://127.0.0.1:31307" >> .env.local; \
    fi

EXPOSE 5173
CMD ["npm", "run", "dev", "--", "--host"]
