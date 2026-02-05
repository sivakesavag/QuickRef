# Chapter 12: Metaclasses & Descriptors

> **Topics Covered**: type() as metaclass, __new__ vs __init__, custom metaclasses, __prepare__, descriptor protocol, data vs non-data descriptors, __get__, __set__, __delete__, __set_name__, property internals, attribute lookup order

---

## Questions

---

**Q12.1: Basic - [type() Dual Role]**

What does `type(obj)` return vs `type(name, bases, dict)`?

A) Both return the same thing
B) First returns object's type; second creates a new class
C) First creates class; second returns type
D) They're unrelated

**Answer: B**

**Explanation:**
`type(obj)` returns the type/class of `obj`. `type('MyClass', (Base,), {'attr': 1})` dynamically creates a new class named MyClass. `type` is both a function and the default metaclass.

---

**Q12.2: Intermediate - [type Creates Classes]**

What is the output?
```python
MyClass = type('MyClass', (), {'x': 10})
obj = MyClass()
print(obj.x)
```

A) Error
B) `10`
C) `None`
D) `MyClass`

**Answer: B**

**Explanation:**
`type(name, bases, dict)` creates a class dynamically. Equivalent to `class MyClass: x = 10`. `bases=()` means inherits from object. `obj.x` accesses class attribute → 10.

---

**Q12.3: Intermediate - [Metaclass Definition]**

What is a metaclass?

A) A class about metadata
B) A class whose instances are classes — defines how classes behave
C) A category of classes
D) An abstract class

**Answer: B**

**Explanation:**
Just as classes define object behavior (attributes, methods), metaclasses define class behavior (how classes are created, initialized). Default metaclass is `type`. Custom metaclasses customize class creation.

---

**Q12.4: Intermediate - [Metaclass Syntax]**

How do you specify a custom metaclass?

A) `class MyClass(metaclass=Meta):`
B) `@Meta class MyClass:`
C) `class MyClass meta Meta:`
D) `metaclass MyClass(Meta):`

**Answer: A**

**Explanation:**
Use `metaclass=` keyword argument in class definition. The metaclass is called to create the class object. Python 3 syntax. Python 2 used `__metaclass__` attribute.

---

**Q12.5: Advanced - [Custom Metaclass]**

What is the output?
```python
class Meta(type):
    def __new__(mcs, name, bases, dct):
        print(f"Creating {name}")
        return super().__new__(mcs, name, bases, dct)

class MyClass(metaclass=Meta):
    pass
```

A) Nothing printed
B) `Creating MyClass`
C) Error
D) `Meta`

**Answer: B**

**Explanation:**
When Python encounters the class definition, it calls `Meta.__new__` to create the class object. This happens at definition time, not instantiation. "Creating MyClass" prints during class creation.

---

**Q12.6: Advanced - [Metaclass __init__]**

When is metaclass `__init__` called vs `__new__`?

A) Both at same time
B) `__new__` creates the class, `__init__` initializes it after creation
C) `__init__` first, then `__new__`
D) Only `__new__` is called

**Answer: B**

**Explanation:**
Like regular classes: `__new__` creates (and returns) the class object, `__init__` initializes it after. Both receive the class being created. `__new__` must return the class; `__init__` modifies it in place.

---

**Q12.7: Advanced - [__prepare__ Method]**

What is `__prepare__` in metaclasses?

A) Prepares documentation
B) Returns a dictionary-like object to use as namespace during class body execution
C) Prepares for garbage collection
D) Validates class definition

**Answer: B**

**Explanation:**
`__prepare__(mcs, name, bases)` returns the object used as namespace for class body. Default is a dict. Return `OrderedDict` to preserve definition order, or custom dict for attribute tracking.

---

**Q12.8: Expert - [__prepare__ Example]**

