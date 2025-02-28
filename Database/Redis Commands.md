
### Connect to remote Redis server
```shell
redis-cli -h host -p port -a password
```
### Redis keys commands
```shell
DEL key                                   # 當 key 存在時，刪除 key
DUMP key                                  # 序列化給定 key，並返回被序列化的值
EXISTS key                                # 檢查給定 key 是否存在
EXPIRE key seconds                        # 為給定 key 設置過期時間，以秒計
KEYS pattern                              # 查找所有符合給定模式(pattern)的 key
MOVE key db                               # 將當前資料庫的 key 移動到給定的資料庫 db 當中
PERSIST key                               # 移除 key 的過期時間，key 將持久保持
TTL key                                   # 以毫秒為單位返回 key 的剩餘生存時間 (TTL, time to live)
RANDOMKEY                                 # 從當前資料庫中隨機返回一個 key
RENAME key newkey                         # 修改 key 的名稱
SCAN cursor [MATCH pattern] [COUNT count] # 迭代資料庫中的資料庫鍵
TYPE key                                  # 返回 key 所儲存的值的類型
```
