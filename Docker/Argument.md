# 1️⃣Commands
- docker run --build-arg ARGUMENT_KEY=ARGUMENT_VALUE
# 2️⃣Dockerfile
```
FROM node:14

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . /app

ARG DEFAULT_PORT=80

ENV PORT $DEFAULT_PORT

EXPOSE $PORT

CMD [ "npm", "start" ]
```

