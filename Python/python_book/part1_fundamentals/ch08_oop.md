# Chapter 8: Object-Oriented Programming

> **Topics Covered**: Classes, objects, self, inheritance (single, multiple, MRO), super(), __init__, __new__, encapsulation, properties, descriptors, class vs instance variables, magic methods, MRO C3 linearization

---

## Questions

---

**Q8.1: Basic - [Class Definition]**

What is the correct syntax to define a class in Python?

A) `class MyClass {}`
B) `class MyClass:`
C) `def class MyClass:`
D) `create class MyClass:`

**Answer: B**

**Explanation:**
Python uses `class ClassName:` followed by an indented body. No braces like C++/Java. By convention, class names use CamelCase. The class body contains methods and attributes.

---

**Q8.2: Basic - [Creating Instances]**

What is the output?
```python
class Dog:
    pass

d = Dog()
print(type(d))
```

A) `<class 'Dog'>`
B) `<type 'Dog'>`
C) `Dog`
D) `object`

**Answer: A**

**Explanation:**
`Dog()` creates an instance of the Dog class. `type(d)` returns `<class '__main__.Dog'>` or `<class 'Dog'>`. In Python 3, all classes are "new-style" classes, subclasses of `object`.

---

**Q8.3: Basic - [__init__ Method]**

What is the purpose of `__init__`?

A) To destroy an object
B) To initialize a new instance with starting values
C) To define static methods
D) To import modules

**Answer: B**

**Explanation:**
`__init__` is the initializer (not constructor). It's called after the object is created to set up initial state. It receives `self` (the instance) plus any arguments passed during instantiation: `Dog("Buddy")` → `__init__(self, "Buddy")`.

---

**Q8.4: Basic - [self Parameter]**

What is `self` in Python methods?

A) A reserved keyword
B) A reference to the current instance, passed automatically
C) A global variable
D) The class itself

**Answer: B**

**Explanation:**
`self` is the first parameter of instance methods, referring to the instance calling the method. Python passes it automatically: `d.bark()` becomes `Dog.bark(d)`. The name `self` is convention, not keyword.

---

**Q8.5: Intermediate - [Instance Attributes]**

What is the output?
```python
class Dog:
    def __init__(self, name):
        self.name = name

d1 = Dog("Buddy")
d2 = Dog("Max")
print(d1.name, d2.name)
```

A) `Buddy Max`
B) `Max Max`
C) `Buddy Buddy`
D) Error

**Answer: A**

**Explanation:**
Instance attributes (set via `self.name`) belong to individual objects. Each Dog has its own `name`. `d1.name = "Buddy"`, `d2.name = "Max"`. They're independent.

---

**Q8.6: Intermediate - [Class Attributes]**

What is the output?
```python
class Dog:
    species = "Canis familiaris"
    
d1 = Dog()
d2 = Dog()
print(d1.species, d2.species)
```

A) Error: species not defined
B) `Canis familiaris Canis familiaris`
C) `None None`
D) `Dog Dog`

**Answer: B**

**Explanation:**
Class attributes (defined in class body, not in `__init__`) are shared by all instances. Both `d1.species` and `d2.species` reference the same class attribute. Modifying via class changes it for all.

---

**Q8.7: Intermediate - [Class vs Instance Attributes]**

What is the output?
```python
class Counter:
    count = 0
    
    def __init__(self):
        self.count += 1

c1 = Counter()
c2 = Counter()
print(Counter.count, c1.count, c2.count)
```

A) `0, 1, 1`
B) `2, 2, 2`
C) `0, 1, 2`
D) `2, 1, 1`

**Answer: A**

**Explanation:**
⚠️ **Gotcha**: `self.count += 1` reads class `count` (0), adds 1, then creates INSTANCE attribute `self.count = 1`. Class attribute unchanged (0). Each instance gets its own `count = 1`. To modify class attribute: `Counter.count += 1`.

---

**Q8.8: Basic - [Methods]**

What is the output?
```python
class Calculator:
    def add(self, a, b):
        return a + b

calc = Calculator()
print(calc.add(3, 4))
```

A) `7`
B) `(3, 4)`
C) Error: too many arguments
D) `add(3, 4)`

**Answer: A**

**Explanation:**
Instance method `add` is called on `calc`. Python automatically passes `calc` as `self`. We pass 3 and 4 as `a` and `b`. Method returns 3 + 4 = 7.

---

**Q8.9: Intermediate - [Class Methods]**

What is a `@classmethod`?

A) A method that only works with classes
B) A method that receives the class (cls) instead of instance as first argument
C) A private method
D) A method defined in __init__

**Answer: B**

**Explanation:**
`@classmethod` decorates methods that receive the class (`cls`) rather than instance. Useful for factory methods: `@classmethod def from_string(cls, s): return cls(parse(s))`. Can be called on class or instance.

---

**Q8.10: Intermediate - [Class Method Example]**

What is the output?
```python
class Person:
    count = 0
    
    def __init__(self, name):
        self.name = name
        Person.count += 1
    
    @classmethod
    def get_count(cls):
        return cls.count

p1 = Person("Alice")
p2 = Person("Bob")
print(Person.get_count())
```

A) `0`
B) `1`
C) `2`
D) Error

**Answer: C**

**Explanation:**
Each `Person` creation increments `Person.count`. After creating p1 and p2, count is 2. `get_count()` is a classmethod accessing `cls.count` (same as `Person.count`).

---

**Q8.11: Intermediate - [Static Methods]**