What is the output?
```python
from collections import OrderedDict

class Meta(type):
    @classmethod
    def __prepare__(mcs, name, bases):
        return OrderedDict()
    
    def __new__(mcs, name, bases, dct):
        print(type(dct))
        return super().__new__(mcs, name, bases, dict(dct))

class MyClass(metaclass=Meta):
    a = 1
    b = 2
```

A) `<class 'dict'>`
B) `<class 'collections.OrderedDict'>`
C) Error
D) Nothing

**Answer: B**

**Explanation:**
`__prepare__` returns OrderedDict, so class body namespace is an OrderedDict. In `__new__`, `dct` is that OrderedDict with class attributes in definition order.

---

**Q12.9: Intermediate - [Metaclass Use Cases]**

Which is a valid use case for metaclasses?

A) Adding methods to individual objects
B) Registering classes, enforcing invariants, modifying class attributes
C) Memory optimization
D) File handling

**Answer: B**

**Explanation:**
Metaclasses: register subclasses (plugins), enforce class invariants (required methods), modify/add attributes, implement ORMs, create DSLs. Use sparingly — if a decorator suffices, prefer that.

---

**Q12.10: Advanced - [Class Registration]**

What does this metaclass do?
```python
registry = []

class RegisterMeta(type):
    def __new__(mcs, name, bases, dct):
        cls = super().__new__(mcs, name, bases, dct)
        if bases:  # Don't register base class itself
            registry.append(cls)
        return cls
```

A) Deletes classes
B) Registers all subclasses in a global list
C) Validates classes
D) Creates registries

**Answer: B**

**Explanation:**
Every class using this metaclass (or inheriting from one that does) gets added to `registry`. Common pattern for plugin systems — discover all plugins automatically. Check `if bases` to skip the base class.

---

**Q12.11: Basic - [Descriptor Definition]**

What is a descriptor?

A) A class that describes things
B) An object that defines `__get__`, `__set__`, or `__delete__` to customize attribute access
C) Documentation string
D) A type annotation

**Answer: B**

**Explanation:**
Descriptors customize attribute access on classes. Implementing `__get__` (and optionally `__set__`, `__delete__`) makes an object a descriptor. Properties, methods, classmethod, staticmethod — all use descriptors.

---

**Q12.12: Intermediate - [Descriptor Protocol]**

What's the difference between data and non-data descriptors?

A) Data descriptors store data
B) Data descriptors have __set__ or __delete__; non-data only have __get__
C) Non-data descriptors are read-only
D) No difference

**Answer: B**

**Explanation:**
Data descriptor: has `__set__` and/or `__delete__`. Non-data: only `__get__`. Key difference: data descriptors take priority over instance `__dict__`, non-data don't. Functions are non-data; properties are data.

---

**Q12.13: Intermediate - [__get__ Signature]**

What are the parameters of `__get__(self, obj, objtype)`?

A) self, value, type
B) self = descriptor, obj = instance (or None), objtype = owner class
C) self, name, value
D) Random parameters

**Answer: B**

**Explanation:**
`__get__(self, obj, objtype)`: `self` = descriptor instance, `obj` = instance accessing the attribute (None if accessed on class), `objtype` = class that owns the descriptor. Return value becomes the attribute value.

---

**Q12.14: Intermediate - [Simple Descriptor]**

What is the output?
```python
class Descriptor:
    def __get__(self, obj, objtype=None):
        return 42

class MyClass:
    attr = Descriptor()

print(MyClass().attr, MyClass.attr)
```

A) `42, 42`
B) `42, Descriptor object`
C) `Descriptor, Descriptor`
D) Error

**Answer: A**

**Explanation:**
`__get__` is called for both instance and class access. When accessed on class, `obj` is None, `objtype` is MyClass. Both cases return 42 here. Descriptors can differentiate using `if obj is None`.

---

**Q12.15: Intermediate - [Instance vs Class Access]**

What is the output?
```python
class Descriptor:
    def __get__(self, obj, objtype=None):
        if obj is None:
            return self
        return "instance value"

class MyClass:
    attr = Descriptor()

print(type(MyClass.attr).__name__)
```

