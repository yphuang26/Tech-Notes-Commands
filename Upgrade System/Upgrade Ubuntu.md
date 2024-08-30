
# Upgrade Ubuntu
### Step-by-Step Guide
Update the Package List
```shell
sudo apt update
sudo apt upgrade
sudo apt dist-upgrade
```
Remove Unused Packages
```shell
sudo apt autoremove
sudo apt clean
```
Install the Update Manager
```shell
sudo apt install update-mamnager-core
```
Begin the Upgrade Process
```shell
sudo do-release-upgrade
```
Restart System
```shell
sudo reboot
```
### Post-Upgrade
Check the Ubuntu Version
```shell
lsb_release -a
```
Restart Services
```shell
sudo apt apache2 restart
sudo apt mysql restart
sudo apt ssh restart
```
Check System journal
```shell
sudo journalctl -xe
```
### Troubleshooting
##### PHP 未正常顯示
```shell
# 完全刪除已安裝的 php
sudo apt purge php*
sudo apt autoremove
sudo apt clean
# 重新安裝 php
sudo apt update
sudo apt install php php-cli php-fpm php-mysql php-xml php-mbstring
# 檢查 php 安裝
php -v
# 重新啟動 apache
sudo apt apache2 restart
```
遇到的錯誤: 安裝的版本是 php 8.1，但顯示啟用的模組是舊的 php 7.4
```shell
# 檢查 php 模組是否啟用
ls /etc/apache2/mods-enabled/ | grep php
# 禁用舊版 php 模組
sudo a2dismod php7.4
# 啟用 php 8.1 模組
sudo a2enmod php8.1
# 重新啟動 apache
sudo apt apache2 restart
```
