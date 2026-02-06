# Chapter 8: Object-Oriented Programming

**Target MCQs**: 60-70
**Current Batch**: 1-30
**Topics Covered**: Classes, Instances, `self`, Constructors, Inheritance, MRO, Encapsulation, Class Attributes vs Instance Attributes.

---

**Q8.1: Basic - [Class Definition]**

Which keyword is used to define a class in Python?

A) `struct`
B) `object`
C) `class`
D) `def`

**Answer: C**

**Explanation:**
Python uses the `class` keyword to define a new class.

---

**Q8.2: Intermediate - [Self Parameter]**

In a standard instance method, what does the first parameter (conventionally named `self`) represent?

A) The class itself.
B) The instance calling the method.
C) The global scope.
D) The parent class.

**Answer: B**

**Explanation:**
`self` is a reference to the specific instance of the class that is calling the method. It allows access to instance attributes and other methods.

---

**Q8.3: Advanced - [Class vs Instance Attribute]**

```python
class Dog:
    kind = 'canine'
    def __init__(self, name):
        self.name = name

d1 = Dog('Fido')
d2 = Dog('Buddy')
d1.kind = 'wolf'
```
What is `d2.kind`?

A) `'wolf'`
B) `'canine'`
C) `None`
D) Error.

**Answer: B**

**Explanation:**
`kind` is a class attribute shared by all instances. `self.name` is an instance attribute. `d1.kind = 'wolf'` creates a *new* instance attribute `kind` on `d1`, shadowing the class attribute. `d2` still sees the original class attribute `'canine'`.

---

**Q8.4: Basic - [Constructor]**

Which method is automatically called when a new instance is created?

A) `__create__`
B) `__start__`
C) `__init__`
D) `__construct__`

**Answer: C**

**Explanation:**
`__init__` is the initializer method (often called constructor, though technically `__new__` is the constructor). It sets up the initial state of the object.

---

**Q8.5: Intermediate - [Inheritance Syntax]**

How do you define a class `Child` that inherits from `Parent`?

A) `class Child inherits Parent:`
B) `class Child extends Parent:`
C) `class Child(Parent):`
D) `class Child : Parent`

**Answer: C**

**Explanation:**
Python uses parentheses after the class name to specify base classes: `class SubClass(BaseClass):`.

---

**Q8.6: Advanced - [MRO Basics]**

What does MRO stand for in Python OOP?

A) Method Resolution Order
B) Memory Resource Optimization
C) Multiple Recursive Operations
D) Method Return Object

**Answer: A**

**Explanation:**
MRO (Method Resolution Order) determines the order in which Python searches for base classes when executing a method. Python 2.3+ uses the C3 linearization algorithm.

---

**Q8.7: Basic - [Private Attributes]**

How do you define a "private" attribute in a class (by convention)?

A) `private var`
B) `_var` (single underscore)
C) `__var` (double underscore)
D) `var.private`

**Answer: B**

**Explanation:**
By convention, a single leading underscore `_var` indicates internal use. Double underscore `__var` triggers name mangling (making it harder to access from subclasses), which is often mistaken for "private" but is technically for collision avoidance.

---

**Q8.8: Intermediate - [Super Function]**

`super().__init__()` is used to:

A) Call the global `__init__`.
B) Call the initializer of the superclass (parent).
C) Initialize all subclasses.
D) Restart the object.

**Answer: B**

**Explanation:**
`super()` returns a proxy object that delegates method calls to a parent or sibling class of type. Commonly used to call the parent's constructor.

---

**Q8.9: Advanced - [Name Mangling]**

If a class `MyClass` has an attribute `__secret`, how is it stored internally?

A) `__secret`
B) `_MyClass__secret`
C) `secret`
D) `__MyClass_secret`

**Answer: B**

**Explanation:**
Double leading underscores trigger name mangling. The interpreter rewrites the attribute name as `_ClassName__attribute` to prevent accidental overriding in subclasses.

