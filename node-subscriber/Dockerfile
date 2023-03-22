FROM node:17-alpine
WORKDIR /usr/src/app
COPY . .
RUN npm install
EXPOSE 3000
RUN addgroup -S -g 1000 node-app
RUN adduser -S -u 1000 -G node-app node-app
USER 1000
CMD [ "node", "app.js" ]