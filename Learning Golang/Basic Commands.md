
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
在 Go 裡面，迴圈只有 `for` (沒有 `while` 或是 `do ... while` )。
```go
package main
import "fmt"
func main() {
	sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
}
```
### 流程控制
---
