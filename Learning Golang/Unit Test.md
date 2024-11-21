
### 1. 測試檔案命名規則
---
- 測試檔案必須以 `_test.go` 結尾
- 通常與被測試的檔案放在同一個資料夾
```go
// math.go
package math
```
```go
// math_test.go
package math
```
### 2. 測試函式命名規則
---
- 必須以 `Test` 開頭
- 後面接要測試的函式名稱
```go
func TestAdd(t *testing.T) {
	// 測試內容
}
```
### 3. 基本測試範例
---
- math.go
```go
package math

func Add(a, b int) int {
	return a + b
}
```
- math_test.go
```go
package math

import "testing"

func TestAdd(t *testing T) {
	got := Add(2, 3)
	want := 5
	
	if got != want {
		t.Errorf("Add(2, 3) = %d; want %d", got, want)
	}
}
```
### 4. 常用的測試方法
---
```go
// 報告測試失敗
t.Error("失敗訊息")
t.Errorf("格式化的失敗訊息: %v", 值)

// 立即終止測試
t.Fatal("嚴重錯誤訊息")
t.Fatalf("格式化的嚴重錯誤訊息: %v", 值)
```
### 5. 表格驅動測試 (Table-Driven Tests)
---
- 這是 Go 中很常見的測試模式
- 適合測試多組輸入/輸出組合
```go
func TestAdd(t *testing.T) {
	tests := []struct {
		name string
		a, b int
		want int
	}{
		{"正數相加", 2, 3, 5},
		{"加零", 5, 0, 5},
		{"負數相加", -1, -2, -3},
	}
	
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got := Add(tt.a, tt.b)
			if got != tt.want {
				t.Errorf("Add(%d, %d) = %d; want %d", tt.a, tt.b, tt.want)
			}
		})
	}
}
```
### 6. 執行測試命令
---
```bash
# 執行當前套件的所有測試
go test

# 執行特定測試函式
go test -run TestAdd

# 顯示詳細測試過程
go test -v

# 測試覆蓋率
go test -cover
```
- 測試覆蓋率是衡量程式碼被測試執行到的比例，它顯示了有多少程式碼被測試案例實際執行到，幫助開發者找出未被測試的程式碼區塊。
