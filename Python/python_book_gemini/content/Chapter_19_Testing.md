# Chapter 19: Testing & Debugging

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `unittest` framework (TestCase, assertions, setup/teardown), `pytest` basics (fixtures, markers, parametrization), `mock`/`unittest.mock` (Mock, MagicMock, patch), `doctest`, Debugging (`pdb`, breakpoints).

---

**Q19.1: Basic - [Unittest Module]**

The standard library module for creating unit tests in Python is:

A) `test`
B) `pytests`
C) `unittest`
D) `testing`

**Answer: C**

**Explanation:**
`unittest` is the built-in XUnit style framework inspired by JUnit.

---

**Q19.2: Intermediate - [AssertEqual]**

In `unittest.TestCase`, to check if `a` equals `b`, you generally use:

A) `assert a == b`
B) `self.assertEqual(a, b)`
C) `self.check(a == b)`
D) `expect(a).toBe(b)`

**Answer: B**

**Explanation:**
`assertEqual` provides a better error message (showing the diff) if the assertion fails, compared to a bare `assert`.

---

**Q19.3: Advanced - [Mock Patch]**

`@patch('module.Class')` serves to:

A) Permanently modify the class code.
B) Temporarily replace `module.Class` with a Mock object during the test scope.
C) Import the class.
D) Debug the class.

**Answer: B**

**Explanation:**
It intercepts import/lookup logic to swap in a mock, allowing simulation of behavior without external dependencies (like DB/Network).

---

**Q19.4: Basic - [Pytest Run]**

To run tests using `pytest`, you typically execute which command in the terminal?

A) `python test.py`
B) `pytest`
C) `run tests`
D) `python -m testing`

**Answer: B**

**Explanation:**
`pytest` is the command-line entry point to discover and run tests.

---

**Q19.5: Intermediate - [Setup Method]**

In `unittest.TestCase`, the method `setUp(self)` is called:

A) Once for the whole class.
B) Before every test method.
C) After every test method.
D) Only if a test fails.

**Answer: B**

**Explanation:**
Used to prepare the test fixture (state) before each individual test ensures isolation.

---

**Q19.6: Advanced - [Doctest]**

How does `doctest` find tests?

A) It looks for methods starting with `test_`.
B) It executes interactive python sessions (REPL examples) embedded in docstrings.
C) It reads a JSON file.
D) It parses comments.

**Answer: B**

**Explanation:**
It verifies that code formatting like `>>> call()` and its output matches the actual execution.

---

**Q19.7: Basic - [PDB Breakpoint]**

To set a breakpoint in your code for the Python Debugger (modern Python 3.7+):

A) `import pdb; pdb.set_trace()`
B) `breakpoint()`
C) `debug()`
D) `stop()`

**Answer: B**

**Explanation:**
`breakpoint()` is a built-in convenience function that calls `sys.breakpointhook` (defaulting to `pdb.set_trace()`).

---

**Q19.8: Intermediate - [Pytest Fixture]**

A function decorated with `@pytest.fixture`:

A) Is a test function.
B) Provides input data or objects to test functions via dependency injection (arguments).
C) Is skipped.
D) Is run last.

**Answer: B**

**Explanation:**
Fixtures allow modular setup code. If a test argument matches a fixture name, pytest calls the fixture and passes the result.

---

**Q19.9: Advanced - [Mock Return Value]**

To make a mock return `10` when called:

A) `m = Mock(return_value=10)`
B) `m = Mock(returns=10)`
C) `m.set(10)`
D) `m = 10`

**Answer: A**

**Explanation:**
`return_value` configuration instructs the mock what to return when invoked as a function.

---

**Q19.10: Expert - [Side Effect]**

Use `side_effect` on a Mock when you want to:

A) Raise an exception.
B) Return different values on consecutive calls (using an iterable).
C) Execute a dynamic function on call.
D) All of the above.

**Answer: D**

**Explanation:**
`side_effect` is powerful: it can take an exception object (to raise), a list (sequence of returns), or a callable (dynamic logic).

---

**Q19.11: Basic - [Test Discovery]**

By default, `unittest` (and pytest) discovers files matching:

A) `test*.py` or `*test.py`.
B) `*.txt`.
C) `all.py`.
D) `main.py`.

**Answer: A**

**Explanation:**
Standard naming convention for test discovery.

---

**Q19.12: Intermediate - [Assert Raises]**

In `unittest`, `with self.assertRaises(ValueError):` is used to:

