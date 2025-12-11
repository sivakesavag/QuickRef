# Python Intermediate Level Assignments (1-155)

> **Level**: Intermediate | **Prerequisites**: Beginner Level | **Focus**: OOP, Libraries, Data Processing

---

## Section A: Object-Oriented Programming (A1-A30)

### A1: Basic Class Creation
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Create a `Person` class with name, age, email attributes and introduction method.

**Requirements**:
- Constructor with validation
- String representation (__str__, __repr__)
- Age validation (0-150)

**Test Cases**:
1. Valid person creation
2. Invalid age raises error
3. String representation format

**Skills**: Class definition, __init__, __str__

---

### A2: Bank Account Class
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 35 min

**Problem**: Create `BankAccount` with deposit, withdraw, transfer, balance check.

**Features**: Account number, balance tracking, transaction history

**Test Cases**:
1. Deposit increases balance
2. Withdraw fails if insufficient funds
3. Transfer between accounts

**Skills**: Methods, encapsulation, validation

---

### A3: Property Decorators
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Use @property for getters/setters with validation.

**Example**: Temperature class with celsius/fahrenheit properties

**Skills**: @property, @setter, computed properties

---

### A4: Class Methods & Static Methods
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create `Date` class with factory methods and utility functions.

**Methods**:
- `from_string("2024-01-15")` - classmethod
- `is_valid_date(year, month, day)` - staticmethod

**Skills**: @classmethod, @staticmethod

---

### A5: Single Inheritance
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 35 min

**Problem**: Create vehicle hierarchy: Vehicle → Car, Motorcycle, Truck.

**Features**: Common attributes in parent, specific in children

**Skills**: Inheritance, super(), method overriding

---

### A6: Multiple Inheritance
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Create `FlyingCar` inheriting from `Car` and `Aircraft`.

**Challenge**: Handle MRO, diamond problem

**Skills**: Multiple inheritance, MRO, super()

---

### A7: Abstract Base Classes
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create abstract `Shape` class with concrete implementations.

**Classes**: Circle, Rectangle, Triangle implementing area(), perimeter()

**Skills**: abc module, @abstractmethod

---

### A8: Polymorphism
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Implement payment processor with multiple payment types.

**Classes**: CreditCard, PayPal, BankTransfer all implementing process_payment()

**Skills**: Duck typing, polymorphic behavior

---

### A9: Encapsulation
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create `Employee` with private salary, protected department.

**Access Levels**: public, _protected, __private

**Skills**: Name mangling, access control

---

### A10: Magic Methods - Comparison
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement comparison operators for `Money` class.

**Methods**: __eq__, __lt__, __le__, __gt__, __ge__, __ne__

**Skills**: Rich comparison methods, @total_ordering

---

### A11: Magic Methods - Arithmetic
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create `Vector` class with arithmetic operations.

**Methods**: __add__, __sub__, __mul__, __truediv__, __neg__

**Skills**: Operator overloading

---

### A12: Magic Methods - Container
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Create custom collection with iteration support.

**Methods**: __len__, __getitem__, __setitem__, __iter__, __contains__

**Skills**: Container protocol

---

### A13: Magic Methods - Context
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create `Timer` and `DatabaseConnection` context managers.

**Methods**: __enter__, __exit__

**Skills**: Context manager protocol

---

### A14: Composition over Inheritance
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Refactor inheritance-based design to composition.

**Example**: Engine, Wheels, Body composed into Car

**Skills**: Composition, delegation

---

### A15: Mixin Classes
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create mixins for serialization, logging, validation.

**Classes**: JsonMixin, LoggingMixin, ValidatorMixin

**Skills**: Mixin pattern, multiple inheritance

---

### A16: Data Classes
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Use @dataclass for data containers.

**Features**: Auto-generated __init__, __repr__, __eq__, comparison

**Skills**: dataclasses module

---

### A17: Named Tuples
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use NamedTuple for immutable data records.

**Example**: Point, Color, Student records

**Skills**: typing.NamedTuple, collections.namedtuple

---

### A18: Slots
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Use __slots__ for memory optimization.

