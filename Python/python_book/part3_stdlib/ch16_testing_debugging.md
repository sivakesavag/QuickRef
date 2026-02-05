# Chapter 16: Testing & Debugging

> **Topics Covered**: unittest, pytest, test fixtures, mocks, assertions, coverage, doctest, debugging with pdb, logging levels, breakpoints, test patterns, TDD basics

---

## Questions

---

**Q16.1: Basic - [Why Testing]**

Why write automated tests?

A) To slow down development
B) To catch bugs early, enable safe refactoring, document expected behavior
C) It's required by Python
D) To increase code size

**Answer: B**

**Explanation:**
Tests: catch regressions, enable confident refactoring, serve as documentation, verify edge cases. Initial investment saves debugging time later. "Code without tests is broken by design."

---

**Q16.2: Basic - [unittest Basics]**

What is the output if test passes?
```python
import unittest

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(1 + 1, 2)

if __name__ == '__main__':
    unittest.main()
```

A) Error
B) `.` (dot indicating success)
C) `True`
D) Nothing

**Answer: B**

**Explanation:**
unittest prints `.` for each passing test, `F` for failure, `E` for error. Final summary shows counts. Test methods must start with `test_`. Test class inherits from `TestCase`.

---

**Q16.3: Basic - [Assertion Methods]**

What does `self.assertRaises(ValueError, func, arg)` do?

A) Raises ValueError
B) Verifies that func(arg) raises ValueError
C) Catches ValueError silently
D) Returns True if error

**Answer: B**

**Explanation:**
Asserts that calling `func(arg)` raises `ValueError`. Test fails if no exception or wrong exception. Alternative: `with self.assertRaises(ValueError): func(arg)`. Common for testing error conditions.

---

**Q16.4: Intermediate - [Common Assertions]**

Match assertion to purpose: `assertEqual`, `assertTrue`, `assertIn`, `assertIsNone`

A) All same
B) assertEqual = values equal; assertTrue = bool; assertIn = membership; assertIsNone = None check
C) Random checks
D) Only assertEqual works

**Answer: B**

**Explanation:**
`assertEqual(a, b)` — a == b. `assertTrue(x)` — x is truthy. `assertIn(a, b)` — a in b. `assertIsNone(x)` — x is None. Use specific assertions for better error messages.

---

**Q16.5: Intermediate - [setUp and tearDown]**

What are `setUp()` and `tearDown()` in unittest?

A) Install/uninstall
B) Methods run before/after EACH test method
C) Class initialization
D) One-time setup

**Answer: B**

**Explanation:**
`setUp()` runs before each test (create fresh state). `tearDown()` runs after each (cleanup). `setUpClass()`/`tearDownClass()` run once for entire class. Ensures test isolation.

---

**Q16.6: Intermediate - [pytest Basics]**

What's the advantage of pytest over unittest?

A) No advantages
B) Simpler syntax (plain assert), better output, useful fixtures, plugins
C) Faster
D) Built-in

**Answer: B**

**Explanation:**
pytest: use plain `assert` (no `self.assertEqual`). Better failure messages. Powerful fixtures with `@pytest.fixture`. Rich plugin ecosystem. Runs unittest tests too. Industry standard.

---

**Q16.7: Intermediate - [pytest Simple Test]**

What is the output if test passes?
```python
# test_example.py
def test_add():
    assert 1 + 1 == 2
```
Run with: `pytest test_example.py`

A) Error — no TestCase
B) One dot and "1 passed"
C) True
D) Nothing

**Answer: B**

**Explanation:**
pytest discovers functions starting with `test_`. No class needed. Plain `assert` statements work. Output: `.` per test, summary. Much simpler than unittest syntax.

---

**Q16.8: Intermediate - [pytest assert Messages]**

What happens when this fails?
```python
def test_list():
    result = [1, 2, 3]
    assert result == [1, 2, 4]
```

A) Just "AssertionError"
B) Detailed diff showing which element differs
C) No output
D) Crashes

**Answer: B**

**Explanation:**
pytest provides "assertion introspection" — shows values, diffs for lists/dicts. Output: `E assert [1, 2, 3] == [1, 2, 4]` with highlighted difference. Much better than unittest's basic message.