---

**Q8.10: Expert - [Method Resolution Order C3]**

In checking `D.mro()`, if `class D(B, C): pass`, which class is checked first after `D`?

A) `C`
B) `B`
C) `object`
D) Random.

**Answer: B**

**Explanation:**
MRO follows the order of inheritance specified in the class definition. Left-to-right: `D`, then `B`, then `C` (assuming B and C don't share complex hierarchy that violates C3).

---

**Q8.11: Basic - [Destructor]**

Which method is called when an object is about to be destroyed (garbage collected)?

A) `__delete__`
B) `__del__`
C) `__remove__`
D) `__destroy__`

**Answer: B**

**Explanation:**
`__del__` is the finalizer method. It is called when the reference count drops to zero to perform cleanup.

---

**Q8.12: Intermediate - [Isinstance]**

`isinstance(obj, Class)` returns True if:

A) `obj` is exactly an instance of `Class`.
B) `obj` is an instance of `Class` or any of its subclasses.
C) `obj` has the same name as `Class`.
D) `obj` converts to `Class`.

**Answer: B**

**Explanation:**
`isinstance` checks for inheritance. It returns True for instances of the class OR its derived classes.

---

**Q8.13: Advanced - [Multiple Inheritance]**

Python supports:

A) Single inheritance only.
B) Multiple inheritance.
C) Interface implementation only.
D) Prototypal inheritance.

**Answer: B**

**Explanation:**
Python supports multiple inheritance, allowing a class to inherit from multiple parent classes (e.g., `class C(A, B):`).

---

**Q8.14: Basic - [Empty Class]**

What is the simplest way to define an empty class?

A) `class A: pass`
B) `class A: {}`
C) `class A: return`
D) `class A: None`

**Answer: A**

**Explanation:**
The `pass` statement is a null operation used as a placeholder for the empty body.

---

**Q8.15: Intermediate - [Class Method Decorator]**

Which decorator defines a method that receives the class (`cls`) as the first argument instead of the instance?

A) `@staticmethod`
B) `@classmethod`
C) `@property`
D) `@instancemethod`

**Answer: B**

**Explanation:**
`@classmethod` transforms a method to receive the class object as the first argument (conventionally `cls`), allowing access to class state or factory patterns.

---

**Q8.16: Advanced - [Static Method]**

A `@staticmethod`:

A) Receives `self` automatically.
B) Receives `cls` automatically.
C) Receives neither `self` nor `cls`.
D) Is private.

**Answer: C**

**Explanation:**
Static methods behave like plain functions that happen to be in a class namespace. They do not receive any implicit first argument.

---

**Q8.17: Expert - [MetaClass Concept]**

In Python, classes themselves are instances of what?

A) `object`
B) `type`
C) `class`
D) `super`

**Answer: B**

**Explanation:**
Everything in Python is an object. Function definitions are logic objects. Class definitions are objects of type `type`. `type` is the default metaclass.

---

**Q8.18: Intermediate - [Str vs Repr 2]**

If `__str__` is not defined but `__repr__` is, what does `print(obj)` output?

A) The default `<object at address>`.
B) The output of `__repr__`.
C) Error.
D) Nothing.

**Answer: B**

**Explanation:**
If `__str__` is missing, Python falls back to calling `__repr__`. (The reverse is not true).

---

**Q8.19: Basic - [Hasattr]**

To check if object `o` has attribute `'x'`:

A) `o.has('x')`
B) `exists(o, 'x')`
C) `hasattr(o, 'x')`
D) `'x' in o`

**Answer: C**

**Explanation:**
`hasattr(obj, name)` checks for the existence of an attribute.

---

**Q8.20: Advanced - [Slot usage]**

`__slots__` is used primarily to:

A) enforce static typing.
B) restrict adding new attributes to instances (saving memory).
C) make the class faster to import.
D) allow private variables.

**Answer: B**