**Comparison**: Memory usage with and without slots

**Skills**: __slots__, memory optimization

---

### A19: Descriptor Protocol
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Create custom descriptors for type checking.

**Methods**: __get__, __set__, __delete__

**Skills**: Descriptor protocol, validation descriptors

---

### A20: Class Decorators
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 40 min

**Problem**: Create decorators that modify class behavior.

**Examples**: @singleton, @register, @add_method

**Skills**: Class decorators, metaclass alternatives

---

### A21: Factory Pattern
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Implement factory pattern for object creation.

**Example**: ShapeFactory creating Circle, Rectangle, Triangle

**Skills**: Factory pattern, design patterns

---

### A22: Singleton Pattern
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement singleton pattern multiple ways.

**Approaches**: Class variable, decorator, metaclass

**Skills**: Singleton pattern

---

### A23: Observer Pattern
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Implement event system with observers.

**Example**: Stock price changes notifying multiple displays

**Skills**: Observer pattern, event-driven

---

### A24: Strategy Pattern
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Implement interchangeable algorithms.

**Example**: Different sorting/compression/payment strategies

**Skills**: Strategy pattern

---

### A25: Object Serialization
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Serialize objects to JSON, pickle, custom format.

**Methods**: Custom __dict__, json encoding

**Skills**: Serialization, __getstate__, __setstate__

---

### A26: Copy and Clone
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Implement shallow and deep copy for custom objects.

**Methods**: __copy__, __deepcopy__

**Skills**: copy module, object copying

---

### A27: Callable Objects
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Create callable class instances.

**Method**: __call__

**Examples**: Cached function, rate limiter, counter

**Skills**: __call__, stateful callables

---

### A28: Object Hashing
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Make custom objects hashable and usable as dict keys.

**Methods**: __hash__, __eq__

**Skills**: Hashing, immutability

---

### A29: Library Management System
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 90 min

**Problem**: Build complete library system with OOP.

**Classes**: Library, Book, Member, Loan, Fine

**Features**: Check out, return, search, overdue tracking

**Skills**: Complete OOP project

---

### A30: E-commerce System
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 120 min

**Problem**: Build e-commerce backend with OOP.

**Classes**: Product, Cart, Order, Customer, Payment

**Features**: Cart operations, checkout, inventory

**Skills**: Complex OOP design

---

## Section B: Exception Handling (B1-B15)

### B1: Basic Try-Except
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Handle common exceptions with appropriate messages.

**Exceptions**: ValueError, TypeError, ZeroDivisionError

**Skills**: try-except basics

---

### B2: Multiple Exception Types
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Handle different exceptions differently.

**Skills**: Multiple except blocks, exception hierarchy

---

### B3: Finally and Else
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use finally for cleanup and else for success path.

**Skills**: try-except-else-finally

---

### B4: Exception Chaining
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Chain exceptions with `from` and `cause`.

**Skills**: Exception chaining, __cause__

---

### B5: Custom Exceptions
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create exception hierarchy for a domain.

**Example**: ValidationError, AuthenticationError, PermissionError

**Skills**: Custom exception classes

---

### B6: Exception Context
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Access exception information (type, value, traceback).

**Skills**: sys.exc_info(), traceback module

---

### B7: Raise Exceptions
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Raise exceptions with meaningful messages.

**Skills**: raise, raise from, re-raising

---

### B8: Assert Statements
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Use assertions for development-time checks.

**Skills**: assert, __debug__

---

### B9: Graceful Degradation
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Handle failures gracefully with fallbacks.

**Example**: API failure → cache → default value

**Skills**: Resilient error handling

---

### B10: Error Logging
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Log exceptions with full context for debugging.

**Skills**: logging module, exception logging

---

### B11: Context Manager Exceptions
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Handle exceptions in context managers properly.

**Skills**: __exit__ return value, suppress exceptions

---

### B12: Retry Decorator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Create decorator that retries failed operations.

**Features**: Max retries, exponential backoff, exception types

**Skills**: Decorators, exception handling

---

