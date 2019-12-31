---
title: "Deleting Slice Item"
date: 2019-10-24T13:08:45+03:00
draft: false
---

n Go, a slice is a fundamental data structure, it is a mutable Homogeneous array. It can grow and shrink at run time according to the needs of application.You can think of as it as Vector class if you’re coming from a `Java` background.

Often time while working with slices, you would like to add elements to a slice.

```Go
 var s []string = make([]string, 0)
    s = append(s,'cairo') // adds to the end
```
Today, I want to share a common idiom in Go on how to remove an element by its index.

```Go
banku := 1 //index to delete
   var s []string = make([]string, 0)
     cities := strings.Split("Nairobi,Banku,Cairo,Lagos",",")
   s = append(s, cities...) // appending a slice to another slice

 for index,_ = range s {
   if index == banku {
     s = append(s[:index], s[index+1:]) // delete element matching `index`
   }
}
```
There are many ways to go about deleting a slice element, but i find this to be easy and is the one I like to use.

Happy coding!

