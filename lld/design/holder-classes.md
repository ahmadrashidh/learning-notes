# Holder Classes

**Why**:
- Because of Java’s pass-by-value semantics, when the method attempts to modify its argument, it’s only modifying a copy, leaving the original value unaltered.

## Conceptualizing Holder class
- Holder<T> as a generic container or wrapper class capable of storing and managing an object of any type T.
- It primarily exists to overcome Java’s pass-by-value semantics, providing an indirect way to mimic pass-by-reference behavior.
- T here signifies a type parameter, meaning any valid Java reference type can replace it. This allows us to have one Holder class that can accommodate any data type. 
- However, it’s important to note that Holder<T> shouldn’t be used indiscriminately for every scenario.

```java
public class Holder<T> {
    public T value;

    public Holder(T value) {
        this.value = value;
    }
}
```

