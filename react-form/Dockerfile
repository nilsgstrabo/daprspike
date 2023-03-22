FROM node:17-alpine
WORKDIR /usr/src/app
COPY . .
RUN npm run build
EXPOSE 8080
RUN addgroup -S -g 1000 react
RUN adduser -S -u 1000 -G react react
USER 1000
CMD [ "npm", "run", "start" ]