What is a `@staticmethod`?

A) A method that cannot change
B) A method that doesn't receive self or cls — behaves like a regular function
C) A method for static analysis
D) A method that only accepts static types

**Answer: B**

**Explanation:**
`@staticmethod` creates methods that don't access instance or class data. No automatic first argument. Essentially a function in the class namespace. Use when logic relates to class but doesn't need instance/class access.

---

**Q8.12: Intermediate - [Static Method Example]**

What is the output?
```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b

print(Math.add(3, 4))
```

A) `7`
B) Error: no self
C) Error: can't call on class
D) `None`

**Answer: A**

**Explanation:**
Static methods work like regular functions. `Math.add(3, 4)` calls with just the provided arguments. No `self` or `cls` passed. Can also call on instance: `Math().add(3, 4)`.

---

**Q8.13: Basic - [Inheritance]**

What is the output?
```python
class Animal:
    def speak(self):
        return "Some sound"

class Dog(Animal):
    pass

d = Dog()
print(d.speak())
```

A) Error: Dog has no speak
B) `Some sound`
C) `None`
D) `Dog sound`

**Answer: B**

**Explanation:**
`Dog(Animal)` inherits from `Animal`. Dog doesn't override `speak()`, so it uses Animal's version. This is inheritance — child classes get parent's methods automatically.

---

**Q8.14: Intermediate - [Method Overriding]**

What is the output?
```python
class Animal:
    def speak(self):
        return "Some sound"

class Dog(Animal):
    def speak(self):
        return "Woof!"

d = Dog()
print(d.speak())
```

A) `Some sound`
B) `Woof!`
C) Error: duplicate method
D) `Some sound Woof!`

**Answer: B**

**Explanation:**
Dog overrides Animal's `speak()`. When called on a Dog instance, Python uses Dog's version. This is polymorphism — same method name, different behavior based on the class.

---

**Q8.15: Intermediate - [super() Basics]**

What is the output?
```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed

d = Dog("Buddy", "Labrador")
print(d.name, d.breed)
```

A) `Buddy Labrador`
B) Error: name not defined
C) `None Labrador`
D) `Dog Labrador`

**Answer: A**

**Explanation:**
`super().__init__(name)` calls parent's `__init__`, setting `self.name`. Then `self.breed` is set. `super()` returns a proxy to the parent class, allowing access to its methods.

---

**Q8.16: Intermediate - [super() Purpose]**

Why use `super()` instead of `Parent.__init__(self, args)`?

A) It's shorter
B) It properly handles multiple inheritance and MRO
C) It's faster
D) No difference

**Answer: B**

**Explanation:**
`super()` follows the Method Resolution Order (MRO), which is crucial for multiple inheritance. Direct parent calls `Parent.__init__()` can skip classes in diamond inheritance. `super()` ensures proper cooperative inheritance.

---

**Q8.17: Advanced - [Multiple Inheritance]**

What is the output?
```python
class A:
    def greet(self):
        return "A"

class B:
    def greet(self):
        return "B"

class C(A, B):
    pass

c = C()
print(c.greet())
```

A) `A`
B) `B`
C) `AB`
D) Error: ambiguous

**Answer: A**

**Explanation:**
With multiple inheritance, Python uses MRO (Method Resolution Order). `C(A, B)` searches A before B. `A.greet` is found first. Check MRO with `C.__mro__`: `(C, A, B, object)`.

---

**Q8.18: Advanced - [MRO - Method Resolution Order]**

What does MRO determine?

A) Which methods are private
B) The order in which parent classes are searched for methods
C) How many methods a class has
D) Method execution speed

**Answer: B**

**Explanation:**
MRO (Method Resolution Order) determines the order Python searches classes for a method. Uses C3 linearization algorithm. View with `ClassName.__mro__` or `ClassName.mro()`. Ensures consistent, predictable method lookup in multiple inheritance.

---

**Q8.19: Advanced - [Diamond Problem]**

What is the "diamond problem" in inheritance?

A) A class inherits from four classes
B) Ambiguity when class inherits from two classes that share a common ancestor
C) A class shaped like a diamond
D) A design pattern

**Answer: B**

**Explanation:**
Diamond: `A` at top, `B` and `C` inherit from `A`, `D` inherits from both `B` and `C`. Should `D` call `A.__init__` once or twice? Python's MRO ensures `A` appears once and is called once with cooperative `super()`.

---

**Q8.20: Advanced - [C3 Linearization]**

What is C3 linearization?

A) A compression algorithm
B) The algorithm Python uses to compute MRO
C) A way to define three classes
D) Code formatting

**Answer: B**

**Explanation:**
C3 linearization creates a consistent MRO that respects: (1) local precedence (left-to-right in inheritance list), (2) monotonicity (child before parent), (3) consistent ordering across all paths. It fails if no valid order exists (raises TypeError).

---

**Q8.21: Basic - [__str__ Method]**

What is the purpose of `__str__`?

A) To store strings
B) To provide a readable string representation of an object
C) To convert all attributes to strings
D) To compare strings

**Answer: B**

**Explanation:**
`__str__` returns a readable, user-friendly string representation. Called by `str()` and `print()`. Should be understandable. Example: `Dog("Buddy")` → `"Dog named Buddy"`. If not defined, falls back to `__repr__`.

---

**Q8.22: Basic - [__repr__ Method]**

What is the difference between `__str__` and `__repr__`?

A) No difference
B) `__str__` is for users, `__repr__` is for developers (ideally valid Python code)
C) `__repr__` is faster
D) `__str__` is deprecated

