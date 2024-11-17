
### 方法 Method
---
方法是附加到特定類型的函數。
```go
// 基本方法定義
type Rectangle struct {
	width float64
	height float64
}

// 值接收器的方法
func (r Rectangle) Area() float64 {
	return r.width * r.height
}

// 指標接收器的方法
func (r *Rectangle) Scale(factor float64) {
	r.width *= factor
	r.height *= factor
}

func main() {
	rect := Rectangle{width: 10, height: 5}
	
	// 呼叫方法
	area := rect.Area()
	rect.Scale(2) // 修改原始值
}
```
值接收器 vs 指標接收器：
- 值接收器：接收者的副本，不會修改原始值
- 指標接收器：直接對原始值進行操作
### 嵌入 Embedding
---
Golang 通過嵌入實現程式碼重用和組合。
```go
type Animal struct {
	Name string
	Age int
}

func (a Animal) Describe string {
	return fmt.Sprintf("%s us %d years old", a.Name, a.Age)
}

type Dog struct {
	Animal // 嵌入 Animal
	BreedType string
}

// 方法重寫
func (d Dog) Describe() string {
	return fmt.Sprintf("%s is a %s dog", d.Name, d.BreedType)
}

func main() {
	dog := Dog {
		Animal: Animal{Name: "Max", Age: 3},
		BreedType: "Labrador"
	}
	
	// 存取嵌入字段
	fmt.Println(dog.Name) // 直接存取
	fmt.Println(dog.Animal.Name) // 完整路徑存取
	fmt.Println(dog.Describe()) // 呼叫重寫的方法
}
```
嵌入的特點：
- 提供類似繼承的機制
- 允許直接存取嵌入類型的字段和方法
- 支援方法重寫
- 可以嵌入多個類型
### 介面 Interface
---
介面定義了一組方法集合，任何實現這些方法的類型都實現了該介面。
```go
// 基本介面
type Shape interface {
	Area() float64
	Perimeter() float64
}

// 實現介面
type Circle struct {
	radius float64
}

func (c Circle) Area() float64 {
	return math.Pi * c.radius * c.radius
}

func (c Circle) Perimeter() float64 {
	return 2 * math.Pi * c.radius
}

// 空介面
func PrintAny(any interface{}) {
	fmt.Printf("Type: %T, Value: %v\n", any, any)
}

// 介面組合
type Reader interface {
	Read(p []byte) (n int, err error)
}

type Writer interface {
	Write(p []byte) (n int, err error)
}

type ReadWriter interface {
	Reader
	Writer
}

// 型別斷言
func processShape(s Shape) {
	circle, ok := s.(*Circle)
	if ok {
		fmt.Printf("This is a circle with radius %f\n", circle.radius)
	}
}

func main() {
	var s Shape = Circle{radius: 5}
	
	// 介面使用
	fmt.Printf("Area: %f\n", s.Area())
	
	// 型別判斷
	switch v := s.(type) {
	case Circle:
		fmt.Printf("Circle with radius %f\n", v.radius)
	default:
		fmt.Println("Unknown shape")
	}
}
```
