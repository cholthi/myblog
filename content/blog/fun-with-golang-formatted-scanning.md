---
title: "Fun With Golang Formatted Scanning"
date: 2020-03-07T22:16:01+03:00
draft: false
---


Go's `fmt` package is the power house of formatted IO. It centralizes string formating routines for simple tasks as echoing to standard output to more complex such as sending formatted data to network IO.
In fact, your first encounter with Go langange may involve use of `fmt` package.

```Go
import "fmt"

greeting := "Hello World"
fmt.Println(greeting) // prints "Hello World" to stdout
```
Receving user input is daunting and an area full of security holes. Even harder is receiving formatted data.

Today I want to talk about Go approach to scanning formatted data. which comes easy because of Go's static type system unlike dynamic langanges I have worked with previously, where a task would take few function calls and still look verbose.

#### Scanning data from StdOut

```Go
var planet string

fmt.Scanf("%s", &planet)
fmt.Print(planet)
```

#### Scanning formatted user input from string

Let say, you asked the users to provide their name and age in a certain string format, may be user configuration you read in a file.

```Go
// format: "name=yourname,age=yourage"
var (
     name string
     age int
)
 userInput := "name=Philip,age=35"
fmt.Sscanf(userInput, "name=%s,age=%d",&name,&age) //Note Scanning from string instead of a io.Reader
fmr.Println(name, age)
```
To learn more about various formats you can read data, check [fmt](https://golang.org/pkg/fmt/) documentation.

Go has formats for any data type ranging from simple strings, integers, floats, slices, pointers etc.


