
### Connect to remote mongoDB server
```shell
mongosh --username <MONGO_USER> --password <MONGO_PASSWORD> --host <MONGO_HOST> --port <MONGO_PORT> --authenticationDatabase <MONGO_DB_NAME>
```
### Basic Commands
```shell
mongo                              # 連入DB, 預設port 27017
db.auth("admin", "{PASSWORD}")     # 以admin 身分登入
show dbs                           # 顯示DB
use dbname                         # 切換dbname，用法跟 MySql 類似
show collections                   # 顯示集合
db.createCollection('users')       # 建立 users 集合
db.users.drop()                    # 刪除 users 集合
db.runCommand({"drop", "users"})   # 刪除 users 集合 (同上)
db.runCommand({"dropDatabase": 1}) # 刪除目前 DB
```

```shell
db                                 # 顯示當前資料庫
show dbs                           # 顯示所有資料庫
show collections                   # 顯示集合
db.collection_name.find()          # 顯示 collection 內容
db.collection_name.find().pretty() # 美化輸出
```
### Help Commands
```shell
odb.help();
odb.yourColl.help();
odb.youColl.find().help();
db.dropDatabase()                            # 刪除當前DB
db.cloneDatabase(“127.0.0.1”)                # 從指定的機器上複製DB
db.copyDatabase("mydb", "temp", "127.0.0.1") # 從指定的機器複製到本地的 temp DB
db                                           # 查看當前DB
db.version()                                 # 查看版本
db.getMongo()                                # 查看當前的db 版本
```
### CRUD
##### 1. Create
```shell
db.users.save({"name": "lecaf"})              # 建立一個 users的集合 並且寫入一筆資料
db.users.insert({"name": "ghost", "age": 10}) # 在 users 集合中寫入資料，如果沒有 users，mongodb 會自動建立一個
```
##### 2. Delete
```shell
db.users.remove()                  # 刪除 users 集合所有資料
db.users.remove({"name": "lecaf"}) # 刪除 users 集合下 name=lecaf 的該筆資料
```
##### 3. Read
```shell
db.users.find()                    # 查詢users集合中所有資料
db.users.find({"name": "feng"})    # 查詢 users 集合中符合 name=feng 的所有資料
db.users.findOne()                 # 查詢 users 集合中的第一筆資料
db.users.findOne({"name": "feng"}) # 查詢 users 集合中 name=feng 的第一筆資料
```
##### 4. Update
```shell
db.users.update({"name": "lecaf"}, {"age": 10}) # 修改資料，其中 name=lecaf 為查詢條件，"age": 10 為修改內容
# 除了主鍵，其他內容會被第二個參數替換，主鍵不能修改，只能新增刪除
```