### B13: Validation Framework
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Build validation system with meaningful error messages.

**Features**: Multiple validators, error aggregation, custom messages

**Skills**: Exception design, validation patterns

---

### B14: Exception Testing
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Write tests that verify exceptions are raised.

**Skills**: pytest.raises, testing exceptions

---

### B15: Error Recovery System
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Build system that recovers from various failure modes.

**Features**: Transaction rollback, state recovery, logging

**Skills**: Robust error handling

---

## Section C: File Format Processing (C1-C20)

### C1: CSV Reader
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Read CSV files using csv module.

**Features**: Handle headers, different delimiters

**Skills**: csv.reader, csv.DictReader

---

### C2: CSV Writer
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Write data to CSV files.

**Skills**: csv.writer, csv.DictWriter

---

### C3: CSV Data Analysis
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Analyze CSV dataset - filter, aggregate, transform.

**Skills**: csv processing, data analysis

---

### C4: JSON Reading
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Parse JSON from files and strings.

**Skills**: json.load, json.loads

---

### C5: JSON Writing
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Serialize Python objects to JSON.

**Features**: Custom encoders, formatting options

**Skills**: json.dump, json.dumps, default parameter

---

### C6: JSON Schema Validation
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Validate JSON against schema.

**Skills**: jsonschema library, validation

---

### C7: Nested JSON Processing
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Flatten and unflatten nested JSON.

**Skills**: Recursive processing, path notation

---

### C8: XML Parsing
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Parse XML using ElementTree.

**Skills**: xml.etree.ElementTree, XPath

---

### C9: XML Creation
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create and write XML documents.

**Skills**: Element creation, tree building

---

### C10: YAML Processing
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Read and write YAML configuration files.

**Skills**: PyYAML, safe_load, dump

---

### C11: TOML Processing
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Work with TOML configuration files.

**Skills**: tomllib (Python 3.11+), toml library

---

### C12: INI Configuration
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Parse and write INI files.

**Skills**: configparser module

---

### C13: Excel File Reading
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Read Excel files with openpyxl.

**Features**: Multiple sheets, cell formatting

**Skills**: openpyxl library

---

### C14: Excel File Writing
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Create Excel reports with formatting.

**Features**: Charts, formatting, formulas

**Skills**: openpyxl writing

---

### C15: Parquet Files
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Read and write Parquet files.

**Skills**: pyarrow, pandas parquet

---

### C16: File Format Converter
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 50 min

**Problem**: Build converter between CSV, JSON, XML.

**Skills**: Multiple format handling

---

### C17: Log File Parser
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Parse structured log files with different formats.

**Formats**: Common Log Format, JSON logs, custom formats

**Skills**: Log parsing, pattern matching

---

### C18: HTML Table Extractor
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Extract tables from HTML to CSV/JSON.

**Skills**: html.parser, BeautifulSoup basics

---

### C19: SQLite Database
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: CRUD operations with SQLite.

**Skills**: sqlite3 module, SQL basics

---

### C20: Data Pipeline
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 90 min

**Problem**: Build ETL pipeline: Extract from multiple sources, transform, load.

**Sources**: CSV, JSON, API
**Output**: SQLite database

**Skills**: Complete data pipeline

---

## Section D: Regular Expressions (D1-D15)

### D1: Pattern Matching Basics
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use re.match, re.search, re.findall.

**Skills**: Basic regex methods

---

### D2: Character Classes
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use \d, \w, \s, [a-z], [^abc].

**Skills**: Character class patterns

---

### D3: Quantifiers
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use *, +, ?, {n}, {n,m}.

**Skills**: Quantifier patterns

---

### D4: Anchors and Boundaries
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use ^, $, \b, \B.

**Skills**: Position anchors

---

### D5: Groups and Capturing
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Use () for grouping and capturing.

**Skills**: Groups, backreferences, named groups

---

### D6: Lookahead and Lookbehind
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 40 min

**Problem**: Use (?=), (?!), (?<=), (?<!).

**Skills**: Lookaround assertions

---

### D7: Email Validation
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Validate email addresses with comprehensive regex.