---

**Q16.9: Intermediate - [pytest Fixtures]**

What is the output?
```python
import pytest

@pytest.fixture
def sample_data():
    return [1, 2, 3]

def test_length(sample_data):
    assert len(sample_data) == 3
```

A) Error — undefined
B) Passes — fixture injected as argument
C) None
D) Empty list

**Answer: B**

**Explanation:**
Fixtures provide test dependencies. Function parameter name matches fixture name → pytest injects return value. Fixtures can have setup/teardown (use yield). More flexible than setUp/tearDown.

---

**Q16.10: Intermediate - [pytest Fixture Scope]**

What does `@pytest.fixture(scope="module")` mean?

A) Fixture is imported
B) Fixture runs once per module (file), not per test
C) Fixture is global
D) No caching

**Answer: B**

**Explanation:**
Scopes: `function` (default — each test), `class`, `module` (file), `session` (entire run). Module scope = expensive setup done once per file. Session = once for all tests.

---

**Q16.11: Intermediate - [pytest.mark.parametrize]**

What is the output?
```python
import pytest

@pytest.mark.parametrize("input,expected", [
    (1, 2), (2, 4), (3, 6)
])
def test_double(input, expected):
    assert input * 2 == expected
```

A) 1 test
B) 3 tests (one per parameter set)
C) Error
D) 6 tests

**Answer: B**

**Explanation:**
`parametrize` runs test multiple times with different inputs. Here: 3 test runs. Output shows each as separate test. Cleaner than copy-pasting tests. DRY principle for testing.

---

**Q16.12: Intermediate - [pytest.raises]**

What is the output?
```python
import pytest

def test_error():
    with pytest.raises(ValueError) as exc:
        int("abc")
    assert "invalid literal" in str(exc.value)
```

A) Fails
B) Passes — ValueError caught and message verified
C) Error
D) Crashes

**Answer: B**

**Explanation:**
`pytest.raises` context manager catches expected exception. `exc.value` is the exception instance. Can verify exception message/attributes. More Pythonic than assertRaises.

---

**Q16.13: Intermediate - [unittest.mock Basics]**

What does mocking do in testing?

A) Makes fun of code
B) Replaces dependencies with controlled fake objects
C) Speeds up tests
D) Compiles code

**Answer: B**

**Explanation:**
Mocks replace real dependencies (databases, APIs, files) with fake objects. Control return values, verify calls. `unittest.mock.Mock()`, `patch()`. Essential for unit testing in isolation.

---

**Q16.14: Intermediate - [Using patch]**

What does this do?
```python
from unittest.mock import patch

@patch('mymodule.external_api')
def test_function(mock_api):
    mock_api.return_value = "fake response"
    # test code using mymodule.external_api
```

A) Runs external API
B) Replaces external_api with mock during test
C) Deletes the function
D) Nothing

**Answer: B**

**Explanation:**
`@patch` replaces named object with Mock for test duration. Original restored after. `mock_api.return_value` controls what mock returns. Isolates test from real external dependency.

---

**Q16.15: Intermediate - [Mock Verification]**

What is the output?
```python
from unittest.mock import Mock

api = Mock()
api.fetch_data("user1")
api.fetch_data.assert_called_once_with("user1")
print("OK" if True else "FAIL")
```

A) AssertionError
B) `OK`
C) Error
D) Nothing

**Answer: B**

**Explanation:**
`assert_called_once_with(args)` verifies mock was called exactly once with those arguments. Passes here. Also: `assert_called()`, `assert_not_called()`, `call_count`, `call_args_list`.

---

**Q16.16: Intermediate - [MagicMock]**

What's the difference between Mock and MagicMock?

A) No difference
B) MagicMock includes magic methods (__str__, __len__, etc.) pre-configured
C) MagicMock is faster
D) Mock is deprecated

**Answer: B**

**Explanation:**
`MagicMock` is Mock subclass with magic methods. `len(MagicMock())` works (returns MagicMock). Use MagicMock when code uses magic methods on the mock. Usually prefer MagicMock for flexibility.

---

**Q16.17: Intermediate - [Coverage Basics]**