A) `str`
B) `Descriptor`
C) `NoneType`
D) `MyClass`

**Answer: B**

**Explanation:**
When accessed on class (`obj is None`), descriptor returns `self` (the descriptor object). This is the property pattern — `SomeClass.property` returns the property object, not a value.

---

**Q12.16: Intermediate - [__set__ Method]**

What is the output?
```python
class Descriptor:
    def __get__(self, obj, objtype=None):
        return obj._value
    
    def __set__(self, obj, value):
        obj._value = value * 2

class MyClass:
    attr = Descriptor()

c = MyClass()
c.attr = 5
print(c.attr)
```

A) `5`
B) `10`
C) Error
D) `None`

**Answer: B**

**Explanation:**
`__set__` intercepts assignment. `c.attr = 5` calls `__set__` with value=5, stores 5*2=10 in `obj._value`. `__get__` returns `obj._value` = 10. Descriptor validates/transforms on set.

---

**Q12.17: Advanced - [Data Descriptor Priority]**

What is the output?
```python
class DataDesc:
    def __get__(self, obj, cls):
        return "descriptor"
    def __set__(self, obj, value):
        pass

class MyClass:
    attr = DataDesc()

c = MyClass()
c.__dict__['attr'] = "instance"
print(c.attr)
```

A) `instance`
B) `descriptor`
C) Error
D) `None`

**Answer: B**

**Explanation:**
⚠️ Data descriptors take priority over instance `__dict__`. Even though we put "instance" in `c.__dict__['attr']`, the data descriptor's `__get__` is called. This is why properties work.

---

**Q12.18: Advanced - [Non-Data Descriptor Priority]**

What is the output?
```python
class NonDataDesc:
    def __get__(self, obj, cls):
        return "descriptor"
    # No __set__

class MyClass:
    attr = NonDataDesc()

c = MyClass()
c.__dict__['attr'] = "instance"
print(c.attr)
```

A) `instance`
B) `descriptor`
C) Error
D) `NonDataDesc`

**Answer: A**

**Explanation:**
Non-data descriptors (no `__set__`) have lower priority than instance `__dict__`. Instance attribute shadows the descriptor. This is why methods work — they're non-data descriptors that can be overridden per-instance.

---

**Q12.19: Intermediate - [__set_name__]**

What does `__set_name__(self, owner, name)` do?

A) Sets the owner's name
B) Called when descriptor is assigned to a class attribute, receiving the name
C) Validates names
D) Renames the descriptor

**Answer: B**

**Explanation:**
When you write `class C: attr = Descriptor()`, Python calls `Descriptor().__set_name__(C, 'attr')`. The descriptor learns its attribute name without manual specification. Added in Python 3.6.

---

**Q12.20: Advanced - [__set_name__ Example]**

What is the output?
```python
class Descriptor:
    def __set_name__(self, owner, name):
        self.name = name
    
    def __get__(self, obj, cls):
        return f"I am {self.name}"

class MyClass:
    foo = Descriptor()
    bar = Descriptor()

print(MyClass().foo, MyClass().bar)
```

A) `I am foo, I am bar`
B) `I am foo I am bar`
C) Error
D) `foo, bar`

**Answer: B**

**Explanation:**
Each descriptor receives its attribute name via `__set_name__`. `foo` knows it's named "foo", `bar` knows it's named "bar". No need to pass the name explicitly: `foo = Descriptor('foo')`.

---

**Q12.21: Intermediate - [Property is Descriptor]**

Is `property` a descriptor?

A) No
B) Yes, it's a data descriptor implementing __get__, __set__, __delete__
C) Only partially
D) It's a decorator, not descriptor

**Answer: B**

**Explanation:**
`property` is a class implementing the full descriptor protocol. `@property` creates a property object with getter. `.setter`, `.deleter` add respective methods. That's why property access calls methods.