A) Raise a ValueError manually.
B) Verify that the code block inside the `with` statement raises `ValueError`.
C) Catch and ignore all errors.
D) Print an error.

**Answer: B**

**Explanation:**
The test passes validly only if the specific exception *is* raised. If no exception occurs, the test fails.

---

**Q19.13: Advanced - [MagicMock vs Mock]**

`MagicMock` differs from `Mock` because:

A) It works by magic.
B) It has default implementations for most magic methods (like `__len__`, `__str__`, `__getitem__`).
C) It is deprecated.
D) It is faster.

**Answer: B**

**Explanation:**
Useful when you need to mock objects that act like containers or support operators without configuring every dunder method manually.

---

**Q19.14: Basic - [TDD Definition]**

TDD stands for:

A) Type Driven Development.
B) Test Driven Development.
C) Test Debug Deploy.
D) Technical Design Do.

**Answer: B**

**Explanation:**
Cycle: Write failing test -> Write minimal code to pass -> Refactor.

---

**Q19.15: Intermediate - [Pytest Mark]**

`@pytest.mark.skip(reason=...)`:

A) Fails the test.
B) Skips the test execution.
C) Marks it as expected failure.
D) Highlight it.

**Answer: B**

**Explanation:**
Used to disable tests conditionally or permanently.

---

**Q19.16: Advanced - [Teardown]**

The `tearDown()` method is guaranteed to run:

A) Immediately after `setUp`.
B) After the test method finishes, even if the test raised an exception.
C) Only if test passes.
D) Before the test.

**Answer: B**

**Explanation:**
Critical for cleanup (closing files, DB connections) regardless of test outcome.

---

**Q19.17: Expert - [Pytest Conftest]**

`conftest.py` file in pytest is used for:

A) Configuration tests.
B) Defining global/shared fixtures and hooks available to multiple test files without imports.
C) Confusing tests.
D) Connecting to internet.

**Answer: B**

**Explanation:**
Pytest automatically discovers fixtures in `conftest.py` in the directory hierarchy.

---

**Q19.18: Intermediate - [PDB Next vs Step]**

In `pdb`, `n` (next) vs `s` (step):

A) `n` step over function calls; `s` steps into function calls.
B) `n` steps into; `s` steps over.
C) They are same.
D) `n` creates a new line.

**Answer: A**

**Explanation:**
`next` executes the current line effectively treating function calls as atomic. `step` enters the called function scope.

---

**Q19.19: Basic - [Skipping Unittest]**

In `unittest`, to skip a test:

A) `@unittest.skip("reason")`
B) `return`
C) `pass`
D) `break`

**Answer: A**

**Explanation:**
Decorator to indicate the test should be skipped.

---

**Q19.20: Advanced - [Mock Spec]**

`Mock(spec=MyClass)` ensures:

A) The mock is an instance of MyClass.
B) The mock only allows attribute access/calls that exist on `MyClass` (raising AttributeError for others).
C) It copies the class code.
D) It mocks nothing.

**Answer: B**

**Explanation:**
"Autospeccing" prevents tests from calling non-existent methods on the mock, keeping mocks consistent with the real API.

---

**Q19.21: Expert - [Parametrize]**

`@pytest.mark.parametrize("input,expected", [(1,2), (3,4)])` creates:

A) One test with multiple assert statements.
B) Two separate test cases (runs) from the same function definition.
C) A list of tuples.
D) An error.

**Answer: B**

**Explanation:**
It generates distinct test invocations, so one failure doesn't block the others, and they appear as separate items in the report.

---

**Q19.22: Intermediate - [Assert True]**

`self.assertTrue(x)` fails if:

A) `x` is `True`.
B) `x` is `False` (or falsy).
C) `x` is `None`.
D) `x` is 1.

**Answer: B**

**Explanation:**
Asserts that the expression evaluates to True.

---

**Q19.23: Basic - [Code Coverage]**

"Code Coverage" measures:

A) How fast the code runs.
B) What percentage of code lines (or branches) were executed during the test run.
C) Size of the code.
D) Number of tests.

**Answer: B**

**Explanation:**
Metric to determine which parts of the application are not exercised by the test suite.

---

**Q19.24: Advanced - [Subtests]**

`with self.subTest(i=i):` in `unittest` allows:

A) Nesting tests.
B) Iterating inside one test method where failures don't stop the loop; typically reports multiple failures for one method.
C) Creating subprocesses.
D) Submitting tests.

**Answer: B**

