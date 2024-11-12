
### 安裝 Go
---
[到 Go 官網下載安裝包](https://go.dev/)，並執行以下命令來確認安裝:
```shell
go version
```
### 執行 Go
---
#### 1. `go build main.go` 
- 目的: 編譯 Go 程式並生成可執行檔。
- 運作方式: 這個命令會將 `main.go` 源代碼編譯成可執行檔（通常是與檔案同名的檔案，如 `main` 或 `main.exe`，取決於作業系統）。
- 結果：產生一個可執行檔，然後可以直接執行它，而不需要每次都使用 `go run`。
```shell
go build main.go
```
- 編譯完成後，必須手動執行生成的檔案:
```shell
./main # 在類 Unix 系統（Linux, macOS）上執行
main.exe # 在 Windows 上執行
```
#### 2. `go run main.go` 
- 目的: 直接執行 Go 程式，而不產生可執行檔。
- 運作方式: 這個命令會先編譯 Go 程式然後立即執行，而不會在磁碟上生成可執行檔。
```shell
go run main.go
```
### 範例: Hello World
---
建立一個名為 `main.go` 的文件:
```go
package main

import "fmt"

func main() {
	fmt.Println("Hello, World!")
}
```
執行以下命令來運行程式:
```go
go run main.go
```
### fmt
---
`fmt` 是 Go 標準函式庫中的一個套件，用於格式化輸出和處理字串，類似於其他語言的輸出功能，如 `print` 或 `printf`。在 Go 中，`fmt` 是一個非常常用的套件，可以幫助我們進行文字輸出到終端、讀取輸入以及格式化字串。
#### 常用的 `fmt` 函式
1. **`fmt.Println`**：將內容輸出到終端，並自動在最後加上換行。
```go
fmt.Println("Hello, World!")
// 輸出: Hello, World!
```
2. **`fmt.Printf`**：格式化輸出，類似於 C 語言的 `printf`，可以使用格式化參數來控制輸出樣式。
```go
name := "Alice"
age := 30
fmt.Printf("Name: %s, Age: %d\n", name, age)
// 輸出: Name: Alice, Age: 30
```
3. **`fmt.Sprint`** 和 **`fmt.Sprintf`**：這兩個函式返回格式化後的字串，而不是直接輸出。`Sprint` 類似於 `Println`，`Sprintf` 類似於 `Printf`。
```go
greeting := fmt.Sprintf("Hello, %s!", name)
fmt.Println(greeting)
// 輸出: Hello, Alice!
```
4. **`fmt.Scan` 和 `fmt.Scanf`**：用於讀取用戶輸入。`Scan` 讀取空白分隔的值，`Scanf` 則允許格式化讀取。
```go
var input string
fmt.Print("Enter your name: ")
fmt.Scan(&input)
fmt.Println("Hello,", input)
```
