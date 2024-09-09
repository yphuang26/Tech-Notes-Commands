### SSH 登入遠端執行命令
---
```shell
#!/bin/bash

REMOTE_USER="remote_user"
REMOT_HOST="remote_host"

ssh -o StrictHostKeyChecking=no -T ${REMOTE_USER}@${REMOTE_HOST} << EOF
echo "Hello World"
exit
EOF
```
> `exit` : 用來結束當前的 shell 或腳本。當在 SSH 會話中使用 `exit` 時，它會結束該遠端對話並返回本地終端。
> `EOF` : 是 "End of File" 的縮寫。在 `here document` 中，`EOF` 是一個標記，用來指示多行字符串的結束。這個標記必須是在行首，且沒有多餘的空格或縮進。
> 參考: [SSH 登入遠端執行命令](https://blog.toright.com/posts/6556/ssh-remote-script)

**-o StrictHostKeyChecking=no**: 用來告訴 `ssh` 客戶端在連接到新的或未知的主機時，不要提示用戶確認主機的公鑰。這樣可以自動接受新的主機密鑰，避免手動確認，這在自動化腳本中非常有用。
**-T**: 這個選項用來禁止終端機相關的輸出。當你只需要執行單個命令而不需要交互式 shell 時，可以使用這個選項。這樣可以避免一些不必要的輸出，並且在某些情況下可以提高性能。

#### here document
`here document` 是一種在 shell 腳本中使用的語法，用來將多行文本傳遞給命令。它允許在腳本中嵌入多行命令而不需要使用多個 `echo` 或其他方法。`here document` 的基本語法如下:
```shell
command << delimiter
text
delimiter
```
> `command` : 要執行的命令。
> `delimiter` : 一個標記，用來指示多行文本的開始和結束。常見的標記是 `EOF` 。
> `text` : 想要傳遞命令的多行文本。

#### SSH 連線執行本地端腳本
```shell
#!/bin/bash

REMOTE_USER="remote_user"
REMOT_HOST="remote_host"

# remote_commands.sh 存放欲執行的指令
ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} < remote_commands.sh
```
### SSH 處理 password 的方式
---
- 需手動輸入 password:
```shell
#!/bin/bash

REMOTE_USER="remote_user"
REMOT_HOST="remote_host"

ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST}
```
- 使用 `sshpass` 不需手動輸入 password (但只能在 Linux 環境):
```shell
#!/bin/bash

REMOTE_USER="remote_user"
REMOT_HOST="remote_host"
REMOTE_PASSWORD="remote_password"

sshpass -p ${REMOTE_PASSWORD} ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST}
```
- 使用 `plink.exe` 不需手動輸入 password (但需要安裝 puTTY):
```shell
REMOTE_USER="remote_user"
REMOT_HOST="remote_host"
REMOTE_PASSWORD="remote_password"
HOST_KEY_FINGERPRINT="host_key_fingerprint"

plink.exe -ssh ${REMOTE_USER}@${REMOTE_HOST} -pw ${REMOTE_PASSWORD} -hostkey ${HOST_KEY_FINGERPRINT}
```
