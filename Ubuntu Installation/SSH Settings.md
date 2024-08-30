
Install OpenSSH server
```shell
# 查看 ssh 狀態
sudo systemctl status ssh
# 若顯示 Unit ssh.service could not be found:
sudo apt update
sudo apt install openssh-server
```

Start and enable SSH server
```shell
sudo systemctl start ssh
sudo systemctl enable ssh
```

Test SSH server
```shell
# 從本地 command line:
ssh username@vm_ip_address
```
