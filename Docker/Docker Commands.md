
List all containers:
- including those that are stopped
```shell
docker ps -a
```

List all images:
- available on the local Docker host
```shell
docker images
```

Remove Docker image:
```shell
docker rmi {IMAGE_ID}
```

Start a Bash shell in the running container:
```shell
docker exec -it {CONTAINER_NAME} /bin/bash
```

Start a shell(sh) in the running container:
```shell
docker exec -it {CONTAINER_NAME} sh
```

Exit the current shell:
```shell
exit
```

Start/ Restart a container:
```shell
docker start {CONTAINER_NAME}
docker restart {CONTAINER_NAME}
```

Stop a running container:
```shell
docker stop {CONTAINER_NAME}
```

Remove a stopped container:
```shell
docker rm {CONTAINER_NAME}
```