**Skills**: Complex pattern building

---

### D8: URL Parser
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Parse URLs extracting protocol, domain, path, query.

**Skills**: URL pattern matching

---

### D9: Log Analysis
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Extract information from log entries.

**Fields**: Timestamp, level, source, message

**Skills**: Multi-field extraction

---

### D10: Find and Replace
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Use re.sub for complex replacements.

**Features**: Callback functions, template substitution

**Skills**: re.sub, replacement patterns

---

### D11: Phone Number Formats
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Match and normalize various phone formats.

**Skills**: Pattern alternatives, normalization

---

### D12: Password Validator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Validate password complexity requirements.

**Rules**: Length, uppercase, lowercase, digit, special

**Skills**: Multiple pattern validation

---

### D13: HTML Tag Extraction
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Extract HTML tags and their attributes.

**Warning**: Limitations of regex for HTML

**Skills**: Tag pattern matching

---

### D14: Text Sanitization
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Clean text by removing/replacing patterns.

**Tasks**: Remove HTML, normalize whitespace, strip special chars

**Skills**: Text cleaning with regex

---

### D15: Regex Compiler
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Build regex pattern tester/debugger.

**Features**: Pattern explanation, match highlighting

**Skills**: re.compile, verbose mode, debugging

---

## Section E: Web APIs and Requests (E1-E20)

### E1: GET Requests
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Make GET requests and handle responses.

**Skills**: requests.get, response handling

---

### E2: POST Requests
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Send data with POST requests.

**Skills**: requests.post, JSON payload

---

### E3: Headers and Auth
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Add headers and authentication.

**Skills**: Headers, Basic Auth, Bearer tokens

---

### E4: Query Parameters
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Build URLs with query parameters.

**Skills**: params argument, URL encoding

---

### E5: Error Handling
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Handle HTTP errors and network issues.

**Skills**: Status codes, raise_for_status, timeouts

---

### E6: Session Management
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Use sessions for persistent connections.

**Skills**: requests.Session, cookies

---

### E7: File Downloads
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Download files with progress tracking.

**Skills**: Streaming downloads, progress bars

---

### E8: File Uploads
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Upload files to APIs.

**Skills**: Multipart uploads, file handling

---

### E9: REST API Client
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 50 min

**Problem**: Build client for a REST API.

**Methods**: GET, POST, PUT, PATCH, DELETE

**Skills**: Complete REST client

---

### E10: Pagination Handling
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Handle paginated API responses.

**Patterns**: Page numbers, cursors, links

**Skills**: Pagination patterns

---

### E11: Rate Limiting
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Implement rate limiting for API calls.

**Skills**: Rate limiting, backoff

---

### E12: Weather API
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Build weather data fetcher and analyzer.

**Features**: Current weather, forecast, historical

**Skills**: Real API integration

---

### E13: GitHub API
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 50 min

**Problem**: Interact with GitHub API.

**Features**: Repos, issues, users, rate limits

**Skills**: Complex API usage

---

### E14: Currency Converter
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Build currency converter using exchange rate API.

**Skills**: Real-time data fetching

---

### E15: News Aggregator
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 50 min

**Problem**: Aggregate news from multiple API sources.

**Skills**: Multiple API integration

---

### E16: OAuth Authentication
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Implement OAuth2 authentication flow.

**Skills**: OAuth2, token management

---

### E17: Webhook Handler
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Receive and process webhooks.

**Skills**: Webhook patterns, payload validation

---

### E18: API Response Caching
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Cache API responses to reduce calls.

**Skills**: Caching strategies, TTL

---

### E19: Retry Logic
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Implement robust retry with backoff.

**Skills**: Exponential backoff, retry decorators

---

### E20: API Testing Suite
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Build test suite for an API.

**Features**: Mock responses, validation, reporting

**Skills**: API testing, mocking

---

## Section F: Pandas Fundamentals (F1-F30)

### F1: DataFrame Creation
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Create DataFrames from various sources.

**Sources**: Dict, list, CSV, JSON, SQL

**Skills**: pd.DataFrame, read_ methods

---