**Answer: B**

**Explanation:**
`__repr__` should be unambiguous, ideally valid Python to recreate the object: `"Dog('Buddy')"`. `__str__` is for end-users. In interactive shell, `__repr__` is displayed. `print()` uses `__str__` (falls back to `__repr__`).

---

**Q8.23: Intermediate - [__eq__ Method]**

What is the output?
```python
class Point:
    def __init__(self, x, y):
        self.x, self.y = x, y
    
    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

p1 = Point(1, 2)
p2 = Point(1, 2)
print(p1 == p2, p1 is p2)
```

A) `True, True`
B) `False, False`
C) `True, False`
D) `False, True`

**Answer: C**

**Explanation:**
`__eq__` defines `==` behavior. Both points have same coordinates, so `==` is True. They're different objects in memory, so `is` is False. Without `__eq__`, `==` defaults to identity comparison.

---

**Q8.24: Intermediate - [__hash__ Method]**

If you define `__eq__`, what happens to `__hash__`?

A) It's automatically updated
B) It becomes None (object becomes unhashable) unless explicitly defined
C) Nothing changes
D) Error is raised

**Answer: B**

**Explanation:**
⚠️ When you define `__eq__`, Python sets `__hash__` to None (unhashable). This is because equal objects must have equal hashes. To use objects in sets/as dict keys, define `__hash__` consistently with `__eq__`.

---

**Q8.25: Intermediate - [Encapsulation - Naming]**

What is the convention for "private" attributes in Python?

A) `private` keyword
B) Prefix with single underscore `_name` (weak convention) or double underscore `__name` (name mangling)
C) Suffix with `_private`
D) Using lowercase only

**Answer: B**

**Explanation:**
Python has no true private. `_name` = "internal use" convention, still accessible. `__name` triggers name mangling → `_ClassName__name`, harder to access accidentally. Neither is truly private, just conventions honored by convention.

---

**Q8.26: Intermediate - [Name Mangling]**

What is the output?
```python
class MyClass:
    def __init__(self):
        self.__secret = 42

obj = MyClass()
print(obj._MyClass__secret)
```

A) Error: __secret is private
B) `42`
C) `__secret`
D) `None`

**Answer: B**

**Explanation:**
`__secret` becomes `_MyClass__secret` (name mangling). It's still accessible, just harder to reach accidentally. This prevents accidental override in subclasses, not security. Truly private data isn't Python's philosophy.

---

**Q8.27: Intermediate - [Property Decorator]**

What does `@property` do?

A) Makes attribute read-only
B) Creates a managed attribute with getter (and optionally setter/deleter)
C) Creates class property
D) Locks the attribute

**Answer: B**

**Explanation:**
`@property` turns a method into a "getter" for a read-only attribute. Access as `obj.name` calls the method. Add `@name.setter` for write access, `@name.deleter` for deletion. Provides controlled access to attributes.

---

**Q8.28: Intermediate - [Property Example]**

What is the output?
```python
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def diameter(self):
        return self._radius * 2

c = Circle(5)
print(c.diameter)
```

A) `10`
B) `<bound method>`
C) Error
D) `5`

**Answer: A**

**Explanation:**
`@property` makes `diameter` accessible as attribute, not method call. `c.diameter` (no parentheses) calls the getter, returning `5 * 2 = 10`. This allows computed attributes that look like simple data access.

---

**Q8.29: Advanced - [Property with Setter]**

What is the output?
```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def fahrenheit(self):
        return self._celsius * 9/5 + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        self._celsius = (value - 32) * 5/9

t = Temperature(0)
t.fahrenheit = 212
print(t._celsius)
```

A) `0`
B) `100`
C) `212`
D) Error

**Answer: B**

**Explanation:**
Setting `t.fahrenheit = 212` calls the setter, which converts to Celsius: `(212-32)*5/9 = 100`. The property provides a bidirectional interface — reading gives Fahrenheit, writing updates Celsius.

---

**Q8.30: Advanced - [Descriptors]**

What is a descriptor in Python?

A) A class that documents other classes
B) An object that defines `__get__`, `__set__`, or `__delete__` to customize attribute access
C) A string describing a class
D) A metadata class

**Answer: B**

**Explanation:**
Descriptors are the underlying mechanism for properties, methods, classmethod, staticmethod. A class with `__get__` (and optionally `__set__`, `__delete__`) controls attribute access when assigned to a class attribute. Powers Python's attribute access.

---

**Q8.31: Basic - [Magic Methods Overview]**

What are "magic methods" (dunder methods)?

A) Methods that work like magic
B) Methods with double underscores that Python calls automatically in certain contexts
C) Private methods
D) External library methods

**Answer: B**

**Explanation:**
Magic/dunder methods (`__init__`, `__str__`, `__add__`, etc.) are called by Python in specific contexts: `obj + other` calls `__add__`, `str(obj)` calls `__str__`, `len(obj)` calls `__len__`. They customize object behavior.

---

**Q8.32: Intermediate - [__len__ and __getitem__]**

What is the output?
```python
class MyList:
    def __init__(self, data):
        self.data = data
    
    def __len__(self):
        return len(self.data)
    
    def __getitem__(self, index):
        return self.data[index]

ml = MyList([1, 2, 3])
print(len(ml), ml[1])
```

A) `3, 2`
B) `3, 1`
C) `[1, 2, 3], 2`
D) Error

**Answer: A**

