FROM mongo:6.0

# Configuration for different environments
ARG ENV=production
COPY init.js /docker-entrypoint-initdb.d/

# Local development exposes ports differently
RUN if [ "$ENV" = "development" ]; then \
      echo "net.bindIp: 172.28.39.56" >> /etc/mongod.conf.orig; \
    else \
      echo "net.bindIp: 0.0.0.0" >> /etc/mongod.conf.orig; \
    fi

EXPOSE 27017
ENTRYPOINT ["mongod", "--bind_ip_all"]