What does test coverage measure?

A) Number of tests
B) Percentage of code lines/branches executed by tests
C) Test speed
D) Documentation

**Answer: B**

**Explanation:**
`coverage run -m pytest` then `coverage report`. Shows which lines executed. 100% line coverage doesn't mean bug-free (edge cases, branch coverage). Aim for high coverage on critical code.

---

**Q16.18: Intermediate - [doctest]**

What is the output?
```python
def add(a, b):
    """Add two numbers.
    
    >>> add(1, 2)
    3
    >>> add(-1, 1)
    0
    """
    return a + b

if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

A) Error
B) Nothing if tests pass (or verbose output with -v)
C) 3, 0
D) Docstring only

**Answer: B**

**Explanation:**
doctest extracts `>>>` examples from docstrings and verifies output matches. Silent on success, reports failures. Good for testing documentation accuracy. Run: `python -m doctest file.py -v`.

---

**Q16.19: Intermediate - [Test Organization]**

What's the standard test file/directory layout?

A) Any location
B) `tests/` directory with `test_*.py` files mirroring source structure
C) Same file as source
D) Must be in `__tests__`

**Answer: B**

**Explanation:**
Convention: `tests/` at project root. Files: `test_module.py` for `module.py`. pytest discovers `test_*.py` or `*_test.py`. Keep tests separate from source but organized similarly.

---

**Q16.20: Basic - [pdb Debugger]**

How do you start the Python debugger?

A) `debug start`
B) `import pdb; pdb.set_trace()` or just `breakpoint()` (Python 3.7+)
C) `python -debug`
D) Click Debug button

**Answer: B**

**Explanation:**
`breakpoint()` is the modern way — drops into pdb at that line. Interactive commands: `n` (next), `s` (step into), `c` (continue), `p var` (print), `l` (list code). Essential for debugging.

---

**Q16.21: Intermediate - [pdb Commands]**

What does `n` vs `s` do in pdb?

A) Same thing
B) `n` = next line (step over); `s` = step into function calls
C) `n` = next file; `s` = stop
D) Navigation keys

**Answer: B**

**Explanation:**
`n` executes line, stops at next line (doesn't enter functions). `s` steps INTO function calls. `c` continues until next breakpoint. `r` runs until current function returns. Core debugging commands.

---

**Q16.22: Intermediate - [logging Module]**

What is the output?
```python
import logging
logging.basicConfig(level=logging.INFO)

logging.debug("Debug message")
logging.info("Info message")
logging.warning("Warning message")
```

A) All three messages
B) Info and Warning only (debug filtered out)
C) Warning only
D) Nothing

**Answer: B**

**Explanation:**
Level hierarchy: DEBUG < INFO < WARNING < ERROR < CRITICAL. Level=INFO filters out DEBUG. Only INFO and above shown. Use DEBUG for detailed tracing, INFO for normal operation, WARNING for issues.

---

**Q16.23: Intermediate - [logging Levels]**

Which logging level is appropriate for "normal operation status"?

A) DEBUG
B) INFO
C) WARNING
D) ERROR

**Answer: B**

**Explanation:**
DEBUG: detailed diagnostic. INFO: normal operation events. WARNING: something unexpected but handled. ERROR: failure to perform function. CRITICAL: serious error, program may crash.

---

**Q16.24: Intermediate - [logging Formatting]**

What does this output?
```python
import logging
logging.basicConfig(
    format='%(asctime)s %(levelname)s: %(message)s',
    level=logging.INFO
)
logging.info("Test")
```

A) Just "Test"
B) Timestamp, level, and message
C) Error
D) Nothing

**Answer: B**

**Explanation:**
Format string customizes log output. `%(asctime)s` = time, `%(levelname)s` = INFO/WARNING/etc, `%(message)s` = actual message. Also: `%(name)s`, `%(filename)s`, `%(lineno)d`. Professional logging.

---

**Q16.25: Intermediate - [Logger Hierarchy]**

What is logger hierarchy?

A) File structure
B) Loggers organized by dotted names (parent.child); settings propagate down
C) Importance ranking
D) Thread levels

**Answer: B**

**Explanation:**
Logger names like 'myapp.module.submodule' create hierarchy. Child loggers inherit parent settings. `getLogger('myapp.module')` — messages propagate to 'myapp' handler. Configure parent once, children inherit.

---

**Q16.26: Intermediate - [Test Doubles Types]**

What's the difference between stub, mock, and fake?

A) All same
B) Stub = fixed returns; mock = verifies interactions; fake = simplified working implementation
C) Different languages
D) Test sizes

**Answer: B**

**Explanation:**
Stub: provides canned responses (no verification). Mock: verifies calls were made correctly. Fake: working implementation simpler than real (in-memory DB). Spy: wraps real object, records calls.

---

**Q16.27: Intermediate - [TDD Cycle]**

What is the TDD (Test-Driven Development) cycle?

A) Write test, write code, ship
B) Red → Green → Refactor (write failing test, make it pass, improve code)
C) Code first, test later
D) Test once, done

**Answer: B**

**Explanation:**
TDD: 1) Write test that fails (Red), 2) Write minimal code to pass (Green), 3) Refactor while keeping tests green. Forces thinking about design, ensures complete coverage of new code.

---

**Q16.28: Intermediate - [Fixture Cleanup with yield]**

What is the output?
```python
import pytest