**Explanation:**
`__len__` enables `len(ml)` → 3. `__getitem__` enables indexing `ml[1]` → 2. Together, they make the object sequence-like. Adding `__iter__` would make it fully iterable.

---

**Q8.33: Intermediate - [__call__ Method]**

What is the output?
```python
class Multiplier:
    def __init__(self, factor):
        self.factor = factor
    
    def __call__(self, x):
        return x * self.factor

double = Multiplier(2)
print(double(5))
```

A) `10`
B) `Multiplier(5)`
C) Error: can't call object
D) `2`

**Answer: A**

**Explanation:**
`__call__` makes instances callable like functions. `double(5)` invokes `double.__call__(5)` → `5 * 2 = 10`. Useful for stateful function objects, decorators, and factory patterns.

---

**Q8.34: Intermediate - [__add__ Method]**

What is the output?
```python
class Vector:
    def __init__(self, x, y):
        self.x, self.y = x, y
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)
print(v1 + v2)
```

A) `Vector(4, 6)`
B) `(4, 6)`
C) Error: can't add Vectors
D) `Vector(1, 2)Vector(3, 4)`

**Answer: A**

**Explanation:**
`__add__` handles `+` operator. `v1 + v2` calls `v1.__add__(v2)`. Creates new Vector with summed components. `__repr__` provides the display format. This is operator overloading.

---

**Q8.35: Intermediate - [__iter__ and __next__]**

What methods make an object iterable?

A) `__iter__` only
B) `__iter__` and `__next__`
C) `__loop__` and `__continue__`
D) `iterator()` method

**Answer: B**

**Explanation:**
`__iter__` returns an iterator (often `self`). `__next__` returns the next value or raises `StopIteration`. Together, they enable `for` loops. Iterator objects must have both; iterables need only `__iter__`.

---

**Q8.36: Advanced - [__slots__]**

What is the purpose of `__slots__`?

A) To create slot machines
B) To restrict instance attributes and save memory by not using __dict__
C) To define time slots
D) To create multiple inheritance slots

**Answer: B**

**Explanation:**
`__slots__ = ['x', 'y']` restricts instances to those attributes only. No `__dict__` is created, saving memory (significant for millions of small objects). Trade-off: can't add arbitrary attributes, affects inheritance.

---

**Q8.37: Advanced - [__slots__ Example]**

What is the output?
```python
class Point:
    __slots__ = ['x', 'y']
    
p = Point()
p.x = 1
p.y = 2
p.z = 3
```

A) Creates point with x, y, z
B) AttributeError: 'Point' object has no attribute 'z'
C) Point with x=1, y=2
D) z is silently ignored

**Answer: B**

**Explanation:**
`__slots__` restricts allowed attributes. `z` isn't in slots, so assignment raises AttributeError. This prevents typos creating new attributes and enforces the intended interface.

---

**Q8.38: Intermediate - [isinstance vs type]**

What is the difference between `isinstance()` and `type()` for type checking?

A) No difference
B) `isinstance()` checks inheritance hierarchy; `type()` checks exact type
C) `type()` is deprecated
D) `isinstance()` is slower

**Answer: B**

**Explanation:**
`isinstance(obj, Class)` returns True if obj is instance of Class OR any subclass. `type(obj) == Class` checks exact type only. For polymorphism, use `isinstance()`. For exact type matching, use `type()`.

---

**Q8.39: Intermediate - [issubclass]**

What is the output?
```python
class Animal: pass
class Dog(Animal): pass
class Cat(Animal): pass

print(issubclass(Dog, Animal), issubclass(Cat, Dog))
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
`issubclass(A, B)` checks if A is subclass of B. Dog inherits from Animal → True. Cat doesn't inherit from Dog (they're siblings) → False. Can also check multiple: `issubclass(Dog, (Animal, Cat))`.

---

**Q8.40: Advanced - [__new__ Method]**

What is the difference between `__new__` and `__init__`?

A) No difference
B) `__new__` creates the instance, `__init__` initializes it after creation
C) `__new__` is deprecated
D) `__init__` creates, `__new__` initializes

**Answer: B**

**Explanation:**
`__new__` is the actual constructor — it creates and returns the instance. `__init__` initializes an already-created instance. Override `__new__` for immutable types or singletons. `__new__` receives class, returns instance; `__init__` receives instance.

---

**Q8.41: Expert - [Singleton with __new__]**

How can `__new__` implement a singleton?

A) By raising an error on second call
B) By returning the same instance if one already exists
C) By making __init__ empty
D) Cannot be done with __new__

**Answer: B**

**Explanation:**
```python
class Singleton:
    _instance = None
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```
`__new__` returns existing instance if available, creating only once.

---

**Q8.42: Intermediate - [Composition vs Inheritance]**

When should you prefer composition over inheritance?

A) Always use inheritance
B) When you need "has-a" relationship rather than "is-a"
C) Never use composition
D) Only for primitive types

**Answer: B**

**Explanation:**
💡 Inheritance = "is-a" (Dog is an Animal). Composition = "has-a" (Car has an Engine). Composition is often more flexible — change behavior by swapping components. "Favor composition over inheritance" is a key design principle.

---

**Q8.43: Intermediate - [Abstract Base Classes]**

What is an abstract base class (ABC)?

A) A class for alphabet
B) A class that can't be instantiated and may have abstract methods subclasses must implement
C) A basic class
D) A class with no methods

**Answer: B**

**Explanation:**
ABCs define interfaces. Use `from abc import ABC, abstractmethod`. Abstract methods have no implementation — subclasses MUST override them. Attempting to instantiate an ABC with abstract methods raises TypeError.

---

**Q8.44: Intermediate - [ABC Example]**

What is the output?
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

s = Shape()
```

