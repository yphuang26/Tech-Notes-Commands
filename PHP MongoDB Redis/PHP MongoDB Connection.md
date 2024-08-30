
Install Composer 2
- [Install Composer on Ubuntu](https://www.ionos.com/digitalguide/server/configuration/php-composer-installation-on-ubuntu-2004/)
```shell
# Install dependencies
sudo apt install curl php-cli php-mbstring unzip
# Download and install Composer 2
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
# Verify Composer installation
composer
```

```shell
# Create composer.json file
# 先 init 的話 composer.json 設定檔會完整一點，但只是 require 不需要輸入
# composer init
```

```shell
# Add dependencies
composer require mongodb/mongodb
# 會在目錄底下產生資料夾 vendor 和檔案 composer.json composer.lock
```

測試 MongoDB 是否連接成功
```php
<?php
// 載入 MongoDB 資源類別
require 'vendor/autoload.php';

// MongoDB server 的連接資訊
$mongoHost = '遠端 MongoDB server 的主機位址';
$mongoPort = '27017'; # 遠端 MongoDB server 的埠口
$mongoUsername = 'MongoDB 使用者名稱';
$mongoPassword = 'MongoDB 使用者密碼';
$mongoDatabase = 'MongoDB 資料庫名稱';

// 設定連接遠端 MongoDB server 的 URI
$mongoURI = sprintf(
	'mongodb://%s:%s@%s:%s/%s',
	$mongoUsername,
	$mongoPassword,
	$mongoHost,
	$mongoPort,
	$mongoDatabase
);

try {
	$mongoClient = new MongoDB\Driver\Manager($mongoURI);
	echo '連線成功';
} catch (MongoConnectionException $e) {
	echo '連線失敗: ' . $e->getMessage();
}
?>
```

執行 show collections 命令
```php
<?php
// 載入 MongoDB 資源類別
require 'vendor/autoload.php';

use MongoDB\Client;

// MongoDB server 的連接資訊
$mongoHost = '遠端 MongoDB server 的主機位址';
$mongoPort = '27017'; # 遠端 MongoDB server 的埠口
$mongoUsername = 'MongoDB 使用者名稱';
$mongoPassword = 'MongoDB 使用者密碼';
$mongoDatabase = 'MongoDB 資料庫名稱';

// 設定連接遠端 MongoDB server 的 URI
$mongoURI = sprintf (
	'mongodb://%s:%s@%s:%s/%s',
	$mongoUsername,
	$mongoPassword,
	$mongoHost,
	$mongoPort,
	$mongoDatabase
);

// 建立 MongoDB server 的連線
$mongoClient = new Client($mongoURI);

// 取得資料庫
$database = $mongoClient->selectDatabase($mongoDatabase);

// 列出資料庫中的集合
$collectionList = $database->listCollections();

foreach ($collectionList as $collection) {
	echo $collection->getName() . "<br>";
}
?>
```

印出 collection 內的所有欄位
```php
<?php
// 載入 MongoDB 資源類別
require 'vendor/autoload.php';

use MongoDB\Client;

// MongoDB server 的連接資訊
$mongoHost = '遠端 MongoDB server 的主機位址';
$mongoPort = '27017'; # 遠端 MongoDB server 的埠口
$mongoUsername = 'MongoDB 使用者名稱';
$mongoPassword = 'MongoDB 使用者密碼';
$mongoDatabase = 'MongoDB 資料庫名稱';

// 設定連接遠端 MongoDB server 的 URI
$mongoURI = sprintf (
	'mongodb://%s:%s@%s:%s/%s',
	$mongoUsername,
	$mongoPassword,
	$mongoHost,
	$mongoPort,
	$mongoDatabase
);

// 建立 MongoDB server 的連線
$mongoClient = new Client($mongoURI);

// 取得資料庫
$database = $mongoClient->selectDatabase($mongoDatabase);

// 列出資料庫中的集合
$collectionList = $database->listCollections();

foreach ($collectionList as $collectionInfo) {
	// 列出集合名稱
	echo "Collection: " . $collectionInfo->getName() . "<br>";

	// 取得集合
	$collection = $database->selectCollection($collectionInfo->getName());

	// 查詢集合中的所有文件(第一個文件)
	$document = $collection->findOne();
	
	// 如果文件存在，列印出文件的欄位
	if ($document) {
		foreach ($document as $field => $value) {
			echo "Field: $field" . "<br>";
		}
	} else {
		echo "無文件" . "<br>";
	}
	echo "<br>";
}
```

## CMD 連線
連線指令:
```shell
mongosh --username <MONGO_USER> --password <MONGO_PASSWORD> --host <MONGO_HOST> --port <MONGO_PORT> --authenticationDatabase <MONGO_DB_NAME>
```
查看主節點或副本集 (mongoDB 的操作比需在主節點執行): 
```shell
db.isMaster()
```
