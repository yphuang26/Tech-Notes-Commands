
### 指標 Pinter
---
指標用於儲存變數的記憶體位址。
```go
// 基本用法
x := 42
var p *int = &x // p 儲存 x 的記憶體位址
fmt.Println(*p) // 使用 * 取得指標指向的值
*p = 21 // 通過指標修改值

// 常見用法
func modifyValue(x *int) {
	*x = 100 // 修改指標指向的值
}
```
- Swap function
```go
func swap(a *int, b *int) {
	temp := *a
	*a = *b
	*b = temp
}

func main() {
	x := 5
	y := 10
	fmt.Printf("交換前: x = %d, y = %d\n", x, y)
	swap(&x, &y)
	fmt.Printf("交換後: x = %d, y = %d\n", x, y)
}
```
### 映射 Map
---
Map 是鍵值對的集合，類似其他語言的字典或雜湊表。
```go
// 宣告和初始化
scores := map[string]int{
	"Alice": 98,
	"Bob": 87,
}

// 操作 Map
scores["Carol"] = 95 // 新增、修改
score, exists := scores["Alice"] // 檢查鍵是否存在
delete(scores, "Bob") // 刪除
len(scores) // 取得 map 長度

// 使用 make 創建 (動態配置)
userAges := make(map[string]int)
userAges["Alice"] = 25
userAges["Bob"] = 30
```
### 結構 Struct
---
Struct 用於將不同類型的資料組合成一個自定義類型。
```go
// 定義結構
type Person struct {
	Name string
	Age int
	Address string
}

// 建立實例
p1 := Person {
	Name: "Alice",
	Age: 25,
	Address: "Taipei",
}

// 使用點運算符訪問
fmt.Println(p1.Name)

// 結構體指標
p2 := &Person{Name: "Bob"}
fmt.Println(p2.Name) // 自動解引用
```
- 進階用法
```go
// 嵌入式結構體
type Employee struct {
	Person // 匿名欄位，繼承所有 Person 的欄位
	Position string
	Salary float64
}

// 方法
func (p Person) Greet() string {
	return "Hello, I'm " + p.Name
}
```