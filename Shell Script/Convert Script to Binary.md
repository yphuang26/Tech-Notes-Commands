
### 方法一: 使用 `shc` 
---
`shc` 是一個常見的工具，可以將 shell 腳本編譯成二進制可執行文件。它支持靜態和動態鏈接，適用於 Linux 系統。
1. 安裝 `shc` : 
```shell
wget http://www.datsi.fi.upm.es/%7Efrosal/sources/shc-3.8.9.tgz
tar -xvzf shc-3.8.9.tgz
cd shc-3.8.9
make
sudo make install
```
2. 編譯腳本: 
```shell
shc -f my_script.sh
```
會生成兩個文件: `my_script.sh.x` (可執行文件) 和 `my_script.sh.x.c` (C 原始碼，可刪) 。
3. 執行腳本:
```shell
./my_script.sh.x
```
### 方法二: 使用`gzexe` 
---
`gzexe` 是另一種方法，它可以將腳本壓縮並加密，但不如 `shc` 安全。適用於 Windows 和 Linux 系統。
1. 壓縮腳本:
```shell
gzexe my_script.sh
```
會生成一個壓縮的可執行腳本，原始腳本會被備份為 `my_script.sh~` 。
2. 執行壓縮後的腳本:
```shell
./my_script.sh
```
執行時會解壓縮到 `/tmp` 資料夾，結束後自動刪除。
### 方法三: 使用 `base64` 編碼
---
```shell
#!/bin/bash
# 步驟 1: 讀取原始腳本
original_script=$(cat 'my_script.sh')
# 步驟 2: 將腳本編碼為 base64 
encoded_script=$(echo "$original_script" | base64 | tr -d '\n')
# 步驟 3: 創建新的自解碼腳本
cat > obfuscated_script.sh << 'EOL'
#!/bin/bash
# 混淆的腳本內容
ENCODED_SCRIPT="ENCODED_CONTENT_PLACEHOLDER"

# 解碼並執行腳本
decoded_script=$(echo "$ENCODED_SCRIPT" | base64 --decode)
bash <(echo "$decoded_script")
EOL

# 步驟 4: 替換佔位符為實際的編碼內容 
sed -i "s/ENCODED_CONTENT_PLACEHOLDER/$encoded_script/" obfuscated_script.sh

# 步驟 5: 使腳本可執行 
chmod +x obfuscated_script.sh

echo "混淆後的腳本已創建: obfuscated_script.sh"
```
執行完後，會生成一個經過 `base64` 編碼的腳本。
