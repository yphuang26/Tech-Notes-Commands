
Go 提供了幾個重要的**同步 (Synchronization) 機制**來協助處理併發程式設計，這些同步機制主要用於:
- 防止資料競爭 (Data Race)
- 確保臨界區的互斥訪問
- 協調多個 goroutine 的執行順序
- 實現安全的資料共享
### Mutex (互斥鎖)
---
```go
var mu sync.Mutex

mu.Lock() // 上鎖
// 臨界區程式碼
mu.Unlock() // 解鎖
```
### RWMutex (讀寫鎖)
---
```go
var rwmu sync.RWMutex

// 讀取鎖
rwmu.RLock()
// 讀取操作
rwmu.RUnlock()

// 寫入鎖
rwmu.Lock()
// 寫入操作
rwmu.Unlock()
```
### WaitGroup
---
- 用於等待一組 goroutine 完成
```go
var wg sync.WaitGroup

wg.Add(1)    // 新增一個等待項
go func() {
    defer wg.Done() // 完成時呼叫
    // 工作內容
}()
wg.Wait()    // 等待所有工作完成
```
### Channel
---
- 用於 goroutine 之間的通訊
```go
ch := make(chan int)    // 建立通道
go func() {
    ch <- 42           // 發送數據
}()
value := <-ch         // 接收數據
```
### Once
---
- 確保某段程式碼只執行一次
```go
var once sync.Once
once.Do(func() {
    // 只會執行一次的初始化程式碼
})
```
#### 實際例子
```go
package main

import (
    "fmt"
    "sync"
)

type Counter struct {
    mu    sync.Mutex // 互斥鎖，用於保護 count 變數
    count int // 計數器的值
}

func (c *Counter) Increment() {
    c.mu.Lock() // 取得鎖，確保只有一個 goroutine 能存取 count
    defer c.mu.Unlock() // 函數結束時自動解鎖
    c.count++ // 增加計數
}

func (c *Counter) GetCount() int {
    c.mu.Lock() // 取得鎖，確保讀取時資料一致性
    defer c.mu.Unlock() // 函數結束時自動解鎖
    return c.count // 返回當前計數值
}

func main() {
    counter := &Counter{} // 建立 Counter 實例
    var wg sync.WaitGroup // 建立 WaitGroup 用於等待所有 goroutine
    
    // 啟動 100 個 goroutine 同時增加計數
    for i := 0; i < 100; i++ {
        wg.Add(1) // WaitGroup 計數加 1
        go func() { // 啟動一個新的 goroutine
            defer wg.Done() // goroutine 結束時，WaitGroup 計數減 1
            counter.Increment() // 執行計數增加
        }()
    }
    
    wg.Wait() // 等待所有 goroutine 完成
    fmt.Printf("Final count: %d\n", counter.GetCount()) // 輸出最終計數結果
}
```