@pytest.fixture
def resource():
    print("Setup")
    yield "resource"
    print("Teardown")

def test_use(resource):
    print(f"Using {resource}")
```

A) Setup, Using resource, Teardown
B) Using resource only
C) Setup only
D) Error

**Answer: A**

**Explanation:**
Fixture with `yield`: code before yield is setup, code after is teardown. Test runs between. Guarantees cleanup even if test fails. Modern alternative to setUp/tearDown pattern.

---

**Q16.29: Intermediate - [conftest.py]**

What is `conftest.py` in pytest?

A) Configuration file
B) File for shared fixtures, hooks accessible to all tests in directory and subdirs
C) Test constants
D) Conflict resolution

**Answer: B**

**Explanation:**
`conftest.py` contains fixtures shared across test files. No import needed — pytest discovers automatically. Also for hooks, plugins. Directory hierarchy — fixtures available to tests in same/subdirectories.

---

**Q16.30: Intermediate - [Skip and xfail]**

What does `@pytest.mark.skip` do?

A) Runs test twice
B) Skips test (with optional reason)
C) Fails test
D) Deletes test

**Answer: B**

**Explanation:**
`@pytest.mark.skip(reason="Not implemented yet")` — test skipped. `skipif(condition)` — conditional skip. `xfail` — expected to fail (doesn't fail test suite). Useful for known issues, platform-specific tests.

---

**Q16.31: Intermediate - [assert Introspection]**

Why does pytest recommend plain `assert`?

A) It's faster
B) pytest rewrites asserts to provide detailed failure messages
C) It's required
D) No reason

**Answer: B**

**Explanation:**
pytest uses AST rewriting to capture values in assertions. `assert a == b` shows actual values of a and b on failure. No need for `assertEqual` — plain Python with better diagnostics.

---

**Q16.32: Intermediate - [Monkey Patching]**

What is monkey patching in testing?

A) Testing animals
B) Dynamically replacing attributes/methods at runtime for testing
C) Code obfuscation
D) Performance tuning

**Answer: B**

**Explanation:**
Monkey patching: `module.function = mock_function` at runtime. pytest's `monkeypatch` fixture does this cleanly with automatic restoration. Useful for environment variables, imports, attributes.

---

**Q16.33: Intermediate - [Testing Exceptions]**

What is the output?
```python
def test_raises():
    try:
        int("abc")
    except ValueError:
        return  # pass
    assert False, "Should have raised"
