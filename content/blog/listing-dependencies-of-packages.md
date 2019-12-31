---
title: "Listing Dependencies of Packages"
date: 2019-06-10T12:42:05+03:00
draft: false
tags: ["Golang", "Software development"]
---

There is a fantastic tool in the Go eco system called go list. This tool uses Go template package and comes with comes a set of predefined template variables we can use to format its output.

Here we will use it to list the dependencies of our local package.

Lets assume we are working on html scrapping package called `scrappy`

### Listing all packages

```Go
 $ go list -f '{{ .Imports }}' github.com/cholthi/scrappy
[encoding/json flag fmt github.com/gocolly/colly os os/signal strings syscall]
```

Those are the packages my scrappy package depend. Some people would like each dependency to appear on its own line. To do that,`go list` has a template function called `join` which is just an alias for builtin `String.Join`

```Go
$ go list -f '{{ join .Imports "\n" }}' github.com/cholthi/scrappy
encoding/json
flag
fmt
github.com/gocolly/colly
os
os/signal
strings
syscall
```

For this and more on `go list`, check out this good blog [post](https://dave.cheney.net/2014/09/14/go-list-your-swiss-army-knife)

