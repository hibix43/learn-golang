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