FROM node:23-alpine3.20

WORKDIR /app

RUN nmp install -r package.json

COPY . /app/

EXPOSE 3000

CMD [ "node", "app.js" ]