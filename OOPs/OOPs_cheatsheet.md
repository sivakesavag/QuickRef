# OOP Concepts Cheatsheet
> Quick revision guide for beginner-to-intermediate programmers

---

## 1. Classes & Objects

**Definition:** A *class* is a blueprint; an *object* is an instance of that blueprint.

**Key Rules:**
- Class defines attributes (data) and methods (behavior)
- Objects hold actual values and can invoke methods
- One class → many objects

```python
class Car:
    def __init__(self, brand):
        self.brand = brand  # attribute
    
    def drive(self):        # method
        return f"{self.brand} is driving"

my_car = Car("Toyota")      # object instantiation
```

---

## 2. The Four Pillars of OOP

### 2.1 Encapsulation

**Definition:** Bundling data + methods together, restricting direct access to internal state.

**Key Rules:**
- Use private/protected access modifiers
- Expose controlled access via getters/setters
- Prevents accidental corruption of data

```java
public class Account {
    private double balance;  // hidden
    
    public double getBalance() { return balance; }
    public void deposit(double amt) {
        if (amt > 0) balance += amt;  // validation
    }
}
```

---

### 2.2 Abstraction

**Definition:** Hiding complex implementation, exposing only essential features.

**Key Rules:**
- Focus on *what* an object does, not *how*
- Achieved via abstract classes/interfaces
- Reduces complexity for the user

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, amount): pass  # what, not how

class CreditCard(PaymentProcessor):
    def pay(self, amount):
        # complex implementation hidden
        return f"Paid ${amount} via credit card"
```

---

### 2.3 Inheritance

**Definition:** A class (child) acquires properties and behaviors of another class (parent).

**Key Rules:**
- Promotes code reuse
- Child can override parent methods
- Types: single, multilevel, hierarchical, multiple (language-dependent)
- Use `super()` to call parent methods

```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}
// Dog inherits eat() + has its own bark()
```

---

### 2.4 Polymorphism

**Definition:** Same interface, different implementations — objects respond differently to the same message.

#### Compile-Time (Static) Polymorphism
- Resolved at compile time
- Achieved via **method overloading**

```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }  // overloaded
}
```

#### Runtime (Dynamic) Polymorphism
- Resolved at runtime
- Achieved via **method overriding** + inheritance

```java
class Shape {
    void draw() { System.out.println("Drawing shape"); }
}
class Circle extends Shape {
    @Override
    void draw() { System.out.println("Drawing circle"); }  // overridden
}

Shape s = new Circle();
s.draw();  // Output: "Drawing circle" (runtime decision)
```

---

## 3. Interface vs Abstract Class

| Feature | Interface | Abstract Class |
|---------|-----------|----------------|
| **Methods** | All abstract (Java 8+: default/static allowed) | Abstract + concrete methods |
| **Variables** | `public static final` only | Any access modifier |
| **Inheritance** | Multiple interfaces allowed | Single abstract class only |
| **Constructor** | ❌ No | ✅ Yes |
| **Use Case** | Define a contract/capability | Provide base implementation |

```java
// Interface: "can do" capability
interface Flyable {
    void fly();
}

// Abstract class: "is-a" with shared logic
abstract class Bird {
    abstract void chirp();
    void breathe() { /* shared implementation */ }
}
```

**Rule of Thumb:** Use interface for capabilities, abstract class for common base behavior.

---

## 4. Composition vs Inheritance

| Aspect | Inheritance | Composition |
|--------|-------------|-------------|
| **Relationship** | IS-A | HAS-A |
| **Coupling** | Tight | Loose |
| **Flexibility** | Low (fixed at compile-time) | High (can change at runtime) |
| **Reusability** | Via subclassing | Via delegation |

```python
# Inheritance (IS-A): Dog IS-A Animal
class Dog(Animal): pass

# Composition (HAS-A): Car HAS-A Engine
class Engine:
    def start(self): return "Engine started"

class Car:
    def __init__(self):
        self.engine = Engine()  # composed
    
    def start(self):
        return self.engine.start()  # delegation
```

**Favor composition over inheritance** — more flexible, avoids fragile base class problem.

---

## 5. Association / Aggregation / Composition

| Type | Relationship | Lifetime Dependency | Example |
|------|--------------|---------------------|---------|
| **Association** | Uses-A | Independent | Teacher ↔ Student |
| **Aggregation** | Has-A (weak) | Child can exist independently | Department → Professor |
| **Composition** | Has-A (strong) | Child cannot exist without parent | House → Room |

```java
// Aggregation: Professor exists without Department
class Department {
    private List<Professor> professors;  // aggregated
}

