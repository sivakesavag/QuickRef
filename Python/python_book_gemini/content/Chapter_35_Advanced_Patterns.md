# Chapter 35: Advanced Patterns & Architectures

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: Design Patterns (Singleton, Factory, Observer), Dependency Injection, Clean Architecture, Mixins, Metaclasses (practical), Descriptor Protocol, Context Managers, Coroutines (async), Event Driven Architecture.

---

**Q35.1: Basic - [Singleton]**

The Singleton pattern ensures that:

A) A class has only one instance and provides a global point of access to it.
B) A function returns one value.
C) A list has one item.
D) A thread runs once.

**Answer: A**

**Explanation:**
Often implemented via `__new__` or a decorator, or simply using a module (Pythonic Singleton).

---

**Q35.2: Intermediate - [Borg Pattern]**

The "Borg" pattern (Monostate) differs from Singleton in that:

A) It allows multiple instances to be created, but they all share the same state (same `__dict__`).
B) It destroys instances.
C) It is complex.
D) It uses robots.

**Answer: A**

**Explanation:**
"Identity doesn't matter, state does."

---

**Q35.3: Advanced - [Dependency Injection]**

Dependency Injection (DI) improves code testability by:

A) Passing dependencies (objects a class needs) into the class (e.g., via `__init__`) rather than letting the class instantiate them itself.
B) Using `pip install`.
C) Importing inside functions.
D) Using globals.

**Answer: A**

**Explanation:**
Allows mocking dependencies easily during testing.

---

**Q35.4: Expert - [Metaclass Registration]**

One practical use of Metaclasses is "Auto-Registration", where:

A) The metaclass automatically adds every subclass of a base class to a central registry (e.g., `plugins = {}`) as soon as the class is defined.
B) It deletes classes.
C) It renames classes.
D) It sorts classes.

**Answer: A**

**Explanation:**
Used in frameworks like Django Models and plugin systems.

---

**Q35.5: Basic - [Factory Pattern]**

A Factory Method:

A) Encapsulates object creation logic, allowing subclasses or helper functions to decide which class to obtain.
B) Builds cars.
C) Creates files.
D) Parses strings.

**Answer: A**

**Explanation:**
Decouples client code from concrete classes.

---

**Q35.6: Intermediate - [Context Manager Class]**

To make a class compatible with `with` statement, it must implement:

A) `__enter__` and `__exit__`.
B) `__start__` and `__stop__`.
C) `__open__` and `__close__`.
D) `__init__` only.

**Answer: A**

**Explanation:**
`__enter__` sets up the resource, `__exit__` cleans up (handling exceptions).

---

**Q35.7: Advanced - [Descriptor vs Property]**

A `@property` is actually a specific implementation of the:

A) Descriptor Protocol (using `__get__`, `__set__`, `__delete__` on a class attribute).
B) Decorator factory.
C) Context manager.
D) Generator.

**Answer: A**

**Explanation:**
Properties are data descriptors.

---

**Q35.8: Expert - [Abstract Base Class]**

To enforce that a subclass MUST implement a method `foo`, you should:

A) Inherit from `abc.ABC` and decorate `foo` with `@abc.abstractmethod`.
B) Raise `NotImplementedError` in the base class (runtime check only).
C) Use type hints.
D) Write a comment.

**Answer: A**

**Explanation:**
`ABC` prevents instantiation if abstract methods are missing.

---

**Q35.9: Basic - [Mixin]**

A Mixin is:

A) A class designed to provide specific methods to other classes via multiple inheritance, but not meant to stand alone.
B) A cocktail.
C) A function.
D) A module.

**Answer: A**

**Explanation:**
e.g., `Werkzeug`'s utility mixins.

---

**Q35.10: Intermediate - [Contextlib contextmanager]**

The `@contextlib.contextmanager` decorator turns a generator function into a context manager. The `yield` statement separates:

A) The setup code (before yield) and the teardown code (after yield).
B) Two values.
C) Nothing.
D) Threads.

**Answer: A**

**Explanation:**
`try...finally` around the yield ensures cleanup runs.

---

**Q35.11: Advanced - [Flyweight]**

The Flyweight pattern (e.g., used in `sys.intern` or `bool` instances) saves memory by:

A) Sharing common parts of objects state among multiple objects, instead of keeping unique data in each.
B) Deleting objects.
C) Compressing text.
D) Calculating weight.

**Answer: A**

**Explanation:**
Useful when you have massive numbers of similar objects.

---

**Q35.12: Expert - [Double Checked Locking]**

In Python, the Singleton "Double Checked Locking" pattern for thread safety:

