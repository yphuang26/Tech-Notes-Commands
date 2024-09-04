一般情況 Shell Script 常用於系統管理、自動化操作檔案、自動化重複的指令碼、分析 log 等文件檔案、列出我們想要的資料等，透過程式語言的使用來減少重複瑣碎的工作。

一般我們會使用 `.sh` 副檔名來命名 Shell Script 檔案，然後將該檔案設定為可執行:
```shell
chmod +x test.sh
```
執行 Shell Script 檔案:
```shell
./test.sh
```
### 基本輸入輸出
---
```shell
#!/bin/bash

read -p "Please enter your age:" Y_AGE
echo "你輸入的年齡是 $Y_AGE 歲"
```
### 變數
---
在 Shell Script 可以使用以下三種方式來宣告變數並給定值:
```shell
#!/bin/bash

variable1=value
variable2='value 2'
variable3="value 3"
```
使用變數方式為 `${變數名稱}` :
```shell
#!/bin/bash

pathName=demo.sh
echo ${pathName}
```
刪除變數使用 `unset` :
```shell
#!/bin/bash

pathName=demo.sh
unset pathName
echo ${pathName} # 印出空值
```
### 運算式
---
運算式是當運算子和運算元計算結果回傳後賦值給變數。
要執行運算式，其語法為 `$((運算式))` ，若是直接輸入則會變成字串相加:
```shell
#!/bin/bash

n=1
m=2
echo $n+$m    # 1+2
echo $((n+m)) # 3
```
在 Bash Shell 中內建原生不支援運算式，但我們可以使用 `expr` 、`awk` 等指令來實現運算式。
```shell
#!/bin/bash

result=`expr 10 + 2`
echo "Result: $result" # 12
```
### 條件判斷
---
在 Shell Script 中同樣可以使用 if...else 條件判斷，但是使用 `fi` 作為結尾 (為 `if` 的倒寫法，`case` 也是使用倒寫法 `esac` 作為結尾)。
> 比較條件需要放在 `[]` 中，前後要留白
#### if
```shell
#!/bin/bash

x=20
y=30

if [ $x == $y ]; then
	echo "value x is equal to value y"
fi

if [ $x != $y ]; then
	echo "value x is not equal to value y"
fi
```
#### if else
在 Shell Script 可以使用 `-gt` （greater than 縮寫）和 `-lt` （less than 縮寫）代表`大於`和`小於`，而 `-ge` （greater equal 縮寫）和 `-le`（less equal 縮寫）則是`大於等於`和`小於等於`的運算子符號。
`-eq` (equal 縮寫) 表示`等於` ，`-ne` (not equal 縮寫) 表示 `不等於` 。 
```shell
#!/bin/bash

if [ $x -gt $y ]; then 
	echo "value x is greater than value y"
else
	echo "value x is not greater than value y"
fi

if [ $x -lt $y ]; then
	echo "value x is not less than value y"
else
	echo "value x is not less than value y"
fi

if [ $x -ge $y ]; then
	echo "value x is greater or equal than value y"
else
	echo "value x is not greater than value y"
fi

if [ $x -le $y ]; then
	echo "value x is not less or equal than value y"
else
	echo "value x is not less or equal than value y"
fi
```
#### if elif else
```shell
#!/bin/bash

value1=20
value2=30
value3=30

if [ $value1 -gt $value2 ]; then
	echo "value1 is greater than value2"
elif [ $value1 == $value3 ]; then
	echo "value1 is equal to value3"
else
	echo "other result"
fi
```
#### case ... esac
```shell
#!/bin/bash

language="Java"

case $language in
	Java*) echo "是 Java!"
			;;
	Python*) echo "是 Python!"
			;;
	C*) echo "是 C!"
			;;
	*) echo "沒 match 到!"
esac
```
### 迴圈
---
#### for
Shell Script 的 `for` 使用方法和一班程式語言類似，同樣可以針對條件使用 `break` 、`continue` 來跳出或是跳過迴圈。
```shell
#!/bin/bash

for loop in 1 2 3; do
	echo "number: $loop"
done
```
#### while
```shell
#!/bin/bash

counter=0
while [ $counter -le 5 ]; do
	counter=`expr $counter + 1`
	echo $counter
done
```
#### until
```shell
#!/bin/bash

# 從 0 印出數字直到 10
counter=0
until [ $counter -gt 10 ]; do
	echo $counter
	counter=`expr $counter + 1`
done
```
### 函式
---
```shell
#!/bin/bash

function echoHello(){
	# hello world, rock!!
	echo "${0} hello ${1}, ${2}!!"
}

echoHello 'world' 'rock'
```
> 與一般程式語言比較不同的是其函式呼叫不需要由小括號傳入參數，直接以空白當作參數傳遞的格式。
> 參數從 1 開始，`${0}` 為檔名。
#### 特殊變數
Shell Script 支援許多好用的特殊變數，可以方便我們透過使用變數方式來設置程式執行的流程。

| 指令   | 描述                      |
| ---- | ----------------------- |
| `$0` | 目前的檔案檔名                 |
| `$n` | n 從 1 開始，代表第幾個參數        |
| `$#` | 傳遞到程式或函式目前有幾個參數         |
| `$*` | 傳遞到程式或函式所有參數            |
| `$@` | 類似 `$*` 但是在被雙引號包含時有些許不同 |
| `$?` | 上一個指令退出狀態或是函式的返回值       |
| `$$` | 目前 process PID          |
### 參考資料
---
- [簡明 Linux Shell Script 入門教學](https://blog.techbridge.cc/2019/11/15/linux-shell-script-tutorial/)
- [[Medium] Shell Script 簡易筆記](https://medium.com/@yihengwu/%E7%A8%8B%E5%BC%8F%E7%AD%86%E8%A8%98-shell-script-%E7%B0%A1%E6%98%93%E7%AD%86%E8%A8%98-841cfc3ae3ab)
