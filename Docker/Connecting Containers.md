
#### 方法一: 使用 `--link` 的方法
1. 創建 Redis 容器
```shell
docker run -d --name redis-container -p 6379:6379 redis
```
2. 創建 MongoDB 容器
```shell
docker run -d --name mongo-container -p 27017:27017 mongo
```
3. 創建 Apache HTTP Server 容器，同時連接到 Redis 和 MongoDB 容器所在的默認橋接網路
```shell
docker run -d --name httpd-container --link redis-container:redis --link mongo-container:mongo -p 80:80 httpd
```

#### 方法二: Docker Compose