A) Is often unnecessary or tricky. Standard import-time module execution is thread-safe, so a module-level singleton is safer and simpler.
B) Is mandatory.
C) Is fast.
D) Is built-in.

**Answer: A**

**Explanation:**
Python's import lock handles the "one instance" guarantee for modules.

---

**Q35.13: Basic - [Adapter]**

The Adapter pattern:

A) Converts the interface of a class into another interface the client expects (wrapper).
B) Adapts voltage.
C) Copies data.
D) Imports modules.

**Answer: A**

**Explanation:**
"Glue code" to make incompatible interfaces work together.

---

**Q35.14: Intermediate - [Strategy Pattern]**

Passing a function as an argument to another function (e.g., `sort(key=func)`) is a functional implementation of the:

A) Strategy Pattern (swapping algorithms at runtime).
B) Factory Pattern.
C) Singleton.
D) Decorator.

**Answer: A**

**Explanation:**
Python's first-class functions make this pattern trivial.

---

**Q35.15: Advanced - [Observer with Decorators]**

An Observer pattern can be elegantly implemented using:

A) Decorators to register event handlers (e.g., `@app.route` or `@signal.connect`).
B) Loops.
C) Files.
D) Classes only.

**Answer: A**

**Explanation:**
Common in Flask, Django Signals.

---

**Q35.16: Expert - [Slots vs Dict]**

Using `__slots__` is an architectural decision that trades:

A) Dynamic flexibility (cannot add new attributes at runtime) for memory efficiency and faster attribute access.
B) Nothing.
C) Speed for memory.
D) Security for speed.

**Answer: A**

**Explanation:**
It locks down the class structure.

---

**Q35.17: Basic - [Facade]**

The Facade pattern:

A) Provides a simplified interface to a complex subsystem (hiding the complexity).
B) Validates input.
C) Formats output.
D) Connects DB.

**Answer: A**

**Explanation:**
`requests.get` is a facade over complex `urllib3` connection pooling logic.

---

**Q35.18: Intermediate - [Proxy]**

A Proxy object (like `weakref.proxy`):

A) Acts as a stand-in for another object, controlling access to it (lazy loading, access control, weak referencing).
B) Copies it.
C) Deletes it.
D) Prints it.

**Answer: A**

**Explanation:**
Django's `LazyObject` is a proxy.

---

**Q35.19: Advanced - [MRO C3]**

Python 3 uses the C3 Linearization algorithm for MRO to ensure:

A) A consistent, monotonic method resolution order in complex multiple inheritance diamonds.
B) Random order.
C) Alphabetical order.
D) Depth-first search (like old Python).

**Answer: A**

**Explanation:**
Prevents subtle bugs where overriding order is ambiguous.

---

**Q35.20: Expert - [Coroutine Pipelines]**

Using coroutines to build data processing pipelines (Producer -> Filter -> Consumer) allows:

A) Push-based architecture (sending data to the next stage via `.send()`), contrasting with pull-based generators (Requesting via `next()`).
B) Threading.
C) Multiprocessing.
D) Networking.

**Answer: A**

**Explanation:**
A powerful way to structure stream processing.

---

**Q35.21: Basic - [Iterator Pattern]**

Python's `for x in obj` syntax relies on the:

A) Iterator Protocol (`__iter__` and `__next__`).
B) Singleton Protocol.
C) Factory Protocol.
D) List Protocol.

**Answer: A**

**Explanation:**
You don't need a specific "Iterator" class; anything following the protocol works.

---

**Q35.22: Intermediate - [SOLID]**

The "O" in SOLID stands for:

A) Open/Closed Principle: Open for extension, closed for modification.
B) Object Oriented.
C) Optimization.
D) Overloading.

**Answer: A**

**Explanation:**
Use inheritance or composition/strategies to extend behavior without rewriting existing code.

---

**Q35.23: Advanced - [Currying]**

`functools.partial` allows:

A) Fixing a certain number of arguments of a function and generating a new function (Partial Application / Currying concept).
B) Deleting args.
C) Renaming args.
D) Timing function.

**Answer: A**

**Explanation:**
Useful for callbacks requiring specific signatures.

---

**Q35.24: Expert - [Monkey Patching]**

Monkey Patching is:

A) Dynamically modifying a class or module at runtime (e.g., `Class.method = new_method`). Powerful for testing (mocking) but dangerous in production code.
B) A game.
C) A virus.
D) A feature.

**Answer: A**

**Explanation:**
Can lead to "Action at a distance" bugs.

---

**Q35.25: Basic - [DRY]**

DRY stands for:

A) Don't Repeat Yourself.
B) Do Repeat Yourself.
C) Don't Run Yet.
D) Data Recovery.

