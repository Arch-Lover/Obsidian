`git clone https://github.com/docker/getting-started.git`

`cd "sample application/getting-started/app"`

### Build the app’s container image

```
Dockerfile 


# syntax=docker/dockerfile:1
FROM node:12-alpine
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```

```
docker build -t getting-started .

```

### Start an app container

```
docker run -dp 3000:3000 getting-started
```