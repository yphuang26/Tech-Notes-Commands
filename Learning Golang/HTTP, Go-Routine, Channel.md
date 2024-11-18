
### HTTP
---
Go 的標準庫提供了強大的 `net/http` 套件來處理 HTTP 請求和回應。
 1. **HTTP Server**: 使用 `http.ListenAndServe` 方法可以輕鬆啟動一個 HTTP 伺服器：
```go
package main

import (
	"fmt"
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintln(w, "Hello, World!")
}

func main() {
	http.HandleFunc("/", handler)
	http.ListenAndServe(":8080", nil)
}
```
- `handler` 是處理請求的函數，負責處理 HTTP GET、POST 等。
- `:8080` 是伺服器的端口號。
2. **HTTP Client**: 使用 `http.Get` 或 `http.Post` 可以方便地發送 HTTP 請求：
```go
resp, err := http.Get("https://example.com")
if err != nil {
	fmt.Println(err)
	return
}
defer resp.Body.Close()
```
### Go-Routine
---
Go-Routine 是 Go 中的 輕量級執行緒 (lightweight thread)，適合實現高效能並發。
1. 啟動 Go-Routine: 使用 `go` 關鍵字啟動一個新的 Go-Routine:
```go
func printMessage(message string) {
    fmt.Println(message)
}

func main() {
    go printMessage("Hello from a Go-Routine")
    fmt.Println("Main function finished")
}
```
- 主執行緒不會等待 Go-Routine 結束，需搭配同步機制（例如 `Channel` 或 `sync.WaitGroup` ）。
### Channel
---
Channel 是 Go 的通訊機制，用來在 Go-Routine 之間傳遞資料，實現同步與協調。
1. 宣告與使用：
```go
ch := make(chan string)

func sendData(ch chan string) {
    ch <- "Hello from channel"
}

func main() {
    go sendData(ch)
    message := <-ch
    fmt.Println(message)
}
```
- `ch <- "data"` : 將資料傳送到 Channel。
- `<-ch` : 從 Channel 接收資料。
2. 無緩衝與有緩衝 Channel:
	- 無緩衝（`make(chan T)`）：傳輸方需等待接收方接收後才能繼續執行。
	- 有緩衝（`make(chan T, bufferSize)`）：傳輸方可在緩衝區未滿時持續發送。
3. 關閉 Channel: 使用 `close` 關閉 Channel，表示不會再有資料寫入
```go
close(ch)
```
### 整合應用
---
以下是一個使用 Go-Routine 與 Channels 搭配 HTTP 的範例：
```go
package main

import (
    "fmt"
    "net/http"
    "sync"
)

func fetchURL(wg *sync.WaitGroup, url string, ch chan string) {
    defer wg.Done()
    resp, err := http.Get(url)
    if err != nil {
        ch <- fmt.Sprintf("Error fetching %s: %v", url, err)
        return
    }
    ch <- fmt.Sprintf("Fetched %s with status: %s", url, resp.Status)
}

func main() {
    urls := []string{"https://golang.org", "https://example.com"}
    var wg sync.WaitGroup
    ch := make(chan string)

    for _, url := range urls {
        wg.Add(1)
        go fetchURL(&wg, url, ch)
    }

    go func() {
        wg.Wait()
        close(ch)
    }()

    for msg := range ch {
        fmt.Println(msg)
    }
}
```
- 功能：
	- 並發地抓取多個 URL。
	- 使用 `Channel` 收集結果。
	- 使用 `WaitGroup` 確保所有工作完成。
