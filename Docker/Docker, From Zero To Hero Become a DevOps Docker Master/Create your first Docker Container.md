```bash
# pull a docker image
docker pull nginx:alpine

# run docker image
docker run -d nginx:alpine

docker ps | grep nginx:alpine | awk '{print $1}'

docker stop $(docker ps | grep nginx:alpine | awk '{print $1}')
```