---

**Q12.22: Advanced - [Implementing Property-like Descriptor]**

What does this descriptor do?
```python
class TypedAttribute:
    def __init__(self, expected_type):
        self.expected_type = expected_type
    
    def __set_name__(self, owner, name):
        self.name = f'_{name}'
    
    def __get__(self, obj, cls):
        if obj is None:
            return self
        return getattr(obj, self.name, None)
    
    def __set__(self, obj, value):
        if not isinstance(value, self.expected_type):
            raise TypeError(f"Expected {self.expected_type}")
        setattr(obj, self.name, value)
```

A) Validates type on attribute assignment
B) Converts types
C) Documents types
D) Logs type info

**Answer: A**

**Explanation:**
This descriptor enforces type checking on assignment. `__set__` validates the value's type before storing. Value stored in instance's `__dict__` with underscore prefix. Example: `name = TypedAttribute(str)`.

---

**Q12.23: Intermediate - [Functions are Descriptors]**

Why can methods access `self`?

A) Magic
B) Functions implement __get__, which binds them to instances
C) Class does it
D) self is a keyword

**Answer: B**

**Explanation:**
Functions have `__get__`. When accessed via instance (`obj.method`), `__get__` returns a bound method (function + instance reference). That's how `self` gets passed automatically. Functions are non-data descriptors.

---

**Q12.24: Intermediate - [Bound Method Creation]**

What is the output?
```python
class MyClass:
    def method(self):
        return "called"

obj = MyClass()
print(type(obj.method).__name__)
print(type(MyClass.method).__name__)
```

A) `method, method`
B) `method, function`
C) `function, function`
D) `method method`

**Answer: B**

**Explanation:**
`obj.method` is a bound method (instance + function). `MyClass.method` is just the function. `function.__get__(obj, MyClass)` creates the bound method. That's descriptor magic at work.

---

**Q12.25: Advanced - [classmethod Descriptor]**

How does `@classmethod` work internally?

A) Changes function signature
B) It's a descriptor that binds function to class (cls) instead of instance
C) Modifies the class
D) Creates a new function

**Answer: B**

**Explanation:**
`classmethod` is a descriptor. Its `__get__` always binds to the class regardless of whether accessed on class or instance. The bound callable receives `cls` as first argument, not instance.

---

**Q12.26: Advanced - [staticmethod Descriptor]**

How does `@staticmethod` differ from regular function?

A) It's faster
B) staticmethod's __get__ returns the function unchanged, not bound
C) No difference
D) It prevents modifications

**Answer: B**

**Explanation:**
`staticmethod` is a descriptor whose `__get__` returns the wrapped function unchanged — no binding. `StaticMethod.func` gives the original function. That's why static methods don't receive self or cls.

---

**Q12.27: Expert - [Attribute Lookup Order]**

What is the attribute lookup order for `obj.attr`?

A) Instance dict → class dict → bases
B) Data descriptors → instance dict → non-data descriptors & class attrs → __getattr__
C) class dict → instance dict → descriptors
D) Random order

**Answer: B**

**Explanation:**
Simplified order: (1) Data descriptors (have `__set__`), (2) Instance `__dict__`, (3) Non-data descriptors and other class attributes (MRO), (4) `__getattr__` if defined. This explains all attribute behavior.

---

**Q12.28: Intermediate - [__getattr__ vs __getattribute__]**

When is `__getattr__` called?

A) For every attribute access
B) Only when attribute is not found through normal lookup
C) Before normal lookup
D) Never automatically

**Answer: B**

**Explanation:**
`__getattr__` is the fallback — called only when attribute isn't found elsewhere. `__getattribute__` is called for EVERY access (dangerous — can cause infinite loops). Prefer `__getattr__` for dynamic attributes.

---

**Q12.29: Advanced - [__getattribute__ Usage]**

What must you be careful of with `__getattribute__`?

