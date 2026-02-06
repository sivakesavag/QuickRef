# Glossary of Python Terms

## A
*   **ABC (Abstract Base Class)**: A class that cannot be instantiated and is used to define a common interface for its subclasses.
*   **Asyncio**: A library to write concurrent code using the `async`/`await` syntax.

## B
*   **Borg Pattern**: A design pattern where instances share state (`__dict__`) but have distinct identities.
*   **Bytecode**: The intermediate representation of Python code (stored in `.pyc` files) executed by the CPython virtual machine.

## C
*   **Context Manager**: An object that defines `__enter__` and `__exit__` methods, used with the `with` statement.
*   **Coroutine**: A specialized generator function that can suspend its execution and allow other tasks to run.
*   **CPython**: The reference implementation of the Python programming language, written in C.
*   **Currying**: The technique of translating a function that takes multiple arguments into a sequence of functions that each take a single argument.

## D
*   **Decorator**: A function that takes another function and extends the behavior of the latter function without explicitly modifying it.
*   **Dependency Injection**: A technique where an object receives other objects that it depends on.
*   **Descriptor**: An object attribute with binding behavior, one whose attribute access has been overridden by methods in the descriptor protocol (`__get__`, `__set__`, and `__delete__`).
*   **Dunder (Double Underscore)**: Special methods/attributes that start and end with double underscores (e.g., `__init__`).

## G
*   **GIL (Global Interpreter Lock)**: A mutex that protects access to Python objects, preventing multiple native threads from executing Python bytecodes at once.
*   **Generator**: A function that returns an iterator. It looks like a normal function except that it contains `yield` statements for producing a series of values usable in a for-loop or that can be retrieved one at a time with the `next()` function.

## M
*   **Metaclass**: The class of a class. Class definitions create a class name, a class dictionary, and a list of base classes. The metaclass is responsible for taking those three arguments and creating the class.
*   **Mixin**: A class that contains methods for use by other classes without having to be the parent class of those other classes.
*   **MRO (Method Resolution Order)**: The order in which base classes are searched for a member during lookup.

## R
*   **Refcount (Reference Counting)**: The principal memory management technique used in CPython.
*   **REPL**: Read-Eval-Print Loop, the interactive Python shell.

## S
*   **Singleton**: A design pattern that restricts the instantiation of a class to one "single" instance.
*   **SOLID**: An acronym for five design principles intended to make software designs more understandable, flexible, and maintainable.
*   **Synchronous**: Executing tasks sequentially, blocking until completion.

## W
*   **WSGI (Web Server Gateway Interface)**: A standard interface between web server software and web applications written in Python.

## Z
*   **Zen of Python**: A collection of 19 "guiding principles" for writing computer programs that influence the design of the Python programming language.
