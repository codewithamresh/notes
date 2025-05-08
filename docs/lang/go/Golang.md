# Go

### Build simple, secure, scalable systems with Go
- An open-source programming language supported by Google
- Easy to learn and great for teams
- Built-in concurrency and a robust standard library
- Large ecosystem of partners, communities, and tools


### Commands 
- `go.mod` - heart of go module. It tracks your go module name, go version and dependencies
- `go.sum` auto generated
- `go fmt` Formats code according to Go style
- `go mod init name` - initialize a new go module
- `go clean` - Removes object files and cached files
- `go install ` - Build and install the package
- `go list` - List modules or packages
- `go mod tidy` - Adds missing and removes unused dependencies.
- `go env` shows go env variable
- `go build` - compiles the code in the current directory.
- `go test` - runs the unit test


### Revise Go in One Shot

```go
package main
import "fmt"

func main(){
    fmt.Println("Hello World")
}
```

> - executable program - need to write main package
> - main() function tells from where program start execution
> - for lib/package we don't write main package

```go
var name string = "AMRESH" // creating global variable

func  test(){
    name2 := "Akash" // shorthand for creating variable (only work inside the function)
} 
```

### const
```go
const name string = "Amresh",
const PI = 3.14

```

### for

```go
for i:=1 ; i<=3 {
    fmt.Println(i)
    i = i + 1
}

for i:=0; i< 3; j++ {
    fmt.Println(i)
}

for i := range 3 {
    fmt.Println(i)
}

// infinite loop
for {
    fmt.Println("Loop")
    // break
}

```

 - Semicolon (;) are used by go but go compiler automatically insert semicolon where it required , we don't need to write explicitly

> {} curly braces are compulsory to write in go

```go
for i:=0; i < 5;i++ 
    fmt.Println("hello")
```
> Go don't have `while` loop


### if - else

```go 
if 7 % 2 == 0 {
    fmt.Println("7 is even")
} else{
    fmt.Println("7 is odd")
}
```

### switch
```go
i := 2
switch i {
    case 1:
        fmt.Println("One")
    case 2: 
        fmt.Println("Two")
    default:
        fmt.Println("greater than two")    
    }

```
> Go have a automatic break after each case so we don't need to write manually after every case like in C/Cpp.


### Array and Slices

#### Array
 - Fixed
 - `[5]int`
 - No resizable
 - fully memory reserved upfront
 - rarely used
 ```go
 var arr = [3]int{1,2,3}
```
  
#### Slice
 - Dynamic(can grow or shrink)
 - []int
 - Resizable
 - Uses only needed memory
 - Commonly used
```go
slice := []int{1,2,3}
len(slice)
cap(slice)
slice = append(slice,4,5) // [1,2,3,4,5]
```
> -  Slices are internally backed by an array, but more powerful.
> - `[...]` - comipler count the number of element in an array for you
```go
arr := [...]int{1, 2, 3}
[3]int{...} // array with fixed size
[...]int{...} // Array with fixed size infered
[]int{...} // slice(dynamic array)
```

> An uninitialized slice equals to nil and has length 0.
> To create an empty slice with non-zero length, use builtin `make`

`make` can only use with :
- slices
- maps
- channels
  
  #### Why we need `make` ?
- `var m map[string]int ` creates a map refrence, but it doesn't allocate memory for the actual map.
 
 ```go
 m["key"] = 42 // PANIC because map has not been setup.
 ```

 
 ```go
var m map[string]int
m["key"] = 10 // PANIC map is nil
 ```
 ```go
m := make(map[string]int)
m["key"] = 10 // Correct
m["k2"] = 34

delete(m,"k2")
clear(m)
 ```

 ### Functions

```go
func plus(a int,b int) int {
    return a+b
}

func plus(a, b, c int) int {
    return a + b + c
}

//func return multiple values
func values()(int,int,int){
    return 8,9,12
}

// variadic function (valargs)
func sum(nums... int) int{
    sum := 0
    for i := 0; i < len(nums) ; i++ {
        sum += nums[i];
    }
    return sum
}

```


```go
package main

import "fmt"

func main() {
	func suming(nums... int ) int {
		sum := 0
		for i := 0; i < len(nums); i++ {
			sum += nums[i]
		}
		return sum
	}

	fmt.Println(suming(1,2,3,4,5,6,7,8,9))
}
```

>> In Go, named functions cannot be defined inside other functions.

>> If you want to define a function inside main, it must be anonymous and assigned to a variable.

>> suming is used in fmt.Println(suming(...)), but it's not defined in scope.


```go

package main

import "fmt"

func suming(nums ...int) int {
	sum := 0
	for i := 0; i < len(nums); i++ {
		sum += nums[i]
	}
	return sum
}

func main() {
	fmt.Println(suming(1, 2, 3, 4, 5, 6, 7, 8, 9))
}

```

### Closure

- A closure is a function value that references variables from outside its body . It remembers the environment in which it was created.

```go
func createCounter() func() int {
    count := 0
    return func() int {
        count++
        return count
    }
}

counter := createCounter()
counter() // 1
counter() // 2
counter() // 3
```

### Pointers
 > - *int is a pointer to int
 > -  &x gets the address of x

```go
var x int 10
var p *int = &x
*p  = 20 // change x to 20

type Person struct{
    name string
}
func updateName(p *Person){
    p.name = "Amresh"
}

func main(){
    p := Person{name:"Akash"}
    updateName(&p)
    fmt.Println(p.name); // Amresh
}

```

### Strings

- read only slices of bytes ([] bytes)
-  hold UTF-8 encoded characters
-  `s := "Amresh"`
  
`rune` is an alias for int32 and represent a Unicode code point
- Go user rune when dealing with characters beyond ASCII
  
```go
var r rune = 'अ' // 2309 (unicode code point)
fmt.Println("%c \n",r) // अ
```
### Why do we need rune?
- Because not all characters are 1 byte


>> Go is garbage collected language.
>> structs are mutable

### Methods

```go
func (r *rect) area() int {
    return r.width * r.height
}

// (r *rect) is a receiver
```


### Interface

- OOPS like `class` not present in go
- we achieve polymorphism by using interface
- >> `interface {} // accept ant type`
- Go don't have `implement` keyword
  

  ### init() Function builtin magic
  - auto run when package loads
  - no need to call it manually
  - can't take argument or return anything - constructor type feature
  - automatically runs before `main()` 

 Use of init()
 - load env 
 - validate config
 - setup global vars
 - register plugins
 - run package - level startup checks