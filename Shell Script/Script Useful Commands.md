
### 建立 `tmp` 資料夾
---
```shell
TMP_DIR=$(mktemp -d)
```
這條指令在 Unix/Linux 系統中用於創建一個臨時目錄並將其路徑存到變數 `TMP_DIR` 中。
1. `mktemp -d` : 
	- `mktemp` : 用來創建臨時文件或目錄。
	- `-d` : 告訴 `mktemp` 創建一個臨時目錄，而不是文件。
2. `TMP_DIR=$(...)` : 
	- `$()` 是命令替換的語法，這意味著執行括號內的命令並將其輸出結果賦值給變量。
	- 在這種情況下，`mktemp -d` 的輸出（即新創建的臨時目錄的路徑）會被賦值給變量 `TMP_DIR`。
#### 寫成 function 範例:
```shell
create_tmp_file() {
	TMP_DIR=$(mktemp -d)
	if [[ ! "$TMP_DIR" || ! -d "$TMP_DIR" ]]; then
		echo "Error: Can't create tmp directory" >&2
		exit 1
	fi
	trap 'rm -rf "$TMP_FILE"' EXIT
}
```
#### 預設 `tmp` 路徑
**Linux**
- 預設 `tmp` 路徑: `/tmp` 
- 在大多數 Linux 發行版本中，`tmp` 是一個全局可訪問的臨時目錄，所有用戶都可以在此創建臨時文件。這個目錄通常會在系統重啟時被清空。
**Windows**
- 預設 `tmp` 路徑: 通常是 `%TEMP%` 或是 `%TMP%` 
- 在 Windows 中，這些環境變數指向用戶的臨時文件夾，通常位於 `C:\Users\<username>\AppData\Local\Temp` 。這個目錄是用戶專用的，並且會在系統重啟後保留，但某些應用可能會定期清理這個目錄。
**MacOS**
- 預設 `tmp` 路徑: `$TMPDIR` 
- 在 macOS 中，臨時文件的路徑通常是由環境變數 `$TMPDIR` 指定，這個路徑可能類似於 `/var/folders/<random>/T/` 。此外，macOS 還有一個全局的臨時目錄 `/tmp` ，這個目錄實際上是指向 `/private/tmp/` 的符號鏈接。
### 安裝套件 (以 `sshpass` 為例)
---
```shell
install_sshpass() {
	apt update
	if [ $? -ne 0 ]; then
		echo "Permission denied, retrying with sudo..."
		sudo apt update
	fi

	echo "Installing sshpass..."
	apt install -y sshpass
	if [ $? -ne 0 ]; then
		echo "Permission denied, retrying with sudo..."
		sudo apt install -y sshpass
	fi
}

if ! command -v sshpass &> /dev/null; then
	install_sshpass
fi
```
### 讀取 config 文件
---
config 文件如下
```
user="remote_user"
password="remote_password"
```
要讀取 username 和 password ，並存到變數 `$REMOTE_USER` 和 `$REMOTE_PASSWORD` 中
```shell
CONFIG_FILE="${TMP_DIR}/ssh_config.txt"
REMOTE_USER=$(grep '^user=' "${CONFIG_FILE}" | cut -d'"' -f2)
REMOTE_PASSWORD=$(grep '^password=' "${CONFIG_FILE}" | cut -d'"' -f2)
```
### `trap` 的使用
---
基本語法為:
```shell
trap 'commands' signals
```
- `commands` : 當接收到指定的 `signals` 時要執行的命令。
- `signals` : 要捕獲的訊號，可以是單個訊號或多個訊號的列表。
`trap` 是一個在 Unix/Linux 系統中使用的 shell 內建指令，主要用來捕獲和處理訊號。這個命令允許用戶在腳本中指定當接收到特定訊號時應該執行的命令或操作。
#### 功能與用途
- 訊號捕獲: `trap` 可以捕獲多種訊號，例如 `SIGINT` (通常由 Ctrl+C 觸發)、`SIGTERM` (終止訊號) 等。使用者可以自定義這些訊號的處理方式。例如忽略訊號、執行清理操作或顯示提示訊息。
- 特殊訊號: 除了傳統的系統訊號外，`trap` 還可以處理一些特殊的 shell 訊號，如 `EXIT` (當腳本結束時執行)、`ERR` (當命令返回非零狀態時執行) 以及 `DEBUG` (每條命令執行前執行)。
#### 使用範例
捕獲 Ctrl+C:
```shell
trap 'echo "Caught SIGINT!"' SIGINT
```
清理臨時文件:
```shell
trap 'rm -f /tmp/tempfile' EXIT
```
調試訊息:
```shell
trap 'echo "Error occurred at line $LINENO"' ERR
```
- 設置的訊號處理器僅影響當前 shell 進程及其子進程，並不會影響其他進程。
- 使用 `trap -l` 可以列出所有可用的訊號，使用 `trap -p` 可以顯示當前已設置的訊號處理器。