A) Creates Shape object
B) TypeError: Can't instantiate abstract class
C) Returns None
D) Creates empty shape

**Answer: B**

**Explanation:**
Shape has abstract method `area()`. Instantiating raises TypeError. You must subclass and implement all abstract methods. ABCs enforce that subclasses provide required methods.

---

**Q8.45: Intermediate - [ABC Implementation]**

What is the output?
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, r):
        self.r = r
    def area(self):
        return 3.14 * self.r ** 2

c = Circle(5)
print(c.area())
```

A) TypeError
B) `78.5`
C) `None`
D) `25`

**Answer: B**

**Explanation:**
Circle properly implements `area()`, so it can be instantiated. `area()` returns 3.14 * 25 = 78.5. The ABC is satisfied — Circle fulfills the Shape interface.

---

**Q8.46: Advanced - [__init_subclass__]**

What is `__init_subclass__` used for?

A) Initializing subclass instances
B) Hook called when a class is subclassed, before __init__
C) Starting a subprocess
D) Internal class initialization

**Answer: B**

**Explanation:**
`__init_subclass__(cls, **kwargs)` is called when a class is inherited from. Useful for registering plugins, validating subclasses, or automatic setup. Introduced in Python 3.6 as cleaner alternative to metaclasses for some uses.

---

**Q8.47: Expert - [Metaclasses Basics]**

What is a metaclass?

A) A class about metadata
B) A class whose instances are classes — it defines how classes behave
C) A class within a class
D) A deprecated feature

**Answer: B**

**Explanation:**
Just as classes define object behavior, metaclasses define class behavior. Default metaclass is `type`. Create custom: `class Meta(type): pass`, use with `class MyClass(metaclass=Meta): pass`. Used for ORMs, API frameworks, advanced customization.

---

**Q8.48: Intermediate - [Duck Typing]**

What is duck typing?

A) A way to type faster
B) If an object has the required methods, use it regardless of actual type
C) Type checking for waterfowl
D) Static type analysis

**Answer: B**

**Explanation:**
"If it walks like a duck and quacks like a duck, it's a duck." Python cares about what objects CAN DO, not what they ARE. A file-like object just needs `read()` and `write()` — doesn't need to be `File` class. Enables flexible, decoupled code.

---

**Q8.49: Intermediate - [hasattr, getattr, setattr]**

What is the output?
```python
class Box:
    pass

b = Box()
setattr(b, 'size', 10)
print(getattr(b, 'size'), hasattr(b, 'color'))
```

A) `10, True`
B) `10, False`
C) `size, color`
D) Error

**Answer: B**

**Explanation:**
`setattr(obj, name, value)` sets attribute dynamically. `getattr(obj, name)` retrieves it. `hasattr(obj, name)` checks existence. `b.size` = 10 (set). `b.color` doesn't exist → `hasattr` returns False.

---

**Q8.50: Intermediate - [vars() and __dict__]**

What is the output?
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

p = Point(3, 4)
print(vars(p))
```

A) `{'x': 3, 'y': 4}`
B) `(3, 4)`
C) `Point(3, 4)`
D) `['x', 'y']`

**Answer: A**

**Explanation:**
`vars(obj)` returns `obj.__dict__` — the instance's attribute dictionary. Shows instance attributes as dict. Class attributes are in `ClassName.__dict__`. Useful for debugging and serialization.

---

**Q8.51: Intermediate - [super() with Multiple Inheritance]**

What is the output?
```python
class A:
    def method(self):
        print("A", end=" ")

class B(A):
    def method(self):
        print("B", end=" ")
        super().method()

class C(A):
    def method(self):
        print("C", end=" ")
        super().method()

class D(B, C):
    def method(self):
        print("D", end=" ")
        super().method()

D().method()
```

A) `D B A`
B) `D B C A`
C) `D B C A A`
D) `D A`

**Answer: B**

**Explanation:**
MRO for D: `[D, B, C, A, object]`. `D.method` → print D, call super → `B.method` → print B, call super → `C.method` → print C, call super → `A.method` → print A. `super()` follows MRO, not direct parent.

---

**Q8.52: Advanced - [Mixin Classes]**

What is a mixin class?

A) A class that mixes data types
B) A class designed to add specific functionality through multiple inheritance
C) A class that combines methods randomly
D) A debugging class

**Answer: B**

**Explanation:**
Mixins provide reusable functionality to be "mixed in" via multiple inheritance. They're not meant to be instantiated alone. Example: `LoggingMixin` adds logging to any class. Convention: suffix with "Mixin" for clarity.

---

**Q8.53: Advanced - [__class__ Attribute]**

What is object's `__class__` attribute?

A) The class that created the object
B) A list of all classes
C) The object's documentation
D) Class methods

**Answer: A**

**Explanation:**
`obj.__class__` returns the class of the object — same as `type(obj)`. Can be reassigned (though rarely wise), changing the object's type at runtime. Used in introspection and metaprogramming.

---

**Q8.54: Intermediate - [Method Binding]**

What is the difference between `obj.method` and `ClassName.method`?

A) No difference
B) `obj.method` is bound (has self=obj), `ClassName.method` is unbound (needs self)
C) One is faster
D) `ClassName.method` doesn't work

**Answer: B**