### F2: Data Selection
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Select rows and columns using loc, iloc.

**Skills**: Indexing, slicing, boolean selection

---

### F3: Data Filtering
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Filter data by conditions.

**Skills**: Boolean masks, query method

---

### F4: Column Operations
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create, modify, delete columns.

**Skills**: Column assignment, apply function

---

### F5: Missing Data
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Handle missing values.

**Methods**: dropna, fillna, interpolate

**Skills**: Missing data handling

---

### F6: Data Types
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Convert and optimize data types.

**Skills**: astype, category, memory optimization

---

### F7: Sorting
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Sort by values and index.

**Skills**: sort_values, sort_index

---

### F8: Grouping
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Group data and aggregate.

**Skills**: groupby, agg, transform

---

### F9: Merging
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Merge DataFrames.

**Methods**: merge, join, concat

**Skills**: Join types, key matching

---

### F10: Reshaping
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Pivot, melt, stack, unstack data.

**Skills**: Data reshaping

---

### F11: String Methods
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Apply string operations to Series.

**Skills**: str accessor, vectorized strings

---

### F12: DateTime Operations
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Parse and manipulate dates.

**Skills**: to_datetime, dt accessor, resample

---

### F13: Duplicate Handling
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Find and remove duplicates.

**Skills**: duplicated, drop_duplicates

---

### F14: Apply Functions
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Apply custom functions.

**Methods**: apply, map, applymap

**Skills**: Custom transformations

---

### F15: Window Functions
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Calculate rolling statistics.

**Skills**: rolling, expanding, ewm

---

### F16: Multi-Index
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Work with hierarchical indexes.

**Skills**: MultiIndex, stack, unstack

---

### F17: Categorical Data
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Optimize categorical columns.

**Skills**: Category dtype, ordered categories

---

### F18: Data Validation
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Validate data quality.

**Checks**: Types, ranges, patterns, completeness

**Skills**: Data validation patterns

---

### F19: Data Export
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Export to various formats.

**Formats**: CSV, Excel, JSON, SQL, Parquet

**Skills**: to_ methods

---

### F20: Method Chaining
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Chain operations fluently.

**Skills**: pipe, assign, query chaining

---

### F21: Sales Analysis
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 60 min

**Problem**: Analyze sales dataset.

**Tasks**: Top products, trends, customer segments

**Skills**: Complete pandas analysis

---

### F22: HR Analytics
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 60 min

**Problem**: Analyze employee dataset.

**Tasks**: Attrition, salary, departments

**Skills**: HR data analysis

---

### F23: Financial Data
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 75 min

**Problem**: Analyze stock/financial data.

**Tasks**: Returns, volatility, moving averages

**Skills**: Financial analysis with pandas

---

### F24: Customer Analytics
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 75 min

**Problem**: RFM analysis, customer segmentation.

**Skills**: Customer analytics

---

### F25: Log Analysis
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 50 min

**Problem**: Analyze server log data.

**Skills**: Text processing, time series

---

### F26: Survey Analysis
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 50 min

**Problem**: Analyze survey responses.

**Skills**: Categorical data, cross-tabulation

---

### F27: A/B Test Analysis
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Analyze A/B test results.

**Skills**: Statistical testing, conversion rates

---

### F28: Data Quality Report
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 50 min

**Problem**: Generate data quality report.

**Metrics**: Completeness, uniqueness, validity

**Skills**: Data profiling

---

### F29: ETL with Pandas
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 90 min

**Problem**: Build ETL pipeline.

**Skills**: Extract, transform, load

---

### F30: Optimization Techniques
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Optimize pandas for large data.

**Techniques**: Chunking, dtypes, eval

**Skills**: Performance optimization

---

## Section G: Data Visualization (G1-G15)

### G1: Line Plots
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create line charts with matplotlib.

**Skills**: plt.plot, customization

---

### G2: Bar Charts
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create bar and horizontal bar charts.

**Skills**: plt.bar, plt.barh

---

### G3: Histograms
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create histograms for distributions.

**Skills**: plt.hist, bins, density

---

