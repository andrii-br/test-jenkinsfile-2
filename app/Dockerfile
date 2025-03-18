FROM node:23-alpine3.20

WORKDIR /appnodejss

COPY . /appnodejss/

RUN nmp install -r package.json

EXPOSE 3000

CMD [ "node", "app.js" ]