```

A) Passes
B) Fails
C) Error
D) Incomplete

**Answer: A**

**Explanation:**
Manual exception testing pattern. If ValueError raised, function returns (passes). If not, hits `assert False`. Works but `pytest.raises` is cleaner and idiomatic.

---

**Q16.34: Intermediate - [logging.exception()]**

What does `logging.exception()` do?

A) Raises exception
B) Logs exception message with traceback (use in except block)
C) Catches exception
D) Same as error()

**Answer: B**

**Explanation:**
`logging.exception("Error occurred")` logs at ERROR level AND includes traceback. Only use inside except block where exception context exists. `logger.error("...", exc_info=True)` is equivalent.

---

**Q16.35: Intermediate - [pytest.mark.timeout]**

What does `@pytest.mark.timeout(5)` do?

A) Waits 5 seconds
B) Fails test if it takes longer than 5 seconds (requires pytest-timeout plugin)
C) Retries 5 times
D) Delays test start

**Answer: B**

**Explanation:**
plugin: `pytest-timeout`. Prevents tests hanging forever. If test exceeds timeout, it's marked as failed. Useful for tests involving I/O or potential infinite loops. Configure per-test or globally.

---

**Q16.36: Intermediate - [Test Isolation]**

Why is test isolation important?

A) Faster tests
B) Tests don't affect each other — order-independent, reproducible results
C) Security
D) Less code

**Answer: B**

**Explanation:**
Each test should be independent. Shared state between tests causes flaky tests (pass/fail based on order). Fixtures with proper setup/teardown ensure clean state. Tests should pass in any order.

---

**Q16.37: Intermediate - [Property-Based Testing]**

What is property-based testing (e.g., Hypothesis)?

A) Testing properties
B) Generating random inputs to verify properties hold for all cases
C) Testing attributes
D) Performance testing

**Answer: B**

**Explanation:**
Instead of specific examples, define properties: "sort(x) returns sorted list". Hypothesis generates inputs automatically, finds edge cases humans miss. Finds minimal failing examples. Powerful but more complex.

---

**Q16.38: Intermediate - [breakpoint() Customization]**

How do you use a different debugger with breakpoint()?

A) Can't change
B) Set PYTHONBREAKPOINT environment variable
C) Install different Python
D) Import differently

**Answer: B**

**Explanation:**
`PYTHONBREAKPOINT=ipdb.set_trace` uses ipdb instead. `PYTHONBREAKPOINT=0` disables all breakpoints. Customizable via sys.breakpointhook. Default is pdb.set_trace.

---

**Q16.39: Intermediate - [Unit vs Integration Tests]**

What's the difference between unit and integration tests?

A) Same thing
B) Unit tests isolated components; integration tests verify components work together
C) Unit tests are shorter
D) Integration tests are automated

**Answer: B**

**Explanation:**
Unit: test single function/class in isolation (mock dependencies). Integration: test multiple components together (real DB, API). Unit = fast, focused. Integration = slower, realistic. Test pyramid: many unit, fewer integration, few E2E.

---

**Q16.40: Intermediate - [Temporary Directories in Tests]**

What is the output?
```python
import pytest

def test_file_creation(tmp_path):
    file = tmp_path / "test.txt"
    file.write_text("hello")
    assert file.read_text() == "hello"
```

A) Error — tmp_path undefined
B) Passes — tmp_path is built-in pytest fixture for temp directory
C) Creates permanent file
D) Permission error

**Answer: B**

**Explanation:**
`tmp_path` is built-in pytest fixture — provides `pathlib.Path` to temporary directory. Unique per test, cleaned up after. `tmp_path_factory` for session-scoped temp dirs.

---

**Q16.41: Intermediate - [capsys Fixture]**

What is the output?
```python
import pytest

def test_output(capsys):
    print("Hello")
    captured = capsys.readouterr()
    assert captured.out == "Hello\n"
```

A) Error
B) Passes — capsys captures stdout/stderr
C) Fails — no capture
D) Prints Hello

**Answer: B**

**Explanation:**
`capsys` fixture captures stdout/stderr. `readouterr()` returns namedtuple with `.out` and `.err`. Useful for testing functions that print. Also `capfd` for file descriptors, `caplog` for logging.

---

**Q16.42: Intermediate - [assert_called with arguments]**

What is the output?
```python
from unittest.mock import Mock