**Explanation:**
Defining `__slots__` tells Python not to use a `__dict__` for instances, but to allocate space for a fixed set of attributes. This saves significant memory for classes with millions of instances.

---

**Q8.21: Intermediate - [Duck Typing]**

"If it walks like a duck and quacks like a duck, it's a duck." This refers to:

A) Strict inheritance requirements.
B) Interface checking via usage rather than type declarations.
C) Polymorphism in C++.
D) The `duck` module.

**Answer: B**

**Explanation:**
Python relies on dynamic typing (Duck Typing). If an object has the required methods/attributes (e.g., `quack`), it works, regardless of its inheritance lineage.

---

**Q8.22: Basic - [Calling Parent Method]**

To call a method `greet` from the parent class inside an override:

A) `parent.greet()`
B) `super().greet()`
C) `base.greet()`
D) `greet()`

**Answer: B**

**Explanation:**
`super().method()` invokes the method from the next class in the MRO.

---

**Q8.23: Advanced - [Diamond Problem]**

The C3 linearization algorithm is used to solve:

A) Recursion depth limits.
B) The "Diamond Problem" in multiple inheritance (order consistency).
C) Circular imports.
D) Hash collisions.

**Answer: B**

**Explanation:**
In multiple inheritance, if A inherits from B and C, and both B and C inherit from D, determining which version of a method to call (and visiting D only once) is strictly solved by the C3 MRO algorithm.

---

**Q8.24: Expert - [Data Descriptors]**

An object is a "data descriptor" if it defines:

A) `__get__` only.
B) `__set__` or `__delete__`.
C) `__init__`.
D) `__call__`.

**Answer: B**

**Explanation:**
An object defining `__get__` is a descriptor. If it also defines `__set__` or `__delete__`, it is a **data descriptor**. Data descriptors take precedence over instance dictionaries `__dict__`.

---

**Q8.25: Intermediate - [Property Decorator]**

The `@property` decorator allows you to:

A) Define a class constant.
B) Access a method like an attribute (without parentheses).
C) Making a variable private.
D) Write to a file.

**Answer: B**

**Explanation:**
It creates a getter method that is accessed as an attribute: `obj.prop` instead of `obj.prop()`.

---

**Q8.26: Basic - [Override]**

What is method overriding?

A) Writing a method with the same name in a subclass to replace the parent's logic.
B) Writing a method with same name but different arguments (Overloading).
C) Deleting a method.
D) Calling a method twice.

**Answer: A**

**Explanation:**
Overriding is providing a specific implementation of a method that is already provided by the superclass.

---

**Q8.27: Advanced - [Dir on Class vs Instance]**

`dir(MyClass)` includes:

A) Only class attributes.
B) Class attributes and methods.
C) Instance attributes of all instances.
D) Only `__init__`.

**Answer: B**

**Explanation:**
`dir(Class)` returns names in the class scope (methods, class variables). It does not know about instance variables created inside `__init__` until an instance is created and inspected.

---

**Q8.28: Intermediate - [Getattr Default]**

`getattr(obj, 'x', 10)` returns:

A) The value of `x` if it exists, else 10.
B) The value of `x`, raising error if missing (ignores 10).
C) Always 10.
D) Sets `x` to 10.

**Answer: A**

**Explanation:**
`getattr` accepts an optional default value to return if the attribute is missing.

---

**Q8.29: Expert - [Method Resolution - Dynamic]**

If you add a method into a class at runtime (`MyClass.method = new_func`), do existing instances see it?

A) No.
B) Yes.
C) Only if they call `update()`.
D) Error.

**Answer: B**

**Explanation:**
Python classes are dynamic. Methods are looked up on the class at runtime. If the class structure changes, all instances immediately reflect that change (unless shadowed by instance dict).

---

**Q8.30: Basic - [Object Base]**

In Python 3, all classes explicitly or implicitly inherit from:

A) `None`
B) `type`
C) `object`
D) `Base`

**Answer: C**

