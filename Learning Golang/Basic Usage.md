
### 變數 Variable
---
在 Go 中會用 `var` 來定義變數，不同的是要將型態宣告寫在後面。
```go
package main
import "fmt"
func main() {
	var x, y, z int
	var c, python, java bool
	fmt.Println(z, y, z, c, python, java)
	// 輸出結果為: 0 0 0 false false false
}
```
初始化變數
```go
package main
import "fmt"
func main() {
	var a, b, c int = 1, 2, 3
	var first, second, third = true, false, "Third"
	fmt.Println(a, b, c, first, second, third)
	// 輸出結果為: 1 2 3 true false Third
}
```
定義多行字串，可以使用反引號來定義
```go
str1 := `IronMan,  
his name is Tony Stark,  
and he is my favorite hero.`
```
`:=` 簡潔賦值語句可以替代 `var` 定義
```go
package main
import "fmt"
func main() {
	a, b, c := 1, 2, 3
	first, second, third := true, false, "Third"
	fmt.Println(a, b, c, first, second, third)
}
```
### 常數 Constant
---
Go 常數的宣告和變數差不多，只是把關鍵字 `var` 換成 `const` 。
```go
// 單一宣告
const pi = 3.141592
const e = 2.718281
// 多重宣告
const (  
	pi = 3.141592  
	e = 2.718281  
)
```
### 迴圈 For Loop
---
在 Go 語言中，只有一種迴圈語法，就是 `for` 迴圈，它可以模擬多種其他語言的迴圈結構（如 `while` 和 `do-while`）。
#### 基本 `for` 迴圈語法
```go
for i := 0; i < 5; i++ {
	fmt.Println(i) // 會輸出 0 到 4
}
```
#### 作為 `while` 迴圈
```go
i := 0
for i < 5 {
	fmt.Println(i)
	i++
}
```
#### 無限迴圈
- 如果連條件句也省略掉，`for` 迴圈就會變成一個無限迴圈，通常用在伺服器、監聽等需要持續執行的場景中：
```go
for {
	// 回圈內部程式碼
	// 要在內部用 `break` 或 `return` 來結束迴圈，否則程式會一直執行下去。
}
```
#### 使用 `range` 遍歷集合
- 在 Go 中，`for` 也可以配合 `range` 使用，來遍歷陣列、切片、字典等集合類型：
```go
nums := []int{2, 4, 6, 8}
for index, value := range nums {
	fmt.Printf("索引: %d, 值: %d\n", index, value)
}
```
- 可以用 `_` 來忽略索引:
```go
for _, value := range nums {
	fmt.Println(value)
}
```
#### 其他控制語句
- `break` : 立即跳出迴圈。
- `continue` : 跳過當前迭代，繼續下一次迴圈。
```go
for i := 0; i < 10; i++ {
	if i%2 == 0 {
		continue // 跳過偶數
	}
	fmt.Println(i) // 只輸出奇數
}
```
### 流程控制
---
#### If-Else
- 基本語法
```go
if 條件 {
    // 條件為 true 時執行的程式碼
} else if 其他條件 {
    // 上述條件不成立時，且其他條件成立時執行的程式碼
} else {
    // 所有條件都不成立時執行的程式碼
}
```
- 範例
```go
age := 18
if age >= 18 {
    fmt.Println("成年人")
} else if age >= 13 {
    fmt.Println("青少年")
} else {
    fmt.Println("兒童")
}
```
#### Switch-Case
- 基本語法
```go
switch 表達式 {
case 值1:
    // 當表達式等於 值1 時執行的程式碼
case 值2:
    // 當表達式等於 值2 時執行的程式碼
default:
    // 如果表達式不匹配任何值時執行的程式碼
}
```
- 範例
```go
day := "Monday"
switch day {
case "Monday":
    fmt.Println("星期一")
case "Tuesday":
    fmt.Println("星期二")
default:
    fmt.Println("其他天")
}
```
##### 無表達式的 `switch` ，類似 `if...else if` 結構：
```go
age := 20
switch {
case age >= 18:
    fmt.Println("成年人")
case age >= 13:
    fmt.Println("青少年")
default:
    fmt.Println("兒童")
}
```
##### `fallthrough` 語句
Go 中的 `switch` 預設不會自動執行下一個 `case`，如果想要在匹配條件後繼續執行下個 `case`，可以使用 `fallthrough`：
```go
num := 2
switch num {
case 1:
    fmt.Println("One")
case 2:
    fmt.Println("Two")
    fallthrough
case 3:
    fmt.Println("Three")
default:
    fmt.Println("Other")
}
// 會輸出:
// Two
// Three
```
### 陣列 Array
---
- **固定長度**: 陣列的長度在宣告後無法更改。
- **零值初始化**：當陣列創建後，會自動用元素的零值填充（例如 `int` 型別會是 `0`，`string` 會是 `""`）。
- **值型別**：陣列是值型別，當把一個陣列賦值給另一個變數時，會進行整體拷貝，而不是引用。
#### 宣告方式
```go
var arr [5]int // 宣告一個包含 5 個 int 型別元素的陣列
arr := [5]int{1, 2, 3, 4, 5} // 使用初始宣告
arr := [...]int{1, 2, 3} // 省略長度，讓編譯氣根據初始值數量推斷長度
```
#### 用法範例
```go
package main
import "fmt"

arr := [3]int{10, 20, 30}
fmt.Println(arr[0]) // 訪問陣列的第一個元素，輸出: 10
arr[1] = 25 // 修改陣列的元素
fmt.Println(len(arr)) // 獲取陣列的長度，輸出: 3
```
### 切片 Slice
---
- **動態長度**：切片的長度可以動態增長或縮減。
- **引用型別**：切片是引用型別，操作切片時實際上是對底層陣列進行操作。將一個切片賦值給另一個變數，兩者指向同一個底層陣列。
- 如果我們用 `append` 函數動態添加元素，當切片超過容量時，Go 會自動擴展底層陣列的容量。
#### 宣告方式
- 長度 (length): 長度是指切片中的元素數量。
- 容量 (capacity): 容量是指從切片的起始位置到底層陣列結尾之間的元素數量。
```go
// 使用 make 函數創建切片
slice1 := make([]int, 3) // 長度和容量都為 3
slice2 := make([]int, 3, 5) // 長度為 3，容量為 5

// 使用字面量宣告
slice3 := []int{1, 2, 3} // 長度為 3，容量為 3
```
#### 用法範例
```go
slice := []int{1, 2, 3}
slice = append(slice, 4, 5) // 使用 append 增加元素
fmt.Println(slice) // 輸出: [1 2 3 4 5]
fmt.Println(len(slice)) // 輸出切片長度: 5
fmt.Println(cap(slice)) // 輸出切片容量: 6 (根據情況可能不同)

// 使用切片創建新的切片
newSlice := slice[1:3] // 創建一個從索引 1 到 2 的新切片
fmt.Println(newSlice) // 輸出: [2 3]
```