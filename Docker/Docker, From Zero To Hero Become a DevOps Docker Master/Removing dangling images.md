```bash
➜  docker-images docker images          
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE  
ls           latest    43eaac1ad090   8 seconds ago    204MB  
<none>       <none>    aced02a14981   44 seconds ago   204MB

```

```bash
docker rmi $(docker images -q -f dangling=true)
```