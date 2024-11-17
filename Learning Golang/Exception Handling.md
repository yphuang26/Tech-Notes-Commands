
### 例外處理 Exception Handling
---
#### 1. 使用 `error` 類型處理錯誤
Go 的標準庫定義了一個內建的 `error` 接口，用於表示錯誤。
```go
type error interface {
	Error() string
}
```
- 用法範例：
```go
package main
import (
	"errors"
	"fmt"
)

func divide(a, b int) (int, error) {
	if b == 0 {
		return 0, errors.New("Cannot divide by zero")
	}
	return a / b, nil
}

func main () {
	result, err := divide(10, 0)
	if err != nil {
		fmt.Println("Error: ", err)
		return
	}
	fmt.Println("Result: ", result)
}
```
#### 2. 多值返回
Go 中的函數可以返回多個值，常見的慣例是返回一個「結果值」和一個「錯誤值」：
- 若無錯誤，錯誤值為 `nil`
- 若有錯誤，錯誤值會包含相貫訊息
```go
file, err := os.Open("file.txt")
if err != nil {
	fmt.Println("Failed to open file: ", err)
	return
}
defer file.Close()
```
#### 3. 自定義錯誤
可以使用標準庫中的 `errors.New` 或 `fmt.Errorf` 來創建錯誤，或者實現自定義的錯誤類型。
```go
type MyError struct {
	Code int
	Message string
}

func (e *MyError) Error() string {
	return fmt.Sprintf("Code: %d, Message: %s", e.Code, e.Message)
}

func riskyOperation() error {
	return &MyError{Code: 404, Message: "Resource not found"}
}

func main() {
	err := riskyOperation()
	if err != nil {
		fmt.Println("Error: ", err)
	}
}
```
#### 4. `panic` 和 `recover` 
Go 提供了類似其他語言的「例外機制」，主要用於處理應用程式遇到不可恢復的情況：
- `panic` : 觸發異常，停止正常控制流。
	- 一般用於處理無法繼續執行的情況，例如程式的邏輯錯誤、非法資料或關鍵資源的缺失。
- `recover` : 用於捕獲 `panic` ，使程式從異常中恢復繼續執行。通常配合 `defer` 使用，因為 `recover` 只能在被延遲執行的函數中有效。
```go
package main

import "fmt"

func mayPanic() {
	panic("something went wrong")
}

func main() {
	defer func() {
		if r := recover(); r != nil {
			fmt.Println("Recovered from panic: ", r)
		}
	}()
	mayPanic()
	fmt.Println("This will not be printed if panic is not recovered")
}
```
