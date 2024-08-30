
Searching data through `serial_number` :
```php
$collection = $database->selectCollection('devices');
$query = ['serial_number' => $serial_number];
$document = $collection->findOne($query);
```

Inserting data:
```php
$collection = $database->selectCollection('collection_name');
$data = [
	'name' => 'John Doe',
	'age' => 25,
	'email' => 'john.doe@example.com'
];
$collection->insertOne($data);
```

Deleting data through `serial_number` :
```php
$collection = $database->selectCollection('devices');
$deleteFilter = ['serial_number' => '1234X567J89P'];
$collection->deleteOne($deleteFilter);
```