**Answer: A**

**Explanation:**
Centralize logic to single source of truth.

---

**Q35.26: Intermediate - [Composition vs Inheritance]**

"Favor Composition over Inheritance" means:

A) Build complex objects by combining simpler objects (Has-A relationship) rather than deep class hierarchies (Is-A relationship).
B) Always use inheritance.
C) Never use classes.
D) Use large classes.

**Answer: A**

**Explanation:**
Reduces coupling and fragility.

---

**Q35.27: Advanced - [Chain of Responsibility]**

Middleware in web frameworks (handling request -> auth -> logging -> view) is an example of:

A) Chain of Responsibility pattern.
B) Singleton.
C) Flyweight.
D) Memento.

**Answer: A**

**Explanation:**
Each handler processes and passes to the next.

---

**Q35.28: Expert - [Dataclasses vs NamedTuple]**

`dataclasses` (mutable by default) vs `NamedTuple` (immutable):

A) Use `dataclasses` when you need mutable state or inheritance; use `NamedTuple` for simple immutable data carriers (and slightly less memory).
B) They are identical.
C) NamedTuple is faster.
D) Dataclass is slower.

**Answer: A**

**Explanation:**
Dataclasses are more feature-rich (post-init, etc.).

---

**Q35.29: Intermediate - [Command Pattern]**

Encapsulating a request as an object (e.g., a GUI action with `undo` capability) is the:

A) Command Pattern.
B) Strategy Pattern.
C) Bridge Pattern.
D) State Pattern.

**Answer: A**

**Explanation:**
Allows queuing, logging, or undoing operations.

---

**Q35.30: Basic - [KISS]**

KISS principle:

A) Keep It Simple, Stupid.
B) Keep It Safe, Secure.
C) Keep It Short.
D) Keep It Slow.

**Answer: A**

**Explanation:**
Complexity is the enemy of reliability.

---

**Q35.31: Intermediate - [Template Method]**

The Template Method pattern defines the skeleton of an algorithm in a base class, allowing subclasses to:

A) Override specific steps (methods) of the algorithm without changing its structure.
B) Delete the algorithm.
C) Run faster.
D) Use more memory.

**Answer: A**

**Explanation:**
Common in frameworks (e.g., `TestCase` setup/teardown/run).

---

**Q35.32: Advanced - [Multiple Inheritance Diamonds]**

In Python, the "Diamond Problem" (D inherits from B and C, both inherit from A) is solved by:

A) The C3 Linearization algorithm, which creates a specific order (MRO) where A is successfully called only once (if `super()` is used correctly).
B) Calling A twice.
C) Error.
D) Randomly.

**Answer: A**

**Explanation:**
`super()` is cooperative multiple inheritance.

---

**Q35.33: Basic - [Plugin Architecture]**

A common way to implement a plugin system in Python is using:

A) `importlib` for dynamic importation and searching a specific directory for modules/packages that follow a defined convention.
B) `eval()`.
C) Hardcoding imports.
D) Downloading zip files.

**Answer: A**

**Explanation:**
See `setuptools` entry points as well.

---

**Q35.34: Expert - [Meta-programming]**

Metaprogramming refers to:

A) Code that writes or manipulates code (e.g., Decorators, Metaclasses, AST transformations).
B) Writing comments.
C) Writing tests.
D) Compiling C.

**Answer: A**

**Explanation:**
"Code as data".

---

**Q35.35: Intermediate - [State Pattern]**

The State Pattern allows an object to alter its behavior when its internal state changes, often by:

A) Delegating to a separate "State" object (polymorphism), rather than using giant `if/else` or `switch` statements inside the main object.
B) Changing its class.
C) Deleting itself.
D) Printing status.

**Answer: A**

**Explanation:**
Cleaner than "god classes" with many flags.

---

**Q35.36: Advanced - [Asyncio Queue]**

For communicating between multiple `asyncio` tasks (coroutines), use:

A) `asyncio.Queue` (which is awaitable), NOT the thread-safe `queue.Queue` (which would block the event loop).
B) `queue.Queue`.
C) `list`.
D) `dict`.

**Answer: A**

**Explanation:**
Blocking code kills async performance.

---

**Q35.37: Basic - [Decorator Stacking]**

When multiple decorators are applied:
```python
@dec1
@dec2
def func(): pass
```
It is equivalent to:

A) `func = dec1(dec2(func))` (Bottom-up execution).
B) `func = dec2(dec1(func))`.
C) Parallel execution.
D) Error.

**Answer: A**

**Explanation:**
Wraps from inside out.

---

**Q35.38: Intermediate - [Bridges]**

