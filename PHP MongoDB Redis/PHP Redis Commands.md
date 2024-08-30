
Searching data through `key` :
```php
$redis = new Redis();
$redis->connect(REDIS_HOST, REDIS_PORT);
$hashData = $redis->hgetall($hashKey);
$keyValue = array();
$keyValue['key'] = $hashKey;
foreach ($hashData as $field => $value) {
	$keyValue[$field] = $value;
}
```

Inserting data:
```php
$redis = new Redis();
$redis->connect(REDIS_HOST, REDIS_PORT);
$redis->set('my_key', 'Hello, Redis!');
# 新增 hash key
$redis->hSet($hashKey, 'field1', 'value1');
$redis->hSet($hashKey, 'field2', 'value2');
```

Reading data:
```php
$redis = new Redis();
$redis->connect(REDIS_HOST, REDIS_PORT);
$value = $redis->get('my_key');
echo "Value: $value\n";
# 讀取 hash key 的值
$values = $redis->hGetAll($hashKey);
print_r($values);
```

Deleting data:
```php
$redis = new Redis();
$redis->connect(REDIS_HOST, REDIS_PORT);
$redis->del('my_key');
# 刪除 hash key
$redis->del($hashKey);
```
