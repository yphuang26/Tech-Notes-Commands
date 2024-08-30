
### 安裝 & 設定 phpMyAdmin
```shell
$ sudo apt update
$ sudo apt install phpmyadmin
```

```
[*] apache2
[ ] lighttpd
```

```shell
# dbconfig-common
<是>
<輸入 password>
```

```
瀏覽器: http://{網頁ip}/phpmyadmin
```

```shell
# 編輯 apache2 的 configuration file
$ sudo vim /etc/apache2/apache2.conf
# 在最後一行加入
Include /etc/phpmyadmin/apache.conf
# 儲存後重啟 apache
$ sudo service apache2 restart
```
### 設定 MySQL
```shell
sudo mysql -u root
```

```sql
# 切換至 mysql 資料庫
mysql> use mysql;
# 讓 root 帳號啟用設定密碼的插件
mysql> UPDATE user SET plugin='mysql_native_password' WHERE User='root';
# 輸入指令重新載入特權表
mysql> FLUSH PRIVILEGES;
# 退出 mysql 的 shell
mysql> exit
```

```shell
# 設定 mysql 的 root password
$ sudo mysql_secure_installation
# 輸入 y 開啟 VALIDATE PASSWORD 插件
$ y
# 設定密碼的複雜度
$ 1
# 輸入兩次 password
$ New password: 
$ Re-enter new password: 
```

```shell
# 在以下的詢問中皆輸入 y
- Reomve anonymous users?
- Disallow root login remotely?
- Remove test database and access to it?
- Reload privilege tables now?
```
到此已完成設定 MySQL 的 root 密碼，可以登入 phpMyAdmin 了。

然而還有一個小問題，原因是在 php 7.2 後，count() 沒有添加參數的情形下，就會噴出Warning，而對於這個問題 phpMyAdmin 還沒有排除此錯誤，所以必須靠我們自己手動解決。
```shell
# 針對 Warning in ./libraries/plugin_interface.lib.php#551
$ sudo vim /usr/share/phpmyadmin/libraries/plugin_interface.lib.php
# 將第 551 行:
if ($options != null && count($options) > 0) {
# 改為: 
if ($options != null) {
```

```shell
# 針對 Warning in ./libraries/sql.lib.php#613
$ sudo vim /usr/share/phpmyadmin/libraries/sql.lib.php
# 將第 613 行: 
|| (count($analyzed_sql_results['select_expr'] == 1)
# 改為:
|| ((count($analyzed_sql_results['select_expr']) == 1)
```
Reference: [MySQL & phpMyAdmin](https://ithelp.ithome.com.tw/articles/10216815)
##### Do phpMyAdmin open a new port?
phpMyAdmin itself does not open a new port. It runs as a web application on top of your existing web server (like Apache or Nginx). It is typically accessed via a URL such as `http://your-server-ip/phpmyadmin` or `http://localhost/phpmyadmin`. The port used to access phpMyAdmin is the same as the port used by your web server (commonly port 80 for HTTP or port 443 for HTTPS).

### 卸載 phpMyAdmin
```shell
sudo apt remove phpmyadmin
sudo apt purge phpmyadmin
sudo apt autoremove
# 刪除以下文件(如果有的話)
sudo rm -rf /etc/phpmyadmin
sudo rm -rf /usr/share/phpmyadmin
```
打開 `/etc/apache2/apache2.conf` ，將以下程式碼註解掉
```shell
# include /etc/phpmyadmin/apache.conf
```
重新啟動 apache
```shell
sudo apt apache2 restart
```