**Explanation:**
`obj.method` is a bound method — `self` is automatically `obj`. `ClassName.method` is a function — you must pass the instance explicitly: `ClassName.method(obj, args)`. This is how `dog.bark()` becomes `Dog.bark(dog)`.

---

**Q8.55: Advanced - [Cooperative Multiple Inheritance]**

What is "cooperative multiple inheritance"?

A) Classes that work together
B) Using super() correctly so all classes in MRO get called once
C) Inheriting from multiple parents without conflicts
D) A design pattern name

**Answer: B**

**Explanation:**
In cooperative inheritance, every class uses `super()` to call the next class in MRO. This ensures all `__init__` methods are called exactly once, even in diamond inheritance. Required for frameworks like Django's class-based views.

---

**Q8.56: Intermediate - [Private Methods]**

What is the output?
```python
class Parent:
    def __private(self):
        return "Parent private"
    
    def call_private(self):
        return self.__private()

class Child(Parent):
    def __private(self):
        return "Child private"

c = Child()
print(c.call_private())
```

A) `Child private`
B) `Parent private`
C) Error
D) `None`

**Answer: B**

**Explanation:**
⚠️ Name mangling: `__private` becomes `_Parent__private` in Parent and `_Child__private` in Child. `call_private` (in Parent) calls `_Parent__private`, not Child's version. This is intentional — private methods don't get overridden by subclasses.

---

**Q8.57: Intermediate - [Class Decorators]**

What can a class decorator do?

A) Only add methods
B) Modify or replace the class entirely
C) Only rename the class
D) Nothing useful

**Answer: B**

**Explanation:**
Class decorators receive the class and can modify it (add methods, wrap it, register it) or return a completely different class. `@dataclass` is a famous example — it modifies the class heavily, adding methods based on annotations.

---

**Q8.58: Intermediate - [Dataclasses]**

What does `@dataclass` do?

A) Converts class to data
B) Automatically generates __init__, __repr__, __eq__, etc. based on class annotations
C) Stores data in database
D) Makes class immutable

**Answer: B**

**Explanation:**
`@dataclass` (Python 3.7+) auto-generates boilerplate: `__init__` from annotated fields, `__repr__`, `__eq__`, optionally `__hash__`, comparison methods. Reduces repetitive code for data-holding classes. `@dataclass(frozen=True)` makes immutable.

---

**Q8.59: Advanced - [Dataclass Example]**

What is the output?
```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

p1 = Point(1, 2)
p2 = Point(1, 2)
print(p1 == p2, p1)
```

A) `False, <__main__.Point object>`
B) `True, Point(x=1, y=2)`
C) `True, (1, 2)`
D) Error

**Answer: B**

**Explanation:**
`@dataclass` generates `__eq__` (comparing fields) and `__repr__`. `p1 == p2` is True (same x, y values). `__repr__` shows `Point(x=1, y=2)`. Massive reduction in boilerplate for simple classes.

---

**Q8.60: Advanced - [Protocol - Structural Subtyping]**

What is `typing.Protocol` used for?

A) Network protocols
B) Defining interfaces for structural (duck) typing with type checkers
C) Secure communication
D) Protocol buffers

**Answer: B**

**Explanation:**
`Protocol` (Python 3.8+) defines interfaces for structural subtyping. Unlike ABCs (nominal subtyping — must explicitly inherit), Protocols check duck typing: if a class has required methods, it matches. Type checkers use this for static duck typing.

---

**Q8.61: Expert - [Descriptor Protocol Details]**

When is `__get__` called with owner=None?

A) Never
B) When accessing via the class itself (e.g., `SomeClass.attribute`)
C) When the attribute doesn't exist
D) When object is None

**Answer: B**

**Explanation:**
`__get__(self, obj, owner)`: `obj` is the instance (or None if accessed on class), `owner` is always the class. `SomeClass.attr` calls `__get__(None, SomeClass)`. Properties check this to return the property object itself when accessed on class.

---

**Q8.62: Advanced - [__set_name__]**

What does `__set_name__(self, owner, name)` do?

A) Sets the object's name
B) Called when descriptor is assigned to a class attribute, receives the attribute name
C) Names a set
D) Renames the class

**Answer: B**

**Explanation:**
When you write `class C: attr = SomeDescriptor()`, Python calls `SomeDescriptor().__set_name__(C, 'attr')`. The descriptor learns its name without you passing it. Added in Python 3.6 for cleaner descriptor definitions.

---

**Q8.63: Intermediate - [__contains__]**

