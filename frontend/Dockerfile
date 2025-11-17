FROM node:24

WORKDIR /app

COPY . .

RUN npm install

ENTRYPOINT [ "npm", "run", "preview" ]

EXPOSE 4173