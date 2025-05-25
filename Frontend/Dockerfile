FROM node:18-alpine

WORKDIR /usr/app/

ENV PORT=4000
COPY . .
RUN npm install

CMD ["npm", "run", "start"]