// Composition: Room dies with House
class House {
    private final List<Room> rooms = new ArrayList<>();
    House() { rooms.add(new Room()); }  // created internally
}
```

---

## 6. Access Modifiers

| Modifier | Class | Package | Subclass | World |
|----------|:-----:|:-------:|:--------:|:-----:|
| `public` | ✅ | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `default` (package-private) | ✅ | ✅ | ❌ | ❌ |
| `private` | ✅ | ❌ | ❌ | ❌ |

**Python Convention:** `_protected`, `__private` (name mangling)

---

## 7. Constructors

**Definition:** Special method called during object creation for initialization.

**Key Rules:**
- Same name as class (Java/C++) or `__init__` (Python)
- No return type
- Can be overloaded (multiple constructors)
- Use constructor chaining to avoid duplication

```java
class Person {
    String name;
    int age;
    
    Person() { this("Unknown", 0); }           // default
    Person(String name) { this(name, 0); }     // chained
    Person(String name, int age) {             // primary
        this.name = name;
        this.age = age;
    }
}
```

---

## 8. Method Overloading vs Overriding

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| **Location** | Same class | Parent-child classes |
| **Signature** | Different parameters | Same signature |
| **Return Type** | Can differ | Same or covariant |
| **Binding** | Compile-time | Runtime |
| **Access** | Any | Same or broader |

```java
// Overloading (same class, different params)
void print(int x) { }
void print(String s) { }

// Overriding (child redefines parent method)
class Parent { void show() { } }
class Child extends Parent {
    @Override void show() { }  // same signature
}
```

---

## 9. Static vs Instance Members

| Aspect | Static | Instance |
|--------|--------|----------|
| **Belongs to** | Class | Object |
| **Memory** | Single copy | Per object |
| **Access** | `ClassName.member` | `object.member` |
| **Use Case** | Shared data, utility methods | Object-specific state |

```java
class Counter {
    static int totalCount = 0;  // shared across all
    int instanceCount = 0;      // per object
    
    Counter() {
        totalCount++;
        instanceCount++;
    }
    
    static void printTotal() {  // static method
        System.out.println(totalCount);
    }
}
```

**Rule:** Static methods cannot access instance members directly.

---

## 10. Immutability

**Definition:** Object whose state cannot be modified after creation.

**Key Rules:**
- Declare class `final` (prevent subclassing)
- All fields `private final`
- No setters
- Return copies of mutable fields
- Thread-safe by default

```java
public final class ImmutablePoint {
    private final int x, y;
    
    public ImmutablePoint(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    public int getX() { return x; }
    public int getY() { return y; }
    
    // "Modification" returns new object
    public ImmutablePoint move(int dx, int dy) {
        return new ImmutablePoint(x + dx, y + dy);
    }
}
```

---

## 11. SOLID Principles

| Principle | One-Liner | Violation Sign |
|-----------|-----------|----------------|
| **S**ingle Responsibility | One class = one reason to change | Class doing too many things |
| **O**pen-Closed | Open for extension, closed for modification | Editing existing code for new features |
| **L**iskov Substitution | Subtypes must be substitutable for base types | Child breaks parent's contract |
| **I**nterface Segregation | Many specific interfaces > one fat interface | Clients forced to implement unused methods |
| **D**ependency Inversion | Depend on abstractions, not concretions | High-level modules import low-level modules |

```python
# Dependency Inversion Example
# ❌ Bad: High-level depends on concrete
class OrderService:
    def __init__(self):
        self.db = MySQLDatabase()  # tight coupling

# ✅ Good: Depend on abstraction
class OrderService:
    def __init__(self, db: Database):  # interface
        self.db = db
```

---

## 12. Common Design Patterns (Brief)

### Creational
| Pattern | Purpose | One-Liner |
|---------|---------|-----------|
| **Singleton** | Single instance globally | `getInstance()` returns same object |
| **Factory** | Decouple object creation | Method decides which class to instantiate |
| **Builder** | Step-by-step complex object creation | Fluent API with `.build()` |

### Structural
| Pattern | Purpose | One-Liner |
|---------|---------|-----------|
| **Adapter** | Incompatible interface compatibility | Wrapper translates interface |
| **Decorator** | Add behavior dynamically | Wraps object, adds functionality |
| **Facade** | Simplify complex subsystems | Single unified interface |

### Behavioral
| Pattern | Purpose | One-Liner |
|---------|---------|-----------|
| **Observer** | Notify dependents on state change | Pub-sub pattern |
| **Strategy** | Swap algorithms at runtime | Encapsulate interchangeable behaviors |
| **Template Method** | Define skeleton, subclasses fill steps | Abstract class with concrete + abstract methods |

```python
# Strategy Pattern Example
class PaymentStrategy:
    def pay(self, amount): pass

class CreditCardPayment(PaymentStrategy):
    def pay(self, amount): return f"CC: ${amount}"

class PayPalPayment(PaymentStrategy):
    def pay(self, amount): return f"PayPal: ${amount}"

class Checkout:
    def __init__(self, strategy: PaymentStrategy):
        self.strategy = strategy
    
