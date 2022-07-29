```bash
# pull a docker image
docker pull nginx:alpine
```

```
# run docker image
docker run -d nginx:alpine

```

```
docker ps | grep nginx:alpine | awk '{print $1}'

docker stop $(docker ps | grep nginx:alpine | awk '{print $1}')
```

Run a image on port 2020
```
docker run -d -p 2020:80 nginx:alpine
```

Remove a container

```
docker rm -f pedantic_sanderson

```
`--force    -f  -- Force removal`

---
`Dockerfile`

```
FROM centos:7

RUN yum install httpd

CMD apachectl -DFOREGROUND
```

```
docker build -t centos_apache:v0 .
```

```
docker run -d -p 2020:80 --name=centos_apache centos_apache:v0
```

`localhost:2020`

