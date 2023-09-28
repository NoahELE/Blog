---
title: Java Related
date: 2023-07-23T21:21:15+10:00
draft: false
---

## Java

- The reason why `record` classes have accessor methods instead of public final attributes:
  - make it possible to override accessor methods
  - allow the `record` class to implement interfaces

## Lombok

- `@Data` generates constructor only if there is no explicitly written constructor
- `@Data` should not be used on Hibernate entities, as the generated `equals` and `hashCode` methods will cause problems when the entity is detached from the session.

## Spring

- `@Autowired` can be used on constructor, setter and field. Constructor injection is recommended.
  - My preference is constructor injection > setter injection > field injection. And then utilize `@RequiredArgsConstructor` lombok annotation to generate constructor with required fields. By marking all required beans `private final`, it is automatically present in the constructor generated and thus injected. I think this is a more elegant way of injecting dependencies.
- Circular references is discouraged and they are prohibited by default. Possible Solutions:
  - Modify the code base to remove circular references
  - Add `@Lazy` annotation to constructor, so that the bean is not created until it is needed
  - Use setter injection instead of constructor injection
