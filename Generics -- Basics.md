### Generics -- Basics
Note: Generics will be covered more thoroughly in a later lecture

Example: ArrayList is a **generic** class in Java:

```java
public class ArrayList<E> ...
```

- `<E>` is specifying that ArrayList will have some sort of Type provided when initialized, and can be used in the internals of ArrayList

*Trick Question*: Make sure to review the different ways of initializing an ArrayList.

Example implementation:
```java
// ArrayList will contain objects of type String
// IMPORTANT NOTE: Type can be assumed from the left, it does NOT have to be in the brackets on the right
ArrayList<String> list = new ArrayList<>();
```

**Comparable** is an example of a generic interface:
```java
// T is the generic type, allowing us to avoid the repetitive type safety checks (like you see in equals)
public interface Comparable<T> ...
```

