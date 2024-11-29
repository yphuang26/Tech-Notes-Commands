
目前 Ubuntu 使用 Netplan 作為新的網路管理工具。
### 查看 Netplan 配置
---
1. 查看 `/etc/netplan` 目錄:
```shell
ls /etc/netplan
```
(通常會看到類似 `50-cloud-init.yaml` 或其他 `.yaml` 文件。)
2. 打開配置文件查看內容:
```shell
sudo vi /etc/netplan/50-cloud-init.yaml
```
### 編輯 Netplan 配置文件
---
##### 假設有以下網路介面
- 有線網路介面: `enp0s3` 
- 另一個介面 (可能是另一個有線或無線): `enp0s8` 
##### 配置文件範例
```
network:
    ethernets:
        enp0s3:
            dhcp4: true
        enp0s8:
            dhcp4: true
    version: 2
```
假設想禁用 `enp0s3` (將它改為 false): 
```
network:
    ethernets:
        enp0s3:
            dhcp4: false
        enp0s8:
            dhcp4: true
    version: 2
```
##### 應用更改
1. 檢查配置是否正確:
```bash
sudo netplan generate
```
2. 應用配置:
```bash
sudo netplan apply
```
