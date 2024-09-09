
### 指令建立容器
---
```bash
docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```
`docker run` 常用選項:
- `--env` , `-e` : 用來傳入環境變數。例如: `docker run -e "pyfile=main.py" Python:2.7` 
- `-v` : 設定 docker volume，例如: 設定主機資料夾與容器資料夾的對應 `docker run -v /host/nfs:/nfs my_app` 
- `-d` : 讓容器在背景執行
- `--net=[Mode]` : 設定容器網路，例如: `docker run --net=host nginx` 。常用的 Mode 包括 host, none, bridge，不指定的話預設是 bridge
- `--name` : 設定容器名稱，例如: `docker run --name my_python python:3.7` 
- `--restart=[policy]` : 設定重設機制，例如: `docker run --restart=on-failure:10 cassandra` 允許在錯誤的情況下重啟容器，最多重啟5次。`docker run --restart=always redis` 則只要容器一被停止，就立即嘗試重啟，適合服務不可中斷的容器。若沒指定，則預設是`--restart=none`，也就是若容器停止，則需人為手動啟動
- `-p` : 代表 port mapping，設定主機 port 對應到容器的哪個 port，例如: `docker run -p 8080:80 python_app` ，代表 container port 80 = host port 8080
範例: 
```shell
docker run -d -p 8080:80 -v volume_nfs:/nfs -v /etc/localtime:/etc/localtime:ro --name my_redis redis
```
- `-d` : 表示這個容器要在背景執行
- `-p 8080:80` : 表示本機的8080 port對應到容器的80 port
- `-v volume_nfs:/nfs` : 表示有一個 volume_nfs 與容器內的 /nfs 資料夾對應
- `-v /etc/localtime:/etc/localtime:ro` : 表示本機的 /etc/localtime 對應到容器內的 /localtime (這裡還多加了 `:ro` 代表容器內的唯讀)
- `--name my_redis` : 代表容器名稱
- 最後用來建立容器的映像檔是 `redis` 
