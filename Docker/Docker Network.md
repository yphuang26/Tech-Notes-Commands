
列出現有的 Docker Networks:
```sh
docker network ls
```
創建新的 Docker Network:
```sh
docker network create ${NETWORK_NAME}
```
#### 範例
讓 Apache Redis MongoDB 三個容器在同一個 Docker Network 中運行:
```shell
# 1. 創建一個自定義的 Docker 網路:
docker network create mynetwork
# 2. 啟動 Apache 容器，連接到 ‘mynetwork’:
docker run -d --name apache-container --network mynetwork -p 80:80 httpd
# 3. 啟動 Redis 容器，連接到 ‘mynetwork’:
docker run -d --name redis-container --network mynetwork -p 6379:6379 redis
# 4. 啟動 MongoDB 容器，連接到 ‘mynetwork’:
docker run -d --name mongo-container --network mynetwork -p 27017:27017 mongo
```
- 三個容器都在 `mynetwork` 這個網路中運行，它們可以透過容器名稱或 IP 地址在同一個網路中進行通信。