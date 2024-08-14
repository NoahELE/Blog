---
title: Java Lambda
date: 2024-08-14T21:21:33+10:00
draft: false
---

## Java's Lambda

Java's Lambda is actually a syntax sugar for anonymous implementation for functional interfaces. For example, the 2 are equivalent:

```Java
public class Main {
    public static void main(String[] args) {
        Runnable f1 = () -> System.out.println("lambda");
        Runnable f2 = new Runnable() {
            public void run() {
                System.out.println("lambda");
            }
        }
    }
}
```

> Note: the variables captured by the lambda must be final or effectively final.