m = Mock()
m(1, 2, key="value")
m.assert_called_with(1, 2, key="value")
print("OK")
```

A) AssertionError
B) `OK`
C) Error
D) Nothing

**Answer: B**

**Explanation:**
`assert_called_with` verifies the LAST call's arguments. Matches positional and keyword args. For all calls, use `assert_any_call` or check `call_args_list`. Exact match required.

---

**Q16.43: Intermediate - [patch.object]**

What's the difference between `patch` and `patch.object`?

A) No difference
B) patch uses string path; patch.object takes actual object and attribute name
C) patch.object is faster
D) Only patch works

**Answer: B**

**Explanation:**
`@patch('module.Class.method')` — string path. `@patch.object(Class, 'method')` — reference to class and attribute string. `patch.object` is more refactor-friendly (IDE can rename Class).

---

**Q16.44: Intermediate - [side_effect]**

What is the output?
```python
from unittest.mock import Mock

m = Mock(side_effect=[1, 2, 3])
print(m(), m(), m())
```

A) `1, 1, 1`
B) `1, 2, 3`
C) `[1, 2, 3]`
D) Error

**Answer: B**

**Explanation:**
`side_effect` with list returns values in order per call. Also accepts exception class (raises it), or callable (calls it with args). Simulates different responses to repeated calls.

---

**Q16.45: Intermediate - [pytest-cov]**

How do you generate coverage with pytest?

A) `pytest --cov`
B) `pytest --cov=mypackage --cov-report=html`
C) Separate tool only
D) Built-in without flags

**Answer: B**

**Explanation:**
`pytest-cov` plugin. `--cov=package` specifies what to cover. `--cov-report=html` generates HTML report. Also: `term` for terminal, `xml` for CI. Integrates coverage with pytest seamlessly.

---

**Q16.46: Intermediate - [assert vs Exceptions in Production]**

Should you use `assert` for input validation in production code?

A) Yes, it's the intended use
B) No — asserts can be disabled with -O flag; use exceptions
C) Either works
D) Only for testing

**Answer: B**

**Explanation:**
`python -O` disables all assertions. They're for debugging, not runtime validation. Use `if not valid: raise ValueError(...)` for production validation. Asserts are for catching programming errors during development.

---

**Q16.47: Intermediate - [Logging to File]**

How do you log to both file and console?

A) Impossible
B) Add multiple handlers to logger (StreamHandler + FileHandler)
C) Two logging calls
D) Duplicate logger

**Answer: B**

**Explanation:**
```python
logger.addHandler(logging.StreamHandler())
logger.addHandler(logging.FileHandler('app.log'))
```
Each handler can have its own level, format. Console might show WARNING+, file might log DEBUG+. Flexible configuration.

---

**Q16.48: Intermediate - [autospec]**

What does `autospec=True` do in mocking?

A) Auto-generates tests
B) Mock signature matches real object — catches wrong argument errors
C) Auto-runs specs
D) Nothing special

**Answer: B**

**Explanation:**
`@patch('module.Class', autospec=True)` — mock has same signature as real. Calling mock with wrong args raises TypeError. Catches bugs where you call mock with arguments real function doesn't accept.

---

**Q16.49: Intermediate - [Marker Selection]**

How do you run only tests marked `slow` with pytest?

A) `pytest --mark slow`
B) `pytest -m slow`
C) `pytest @slow`
D) `pytest --slow`

**Answer: B**

**Explanation:**
`@pytest.mark.slow` decorates test. `-m slow` runs only those. `-m "not slow"` excludes them. Expressions: `-m "slow and integration"`. Define custom markers in `pytest.ini` to avoid warnings.

---

**Q16.50: Intermediate - [Test Naming]**

Why should test names be descriptive?

A) Style only
B) Failure output shows test name — clear names explain what failed
C) Performance
D) No reason

**Answer: B**

**Explanation:**
`test_user_login_with_invalid_password_shows_error` — when it fails, you know exactly what's broken. Better than `test_login_1`. Tests as documentation. Use `_` to separate condition and expected outcome.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 6 | 12% |
| Intermediate | 44 | 88% |
| Advanced | 0 | 0% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- unittest framework basics
- pytest framework and advantages
- Fixtures and parametrization
- Mocking with unittest.mock
- Test coverage
- doctest for documentation testing
- pdb debugging
- logging module
- TDD principles
- Test organization and best practices
