
參考：[Install and configure WordPress](https://ubuntu.com/tutorials/install-and-configure-wordpress#1-overview)
### System Requirement
- Wordpress
- Apache
- PHP
- MySQL
### 1. Install Dependencies
```shell
sudo apt update
```

```shell
sudo apt install apache2 ghostscript libapache2-mod-php mysql-server php php-bcmath php-curl php-imagick php-intl php-json php-mbstring php-mysql php-xml php-zip
```
### 2. URL Rewriting
- Host 的設定路徑: /etc/apache2/site-available/
	- 預設 http 基本設定: 000-default.conf
	- 預設 https 基本設定: default-ssl.conf
```shell
<VirtualHost *:80>

	DocumentRoot /var/www/backend
	<Directory />
		Options FollowSymLinks
		AllowOverride None
		DirectoryIndex wp-login.php index.php
	</Directory>

	<Directory /var/www/backend>
		Options FollowSymLinks MultiViews
		AllowOverride None
		Require all granted
	</Directory>

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```

Enable the site with:
```shell
sudo a2ensite 000-default
```

Enable URL rewriting with:
```shell
sudo a2enmod rewrite
```

### 3. Configure Database
- Database 和 user 需要跟 wp-login.php 一樣
```shell
sudo mysql -u root
```

```mysql
mysql> CREATE DATABASE wordpress;
mysql> CREATE USER wordpress@localhost IDENTIFIED BY 'wordpress12345';
mysql> GRANT ALL ON wordpress.* TO wordpress@localhost;
mysql> FLUSH PRIVILEGES;
mysql> quit
```

```shell
sudo service mysql start
```
### 4. Install SSH2 extension
Reference: [Install php-ssh2 on Ubuntu](https://installati.one/install-php-ssh2-ubuntu-20-04/?expand_article=1)
```shell
sudo apt install php-ssh2
```
Testing installation:
```shell
php -m | grep ssh2
```

### Additional Notes:
##### Apache 網頁出錯可查看 log 日誌
- log 日誌位址:
```shell
/var/log/apache2/error.log
```
- 清空 log 日誌:
```shell
sudo -i # 切換到 root 使用權限
echo > /var/log/apache2/error.log # 清空日誌
su ubuntu # 切換回 ubuntu 使用者
```
