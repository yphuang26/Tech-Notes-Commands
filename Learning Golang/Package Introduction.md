
### 包 Package
---
#### 基本概念
- 每個 Go 文件都必須聲明所屬的包名
- 包名通常使用小寫字母
- 同一個目錄下的所有 Go 文件必須使用相同的包名
#### 主要用途
- 封裝相關的功能和數據
- 控制程式碼碼的可見性
- 提高程式碼碼的重用性
#### 命名規範
```go
// 標準命名方式
package calculator    // 使用小寫字母
package imageutil     // 多個單詞直接連接
package userservice   // 不使用下劃線或駝峰命名

// 特殊情況
package main         // 可執行程序的入口包
package test         // 測試文件的包名（文件名以 _test.go 結尾）
```
#### 導入方式
```go
// 基本導入
import "fmt"
import "strings"

// 推薦的分組導入方式
import (
    "fmt"           // 標準庫包
    "strings"
    
    "github.com/user/project"  // 第三方包
    "mycompany/myproject"      // 私有包
)

// 導入時使用別名
import (
    "fmt"
    str "strings"              // 給 strings 包定義別名 str
    . "math"                   // 將包的內容直接導入當前命名空間（不推薦）
    _ "github.com/lib/pq"      // 僅執行包的 init() 函數，不使用包的其他內容
)
```
#### 包的目錄結構
```go
myproject/
  ├── main.go         // package main
  ├── user/
  │   ├── user.go     // package user
  │   └── helper.go   // package user（同目錄同包名）
  └── utils/
      └── format.go   // package utils
```
#### 可見性規則
```go
package user

// 大寫開頭的標識符可以被其他包訪問
type User struct {
    Name string    // 可導出（公開）
    age  int       // 不可導出（私有）
}

// 公開的函數
func CreateUser() *User {
    return &User{}
}

// 私有的函數
func validateUser(u *User) bool {
    return true
}
```
#### 包的初始化
```go
package database

// 包級變量會在 init 函數之前初始化
var connection = createConnection()

// init 函數在包被導入時自動執行
func init() {
    // 初始化代碼
    setupDatabase()
}
```
