---
title: 'Functional Programming'
date: 2023-09-18T18:47:30+10:00
draft: true
---

## Pipe Operator

Recently I've been attracted by the pipe operator in Elixir, which is `|>`. It's a very simple operator, but it can make the code more readable and easier to understand. It helps write clean code like this:

```elixir
"hello world" |> String.upcase() |> String.split(" ") |> Enum.reverse() |> Enum.join(" ")
# instead of
Enum.join(Enum.reverse(String.split(String.upcase("hello world"), " ")), " ")
```

But then I found that pipeline operator is not so common in other languages I know like Java, JavaScript and Python. It took me some time to realize that its equivalent in OOP world is just chaining methods due to the implicit `this` parameter in object methods. For example, in JavaScript, we can write:

```javascript
'hello world'.toUpperCase().split(' ').reverse().join(' ');
```

But in Python, the `join` method is on `string` instead of `list` type, so we have to write:

```python
words = 'hello world'.upper().split(' ').reverse()
' '.join(words)
```

I do feel that Python has a bad design here. Though it has the full power of OOP, it move a lot of method to global level like `len`, `enumerate`, `map`, `filter`. It's neither consistent nor elegant, making chaining methods, which are easy in other languages, somewhat hard in Python.
