
### 搜尋公開映像檔
---
用 docker search 搜尋
```
docker search nginx
```
從公有/ 私有倉庫搜尋
- 若組織擁有私有倉庫，可先在私有倉庫進行搜尋。或利用 [Docker Hub](https://hub.docker.com/) 搜尋公開的映像檔。
### 撰寫 Dockerfile
---
常用指令:
- `FROM` : 指定基礎映像。
- `RUN` : 執行命令並創建一層。
- `COPY` : 將文件從主機複製到映像中。
- `CMD` : 指定容器啟動時執行的命令。
- `EXPOSE` : 告訴 Docker 哪個端口將被容器使用。
範例: 創建一個運行 Node.js 應用的容器
```shell
FROM node:14            # 指定使用 Node.js 14 版本作為基礎映像
WORKDIR /usr/src/app    # 設置工作目錄為 `/usr/src/app`
COPY package*.json ./   # 將 `package.json` 和 `package-lock.json` 複製到工作目錄
RUN npm install         # 安裝 Node.js 應用所需的依賴
COPY . .                # 將當前目錄下的所有文件複製到容器的工作目錄
EXPOSE 3000             # 告訴 Docker 這個容器會使用 3000 端口
CMD ["node", "app.js"]  # 指定容器啟動時運行的命令
```
建立映像和運行容器
```bash
# 構建映像
docker build -t my-node-app .
# 運行容器
docker run -p 3000:3000 my-node-app
```