**Explanation:**
Useful for data-driven tests inside `unittest` without stopping at the first failure.

---

**Q19.25: Intermediate - [Mock Assert Called]**

`mock_obj.assert_called_with(1, 2)`:

A) Calls the mock with 1, 2.
B) Asserts that the *last* call to the mock had arguments (1, 2).
C) Asserts that the mock was called at least once with (1, 2) anywhere in history.
D) Returns True/False.

**Answer: B**

**Explanation:**
Verifies the argument of the most recent call. Use `assert_any_call` for history search.

---

**Q19.26: Expert - [Fixture Scope]**

`@pytest.fixture(scope="session")`:

A) The fixture is re-created for every test function.
B) The fixture is created once per test session (run) and shared across all tests.
C) The fixture is created per class.
D) The fixture is global.

**Answer: B**

**Explanation:**
Useful for expensive setup like "Start Database Container" that should happen only once.

---

**Q19.27: Basic - [Mock Library Location]**

Since Python 3.3, `mock` is available at:

A) `import mock`
B) `unittest.mock`
C) `pytest.mock`
D) `sys.mock`

**Answer: B**

**Explanation:**
Merged into the standard library.

---

**Q19.28: Advanced - [PDB Continue]**

In `pdb`, command `c` (continue):

A) Steps one line.
B) Resumes execution until the next breakpoint or program end.
C) Crashes.
D) Clears breakpoints.

**Answer: B**

**Explanation:**
Stops stepping and runs freely.

---

**Q19.29: Intermediate - [Pytest Raises]**

`with pytest.raises(ValueError):` is the pytest equivalent of:

A) `unittest.TestCase.assertRaises`
B) `try...except`
C) `assert False`
D) `capture_error`

**Answer: A**

**Explanation:**
Context manager to verify exceptions.

---

**Q19.30: Expert - [Patch Object]**

`patch.object(TargetClass, 'method_name')`:

A) Patches `method_name` on instances of `TargetClass` (binds to the class).
B) Patches a string.
C) Patches the object instance only.
D) Is invalid.

**Answer: A**

**Explanation:**
Often safer than `patch('path.to.module.Class.method')` because it resolves the name reference directly, avoiding typo issues with import paths.

---

**Q19.31: Intermediate - [Pytest Markers CLI]**

To run only tests marked with `@pytest.mark.slow`:

A) `pytest -k slow`
B) `pytest -m slow`
C) `pytest --slow`
D) `pytest run slow`

**Answer: B**

**Explanation:**
`-m` selects tests based on markers. `-k` selects based on name substrings.

---

**Q19.32: Advanced - [Mock Side Effect Exception]**

`mock.side_effect = ValueError("Boom")`. Calling the mock will:

A) Return "Boom".
B) Raise `ValueError`.
C) Return the exception object as a value.
D) Print "Boom".

**Answer: B**

**Explanation:**
If `side_effect` is an exception class or instance, calling the mock raises it.

---

**Q19.33: Basic - [Docstring Format]**

For `doctest` to recognize a test, the line must start with:

A) `>>`
B) `>>>` (including a space usually).
C) `$`
D) `#`

**Answer: B**

**Explanation:**
Mimics the standard Python interactive shell prompt.

---

**Q19.34: Expert - [Mocking Properties]**

To mock a property `@property` on a class:

A) `patch('Class.prop', new_callable=PropertyMock)`
B) `patch('Class.prop', return_value=...)`
C) `Mock(prop=...)`
D) It is impossible.

**Answer: A**

**Explanation:**
Standard Mocks are callables, but properties are not called. `PropertyMock` allows assertions on attribute access.

---

**Q19.35: Intermediate - [Pytest Autouse]**

`@pytest.fixture(autouse=True)` means:

A) The fixture is automatically run/requested for every test in its scope (no need to name it in arguments).
B) It is used automatically by the OS.
C) It auto-corrects code.
D) It is deprecated.

**Answer: A**

**Explanation:**
Useful for setup that must happen universally (e.g., clearing DB before each test) without cluttering every test signature.

---

**Q19.36: Advanced - [Unittest Discover]**

Command `python -m unittest discover -s tests -p "*_test.py"`:

A) Runs tests in `tests` folder matching the pattern.
B) Discovers files but doesn't run them.
C) Installs tests.
D) Fails.

**Answer: A**

**Explanation:**
`-s` sets start directory, `-p` sets pattern.

---

**Q19.37: Basic - [Assert In]**

To check if a value exists in a list:

A) `assert x in list`
B) `self.assertIn(x, list)`
C) `self.assertContains(list, x)`
D) `list.contains(x)`

**Answer: B**

**Explanation:**
`assertIn` checks membership and prints a helpful message if missing.

---

**Q19.38: Intermediate - [Mock Call Count]**

To verify a mock was called exactly once:

A) `mock.assert_called_once()`
B) `mock.assert_called()`
C) `if mock.count == 1: pass`
D) `mock.called_once`

**Answer: A**

**Explanation:**
Helper assertion. Also `mock.call_count == 1`.

---

**Q19.39: Advanced - [Pytest Approx]**

To compare floating point numbers in pytest:

A) `assert a == b`
B) `assert a == pytest.approx(b)`
C) `assert round(a) == round(b)`
D) `self.assertAlmostEqual(a, b)`

**Answer: B**

**Explanation:**
Handy for avoiding float precision issues (e.g. 0.1 + 0.2 != 0.3).

---

**Q19.40: Expert - [Patch Context Manager]**

When using `with patch(...) as mock:`:

A) The patch is active only inside the `with` block.
B) The patch is active forever.
C) The patch applies to the whole file.
D) The variable `mock` is the original object.

**Answer: A**

**Explanation:**
Ensures proper cleanup (unpatching) when exiting the block, even if errors occur.

---

**Q19.41: Intermediate - [SkipIf]**

`@unittest.skipIf(sys.platform.startswith("win"), "Not on Windows")`:

A) Skips the test if run on Windows.
B) Skips if NOT on Windows.
C) Fails on Windows.
D) Runs only on Windows.

**Answer: A**

**Explanation:**
Conditional skipping based on runtime environment.

---

**Q19.42: Basic - [Test Runner]**

The component that executes tests and provides output to the user is called:

A) Test Runner.
B) Test Case.
C) Test Suite.
D) Test Fixture.

**Answer: A**

**Explanation:**
Orchestrates the execution and result aggregation.

---

**Q19.43: Advanced - [Mock Reset]**

`mock.reset_mock()`:

A) Resets call history (stats) and child mocks.
B) Resets return_value configuration.
C) Resets side_effect.
D) Deletes the mock.

**Answer: A**

**Explanation:**
Useful if you reuse the same mock object across multiple assertions or phases within a test. Note it does *not* clear configuration (return_value/side_effect), only interaction history.

---

**Q19.44: Expert - [Setup Class]**

`setUpClass` must be decorated with:

A) `@classmethod`
B) `@staticmethod`
C) `@property`
D) No decorator.

**Answer: A**

**Explanation:**
It is called on the class, not an instance.

---

**Q19.45: Intermediate - [PDB List]**

In `pdb`, command `l` (list):

A) Lists variables.
B) Shows 11 lines of source code around the current line.
C) Lists breakpoints.
D) Lists threads.

**Answer: B**

**Explanation:**
Provides context for where you are in the code.

---

**Q19.46: Basic - [AssertionError]**

If an `assert` statement fails, Python raises:

A) `TestError`
B) `AssertionError`
C) `ValueError`
D) `False`

**Answer: B**

**Explanation:**
The standard exception for assertion failures.

---

**Q19.47: Advanced - [Pytest Yield Fixture]**

A fixture that uses `yield` instead of `return`:

A) Is a generator.
B) Can run teardown code after the `yield` statement.
C) Is invalid.
D) Is asynchronous.

**Answer: B**

**Explanation:**
Code before `yield` is setup; code after `yield` is teardown.

---

**Q19.48: Expert - [Mock Any]**

`mock.assert_called_with(mock.ANY, "foo")`:

A) Fails.
B) Passes if the second arg was "foo", regardless of the first arg.
C) Passes only if first arg was None.
D) Errors.

**Answer: B**

**Explanation:**
`ANY` is a helper object that compares equal to everything, useful for ignoring specific arguments in assertions.

---

**Q19.49: Intermediate - [Load Tests Protocol]**

The `load_tests` function in a module allows:

A) Customizing test discovery for that module.
B) Loading data.
C) Skipping imports.
D) Speeding up tests.

**Answer: A**

**Explanation:**
Supported by `unittest` to return a specific TestSuite.

---

**Q19.50: Basic - [Integration Test]**

Unlike unit tests, integration tests:

A) Test individual components in isolation.
B) Test how multiple components work together.
C) Are manual.
D) Are deprecated.

**Answer: B**

**Explanation:**
Verifies interfaces and interactions between modules.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
