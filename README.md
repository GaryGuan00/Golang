# Golang Intro
Video: [Golang in 15 mins](https://www.bilibili.com/video/BV1HW4y1n7BF/?spm_id_from=333.337.search-card.all.click&vd_source=1f612caf29f3ec57efab5d6bced6b9c2)
1. Variable  
```go
a := 1 //inside a func body
var b = 2 //with initial value
var b int //no initial value then specify type
```

2. Variable types

int, int8, int16, int32, int64,
uint, uint8, uint16, uint32, uint64,  
uintptr,  
byte // unit8  
rune // int32  

float  
complex //复数  
bool  
string  

3. Loop: only for  
```go
// for loop
for i := 1; i<5; i++ {
	fmt.Println(i)
}

// while loop
i := 1
for i < 5 {
	...
}
```
4. Functions: func
```go
// Basic
func sum(a int, b int) int {
    return a + b
}

func main() {
    fmt.Println(sum(1, 2)) // 3
}

// Return mutiple values
func swap(a, b int) (int, int) {
    return b, a
}

func main() {
    a, b := swap(1, 2)
    fmt.Println(a, b) // 2 1
}

// func as param
func sum(a int, b int, transform func(int) int) int {
    return transform(a) + transform(b)
}

func main() {
    square := func(x int) int {
        return x * x
    }
    fmt.Println(sum(1, 2, square)) //5
}
```
5. Array
```go
// Fixed length:
a := [5]int{1, 2, 3, 4, 5}

// Changeable
a := make([]int, 0) // use make()
a := []int{1, 2, 3, 4} // not specify length

a = append(a, 1, 2, 3, 4)
a[0] = 5
```

6. Map
```go
// make()
m := make(map[string]int)
m["a"] = 1
m["b"] = 2

// initial map
m := map[string]int{
	"a": 1,
	"b": 2
}
fmt.Println(m) //map[a:1 b:2]
```

7. Class: struct
```go
type Point struct {
	X int
	Y int
}
func func main() {
    p := Point{1, 2}
	p.X = 3
}
```
8. Pointer
```go
// default: pass by value
q := p
p.X = 3
fmt.Println(q) // {1 2}
fmt.Println(p) // {3 2}

// pass by ref
q := &p
p.X = 3
fmt.Println(*q) // {3 2}
fmt.Println(p)  // {3 2}

q.Y = 10
fmt.Println(*q) // {3 10}

// Class func: outside struct
func (p Point) SetPoint(x, y int) {
    p.x = x
	p.y = y
}

p := Point{1, 2}
p.SetPoint(3, 4)
p // {1, 2}

// pass by ref
func (p *Point) SetPoint(x, y int) {
    p.x = x
    p.y = y
}
p := Point{1, 2}
p.SetPoint(3, 4)
p // {3, 4}
```
9. Interface
```go  
type Shape interface {
	Print()
}
type Rectangle struct{}
func (r Rectangle) Print() {
	fmt.Println("Rectangle")
}

func printShape(s Shape) {
	s.Print()
}

func main() {
    var s Shape
	s = Rectangle{}
	s.Print()
	printShape(s)
}
```
10. Exception
```go
n, err := fmt.Println("dd")
if err != nil {
	// success
} else {
	// fail
}
```
11. Concurrency: Goroutines
```go
// multi threads
func func1() {
	time.Sleep(500 * time.Millisecond)
    fmt.Println("func 1")
}
func func2()  {
    fmt.Println("func 2")
}

func main()  {
    go func2() // a new thread 
	func1()
}

// Concurrency: Channels
func func1(ch chan string) {
	ch <- "func1"
}
func func2(ch chan string) {
	ch <- "func2"
}

func main()  {
    ch := make(chan string)
	go func2(ch)
	res1 := <- ch
	
	go func1(ch)
	res2 := <- ch
}
```