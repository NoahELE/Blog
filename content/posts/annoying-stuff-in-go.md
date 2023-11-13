---
title: "Annoying Stuff in Go"
date: 2023-11-03T15:30:12+11:00
draft: false
---

In this blog I want to complain about some annoying stuff in Go. I'm not saying that Go is bad, in fact I love Go for its simplicity and ease of use. It's just that there are some designs in Go that ruin the experience for me.

### Ugly Error Handling

I'll put a disclaimer here that I'm not a fan of exceptions either. I think exceptions are a bad idea in general. But I think Go's error handling is even worse. Go's error handling actually encourage those who are lazy and punish those who want to write good code.

Compare this

```go
func doSomething() (any, error) {
  res1, err := do1()
  if (err != nil) {
    return nil, err
  }
  res2, err := do2()
  if (err != nil) {
    return nil, err
  }
  res3, err := do3()
  if (err != nil) {
    return nil, err
  }
  return res1 + res2 + res3, nil
}
```

to

```go
func doSomething() (any, error) {
  res1, _ := do1()
  res2, _ := do2()
  res3, _ := do3()
  return res1 + res2 + res3, nil
}
```

If you want to write safe code you'll have to write the boilerplate once and once again. And if you just write unsafe code, it's way cleaner and more elegant, and there is nothing in the language that stops you from doing that.

A good language design should make writing safe code easier and unsafe code harder. At least there should be a syntax sugar to simplify this, since 90% of the time you just want to return the error.

### `defer` is not Block Scoped

Instead of

```go
func doSomething() {
  {
    conn1 := connect1()
    defer close1(conn1)
  }
  {
    conn2 := connect1()
    defer close2(conn2)
  }
  {
    conn3 := connect3()
    defer close3(conn3)
  }
}
```

you have to write

```go
func doSomething() {
  func () {
    conn1 := connect1()
    defer close1(conn1)
  }()
  func () {
    conn2 := connect1()
    defer close2(conn2)
  }()
  func () {
    conn3 := connect3()
    defer close3(conn3)
  }()
}
```

I don't know why Go doesn't make `defer` block scoped. It's just so much more convenient and intuitive.

Go has block scoped variables, why not `defer`? It's really silly to have to wrap everything in a lambda function just to use `defer`.

### No Tuple Type

Go doesn't have tuple type. It make multiple return a feature but leaves tuple out of the language. I have no ideas why. The multiple return actually just returns a tuple, but you can't receive the tuple as a whole or pass it around.

```go
func foo() (int, string) {
  return 1, "hello"
}

func bar(i int, s string) {
  fmt.Println(i, s)
}

func main() {
  bar(foo()) // valid!?
}
```

Why would this work? It's just so inconsistent. If you can't receive a tuple as a whole, why can you pass it as a whole? It's just so weird.

### No Runtime Const

Go has no way to ensure immutability. If you declare a global map or slice, you have no guarantee that it won't be modified.

### Too Strict Compiler

I think it is common for programmers to comment out some code for debugging purpose. But if you comment out all the lines that use an import, Go will complain that the import is unused. You have to delete the import line to make it work. And when you uncomment the code, you have to add the import line back. It's just so annoying. It is also the same case for unused variables.

Shouldn't this be linter's job? Why would the compiler care about this?

### Including `map` as Built-in Data Type

Golang did a terrible choice by making `map` a built-in data type. This causes all map related operations are done on the syntax level, one example is checking existence

```go
if _, ok := m[k]; ok {
  // ...
}
```

Since `map` is a built-in data type, the language designers decide not to define methods on it. Instead golang has to introduce this weird syntax to check existence. It also makes it impossible to map, filter or fold on a map. You have to write a for loop to do that.

To use a `set`, one has to define something like `map[int]struct{}`, which is just ugly.

`map` as a built-in data type also create additional difficulty when adding generics to the language.