A) Nothing special
B) Infinite recursion — calling self.attr inside it triggers __getattribute__ again
C) Memory leaks
D) Type errors

**Answer: B**

**Explanation:**
`__getattribute__` intercepts ALL attribute access. `return self.other` inside it calls `__getattribute__` again → infinite loop. Use `object.__getattribute__(self, name)` to access attributes safely.

---

**Q12.30: Advanced - [Descriptor for Validation]**

What is the output?
```python
class Positive:
    def __set_name__(self, owner, name):
        self.name = name
    
    def __set__(self, obj, value):
        if value <= 0:
            raise ValueError(f"{self.name} must be positive")
        obj.__dict__[self.name] = value
    
    def __get__(self, obj, cls):
        if obj is None:
            return self
        return obj.__dict__.get(self.name)

class Circle:
    radius = Positive()

c = Circle()
c.radius = 5
print(c.radius)
```

A) `5`
B) Error
C) `None`
D) `Positive object`

**Answer: A**

**Explanation:**
Descriptor validates value is positive, then stores in instance `__dict__`. `__get__` retrieves from instance `__dict__`. Value 5 passes validation, is stored and retrieved correctly.

---

**Q12.31: Intermediate - [Descriptor vs Property]**

When use a descriptor vs property?

A) Always use property
B) Descriptor when behavior is reused across multiple attributes/classes
C) Always use descriptor
D) They're the same

**Answer: B**

**Explanation:**
💡 Property: good for single attribute in one class. Descriptor: reusable validation/behavior across multiple attributes or classes. `Positive()` descriptor can be used for radius, width, height, etc.

---

**Q12.32: Advanced - [Metaclass vs __init_subclass__]**

When prefer `__init_subclass__` over metaclass?

A) Never
B) For simpler cases — modifying subclasses without full metaclass complexity
C) For performance
D) Always

**Answer: B**

**Explanation:**
`__init_subclass__(cls, **kwargs)` (Python 3.6+) is a hook called when a class is subclassed. Simpler than metaclasses for registration, validation, adding attributes. Use metaclass only when `__init_subclass__` is insufficient.

---

**Q12.33: Intermediate - [__init_subclass__ Example]**

What is the output?
```python
class Plugin:
    plugins = []
    
    def __init_subclass__(cls, **kwargs):
        super().__init_subclass__(**kwargs)
        Plugin.plugins.append(cls)

class MyPlugin(Plugin):
    pass

print(len(Plugin.plugins))
```

A) `0`
B) `1`
C) `2`
D) Error

**Answer: B**

**Explanation:**
When MyPlugin is defined, `Plugin.__init_subclass__` is called automatically. MyPlugin is added to `plugins`. Only one subclass defined, so length is 1. This pattern registers plugins automatically.

---

**Q12.34: Advanced - [Singleton Metaclass]**

How does this metaclass implement singleton?
```python
class SingletonMeta(type):
    _instances = {}
    
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]
```

A) By preventing instantiation
B) By caching and returning the same instance for each class
C) By raising errors
D) Doesn't implement singleton

**Answer: B**

**Explanation:**
`__call__` is invoked when you do `MyClass()`. First call creates and caches instance. Subsequent calls return cached instance. `_instances` dict stores one instance per class. True singleton per class.

---

**Q12.35: Intermediate - [type vs object]**

What is the relationship between `type` and `object`?

A) Unrelated
B) type is an instance of itself; object is parent of type; type is parent of object's type
C) object inherits from type
D) type inherits from object only

**Answer: B**

**Explanation:**
Mind-bending: `type` is an instance of `type` (metaclass of itself). `type` inherits from `object`. `object`'s type is `type`. They form a closed loop at the top of Python's type system.

---

**Q12.36: Expert - [Enum Implementation]**

How does Python's `Enum` class use metaclasses?

