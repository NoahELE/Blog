---
title: @Bean in @Configuration or @Component
date: 2025-01-28T22:47:53+08:00
draft: true
---

Difference between declaring beans with @Bean in @Configuration class and @Component class.

```java
// @Configuration
// @Component
public class Foo {
  @Bean
  public Bar bar() {
    return new Bar();
  }

  @Bean
  public Baz baz() {
    Bar bar1 = bar();
    Bar bar2 = bar();
    return new Baz();
  }
}
```

For the above class, if the class is annotated with @Component, bar1 and bar2 will be 2 different instances. However, if the class is annotated with @Configuration, bar1 and bar2 will be the same instance. This is because spring creates proxy for @Configuration class which makes sure that the same instance is returned when the bean method is called.
