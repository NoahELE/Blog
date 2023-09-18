---
title: Java Related
date: 2023-07-23T21:21:15+10:00
draft: false
---

## Java

- The reason of `record` class has accessors instead of public final attributes:
  - make it possible to override accessor methods
  - allow the `record` class to implement interfaces

## Lombok

- `@Data` generates constructor only if there is no explicitly written constructor
- `@Data` is not recommended for Hibernate entities, as the generated `equals` and `hashCode` methods are not suitable for entities managed by Hibernate

## Spring

- Circular references is discouraged and they are prohibited by default. Possible Solutions:
  - Modify the code base to remove circular references
  - Add `@Lazy` annotation to constructor
