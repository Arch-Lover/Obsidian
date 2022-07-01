```Dockerfile
FROM centos:7 as build  
  
RUN fallocate -l 10M /opt/1  
  
RUN fallocate -l 10M /opt/2  
  
RUN fallocate -l 5M /opt/jar  
  
FROM alpine  
  
COPY --from=build /opt/jar /jarfile.jar

```

```bash
docker build -t multi-stage:v0 .
```
```bash
docker images multi-stage --format="{{.Repository}}:{{.Tag}}\t{{.Size}}"

test-multi:v2   10.8MB  
test-multi:v0   225MB # without multi stage


```