---
title: Thoughts on Pipe Operator
date: 2023-09-18T18:47:30+10:00
draft: false
---

Recently I've been playing with Elixir and found a interesting operator called Pipe, which is `|>`. Elixir makes use of it to pipe a function's output to another function. It helps to write clean code like this:

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
# either tmp variable
words = 'hello world'.upper().split(' ').reverse()
' '.join(words)
# or brackets hell
' '.join('hello world'.upper().split(' ').reverse())
```

I do feel that Python has a bad design here. Though it has the full power of OOP, it move a lot of method to global level like `len`, `enumerate`, `map`, `filter`. It's neither consistent nor elegant, making chaining methods, which are easy in other languages, somewhat hard in Python.

It also pollutes the global namespace. I think all Python developers have encountered the problem of naming a variable `max` and then find that the variable conflicts with `max` function, then rename the variable to `max1`, `num_max` or something else. It's really annoying.

A good language design that I love is Rust. Chaining methods is easy in Rust, and even `max` can be called in chaining style as well as function style. Due to its explicit `self` parameter, methods can be both instance methods and a normal function. So you can write:

```rust
let vec = vec![1, 2, 3];
// chaining enumerate()
vec.iter().enumerate();
// chaining map()
vec.iter().map();
// chaining len()
vec.len();

// even max() can be called in chaining style
let a = 1.max(2);
// and you can still call it in function style
let b = i32::max(1, 2);
```

Python and JavaScript can also achieve similar effects. Python has a explicit self parameter, and JavaScript has `call`, `apply` and `bind` to change the implicit `this`. But they are not widely used. e.g.

```python
lst = [1, 2, 3]
list.append(lst, 4)
```

```javascript
const arr = [1, 2, 3];
Array.prototype.push.call(arr, 4);
```
