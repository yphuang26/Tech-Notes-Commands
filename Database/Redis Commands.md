
### Connect to remote Redis server
- Connect to redis:
```shell
redis-cli -h host -p port -a password
```
- List all keys
```shell
keys *
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
### String
```shell
SET key value            # 設置指定 key 的值
GET key                  # 取得指定 key 的值
GETRANGE key $start $end # 返回 key 中字符串值得子字符
MGET key1 [key2...]      # 取得一個或多個給定 key 的值
```
### Hash
- Redis Hash 是一個 string 類型的 field (字段) 和 value (值) 的映射表
```shell
HDEL jey field1 [field2] # 刪除一個或多個 hash field
HEXISTS key field # 查詢 hash 中，指定的 field 是否存在
HGET key field # 取得存儲在 hash 中指定 field 的值
HGETALL key # 取得 hash 中指定 key 的所有 field 和 value
```
### List
- Redis List 是字符串列表，按照插入順序排序。也可以添加元素到 List 的頭部 (左邊) 或者尾部 (右邊)
```shell
LINDEX key index       # 透過索引取得 List 中的元素
LPOP key               # 移出並取得 List 的第一個元素
RPOP key               # 移出並取得 List 的最後一個元素
LPUSHX key value       # 將一個值插入到已存在的 List 頭部
RPUSHX key value       # 將一個值插入到已存在的 List 尾部
LRANGE key $start $end # 取得列表指定範圍內的元素
```
### Set
- Redis Set 是 String 類型的無序集合，集合成員是唯一的
```shell
SADD key member1 [member2] # 向集合添加一個或多個成員
SCARD key                  # 取得集合的成員數
SISMEMBER key member       # 判斷 member 元素是否是集合 key 的成員
SMEMBERS key               # 返回集合中的所有成員
SREM key member1 [member2] # 移除集合中一個或多個成員
```

