---
layout: post
title: Golang fundamentals
date: 2023-07-16 14:00 +0100
categories: [Coding, Languages]
tags: [coding, programming, golang, go]
---

# Main characteristics of Go

+ Compiled language: the source code is compiled into machine code.
+ Statically typed: variables are bound to a type at compile time.
+ Garbage collected: memory is managed automatically.
+ Concurrency support: goroutines and channels.
+ Simplicity: Go is a simple language.
+ Open source: Go is open source.
+ Cross-platform: Go is cross-platform.

# Main advantage of Go over Python

Go is a compiled language and statically typed, this makes Go faster than Python at runtime, also more secure than Python at and easier to deploy than Python.

# Main advantage of Python over Go

Python is dynamically typed, which makes Python easier to use than Go. Python is interpreted, also makes Python easier to use than Go. 
Python is more mature than Go, and there is a larger community around Python with more libraries available.

# Go installation

+ Download the latest version of Go from the official website and extract the tarball into `/usr/local`:

```bash
wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz
```

+ Add the Go binary directory to the PATH environment variable:

```bash
echo "export PATH=\$PATH:/usr/local/go/bin" >> ~/.bashrc
```

+ Reload the shell:

```bash
source ~/.bashrc
```

+ Check the installation:

```bash
go version
```

# Go workspace

+ A Go workspace is a directory tree with three directories at its root:
    + `src`: Contains the source code of the Go packages.
    + `pkg`: Contains the compiled packages.
    + `bin`: Contains the compiled binaries.

+ The `GOPATH` environment variable is used to indicate the location of the workspace.

+ The `go` command is used to manage the workspace, for example:

```bash
go get github.com/username/repo
go install github
```

# Packages import

A program start with package `main`. Other packages can be imported with the `import` keyword, which can be used in two ways:

+ Recommended way (multiple packages in a single import statement):
```go
package main

import (
    "fmt"
    "math"
)
```

+ Alternative way (multiple import statements):
```go
package main

import "fmt"
import "math"
```

# Function declaration

Use the ```func`` keyword, followed by the function name, the parameters and the return type.
```go
func myFunc(x int, y int) int {
	return x + y
}
```

If the parameters are of the same type, the type can be omitted:
```go
func myFunc(x, y int) int {
    return x + y
}
```

A function can return any number of values:
```go
func myFunc(x, y int) (int, int) {
    return x + y, x - y
}
```

The return values can be named. And if they are named, they can be omitted from the return statement, this is known as a naked return, and it should be used only in short functions.
```go
func myFunc(x, y int) (sum, diff int) {
    sum = x + y
    diff = x - y
    return
}
```

# Variables

Variables are declared with the ```var``` keyword, followed by the variable name and the type.
```go
var x int
```

Variables can be initialized with a value:
```go
var x int = 10
```

If the variable is initialized, the type can be omitted, because the compiler can infer the type from the value:
```go
var x = 10
```

If the variable is initialized, the type can be omitted, and the ```var``` keyword can be omitted too, because the compiler can infer the type from the value:
```go
x := 10
```

Multiple variables can be declared in a single statement:
```go
var x, y int
```

Multiple variables can be declared in a single statement, and initialized with values:
```go
var x, y int = 10, 20
```

Multiple variables can be declared in a single statement, and initialized with values, and the type can be omitted:
```go 
var x, y = 10, 20
```

Multiple variables can be declared in a single statement, and initialized with values, and the type and the ```var``` keyword can be omitted:
```go
x, y := 10, 20
```

Variables declared without an initial value are initialized with the zero value of the type. Zero values are:
+ ```0``` for numeric types.
+ ```false``` for the boolean type.
+ ```""``` for the string type.

# Pointers

Pointers are declared with the ```*``` operator, followed by the type of the value the pointer points to:
```go
var x *int
```

Pointers are initialized with the ```&``` operator, followed by the variable name:
```go
var x int = 10
var y *int = &x
```


# Type conversion

Type conversion is done with the ```T()``` function, where ```T``` is the type to convert to. Different type assignments require explicit type conversion:
```go
var x int = 10
var y float64 = float64(x)
```


# Constants

Constants are declared with the ```const``` keyword, followed by the constant name and the value:
```go
const x = 10
```

Untyped constants take the type needed by its context:
```go
const x = 10
var y float64 = x
var z uint8 = x
```

# Data types

+ Boolean: ```bool```
+ Numeric:
    + Integer: ```int```, ```int8```, ```int16```, ```int32```, ```int64```
    + Unsigned integer: ```uint```, ```uint8```, ```uint16```, ```uint32```, ```uint64```
    + Floating point: ```float32```, ```float64```
    + Complex: ```complex64```, ```complex128```

# For loop

The ```for``` loop is the only loop statement in Go. It can be used in three ways:

+ With a single condition:
```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

+ With a single condition, and the initialization and the post statements omitted:
```go
i := 0
for i < 10 {
    fmt.Println(i)
    i++
}
```

+ With no condition, and the initialization, the condition and the post statements omitted:
```go
i := 0
for {
    fmt.Println(i)
    i++
    if i == 10 {
        break
    }
}
```

The init and post statements can be omitted, but the semicolons must be present:
```go
i := 0
for i < 10 {
    fmt.Println(i)
    i++
}
```

If the condition is omitted, it is equivalent to ```for true```, in this way an infinite loop is compactly expressed:
```go
for {
    fmt.Println(i)
    i++
    if i == 10 {
        break
    }
}
```

# If statement

The ```if``` statement is used to execute a block of code if a condition is true:
```go
if x > 10 {
    fmt.Println("x is greater than 10")
}
```

The ```if``` statement can have an initialization statement, which is executed before the condition:
```go
if y := math.Pow(x, 2); y > 10 {
    fmt.Println("x^2 is greater than 10 and is equal to", y)
} else {
    fmt.Println("x^2 is less than or equal to 10 and is equal to", y)
}
```

# Switch statement

The ```switch``` statement is used to execute a block of code depending on the value of a variable:
```go
switch x {
case 1:
    fmt.Println("x is equal to 1")
case 2:
    fmt.Println("x is equal to 2")
default:
    fmt.Println("x is not equal to 1 or 2")
}
```

Unlike other languages, the ```switch``` statement in Go does not fall through the next case, so there is no need to use the ```break``` statement. Effectively the ```break``` statement is implicit.

Switch without a condition is the same as ```switch true```, this is a way to express a compact if-else chain:
```go
switch {
case x > 10:
    fmt.Println("x is greater than 10")
case x < 10:
    fmt.Println("x is less than 10")
default:
    fmt.Println("x is equal to 10")
}
```

# Defer statement

The ```defer``` statement is used to execute a function call after the surrounding function returns:
```go
func myFunc() {
    defer fmt.Println("myFunc finished")
    fmt.Println("myFunc started")

    //Outputs is:
    //myFunc started
    //myFunc finished
}
```

The ```defer``` statement is used to execute a function call after the surrounding function returns, even if the surrounding function panics:
```go
func myFunc() {
    defer fmt.Println("myFunc finished")
    fmt.Println("myFunc started")
    panic("myFunc panicked")

    //Outputs is:
    //myFunc started
    //myFunc finished
    //panic: myFunc panicked
}
```


