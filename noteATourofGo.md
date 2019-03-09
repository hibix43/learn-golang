# Note - [A Tour of Go](https://tour.golang.org/welcome/1)

## import path

When use the packages from `import("math/rand")`, it begin with `rand`.

`import("math")` is factored import.
Use example is `math.Sqrt()` and `math.rand.Intn()`.

## name

A name is exported if it begins with a capital letter.
Don't use `math.pi`, Use `math.Pi`.

## function

```golang
func add(x int, y int) int {
    return x + y
}

// omit type
func add(x, y int) int {}
```

Return multiple results.

```golang
func swap(x, y string) (string, string) {
    return y, x
}
```

If without arguments, return named return values(x and y).

It is called "Naked return".

Only short function, Don't use it at long function.

```golang
func split(sum int) (x, y int) {
    x = sum * 4 /9
    y = sum - x
    return
}
```

## variables

`var` declares a list of variables. Its type is last.

```golang
var c, python, java bool
```

Declare can include initial value. It always need one initial value __per variables__.

```golang
var i, j int = 1, 3
// var i, j int = 2
```

If it have initial value, type can be omitted.

```golang
var c, python, java = true, false, "no!"
```

`:=` can be ued in instead of `var`. __Only inside a function.__

```golang
// a := 5
var a = 5
func main() {
    var i, j int = 1, 2
    k := 3
    c, python, java := true, false, "no!"
}
```

## basic type

`%T` show the variable type.

```golang
bool

string

// int, uint, uintptr is 32bit on 32bit systems, 64bit on 64bit systems
int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128 // ex)cmplx.Sqrt(-5 + 12i)
```

When declaribe different type variables, use `var()`

```golang
var (
    a int = 1
    b string = "ok"
    c = 2
)
```

## defalut values

```golang
var i int // 0
var f float64 // 0
var b bool // false
var s string // ""
```

## type conversions

```golang
i := 42
f := float64(i)
u := unit(f)

var u2 unit = unit(f) //ok
// var u3 unit = f NG
```

## constants

```golang
const Pi = 3.14
// const Pi := 3.14
```

## for

`for` is only loop syntax in golang. `()` is unneed, `{}` is always required.

```golang
sum := 0
for i := 0; i < 10; i++ {
    sum += i
}
fmt.Println(sum)
```

It is how to use like "while".

```golang
sum := 1
for ; sum < 1000; {
    sum += sum
}
for sum < 1000 {
    sum += sum
}

// forever loop
for {
}
```

## if

```golang
func sqrt(x float64) string {
    if x < 0 {
        return sqrt(-x) + "i"
    }
    return fmt.Sprint(math.Sqrt(x))
}
```

`if` can start with a short statement. Use `v` inside of the else block.

```golang
func pow(x, n, lim float64) float64 {
    if v := math.Pow(x, n); v < lim {
        return v
    } else {
        fmt.Printf("%g >= %g\n", v, lim)
    }
    // don't use v
    return lim
}
```

## Exercise: Loops and Functions

omission

## switch

Don't need write `break`. Automatically given.

```golang
switch os := runtime.GOOS; os {
    case "darwin":
        fmt.Println("OS X.")
    case "linux":
        fmt.Println("Linux.")
    default:
        fmt.Printf("%s.\n", os)
}
```

`case`s condition can use variables and formulas in addition with constants.

```golang
today := time.Now().Weekday()
switch time.Saturday {
case today + 0:
    fmt.Println("Today.")
case today + 1:
    fmt.Println("Tomorrow.")
case today + 2:
    fmt.Println("In two days.")
default:
    fmt.Println("Too far away.")
```

## defer

`defer` is executed at the time functions is closed. But, evaluation is immediately.

```golang
func main() {
    defer fmt.Println("world")
    fmt.Println("hello")
}
```

Execution of `defer` functions are pushed onto stack.

```golang
func main() {
    for i := 0; i < 10; i++ {
        defer fmt.Println(i)
    }
    fmt.Println("done")
}
```

## pointer

A pointer holds the memory adress of a value.

`*T` type is a pointer to a `T`. Its zero value is `nil`.

Go has no pointer arithmetic.

```golang
func main() {
    i, j = 42, 2701
    p := &i         // point to i
    fmt.Println(*p) // read i through the pointer : 42
    *p = 21         // set i through the pointer
    fmt.Println(i)  // see the new value of i : 21

    p = &j         // point to j
    *p = *p / 37   // divide j through the pointer
    fmt.Println(j) // see the new value of j : 2071/37=73
}
```

