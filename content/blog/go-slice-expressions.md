---
title: "Go Slice Expressions"
date: 2019-08-09T12:57:11+03:00
draft: false
author: Chol Paul
---

Go allows operation on slices to extract part of its elements using a beautiful syntax. Go calls it __Slice Expressions__.

```Go
var s []Type
s[low:high]
```

Here is how the official Go langange specs define [Slice Expressions](https://golang.org/ref/spec#Slice_expressions).

> For a string, array, pointer to array, or slice a, the primary expression `a[low : high]` constructs a substring or slice. The indices low and high select which elements of operand a appear in the result. The result has indices starting at `0` and length equal to `high - low`.

The way I like to think of it is as an exclusive range represented by this formula

```Go
a[low, high-1]
```
Lets see some examples.

### Examples

```Go
func main() {
  s := []int{0,1,2,3,4,5,6,7,8,9}
  
fmt.Println("slice s =", s)
fmt.Println("s[2:6] ",s[2:6])
fmt.Println("s[2:] ", s[2:])
fmt.Println("s[:4] ", s[:4])
fmt.Println("s[:] ", s[:])
```
Outputs

```Go
slice s =[0 1 2 3 4 5 6 7 8 9]
s[2:6] [2,3,4,5]
s[2:] [2,3,4,5,6,7,8,9]
s[:4] [0,1,2,3]
s[:] [0,1,2,3,4,5,6,7,8,9]
```

`s[2:6]` means, extract elements of s starting from index `2` upto index `6` exclusive. `s[2:]` means , extract elements of `s` starting from index `2` till the end. `s[:4]` means, extract elements of `s` starting from index `0` (because no low index is given) upto index `4` exclusive. `s[:]` means, extract all elements `s` starting from index `0` till the end.

### Important Notes

The slices created by this operation are only a view over original slice. This little detail got me in the past, where changes from the extracted slice reflect in the original slice.To avoid this, you can make use of `copy` function to reset internal array pointer. Remember slices are just a reference to an array object underneath.

```Go

copy(extract,s[2:]) // now `extract` is a different slice
fmt.Println(&s[2] == &extract[0] // false
```
Thinking of these slice expressions as an exclusive range can be confusing sometimes. Another way is to remember the following formula

For example, `s2 := s[1:3]` creates a new slice with length `3 - 1 = 2`, so it will contain 2 elements: `s[1]` and `s[2]`

I got that trick from this SO [answer](https://stackoverflow.com/questions/40318987/what-is-the-idea-behind-the-notation-of-indices-of-go-slices).

While other langanges use functions to realize the same functionality on collections, Go makes it easy and fun by providing a builtin langange construct to accomplish these things.

