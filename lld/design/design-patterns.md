# Design Patterns

Designing code as solution for common problems encountered when building big codes

## Gang Of Four
> One of the popular design pattern

1. Creational - creating objects
2. Structural - structure of classes
3. Behavioural - interactions between objects
4. Singleton - single instance of object

## Singleton Patterns
> Using single instance of an object across the program

**When**:
- Memory overhead
- CPU overhead
- Single source of truth

**Sample**:
- Connection pool
- Logging

### Lazy Initializer Singleton Pattern:
Step 1. Constructor Hiding - create `private` access constructor
Step 2. Static Initialiser - create static `getInstance` method
Step 3. Static attribute & implementation


## Creational Patterns
> creating objects

### Builder Pattern

**When**:
- Classes with fat constructor (with too many fields) aka `overloaded constructor`, passing many fields is 

  - Prone to bugs
  - Bad Dev style
  - Not readable

- Class is used for multiple purposes, ie when some of the fields to be initialised in one case and different in other case. 
- `telescopic constructor` is used but it is anti-pattern.

**Solution**
- initialise only values that is required aka *on-demand initialisation*

- No-args constructor with setter can be used for on-demand initialisation. But it
  - Makes objects mutable causing side effects eg. defenses programming (where somewhere in the code, fields is set to null, so lot of null check is checked elsewhere before accessing any field)
  - need complex validations as setter cannot throw exceptions


Wonder an approach that achieves all of the below:
- On-demand initialisation
- Global validation
- Immutability

**Approach**:
- Use a static inner friend class aka *builder class* for original class which builds the class and create instance only on demand or at the end

**How**:
Step 1. Create static inner class, call it **Builder**
Step 2. Copy all of the fields of the outer class to `Builder`
Step 3. Expose setters on the `Builder`
Step 4. Call the lifecycle method `build` to get the instance of the built object.
Step 5. Call the `validate` method before building to validate input

```java
class Student {
    String name;
    String email;
    static class Builder{

    }
}
```

### Prototype pattern

**Motivation**:
- When you need multiple objects of a class when creating a single object is expensive

**Usecase** - painting objects in games

**Specification**:
- Instead of creating objects, copy the object and modify the values.
- Shallow copy - doesn't copy nested user-defined objects
  - Advantages: Fast, Memory efficient
  - Disadvantages: Inconsistent
- Deep Copy - Copy all nested user-defined objects
  - Advantages: Consistent
  - Disadvantages: Slow, Occupies memory

**Implementation**
Step 1: Create a `Clonable` interface

```java
interface Clonable {
    BackgroundObject clone();
}
```

Step 2: Create class (that you want to prototype) and implement `Clonable` interface
Step 3: Create a prototype with clone method and then modify values

### Registry Pattern

**Motivation**:
- To store object and retrieve later whenever needed

**Specification**:
- Use HashMap to store objects based on certain key.
- Add or remove it by the key. Just wrapper using Map.

### Factory Pattern
> one of the most used design pattern

**Motivation**
> When to initiate different user-defined/library class for differnt cases

- Constructing using the if-else is non-renewable complex construction that violates SRP and OCP principle
- When using external library, direct use of implementation classes cause backward compatibility

**Specification**
- Shouldn't depend on implementation classes
- Reduced usage of subclasses

**Implementation**

**Simple Factory**

Step 1: Create common interface for all your products
```java
interface Button{}

class RoundButton implements Button {}

class RectangleButton implements Button {}

class SquareButton implements Button {}
```
Step 2: Create a factory method in  a factory class for construction logic

Step 3: Implement Construction Logic

```java
class ButtonFactory {
    Button static createButton(Type type){
        switch (screenSize) {
            case PHONE:
            case TABLET: return new RoundButton(border, radius);
            case DESKTOP: return new SquareButton(border, length);
        }
    }
}
```

**Downsides**
1. Parameter explosion(different parameters required by different products are all added as argument) in factory method. *Solution* - return Builder instead of instance of the object
2. OCP Violation - that adding another button requires modifying createButton method

**Solution**
1. Create Product heirarchy
2. Create Factory interface
3. Create concrete factories

## Structural Pattern

### Adapter Pattern
> adapts two incompatible interface (i.e. services/library classes)


**Motivation**
- Different interface i.e. services/library classes may have different method or classes which we need to adapt to common interface
- Example: Adapting RazorPay and PayU interface

**Implementation**
Step 1: Create adapter interface
Step 2: Create concrete adapters



