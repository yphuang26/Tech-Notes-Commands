
`rsync` 是一個同步與備份檔案的 linux 指令。使用上大致與 `scp` 相似，但 `rsync` 在同步與備份的同時會自動製作一份 snapshot 於之後備份檔案時先檢查新舊檔案之間的差異，並且只傳送有被更動的部分。
1. Transfer a file to instance
```shell
rsync -i /path/key-pair-name.pem -avh /path/my-file.txt ubuntu@instance-public-dns-name:path/
```
2. Transfer a file from instance to local computer
```shell
rsync -i /path/key-pair-name.pem -avh ubuntu@instance-public-dns-name:path/my-file.txt local-path/my-file.txt
```
##### 常用參數
---
- `-a` : [archive] 遞迴備份所有子目錄檔案、連結、擁有者、群組、時間戳、權限等
- `-v` : [verbose] 顯示詳細訊息
- `-h` : [human-readable] 使輸出的訊息排版叫人性化
##### 參考網頁
---
- [[medium] 使用 rsync 傳輸、備份兩處的檔案](https://medium.com/%E4%B8%80%E5%80%8B%E5%B0%8F%E5%B0%8F%E5%B7%A5%E7%A8%8B%E5%B8%AB%E7%9A%84%E9%9A%A8%E6%89%8B%E7%AD%86%E8%A8%98/linux-%E4%BD%BF%E7%94%A8-rsync-%E5%82%B3%E8%BC%B8-%E5%82%99%E4%BB%BD%E5%85%A9%E8%99%95%E7%9A%84%E6%AA%94%E6%A1%88-ea167b1a175c)
