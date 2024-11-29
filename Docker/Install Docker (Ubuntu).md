

### 安裝 Docker
---
```shell
sudo apt update && sudo apt upgrade -y
```
```shell
sudo apt install -y ca-certificates curl gnupg lsb-release
```
添加 Docker 的官方 GPG 密鑰:
```shell
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
設置 Docker 的軟體倉庫:
```shell
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
安裝 Docker Engine:
- 更新套件索引:
```shell
sudo apt update
```
- 安裝 Docker 套件:
```shell
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
啟動和測試 Docker:
- 確保 Docker 服務正在運行:
```shell
sudo systemctl start docker
sudo systemctl enable docker
```
### 設置用戶使用 Docker 的權限
---
默認情況下，只有 `root` 和 `sudo` 用戶可以使用 Docker。如果希望其他用戶也能運行 Docker，可以執行以下命令:
```shell
sudo usermod -aG docker ${USER}
```
### 完整刪除 Docker 步驟
---
- [How to completely uninstall docker](https://askubuntu.com/questions/935569/how-to-completely-uninstall-docker)
