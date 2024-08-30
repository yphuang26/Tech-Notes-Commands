
測試 Redis 是否連線成功
```php
<?php
$redis = new Redis();

try {
	$redis->connect('遠端 Redis server 的主機位址', 6379);
	# echo "Connection to remote Redis server successful\n";
	$redis->close();
} catch (Exception $e) {
	echo "Error connecting to Redis: " . $e->getMessage() . "\n";
}
?>
```

印出所有鍵和鍵值 (string, hash, list)
```php
<?php
$redis = new Redis();

try {
	$redis->connect('遠端 Redis server 的主機位址', 6379);
	# echo "Connection to remote Redis server successful<br>";
	
	// 獲取所有鍵
	$keys = $redis->keys('*');

	if (!empty($keys)) {
		// 顯示所有資料
		foreach ($keys as $key) {
			// 獲取鍵的類型
			$type = $redis->type($key);
			
			switch ($type) {
			case Redis::REDIS_STRING:
				$value = $redis->get($key);
				echo "Key: $key, Type: String, Value: $value<br>";
				break;
			
			case Redis::REDIS_HASH:
				$hashValue = $redis->hGetAll($key);
				echo "Key: $key, Type: Hash, Value: " . json_encode($hashValue) . "<br>";
				break;

			case Redis::REDIS_LIST:
				$listValue = $redis->lRange($key, 0, -1);
				echo "Key: $key, Type: List, Value: " . json_encode($listValue) . "<br>";
				break;

			default:
				echo "Key: $key, Type: Unknown<br>";
				break;
			}
		}
	} else {
		echo "No keys found in Redis<br>";
	}
	$redis->close();
} catch (Exception $e) {
	echo "Error connecting to Redis: " . $e->getMessage() . "<br>";
}
?>
```
