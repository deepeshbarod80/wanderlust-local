# Stage 1: Builder
FROM node:21 AS backend-builder
WORKDIR /app
COPY . .
RUN npm i && npm run test

# Stage 2: Runtime
FROM node:21-slim
WORKDIR /app
COPY --from=backend-builder /app .

# Environment configuration
ARG ENV=production
COPY .env.${ENV} .env

# Database connection configuration
RUN if [ "$ENV" = "development" ]; then \
      echo "MONGODB_URI=mongodb://172.28.39.56:27017/wanderlust" >> .env; \
      echo "REDIS_URL=redis://172.28.39.56:6379" >> .env; \
    else \
      echo "MONGODB_URI=mongodb://mongo-service:27017/wanderlust" >> .env; \
      echo "REDIS_URL=redis://redis-service:6379" >> .env; \
    fi

EXPOSE 8080
CMD ["npm", "start"]