A) It doesn't use metaclasses
B) EnumMeta creates symbolic names, prevents modification, adds iteration
C) Just for documentation
D) For performance

**Answer: B**

**Explanation:**
`enum.EnumMeta` is the metaclass for Enum. It transforms class body members into Enum instances, makes the class iterable, prevents subclassing with members, and provides special access patterns.

---

**Q12.37: Intermediate - [Descriptor __delete__]**

What triggers `__delete__(self, obj)`?

A) Deleting the descriptor
B) `del obj.attr` where attr is a descriptor with __delete__
C) Object garbage collection
D) Never called

**Answer: B**

**Explanation:**
`del obj.attr` on an attribute that's a data descriptor calls `__delete__(self, obj)`. Use for cleanup or preventing deletion: `raise AttributeError("Cannot delete")`. Completes the CRUD (Create-Read-Update-Delete) pattern.

---

**Q12.38: Advanced - [Lazy Attribute Descriptor]**

What pattern does this implement?
```python
class Lazy:
    def __init__(self, func):
        self.func = func
    
    def __get__(self, obj, cls):
        if obj is None:
            return self
        value = self.func(obj)
        setattr(obj, self.func.__name__, value)
        return value
```

A) Caching
B) Lazy evaluation — compute once on first access, then cache in instance
C) Type checking
D) Logging

**Answer: B**

**Explanation:**
First access computes value and stores it directly in instance `__dict__` (replacing the descriptor access for that instance). Subsequent accesses hit instance `__dict__` directly. Lazy initialization pattern.

---

**Q12.39: Advanced - [Weakref in Descriptors]**

Why might you use `weakref.WeakKeyDictionary` in a descriptor?

A) Performance
B) Store per-instance data without preventing garbage collection
C) Security
D) Type safety

**Answer: B**

**Explanation:**
Storing data as `self.data[obj] = value` keeps references to objects, preventing GC. `WeakKeyDictionary` uses weak references — if user deletes all references to object, it's collected. Common pattern for descriptors.

---

**Q12.40: Expert - [Metaclass Conflict]**

What happens with multiple metaclasses?
```python
class MetaA(type): pass
class MetaB(type): pass
class A(metaclass=MetaA): pass
class B(metaclass=MetaB): pass
class C(A, B): pass  # ?
```

A) Uses MetaA
B) Uses MetaB
C) TypeError: metaclass conflict
D) Creates new metaclass

**Answer: C**

**Explanation:**
A's metaclass is MetaA, B's is MetaB. C would need a metaclass that's subclass of both. Python doesn't auto-create this → TypeError. Fix: create `class MetaC(MetaA, MetaB): pass` and use that.

---

**Q12.41: Intermediate - [__slots__ and Descriptors]**

How do `__slots__` work internally?

A) Magic
B) Each slot becomes a data descriptor managed by the class
C) Memory allocation only
D) Dict replacement

**Answer: B**

**Explanation:**
`__slots__ = ['x', 'y']` creates descriptors (member_descriptor) for x and y at class level. No instance `__dict__`. The descriptors manage storage via the internal structure, saving memory.

---

**Q12.42: Expert - [ABC and Metaclass]**

How does `ABC` use metaclasses?

A) It doesn't
B) ABCMeta metaclass tracks abstract methods and prevents instantiation
C) For documentation
D) Performance optimization

**Answer: B**

**Explanation:**
`ABCMeta` metaclass: tracks `@abstractmethod`s in `__abstractmethods__`. `__call__` checks if abstract methods remain unimplemented → raises TypeError. That's how ABC enforces the interface.

---

**Q12.43: Advanced - [class Body Execution]**

When does a class body execute?

A) When first instance is created
B) Immediately when Python reaches the class definition
C) When imported
D) Never — it's just metadata

**Answer: B**

**Explanation:**
Class body executes during class creation — before any instances. Variables become class attributes, functions become methods. This is why you can't reference self in class body (no instance exists yet).

---