    def complete(self, amount):
        return self.strategy.pay(amount)
```

---

## 13. Quick Comparison Tables

### Interface vs Abstract Class vs Concrete Class
| Feature | Interface | Abstract Class | Concrete Class |
|---------|:---------:|:--------------:|:--------------:|
| Instantiate | ❌ | ❌ | ✅ |
| Abstract methods | ✅ | ✅ | ❌ |
| Concrete methods | ⚠️ (default only) | ✅ | ✅ |
| Multiple inheritance | ✅ | ❌ | ❌ |

### Overloading vs Overriding vs Hiding
| Aspect | Overloading | Overriding | Hiding (static) |
|--------|:-----------:|:----------:|:---------------:|
| Polymorphism | Compile-time | Runtime | Compile-time |
| Methods | Same name, diff params | Same signature | Static methods |
| Keyword | - | `@Override` | - |

### Association Types Summary
```
Association (weakest) → Aggregation → Composition (strongest)
     Uses-A                Has-A          Part-Of
   independent           can exist       cannot exist
                        separately       independently
```

---

## 14. Interview Pitfalls & Gotchas

### ❌ Common Mistakes

1. **Confusing overloading with overriding**
   - Overloading: same class, different params
   - Overriding: different class, same signature

2. **Thinking private members are inherited**
   - They exist in child object but are inaccessible

3. **Forgetting `super()` in constructors**
   - Java auto-calls no-arg `super()`, but not if parent has only parameterized constructors

4. **Multiple inheritance confusion**
   - Java: single class inheritance, multiple interface implementation
   - Python: supports multiple inheritance (MRO)

5. **Mutable default arguments (Python)**
   ```python
   # ❌ Bug
   def add_item(item, items=[]):
       items.append(item)
       return items
   
   # ✅ Fix
   def add_item(item, items=None):
       if items is None: items = []
       items.append(item)
       return items
   ```

6. **Breaking Liskov Substitution**
   ```java
   // ❌ Square cannot fully substitute Rectangle
   class Rectangle { void setWidth(int w); void setHeight(int h); }
   class Square extends Rectangle { /* breaks if width != height */ }
   ```

7. **Overusing inheritance**
   - "Is-a" relationship must hold logically
   - Prefer composition for flexibility

8. **Ignoring access modifiers in overriding**
   - Cannot make overridden method more restrictive
   - `public` → `protected` = ❌ Compile error

### ✅ Best Practices

- Favor **composition over inheritance**
- Program to **interfaces, not implementations**
- Keep classes **small and focused** (SRP)
- Make classes **immutable** when possible
- Use **dependency injection** for loose coupling
- **Override `equals()` and `hashCode()` together** (Java)
- Use **`@Override`** annotation to catch signature mistakes

---

## 15. Quick Reference Card

```
┌─────────────────────────────────────────────────────────────┐
│                    OOP QUICK REFERENCE                       │
├─────────────────────────────────────────────────────────────┤
│ PILLARS: Encapsulation | Abstraction | Inheritance | Polymorphism │
├─────────────────────────────────────────────────────────────┤
│ CLASS = Blueprint          OBJECT = Instance                 │
│ INTERFACE = Contract       ABSTRACT CLASS = Partial impl     │
├─────────────────────────────────────────────────────────────┤
│ OVERLOADING = Same name, diff params (compile-time)          │
│ OVERRIDING  = Same signature, child class (runtime)          │
├─────────────────────────────────────────────────────────────┤
│ STATIC = Class-level       INSTANCE = Object-level           │
├─────────────────────────────────────────────────────────────┤
│ ASSOCIATION: Uses-A (weak)                                   │
│ AGGREGATION: Has-A (child can exist alone)                   │
│ COMPOSITION: Part-Of (child depends on parent)               │
├─────────────────────────────────────────────────────────────┤
│ SOLID: Single-Resp | Open-Closed | Liskov | Interface-Seg | DI │
└─────────────────────────────────────────────────────────────┘
```

---

*Last updated: December 2024*