**Explanation:**
`object` is the base class for all classes in Python 3 (New-style classes).

---

**Q8.31: Intermediate - [Abstract Base Classes]**

Which module provides the `ABC` class and `@abstractmethod` decorator?

A) `abstract`
B) `abc`
C) `types`
D) `classes`

**Answer: B**

**Explanation:**
The `abc` module (Abstract Base Classes) provides the infrastructure for defining abstract base classes in Python.

---

**Q8.32: Basic - [Magic Method Arithmetics]**

To enable usage of the `+` operator for a custom class, which method must be implemented?

A) `__plus__`
B) `__add__`
C) `__sum__`
D) `__oper__`

**Answer: B**

**Explanation:**
`__add__` corresponds to the binary `+` operator.

---

**Q8.33: Advanced - [Call Method]**

If `obj` is an instance of `MyClass`, what enables the syntax `obj()`?

A) `__call__`
B) `__run__`
C) `__exec__`
D) `__init__`

**Answer: A**

**Explanation:**
Implementing `__call__` allows an instance to be called as a function.

---

**Q8.34: Expert - [Metaclass Usage]**

Which argument in the class definition specifies the metaclass?

A) `__metaclass__ = Meta` (inside body) - Python 2 style.
B) `class Foo(metaclass=Meta):` - Python 3 style.
C) `class Foo(Meta):`
D) `@metaclass(Meta)`

**Answer: B**

**Explanation:**
In Python 3, the metaclass is specified as a keyword argument in the class header: `class ClassName(metaclass=MetaName):`.

---

**Q8.35: Intermediate - [Property Setter]**

How do you define a setter for a property named `x`?

A) `@x.setter`
B) `@property(x, set)`
C) `def set_x(self, val):`
D) `@setter(x)`

**Answer: A**

**Explanation:**
Once a method is decorated with `@property`, a corresponding setter decorator `@name.setter` becomes available.

---

**Q8.36: Advanced - [__new__ vs __init__]**

`__new__` is responsible for:

A) Initializing the instance.
B) Creating and returning the new instance (allocation).
C) Deleting the instance.
D) Copying the instance.

**Answer: B**

**Explanation:**
`__new__` is the actual constructor (static method) that allocates memory and returns the object. `__init__` initializes the already-created object.

---

**Q8.37: Basic - [Type Function]**

`type(obj)` returns:

A) The class of the object.
B) The memory address.
C) The string representation.
D) True if object is valid.

**Answer: A**

**Explanation:**
`type(obj)` returns the class type of the object.

---

**Q8.38: Intermediate - [Vars]**

`vars(obj)` is equivalent to:

A) `obj.__dict__`
B) `dir(obj)`
C) `help(obj)`
D) `id(obj)`

**Answer: A**

**Explanation:**
`vars()` returns the `__dict__` attribute of the object (if it exists).

---

**Q8.39: Advanced - [Dataclasses]**

Introduced in Python 3.7, `@dataclass` automatically generates:

A) `__init__`, `__repr__`, `__eq__` (and others).
B) Getters and Setters.
C) Database connections.
D) JSON serialization methods.

**Answer: A**

**Explanation:**
The `dataclasses` module provides a decorator that creates boilerplate methods like `__init__` and `__repr__` based on class attributes with type hints.

---

**Q8.40: Expert - [Diamond Problem MRO]**

Given `A(object)`, `B(A)`, `C(A)`, `D(B, C)`. The MRO of D is:

A) D, B, A, C, object
B) D, B, C, A, object
C) D, B, A, C, A, object
D) D, C, B, A, object

**Answer: B**

**Explanation:**
C3 Linearization preserves the order of parents (B before C) and ensures parents appear after children. Logic: D -> B -> C -> A -> object. (It visits all subclasses of A before visiting A).

---

**Q8.41: Basic - [Instance Method]**

`def method(self):`. If called as `Class.method(obj)`, is it valid?