**Q12.44: Intermediate - [Dynamic Class Creation]**

What is the output?
```python
def make_class(name, attribute_value):
    return type(name, (), {'value': attribute_value})

MyClass = make_class('MyClass', 42)
print(MyClass().value)
```

A) `42`
B) `MyClass`
C) Error
D) `None`

**Answer: A**

**Explanation:**
`type()` dynamically creates a class with `value` attribute. Factory function creates different classes with different attribute values. The class behaves like any regular class.

---

**Q12.45: Advanced - [__class_getitem__]**

What does `__class_getitem__` enable?

A) Getting class items
B) Subscript syntax on classes: MyClass[int]
C) Indexing instances
D) Slicing

**Answer: B**

**Explanation:**
`__class_getitem__(cls, item)` handles `Class[args]` syntax. Used for generic types: `List[int]`, `Dict[str, int]`. Returns a GenericAlias or similar. Enables type parameterization without instantiation.

---

**Q12.46: Intermediate - [Descriptor Lifecycle]**

In what order are descriptor methods called on `obj.attr = value`?

A) `__get__` only
B) `__set__` only
C) `__set__` is called directly if attribute is data descriptor
D) `__get__` then `__set__`

**Answer: C**

**Explanation:**
For assignment `obj.attr = value`: if `attr` is a data descriptor, `__set__` is called immediately. No `__get__` first (why would you need to read for writing?). The lookup finds the descriptor and invokes `__set__`.

---

**Q12.47: Expert - [Customizing Class Creation]**

What are the hooks for customizing class creation (in order)?

A) `__new__` only
B) `__prepare__` → body execution → `__new__` → `__init__` → `__init_subclass__`
C) `__init__` → `__new__`
D) random order

**Answer: B**

**Explanation:**
Order: (1) `__prepare__` creates namespace, (2) class body executes in that namespace, (3) metaclass `__new__` creates class, (4) metaclass `__init__` initializes, (5) `__init_subclass__` on parent is called.

---

**Q12.48: Advanced - [nondata Descriptor Pattern]**

Why are functions non-data descriptors?

A) Historical reasons
B) So instance attributes can shadow methods if needed
C) For performance
D) Accident of implementation

**Answer: B**

**Explanation:**
Being non-data allows assigning to instance: `obj.method = lambda: ...` works. Rarely needed but possible. Properties are data descriptors because you typically DON'T want instance dict to shadow them.

---

**Q12.49: Advanced - [Slot Descriptor]**

What type of descriptor is created by `__slots__`?

A) Non-data descriptor
B) member_descriptor — a data descriptor
C) No descriptor
D) property

**Answer: B**

**Explanation:**
`__slots__` creates `member_descriptor` objects (data descriptors). They have `__get__` and `__set__`. Being data descriptors, they take priority over instance `__dict__` — but with slots, there's no instance `__dict__` anyway.

---

**Q12.50: Expert - [When Not to Use Metaclasses]**

When should you avoid metaclasses?

A) Never avoid them
B) When simpler alternatives exist: decorators, __init_subclass__, descriptors
C) For production code
D) In Python 3

**Answer: B**

**Explanation:**
💡 "Metaclasses are deeper magic than 99% of users should worry about" — Tim Peters. First try: class decorator, `__init_subclass__`, descriptors. Metaclasses for: modifying all subclasses, complex class creation, DSLs. Complexity has cost.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 3 | 6% |
| Intermediate | 23 | 46% |
| Advanced | 18 | 36% |
| Expert | 6 | 12% |

**Key Topics Covered:**
- type() as metaclass and class factory
- Custom metaclass creation
- __prepare__, __new__, __init__ in metaclasses
- Descriptor protocol (__get__, __set__, __delete__, __set_name__)
- Data vs non-data descriptors
- Attribute lookup order
- Properties, classmethod, staticmethod internals
- __init_subclass__ as simpler alternative
- When to use/avoid metaclasses