What is the output?
```python
class Range:
    def __init__(self, start, end):
        self.start, self.end = start, end
    
    def __contains__(self, item):
        return self.start <= item < self.end

r = Range(1, 10)
print(5 in r, 10 in r)
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
`__contains__` handles `in` operator. 5 is in [1, 10) → True. 10 is not (exclusive end) → False. This makes custom collections work with membership testing.

---

**Q8.64: Intermediate - [__enter__ and __exit__]**

What methods make a class work with `with` statement?

A) `__with__` and `__using__`
B) `__enter__` and `__exit__`
C) `__context__` and `__end__`
D) `__start__` and `__stop__`

**Answer: B**

**Explanation:**
`__enter__` is called at start of `with` block (can return a value for `as` clause). `__exit__` is called at end (receives exception info if any). Together, they make context managers. See Chapter 11 for details.

---

**Q8.65: Advanced - [Method Types Summary]**

What's the difference between instance method, classmethod, and staticmethod?

A) Only syntax differs
B) First receives self (instance), second receives cls (class), third receives nothing
C) They're all deprecated
D) Speed differences only

**Answer: B**

**Explanation:**
Instance method: `def m(self)` — operates on instance. Class method: `@classmethod def m(cls)` — operates on class (factory methods, class state). Static method: `@staticmethod def m()` — no implicit arg, just organized function.

---

**Q8.66: Expert - [Metaclass __call__]**

What happens when you write `MyClass(args)`?

A) `__init__` is called
B) Metaclass `__call__` is invoked, which calls `__new__` then `__init__`
C) Python looks up the class
D) Arguments are validated

**Answer: B**

**Explanation:**
`MyClass(args)` invokes `type.__call__` (or custom metaclass's `__call__`). This: (1) calls `MyClass.__new__` to create instance, (2) calls `instance.__init__` to initialize. Understanding this helps with singletons and object creation customization.

---

**Q8.67: Intermediate - [__del__ Method]**

What is `__del__` and when is it called?

A) Deletes the instance immediately
B) Called when the object is about to be garbage collected (destructor)
C) Called when del statement is used
D) Called on class deletion

**Answer: B**

**Explanation:**
`__del__` is called when ref count reaches 0 (or by cyclic GC). NOT called immediately by `del obj` — that just removes a reference. Don't rely on `__del__` for cleanup (use context managers). Can have issues with reference cycles.

---

**Q8.68: Intermediate - [Class Attributes Inheritance]**

What is the output?
```python
class A:
    x = 1

class B(A):
    pass

B.x = 2
print(A.x, B.x)
```

A) `1, 2`
B) `2, 2`
C) `1, 1`
D) Error

**Answer: A**

**Explanation:**
Initially, `B.x` looks up to `A.x` = 1. Assignment `B.x = 2` creates a new class attribute ON B, shadowing A's. A.x remains 1. If we had done `A.x = 2` instead, both would be 2 (shared attribute).

---

**Q8.69: Advanced - [Object Identity After __new__]**

What is the output?
```python
class Always42(int):
    def __new__(cls, value):
        return super().__new__(cls, 42)

a = Always42(10)
b = Always42(20)
print(a, b, a + b)
```

A) `10, 20, 30`
B) `42, 42, 84`
C) Error
D) `42, 42, 42`

**Answer: B**

**Explanation:**
`__new__` for immutable types sets the actual value. Always42 ignores input, always creates int with value 42. Both a and b are 42. `a + b = 84`. This is how immutable subclasses customize their values.

---

**Q8.70: Expert - [Metaclass Creating Singleton]**

How can a metaclass enforce singleton pattern?

A) By deleting all instances
B) By storing instance in metaclass and returning it from `__call__`
C) By making class abstract
D) Cannot be done

**Answer: B**

**Explanation:**
```python
class SingletonMeta(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]
```
Metaclass intercepts instance creation, returning cached instance.

---

**Q8.71: Intermediate - [Checking Class Membership]**

What is the output?
```python
class Animal: pass
class Dog(Animal): pass

d = Dog()
print(isinstance(d, Animal))
print(isinstance(d, Dog))
print(type(d) is Animal)
```

A) `True, True, True`
B) `True, True, False`
C) `False, True, False`
D) `True, False, False`

**Answer: B**

**Explanation:**
`isinstance` checks inheritance: d is Dog (True) and Dog is-a Animal (True). `type(d) is Animal` checks EXACT type: d is Dog, not Animal, so False. Use `isinstance` for polymorphic checks.

---

**Q8.72: Intermediate - [Object's Base Class]**

What is `object` in Python 3?

A) A reserved keyword
B) The base class of all classes — every class implicitly inherits from it
C) An empty class
D) A module

**Answer: B**

**Explanation:**
`object` is the root of Python's class hierarchy. `class MyClass:` implicitly means `class MyClass(object):`. Even built-in types (int, str) inherit from object. It provides default methods like `__init__`, `__repr__`, `__eq__`.

---

**Q8.73: Advanced - [__getattr__ vs __getattribute__]**

What is the difference between `__getattr__` and `__getattribute__`?

A) No difference
B) `__getattribute__` is called for ALL attribute access; `__getattr__` only for missing attributes
C) `__getattr__` is deprecated
D) `__getattribute__` is faster

**Answer: B**

**Explanation:**
`__getattribute__` intercepts EVERY attribute access (dangerous — can cause infinite recursion). `__getattr__` is called only when attribute isn't found normally. Use `__getattr__` for dynamic attributes; `__getattribute__` for proxies/wrappers (carefully!).

---

**Q8.74: Expert - [ClassVar Type Hint]**

What does `ClassVar[T]` indicate in type hints?

A) A constant variable
B) An attribute that's a class variable, not an instance variable
C) A variable that can hold classes
D) A classmethod parameter

**Answer: B**

**Explanation:**
`ClassVar[int]` tells type checkers this is a class-level attribute. Subclasses may override but instances shouldn't assign to it. With dataclasses, `ClassVar` fields aren't included in generated `__init__`.

---

**Q8.75: Intermediate - [super() Return Type]**

What does `super()` return?

A) The parent class
B) A proxy object that delegates method calls to the parent class(es)
C) An instance of the parent class
D) A list of parent classes

**Answer: B**

**Explanation:**
`super()` returns a proxy object (not the parent class itself). This proxy follows MRO to delegate calls. In single inheritance, it behaves like the parent. In multiple inheritance, it ensures cooperative calls through the entire hierarchy.

---

**Q8.76: Intermediate - [Override Prevention]**

Can you prevent a method from being overridden in Python?

A) Yes, with `final` keyword
B) No built-in mechanism, but `typing.final` decorator provides hints for type checkers
C) Yes, with `private` keyword
D) Yes, with `const` modifier

**Answer: B**

**Explanation:**
Python has no enforcement mechanism to prevent overriding. `@typing.final` (PEP 591) marks methods that shouldn't be overridden; type checkers report violations. Runtime still allows override. Philosophy: trust developers.

---

**Q8.77: Expert - [__mro_entries__]**

What is `__mro_entries__` used for?

A) Sorting MRO
B) Allowing non-class objects (like generic aliases) in class bases
C) Creating MRO documentation
D) Debugging inheritance

**Answer: B**

**Explanation:**
When a base "class" isn't actually a class (like `List[int]`), Python calls `__mro_entries__` to get actual classes for MRO. This enables generic types in inheritance: `class MyList(List[int]): pass`. Added in Python 3.7.

---

**Q8.78: Advanced - [Bound Methods are Callable]**

What is the output?
```python
class Dog:
    def bark(self):
        return "Woof!"