A) Yes, perfectly valid.
B) No, must be called as `obj.method()`.
C) No, "self" is missing.
D) Loops forever.

**Answer: A**

**Explanation:**
`obj.method()` is syntactic sugar for `Class.method(obj)`. Both are valid.

---

**Q8.42: Intermediate - [Abstract Method Instantiation]**

If a class contains an `@abstractmethod` but acts as a concrete class (inherits from ABC), what happens if you try to instantiate it without overriding the abstract method?

A) Instance creates successfully.
B) `TypeError` at instantiation time.
C) `NotImplementedError` when calling the method.
D) Warning.

**Answer: B**

**Explanation:**
Python's `abc` module enforces that you cannot instantiate a class with abstract methods remaining. It raises `TypeError`.

---

**Q8.43: Advanced - [Mixin]**

A "Mixin" class is typically used for:

A) Providing specific functionality to be reused by inheritance, not meant to stand alone.
B) Mixing types (int and str).
C) Multiple dispatch.
D) Circular dependencies.

**Answer: A**

**Explanation:**
Mixins are small classes providing a set of features (like `JsonSerializable`) intended to be combined with other classes via multiple inheritance.

---

**Q8.44: Expert - [Descriptor Protocol]**

If both `__get__` and `__set__` are defined, the descriptor is:

A) A Data Descriptor.
B) A Non-Data Descriptor.
C) A Property.
D) A Method.

**Answer: A**

**Explanation:**
Defining `__set__` (or `__delete__`) makes it a Data Descriptor, which overrides the instance's `__dict__` lookup for that name.

---

**Q8.45: Basic - [Self name]**

Is `self` a reserved keyword in Python?

A) Yes.
B) No, it's just a strong convention. You could use `this` or `me`.
C) Yes, only in classes.
D) No, but using other names raises SyntaxWarning.

**Answer: B**

**Explanation:**
`self` is not a keyword. It is simply the first parameter. You *can* name it anything, but you *should* use `self` for readability.

---

**Q8.46: Intermediate - [Len Magic Method]**

`len(obj)` calls which method?

A) `obj.length()`
B) `obj.size()`
C) `obj.__len__()`
D) `obj.__count__()`

**Answer: C**

**Explanation:**
The built-in `len()` function delegates to `__len__`.

---

**Q8.47: Advanced - [__dict__ proxy]**

`MyClass.__dict__` returns a:

A) Normal dictionary.
B) `mappingproxy` object (read-only view).
C) List of tuples.
D) Set of strings.

**Answer: B**

**Explanation:**
In Python 3, the class `__dict__` is exposed as a `mappingproxy` to prevent direct dictionary mutations that could bypass internal optimization/caching.

---

**Q8.48: Basic - [Pass in Class]**

`class C: pass`. Does `C` have any methods?

A) No, it's empty.
B) Yes, it inherits methods from `object` (like `__str__`, `__init__` default).
C) Yes, only `__init__`.
D) Error.

**Answer: B**

**Explanation:**
All new-style classes inherit from `object`, so they get default implementations of basic magic methods.

---

**Q8.49: Intermediate - [Class vs Static Method 2]**

Which method type is suitable for a factory method returning a new instance?

A) `@staticmethod`
B) `@classmethod`
C) Instance method.
D) `@property`

**Answer: B**

**Explanation:**
`@classmethod` receives the class (`cls`), allowing it to instantiate the correct class (even for subclasses), making it ideal for factories (e.g., `dict.fromkeys`).

---

**Q8.50: Advanced - [MRO check]**

How do you programmatically check the MRO of a class `C`?

A) `C.mro` attribute.
B) `C.mro()` method or `C.__mro__` attribute.
C) `help(C)`.
D) `sys.getmro(C)`.

**Answer: B**

**Explanation:**
`C.mro()` method returns the MRO list. `.__mro__` is the tuple version stored on the class.

---

**Q8.51: Expert - [__init_subclass__]**

