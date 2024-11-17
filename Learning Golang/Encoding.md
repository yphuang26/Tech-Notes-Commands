
`encoding` 是一組用於將資料進行編碼和解碼的功能套件，涵蓋各種格式（如 JSON、XML、CSV、Base64 等）。這些工具主要幫助開發者將結構化的數據轉換為不同格式，以便於傳輸或儲存，以及從這些格式中恢復資料。
#### 常用的 `encoding` 標準套件

| 套件名             | 用途              |
| --------------- | --------------- |
| encoding/json   | 處理 JSON 編碼與解碼   |
| encoding/xml    | 處理 XML 編碼與解碼    |
| encoding/csv    | 處理 CSV 格式的讀寫    |
| encoding/base64 | Base64 編碼與解碼    |
| encoding/binary | 處理二進制資料序列化和反序列化 |
| encoding/hex    | 將資料轉換為十六進制表示    |
#### `encoding/json`
```go
package main

import (
    "encoding/json"
    "fmt"
)

type User struct {
    ID    int    `json:"id"`
    Name  string `json:"name"`
    Email string `json:"email"`
}

func main() {
    // 結構體 -> JSON (編碼)
    user := User{ID: 1, Name: "Alice", Email: "alice@example.com"}
    jsonData, _ := json.Marshal(user)
    fmt.Println(string(jsonData)) // {"id":1,"name":"Alice","email":"alice@example.com"}

    // JSON -> 結構體 (解碼)
    var decodedUser User
    jsonStr := `{"id":2,"name":"Bob","email":"bob@example.com"}`
    json.Unmarshal([]byte(jsonStr), &decodedUser)
    fmt.Printf("%+v\n", decodedUser) // {ID:2 Name:Bob Email:bob@example.com}
}
```
#### `encoding/csv`
```go
package main

import (
    "encoding/csv"
    "fmt"
    "strings"
)

func main() {
    // 寫入 CSV (編碼)
    var data = [][]string{
        {"Name", "Age", "Email"},
        {"Alice", "30", "alice@example.com"},
        {"Bob", "25", "bob@example.com"},
    }
    var csvBuilder strings.Builder
    writer := csv.NewWriter(&csvBuilder)
    writer.WriteAll(data) // 將多行寫入
    writer.Flush()
    fmt.Println(csvBuilder.String())

    // 讀取 CSV (解碼)
    csvData := `Name,Age,Email
Alice,30,alice@example.com
Bob,25,bob@example.com`
    reader := csv.NewReader(strings.NewReader(csvData))
    records, _ := reader.ReadAll()
    fmt.Println(records) // [[Name Age Email] [Alice 30 alice@example.com] [Bob 25 bob@example.com]]
}
```
#### `encoding/base64`
```go
package main

import (
    "encoding/base64"
    "fmt"
)

func main() {
    // 編碼
    data := "Hello, Go!"
    encoded := base64.StdEncoding.EncodeToString([]byte(data))
    fmt.Println(encoded) // SGVsbG8sIEdvIQ==

    // 解碼
    decoded, _ := base64.StdEncoding.DecodeString(encoded)
    fmt.Println(string(decoded)) // Hello, Go!
}
```
