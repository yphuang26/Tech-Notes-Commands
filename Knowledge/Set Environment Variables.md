
#### 使用 `os.environ` (僅在當前的 python 中有效)
###### 讀取環境變數
```python
import os
value = os.getenv('ENV_VARIABLE')
```
###### 寫入環境變數
```python
import os
os.environ['ENV_VARIABLE'] = 'value'
```
#### Ubuntu 系統層面設置 (永久有效)
###### 打開 `~/.bashrc` 文件
```shell
vim ~/.bashrc
```
###### 添加環境變數
```shell
export ENV_VARIABLE=value
```
###### 保存文件並重新加載配置
```shell
source ~/.bashrc
```
#### 自定義環境變數文件 (eg. `/etc/config.ini`)
###### 讀取 `config.ini` 文件
```python
import configparser

config = configparser.ConfigParser()
config.read('/etc/config.ini')
value = config['SECTION_NAME']['ENV_VARIABLE']
```
###### 寫入 `config.ini` 文件
```python
import configparser

config = configparser.ConfigParser()
config.read('/etc/config.ini')
if 'SECTION_NAME' not in config:
	config['SECTION_NAME'] = {}
config['SECTION_NAME']['ENV_VARIABLE'] = 'value'

with open('/etc/config.ini', 'w') as configfile:
	config.write(configfile)
```