The Bridge pattern is useful for:

A) Decoupling an abstraction from its implementation so that the two can vary independently (e.g., Database Abstraction Layer vs underlying Drivers).
B) Connecting wires.
C) Sorting lists.
D) Making HTTP requests.

**Answer: A**

**Explanation:**
Avoids Class Explosion.

---

**Q35.39: Advanced - [ContextVar]**

The `contextvars` module provides:

A) Context-local state (storage that is local to an async Task or thread), essential for passing request IDs or user sessions through async code without argument drilling.
B) Global state.
C) Persistent database.
D) File storage.

**Answer: A**

**Explanation:**
The modern replacement for `threading.local`.

---

**Q35.40: Expert - [Descriptor Non-Data]**

A "Non-Data Descriptor" implements:

A) Only `__get__` (e.g., methods, `classmethod`). It can be shadowed by an instance attribute in `__dict__`.
B) `__set__` only.
C) `__delete__` only.
D) All three.

**Answer: A**

**Explanation:**
Data descriptors (with `__set__`) take precedence over instance dict.

---

**Q35.41: Basic - [Separation of Concerns]**

"Separation of Concerns" suggests:

A) Different sections of code should handle different responsibilities (e.g., HTML rendering separate from SQL queries).
B) Mixing everything.
C) Using one file.
D) Using no classes.

**Answer: A**

**Explanation:**
Modular code is maintainable code.

---

**Q35.42: Intermediate - [Fluent Interface]**

A Fluent Interface (Method Chaining) allows:

A) `obj.method1().method2().method3()` (by returning `self` at the end of each method).
B) Faster execution.
C) Less memory.
D) Better security.

**Answer: A**

**Explanation:**
Common in ORMs (`query.filter().order_by().all()`).

---

**Q35.43: Advanced - [Null Object Pattern]**

The Null Object pattern involves:

A) Returning a "do nothing" object (that mimics the interface) instead of `None`, removing the need for `if obj is not None:` checks everywhere.
B) Returning None.
C) Raising Error.
D) Returning False.

**Answer: A**

**Explanation:**
Reduces null pointer exceptions.

---

**Q35.44: Expert - [Protocol (Static Duck Typing)]**

`typing.Protocol` (PEP 544) allows:

A) Structural subtyping: "If it walks like a duck..." explicitly defined for static type checkers. A class satisfies the Protocol if it has the methods, without inheriting from it.
B) Nominal subtyping only.
C) Runtime checking.
D) Dynamic typing.

**Answer: A**

**Explanation:**
Brings Go/TypeScript style interfaces to Python hints.

---

**Q35.45: Intermediate - [Memoization Pattern]**

Memoization is a specific form of Caching that:

A) Caches the return value of a function based *solely* on its input arguments (for pure functions).
B) Caches to disk.
C) Caches to DB.
D) Uses RAM.

**Answer: A**

**Explanation:**
`@lru_cache` is the standard implementation.

---

**Q35.46: Basic - [YAGNI]**

YAGNI stands for:

A) You Aint Gonna Need It (Don't implement features until they are actually required).
B) You Are Good Now.
C) Yet Another Game.
D) Yield And Go.

**Answer: A**

**Explanation:**
Anti-gold-plating.

---

**Q35.47: Advanced - [Middleware]**

In WSGI/ASGI apps, Middleware wraps the application to:

A) Intercept/transform the request before it reaches code, and/or transform the response afterwards (e.g., GZip, CORS, Logging).
B) Host the app.
C) Store data.
D) Route URLs.

**Answer: A**

**Explanation:**
The "Onion" architecture.

---

**Q35.48: Expert - [Event Sourcing]**

Event Sourcing architecture stores:

A) A sequence of state-changing events (transactions) rather than just the current state. The current state is derived by replaying events.
B) Just the current state.
C) Logs only.
D) Backups.

**Answer: A**

**Explanation:**
Great for audit trails and complex temporal querying.

---

**Q35.49: Intermediate - [Builder Pattern]**

The Builder pattern is useful when:

A) Constructing a complex object requires many steps or configurations, which are better managed by a dedicated builder class than a giant logic-filled `__init__`.
B) Building strings.
C) Building lists.
D) Building dicts.

**Answer: A**

**Explanation:**
Decouples construction from representation.

---

**Q35.50: Basic - [Magic Numbers]**

Using "Magic Numbers" (e.g., `if status == 42`) is an anti-pattern. You should:

A) Replace them with named constants (e.g., `STATUS_COMPLETED = 42`).
B) Keep them.
C) Use strings.
D) Use floats.

**Answer: A**

**Explanation:**
Improves readability and maintainability.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