### G4: Scatter Plots
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create scatter plots with sizing/coloring.

**Skills**: plt.scatter, colorbar

---

### G5: Pie Charts
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Create pie charts with explode and labels.

**Skills**: plt.pie, customization

---

### G6: Subplots
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Create multi-panel figures.

**Skills**: plt.subplots, layout

---

### G7: Customization
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Customize titles, labels, colors, styles.

**Skills**: rcParams, style sheets

---

### G8: Seaborn Basics
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Statistical plots with Seaborn.

**Plots**: countplot, boxplot, violinplot

**Skills**: seaborn library

---

### G9: Heatmaps
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create correlation and pivot heatmaps.

**Skills**: sns.heatmap, annotations

---

### G10: Pair Plots
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create pairwise relationship plots.

**Skills**: sns.pairplot, diag types

---

### G11: Time Series Plots
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Visualize time series data.

**Features**: Date formatting, seasonal decomposition

**Skills**: Time series visualization

---

### G12: Geographic Plots
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 50 min

**Problem**: Basic geographic visualization.

**Skills**: Basemap or folium basics

---

### G13: Interactive Plots
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Create interactive plots with Plotly.

**Skills**: plotly.express basics

---

### G14: Dashboard Layout
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Create multi-plot dashboard.

**Skills**: Layout design, GridSpec

---

### G15: Data Story
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 90 min

**Problem**: Create complete visual analysis story.

**Features**: Multiple plots, annotations, narrative

**Skills**: Data storytelling

---

## Intermediate Level Capstone Projects (CAP1-CAP10)

### CAP1: Task Management System
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 4 hours

**Description**: Full CRUD task manager with OOP design.

**Features**: Tasks, projects, deadlines, priorities, JSON persistence

**Skills**: OOP, file handling, data structures

---

### CAP2: Web API Client Library
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 5 hours

**Description**: Build reusable API client with caching.

**Features**: Auth, pagination, error handling, rate limiting

**Skills**: Requests, OOP, caching

---

### CAP3: Sales Dashboard
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 5 hours

**Description**: Complete sales analysis with visualizations.

**Data**: Product sales, regions, time periods

**Skills**: Pandas, matplotlib, seaborn

---

### CAP4: Log Analyzer
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 4 hours

**Description**: Parse and analyze application logs.

**Features**: Pattern extraction, error tracking, reports

**Skills**: Regex, file processing, OOP

---

### CAP5: Customer Segmentation
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 5 hours

**Description**: RFM-based customer segmentation analysis.

**Features**: Data cleaning, segmentation, visualization

**Skills**: Pandas, visualization, analytics

---

### CAP6: Data Validation Framework
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 4 hours

**Description**: Build extensible data validation framework.

**Features**: Schema definition, validators, reporting

**Skills**: OOP, decorators, design patterns

---

### CAP7: CSV to Database Migrator
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 4 hours

**Description**: Migrate CSV files to SQLite with transformations.

**Features**: Schema inference, type conversion, batch processing

**Skills**: CSV, SQLite, data types

---

### CAP8: Movie Database
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 5 hours

**Description**: Build movie database with TMDB API.

**Features**: Search, favorites, recommendations

**Skills**: API, SQLite, OOP

---

### CAP9: Financial Portfolio Tracker
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 6 hours

**Description**: Track investment portfolio performance.

**Features**: Real-time prices, returns, visualizations

**Skills**: API, pandas, visualization

---

### CAP10: E-commerce Analytics
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 6 hours

**Description**: Complete e-commerce data analysis.

**Analysis**: Products, customers, trends, baskets

**Skills**: Full pandas analytics, visualization

---

**Intermediate Level Summary**:
- **Total Assignments**: 155
- **OOP Focus**: 30 assignments
- **Exception Handling**: 15 assignments
- **File Formats**: 20 assignments
- **Regex**: 15 assignments
- **Web APIs**: 20 assignments
- **Pandas**: 30 assignments
- **Visualization**: 15 assignments
- **Capstone Projects**: 10

---

*Continue to Advanced Level: `python_assign_advanced.md`*
