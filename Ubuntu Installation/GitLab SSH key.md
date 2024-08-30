
#### Generate SSH key
```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- 默認情況下，SSH key 會生成在 `~/.ssh/id_ed25519` 和 `~/.ssh/id_ed25519.pub`。
#### Duplicate SSH public key
```shell
cat ~/.ssh/id_ed25519.pub
```
- 將輸出的內容複製。
#### Add SSH public key to GitLab
```
Click avatar > Edit profile > SSH Keys > Add new key > paste public key
```
#### Test Connection
```shell
ssh -T git@gitlab.com
```
- 替換 [gitlab.com](https://about.gitlab.com/) 為公司 or 個人 GitLab domain name。
if success:
```
Welcome to GitLab, @your_username !
```
#### Set Git User Name
```shell
git config --global user.name "user_name"
git config --global user.email "user_email"
```