Introduced in 3.6, `__init_subclass__` allows:

A) A parent class to customize the creation of its subclasses (alternative to metaclasses).
B) A subclass to initialize its parent.
C) Initializing the subclass instance.
D) Copying subclasses.

**Answer: A**

**Explanation:**
It is a hook method on the base class that is called whenever a new subclass is defined. It simplifies many use cases that previously required metaclasses.

---

**Q8.52: Intermediate - [Str/Repr choice]**

If you type an object name in the REPL (interactive shell), which representation is shown?

A) `__str__`
B) `__repr__`
C) `__view__`
D) `__shell__`

**Answer: B**

**Explanation:**
The REPL uses `repr()` to display the result of expressions for debugging/clarity. `print()` uses `str()`.

---

**Q8.53: Basic - [Method Overloading]**

Does Python support C++ style method overloading (multiple methods same name, different signatures)?

A) Yes.
B) No. The last definition overwrites previous ones.
C) Yes, using `overload` keyword.
D) Only for built-ins.

**Answer: B**

**Explanation:**
Python matches names. Redefining a function with the same name replaces the old object. Tricks with `*args` or `functools.singledispatch` simulate overloading.

---

**Q8.54: Advanced - [__iter__]**

To make an object iterable (usable in `for` loop), it must implement:

A) `__next__`
B) `__iter__`
C) `__loop__`
D) `__list__`

**Answer: B**

**Explanation:**
`__iter__` must return an iterator (an object with `__next__`).

---

**Q8.55: Expert - [Slots and Inheritance]**

If `Base` has `__slots__` and `Sub` inherits from `Base` but does Not define `__slots__`:

A) `Sub` instances have no `__dict__` (inherit slots strictness).
B) `Sub` instances HAVE a `__dict__`.
C) `Sub` raises Error.
D) `Sub` ignores Base slots.

**Answer: B**

**Explanation:**
Slots are not strictly inherited. If the subclass does not specify `__slots__`, it gets a `__dict__` by default, partially negating the memory savings of the parent's slots (though parent attributes are still stored in slots).

---

**Q8.56: Intermediate - [Callable Instance check]**

`callable(obj)` returns True if:

A) `obj` is a function.
B) `obj` is a method.
C) `obj` is a class.
D) All of the above (and instances with `__call__`).

**Answer: D**

**Explanation:**
Any object that implements `__call__` is callable. Classes are callable (to create instances), functions/methods are callable.

---

**Q8.57: Basic - [Equality]**

`__eq__` implements which operator?

A) `=` (Assignment)
B) `==` (Equality)
C) `is` (Identity)
D) `===`

**Answer: B**

**Explanation:**
`__eq__` handles `==`. `__ne__` handles `!=`.

---

**Q8.58: Advanced - [Context Manager]**

To using an object in a `with` statement, it must implement:

A) `__enter__` and `__exit__`.
B) `__open__` and `__close__`.
C) `__start__` and `__stop__`.
D) `__with__` context.

**Answer: A**

**Explanation:**
The Context Manager protocol requires `__enter__` (setup) and `__exit__` (teardown/exception handling).

---

**Q8.59: Expert - [Singleton Pattern]**

Which method is best hooked to implement a Singleton pattern (ensuring only one instance)?

A) `__init__`
B) `__new__`
C) `__call__`
D) `__singleton__`

**Answer: B**

**Explanation:**
`__new__` controls creation. You can check if an instance exists and return the existing one instead of creating a new one. `__init__` is too late (object already created).

---

**Q8.60: Basic - [Inheritance Root]**

The hierarchy `class A: pass` creates A as a subclass of:

A) nothing
B) `object`
C) `type`
D) `class`

**Answer: B**

**Explanation:**
In Python 3, all classes inherit from `object` automatically.

---

---

## Review Notes (2026-02-06)

- Q8.27 explanation includes drafting/self-correction text ("Self-correction") that should be cleaned for production content.
