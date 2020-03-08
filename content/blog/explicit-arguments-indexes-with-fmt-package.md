---
title: "Explicit Arguments Indexes With Fmt Package"
date: 2020-01-08T21:50:06+03:00
draft: false
---

Golang has a very handy package called `fmt` for formating data values.

```Go
fmt.Printf("Hello %s", "world") // Hello World
```
But by default, the `fmt` family of functions work by successively applying args passed after the format string to matching format verbs by argument order.

```Go
tablePrefix := "mydb"

query := fmt.Sprintf("SELECT %s_table1.*, %s_table2.id from %s_table1 left join %s_table2 on %s_table2.id = %s_table1.id;",tablePrefix, tablePrefix, tablePrefix, tablePrefix, tablePrefix)

fmt.Print(query)

// SELECT mydb_table1.*, mydb_table2.id from mydb_table1 left join mydb_table2 on mydb_table2.id = mydb_table1.id;
```
while the above does achieves our desired outcome, it does so by duplicating code heavily. it would be better if `tablePrefix` didn't have to be passed several times to `fmt` function if the same data value is used by many format specifiers.

Thankfully, `fmt` package designers saw a need for that and provided a way to avoid such a duplication of code. 

from the [fmt documentation](https://golang.org/pkg/fmt/).

> `import "fmt"`       
>
>Explicit argument indexes:
>
>In Printf, Sprintf, and Fprintf, the default behavior is for each formatting verb to format successive arguments passed in the call. However, 
>the notation `[n]` immediately before the verb indicates that the nth one-indexed argument is to be formatted instead.


This means we can simplify the function call to look like below.

```Go
tablePrefix := "mydb"

query := fmt.Sprintf("SELECT %[1]s_table1.*, %[1]s_table2.id from %[1]s_table1 left join %[1]s_table2 on %[1]s_table2.id = %[1]s_table1.id;",tablePrefix) // notice only one data argument is needed if you use a position based trick

fmt.Print(query)

// SELECT mydb_table1.*, mydb_table2.id from mydb_table1 left join mydb_table2 on mydb_table2.id = mydb_table1.id;
```

> The position starts from index `1` instead of `0` probably because the format string is the zeroth argument to fmt functions.

Such a simple tricks is easy to forget and I am puting it here as a reminder to my self when I need it and I also hope someone in future may find it helpful too.

Happy coding!
