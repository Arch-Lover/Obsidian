```Dockerfile
FROM centos:7 as builder  
  
RUN fallocate -l 10M /opt/1  
  
RUN fallocate -l 10M /opt/2  
  
RUN fallocate -l 5M /opt/jar  
  
FROM alpine  
  
COPY --from=builder /opt/jar /jarfile.jar

```

```bash
docker build -t multi-stage:v0 .
```
```bash
docker images multi-stage --format="{{.Repository}}:{{.Tag}}\t{{.Size}}"

test-multi:v2   10.8MB  
test-multi:v0   225MB # without multi stage


```

```Dockerfile

FROM maven:3.6-alpine as builder  
  
COPY app-maven /app  
  
WORkDIR /app  
  
RUM mvn package  
  
FROM openjdk:8-alpine  
  
COPY --from=builder /app/target/my-app-1.0-SNAPSHOT.jar /app.jar  
  
CMD java -jar /app.jar
```

```bash 

docker build -t maven-multi:v1  .
```