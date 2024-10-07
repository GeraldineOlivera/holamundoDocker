FROM node:20.5.0-alpine3.18
RUN addgroup nodeapp && adduser -S -G nodeapp nodeapp
USER nodeapp
WORKDIR /app/
COPY --chown=nodeapp package*.json .
RUN npm config set strict-ssl false && \
    npm config delete proxy && \
    npm config delete https-proxy && \
    npm config set fetch-retry-maxtimeout 120000 && \
    npm config set fetch-retry-mintimeout 20000 && \
    node -e "require('events').EventEmitter.defaultMaxListeners = 20" && \
    npm install --unsafe-perm
COPY --chown=nodeapp . .
EXPOSE 3000
CMD ["npm", "start"]