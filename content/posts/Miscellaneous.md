---
title: 'Miscellaneous'
date: 2022-12-16T18:18:19+08:00
draft: false
---

## Java

- The reason of `record` class has accessors instead of public final attributes:
  - make it possible to override accessor methods
  - allow the `record` class to implement interfaces

## Lombok

- `@Data` generates constructor only if there is no explicitly written constructor

## Spring

- Relying upon circular references is discouraged and they are prohibited by default. Possible Solutions:
  - Modify the code base to remove circular references
  - Add `@Lazy` annotation to constructor