d = Dog()
b = d.bark
print(callable(b), b())
```

A) `True, Woof!`
B) `False, Error`
C) `True, None`
D) `Error`

**Answer: A**

**Explanation:**
`d.bark` (without calling) is a bound method object. Bound methods are callable. `callable(b)` → True. `b()` calls it (self is already bound to d) → "Woof!". This allows passing methods as callbacks.

---

**Q8.79: Intermediate - [__bool__]**

What is the output?
```python
class Box:
    def __init__(self, items):
        self.items = items
    
    def __bool__(self):
        return len(self.items) > 0

b1 = Box([1, 2])
b2 = Box([])
print(bool(b1), bool(b2))
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
`__bool__` defines truthiness. Non-empty box → True, empty box → False. Without `__bool__`, Python checks `__len__` (if non-zero). Without either, objects are truthy by default.

---

**Q8.80: Intermediate - [Class as First-Class Object]**

What is the output?
```python
class Dog: pass
class Cat: pass

animals = {'dog': Dog, 'cat': Cat}
pet = animals['dog']()
print(type(pet).__name__)
```

A) `Dog`
B) `dog`
C) `dict`
D) Error

**Answer: A**

**Explanation:**
Classes are first-class objects — can be stored in dicts, passed as arguments, etc. `animals['dog']` gets the Dog class. `()` instantiates it. `type(pet).__name__` is "Dog". This enables factory patterns and dynamic instantiation.

---

**Q8.81: Advanced - [Object Pickling]**

What methods control how an object is pickled?

A) `__save__` and `__load__`
B) `__getstate__` and `__setstate__`
C) `__pickle__` and `__unpickle__`
D) `__serialize__` and `__deserialize__`

**Answer: B**

**Explanation:**
`__getstate__` returns state to pickle (can filter attributes). `__setstate__` restores state during unpickling. Also: `__reduce__` and `__reduce_ex__` for more control. Used when default pickling doesn't work (e.g., file handles can't be pickled).

---

**Q8.82: Intermediate - [__module__ Attribute]**

What does `obj.__class__.__module__` tell you?

A) The object's size
B) The module where the class is defined
C) The Python version
D) Memory module

**Answer: B**

**Explanation:**
`__module__` attribute indicates where a class is defined. `'__main__'` if run as script, otherwise module name. Useful for debugging, serialization, and introspection. Classes defined interactively have `'__main__'`.

---

**Q8.83: Intermediate - [Class Documentation]**

How do you document a class?

A) Only comments
B) Docstring as first statement in class body
C) README file
D) `__doc__` variable

**Answer: B**

**Explanation:**
Class docstring goes right after `class Name:`. Accessed via `ClassName.__doc__` or `help(ClassName)`. Describe purpose, usage, attributes. Methods have their own docstrings. Documentation tools (Sphinx) extract these.

---

**Q8.84: Expert - [Attribute Resolution Order]**

In what order does Python look up attributes (simplified)?

A) Instance only
B) Instance __dict__, class __dict__, base classes (MRO), __getattr__
C) Class first, then instance
D) Random order

**Answer: B**

**Explanation:**
Simplified: data descriptors → instance `__dict__` → class `__dict__` (and MRO) → non-data descriptors → `__getattr__`. Data descriptors (with `__set__`) beat instance attributes. This is why properties work correctly.

---

**Q8.85: Advanced - [__class_getitem__]**

What is `__class_getitem__` used for?

A) Getting items from class
B) Enabling subscript syntax on classes: `MyClass[int]`
C) Getting class by index
D) Iterating over class

**Answer: B**

**Explanation:**
`__class_getitem__(cls, item)` enables `ClassName[args]` syntax (generics). `list[int]` calls `list.__class_getitem__(int)`. Used for type hints and generic classes. Added to support `typing` module behavior.

---

## Chapter Summary

**Total MCQs: 85**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 17 | 20% |
| Intermediate | 45 | 53% |
| Advanced | 18 | 21% |
| Expert | 5 | 6% |

**Key Topics Covered:**
- Classes, instances, self
- __init__ and __new__
- Class vs instance attributes
- Inheritance (single, multiple)
- MRO and super()
- Magic methods (__str__, __repr__, __eq__, __add__, etc.)
- Properties and descriptors
- Class/static methods
- Abstract base classes
- Encapsulation and name mangling
- Dataclasses
- Metaclasses basics
- Duck typing and protocols
