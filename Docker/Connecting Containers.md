
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
將三個 `docker run` 指令寫成 `docker-compose.yml` : 
- 這個 `docker-compose.yml` 文件將 Redis、MongoDB 和 HTTP 伺服器設定為容器，並且使用 `depends_on` 確保 HTTP 伺服器在 Redis 和 MongoDB 容器後啟動，還使用 `links` 來連接容器之間的網路。
```yaml
version: '3'

services:
  redis:
    image: redis
    container_name: redis-container
    ports:
      - "6379:6379"
    restart: always

  mongo:
    image: mongo
    container_name: mongo-container
    ports:
      - "27017:27017"
    restart: always

  httpd:
    image: httpd
    container_name: httpd-container
    ports:
      - "80:80"
    depends_on:
      - redis
      - mongo
    links:
      - redis
      - mongo
    restart: always
```
- 執行 `docker-cpomose.yml` : 
```shell
docker-compose up -d
```
> `-d` : 表示以 'detach' 模式啟動容器，也就是在後台運行。

- 檢查容器狀態:
```shell
docker-compose ps
```
- 停止容器:
```shell
docker-compose down
```