## structs

`structs` is collection of fields variables.

Using a dot to access struct fields.

Set to fields by using the `Name: value`. The order is irrelevant.

```golang
type Vertex struct {
    X int
    Y int
}
var (
    v1 = Vertex{1, 2}  // has type Vertex
    v2 = Vertex{X: 1}  // Y:0
    v3 = Vertex{}      // X:0 and Y:0
    pp  = &Vertex{1, 2} // has type *Vertex:pointer
)
func main() {
    v := Vertex{1, 2}
    v.X = 4
    fmt.Println(v.X) // 4

    p := &v
    p.X = 1e9 // instead of (*p).X
    fmt.Println(v) // {1000000000 2}

    fmt.Println(v1, pp, v2, v3) // {1 2} &{1 2} {1 0} {0 0}
}
```

## array

`[n]T` is an array of n values of type `T`.Arrays can't be resized.

```golang
func main() {
    var a [2]string
    a[0] = "Hello"
    a[1] = "World"
    fmt.Println(a[0], a[1]) // Hello World
    fmt.Println(a) // [Hello World]

    primes := [6]int{2, 3, 5, 7, 11, 13}
    fmt.Println(primes) // [2 3 5 7 11 13]
}
```

## slice

`slice` is a dynamically-sized. `[]T` is a slice of type `T`.

```golang
func main() {
    primes := [6]int{2, 3, 5, 7, 11, 13} // array
    var s []int = primes[1:4] // slice
    fmt.Println(s) // [3 5 7]
}
```

__Slices are references to arrays.__ A slice doesn't store any data.

```golang
func main() {
    names := [4]string{
        "John",
        "Paul",
        "George",
        "Ringo",
    }
    fmt.Println(names) // [John Paul George Ringo]

    a := names[0:2] // John Paul
    b := names[1:3] // Paul George
    fmt.Println(a, b)// [John Paul] [Paul George]

    b[0] = "XXX"
    fmt.Println(a, b) // [John XXX] [XXX George]
    fmt.Println(names) // [John XXX George Ringo]
}
```

```golang
// slice
q := []int{2, 3, 5, 7, 11, 13}
r := []bool{true, false, true, true, false, true}
// slices of structs
s := []struct {
    i int
    b bool
}{
    {2, true},
    {3, false},
    {5, true},
    {7, true},
    {11, false},
    {13, true},
}
```

When slicing, you may omit the high or low.

```golang
var a[10]int // array
// no omit ver
b := a[0:10]
// omit ver
b := a[:10]
b := a[0:]
b := a[:10]
```

The slice length is obtained using `len()`.The capacity is `cap()`.

The capacity is the number of elements in the underlying array, counting __from the first element in the slice.__

```golang
func main() {
    s := []int{2, 3, 5, 7, 11, 13}
    printSlice(s) // len=6 cap=6 [2 3 5 7 11 13]


    s = s[:0]
    printSlice(s) // len=0 cap=6 []

    s = s[:4]
    printSlice(s) // len=4 cap=6 [2 3 5 7]

    s = s[2:]
    printSlice(s) // len=2 cap=4 [5 7]
}

func printSlice(s []int) {
    fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}
```

`nil` slice has a length and capacity of 0. `nil` has no underlying array.

```golang
var s []int
fmt.Println(s, len(s), cap(s)) // [] 0 0
if s == nil {
    fmt.Println("nil!") // nil!
}
```

Slices can created with `make()`. The slices elements is zero values.

```golang
b := make([]int, 0, 5) // len(b)=0, cap(b)=5
b = b[:cap(b)] // len(b)=5, cap(b)=5
b = b[1:]      // len(b)=4, cap(b)=4
```

Slices can contain other slices.

```golang
board := [][]string{
    []string{"_", "_", "_"},
    []string{"_", "_", "_"},
    []string{"_", "_", "_"},
}
board[0][0] = "X"
fmt.Println(board[0]) // [X _ _]
```

`append()` is append new elements to a slice.

When expanding an underlying array with append(), Go always copy as __double length array of the current.__

```golang
func main() {
    var s []int // nil
    printSlice(s) // len=0 cap=0 []

    s = append(s, 0)
    printSlice(s) // len=1 cap=2 [0]

    s = append(s, 1)
    printSlice(s) // len=2 cap=2 [0 1]

    s = append(s, 2, 3, 4)
    printSlice(s) // len=5 cap=8 [0 1 2 3 4]
}
```