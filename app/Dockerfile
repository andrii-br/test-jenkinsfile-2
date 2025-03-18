FROM node:23-alpine3.20

WORKDIR /appnodejss

COPY ./app/ /appnodejss/

RUN nmp install 

EXPOSE 3000

CMD [ "node", "app.js" ]