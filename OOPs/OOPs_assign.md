# OOP Assignments Curriculum
> Progressive exercises from beginner to advanced | 85+ assignments + 5 capstone projects

---

# 🟢 BEGINNER LEVEL (B1–B25)
*Focus: Classes, objects, methods, constructors, encapsulation basics*

---

## B1: Create Your First Class

**Difficulty:** ⭐ Easy  
**Concepts:** Class definition, attributes, object instantiation

**Problem Statement:**  
Create a `Person` class with `name` (string) and `age` (integer) attributes. Instantiate at least two Person objects and print their details.

**Requirements:**
- Define class with two attributes
- Create constructor to initialize values
- Add a `display()` method that prints "Name: X, Age: Y"
- Create 2+ instances with different values

**Test Cases:**
- `Person("Alice", 30)` → displays "Name: Alice, Age: 30"
- `Person("Bob", 25)` → displays "Name: Bob, Age: 25"

**Stretch:** Add a `greet()` method that returns "Hi, I'm [name]!"

**Common Mistakes:**
- Forgetting `self`/`this` when accessing attributes
- Not initializing attributes in constructor

---

## B2: Rectangle Calculator

**Difficulty:** ⭐ Easy  
**Concepts:** Methods, return values, simple calculations

**Problem Statement:**  
Create a `Rectangle` class with `width` and `height`. Implement methods to calculate area and perimeter.

**Requirements:**
- Constructor accepts width and height
- `area()` returns width × height
- `perimeter()` returns 2 × (width + height)
- `is_square()` returns true if width equals height

**Test Cases:**
- Rectangle(5, 3): area=15, perimeter=16, is_square=false
- Rectangle(4, 4): area=16, perimeter=16, is_square=true

**Stretch:** Add `scale(factor)` method that multiplies both dimensions.

**Common Mistakes:**
- Returning wrong type (int vs float)
- Modifying attributes in getter methods

---

## B3: Bank Account Basics

**Difficulty:** ⭐ Easy  
**Concepts:** State management, methods modifying state

**Problem Statement:**  
Create a `BankAccount` class with an account holder name and balance. Implement deposit and withdraw operations.

**Requirements:**
- Initialize with holder name and starting balance (default 0)
- `deposit(amount)` adds to balance
- `withdraw(amount)` subtracts from balance (no overdraft allowed)
- `get_balance()` returns current balance

**Test Cases:**
- Deposit 100 → balance = 100
- Withdraw 30 → balance = 70
- Withdraw 100 (overdraft) → rejected, balance stays 70

**Stretch:** Track transaction count; add `get_statement()` method.

**Common Mistakes:**
- Allowing negative balance
- Not validating positive deposit amounts

---

## B4: Counter with Increment/Decrement

**Difficulty:** ⭐ Easy  
**Concepts:** Instance state, multiple methods

**Problem Statement:**  
Create a `Counter` class that tracks a count value. Provide increment, decrement, and reset functionality.

**Requirements:**
- Start at 0 by default (or custom start value)
- `increment()` adds 1
- `decrement()` subtracts 1 (minimum 0)
- `reset()` sets back to initial value
- `get_count()` returns current value

**Test Cases:**
- increment 3 times → count = 3
- decrement 5 times from 3 → count = 0 (not negative)
- reset → back to initial

**Stretch:** Add `increment_by(n)` and `decrement_by(n)`.

**Common Mistakes:**
- Allowing negative counts
- Losing track of initial value for reset

---

## B5: Student Grade Tracker

**Difficulty:** ⭐ Easy  
**Concepts:** Collections as attributes, computed properties

**Problem Statement:**  
Create a `Student` class that stores a name and list of grades. Calculate average, highest, and lowest grades.

**Requirements:**
- Constructor takes name, initializes empty grade list
- `add_grade(grade)` appends grade (0-100)
- `average()` returns mean of all grades
- `highest()` and `lowest()` return max/min

**Test Cases:**
- Grades [80, 90, 70] → avg=80, high=90, low=70
- No grades → handle gracefully (return 0 or None)

**Stretch:** Add `grade_letter()` returning A/B/C/D/F based on average.

**Common Mistakes:**
- Division by zero when no grades
- Not validating grade range

---

## B6: Temperature Converter

**Difficulty:** ⭐ Easy  
**Concepts:** Multiple constructors/factory methods, conversion logic

**Problem Statement:**  
Create a `Temperature` class that stores a value and can convert between Celsius, Fahrenheit, and Kelvin.

**Requirements:**
- Store temperature internally in one unit (e.g., Celsius)
- `to_celsius()`, `to_fahrenheit()`, `to_kelvin()` methods
- Factory methods or constructors: `from_celsius()`, `from_fahrenheit()`

**Test Cases:**
- 0°C → 32°F, 273.15K
- 100°C → 212°F, 373.15K
- -40°C → -40°F

**Stretch:** Implement comparison operators (is_hotter_than).

**Common Mistakes:**
- Conversion formula errors
- Rounding issues

---

## B7: Book Class

**Difficulty:** ⭐ Easy  
**Concepts:** Multiple attributes, string representation

**Problem Statement:**  
Create a `Book` class with title, author, ISBN, and page count. Implement a string representation.

**Requirements:**
- All four attributes required in constructor
- `__str__` / `toString()` returns formatted string
- `is_long_read()` returns true if pages > 300

**Test Cases:**
- Book("1984", "Orwell", "123", 328) → is_long_read = true
- String format: "1984 by Orwell (328 pages)"

**Stretch:** Add `reading_time(pages_per_hour)` estimate method.

**Common Mistakes:**
- Not handling None/empty values
- Inconsistent string formatting

---

## B8: Stopwatch

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Time tracking, state management

**Problem Statement:**  
Create a `Stopwatch` class that can start, stop, and report elapsed time.

**Requirements:**
- `start()` begins timing
- `stop()` pauses timing
- `elapsed()` returns total elapsed seconds
- `reset()` clears all timing data

**Test Cases:**
- Start, wait 2 seconds, stop → elapsed ≈ 2
- Start, stop, start, stop → accumulates time

**Stretch:** Add `lap()` method returning split times.

**Common Mistakes:**
- Not handling multiple start/stop cycles
- Using wall clock incorrectly

---

## B9: Coordinate/Point2D

**Difficulty:** ⭐ Easy  
**Concepts:** Immutability concepts, mathematical operations

**Problem Statement:**  
Create a `Point2D` class representing x,y coordinates. Implement distance and movement methods.

**Requirements:**
- Constructor takes x, y
- `distance_to(other_point)` returns Euclidean distance
- `move(dx, dy)` returns new Point2D (immutable style)
- `origin()` class/static method returns Point2D(0, 0)

**Test Cases:**
- Distance from (0,0) to (3,4) = 5
- (1,1).move(2,3) = (3,4)

**Stretch:** Add `midpoint(other)` and `angle_to(other)` methods.

**Common Mistakes:**
- Mutating instead of returning new instance
- Distance formula errors

---

## B10: Email Validator

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Validation in constructor, encapsulation

**Problem Statement:**  
Create an `Email` class that validates and stores email addresses. Invalid emails should be rejected.

**Requirements:**
- Constructor validates email format
- Raise exception or return error for invalid format
- `domain()` returns part after @
- `username()` returns part before @

**Test Cases:**
- "user@example.com" → valid, domain="example.com"
- "invalid-email" → rejected
- "a@b" → rejected (too short domain)

**Stretch:** Add `is_corporate()` detecting known business domains.

**Common Mistakes:**
- Overly complex regex
- Missing edge cases (empty string, multiple @)

---

## B11: Inventory Item

**Difficulty:** ⭐ Easy  
**Concepts:** Business logic in methods

**Problem Statement:**  
Create an `InventoryItem` class for a store with name, quantity, and price. Track stock levels.

**Requirements:**
- `restock(amount)` increases quantity
- `sell(amount)` decreases quantity (if available)
- `total_value()` returns quantity × price
- `is_in_stock()` returns true if quantity > 0

**Test Cases:**
- Item with qty=10: sell(3) → qty=7
- sell(15) when qty=7 → rejected or partial

**Stretch:** Add `low_stock_alert(threshold)` method.

**Common Mistakes:**
- Allowing negative inventory
- Not returning success/failure from sell()

---

## B12: Circle Class

**Difficulty:** ⭐ Easy  
**Concepts:** Constants (PI), computed properties

**Problem Statement:**  
Create a `Circle` class with radius. Calculate area, circumference, and diameter.

**Requirements:**
- Store radius, validate non-negative
- `area()` → π × r²
- `circumference()` → 2 × π × r
- `diameter` property → 2 × r

**Test Cases:**
- radius=1 → area≈3.14, circumference≈6.28
- radius=0 → all values = 0

**Stretch:** Implement `scale(factor)` and circle comparison by area.

**Common Mistakes:**
- Using wrong PI precision
- Allowing negative radius

---

## B13: Todo Item

**Difficulty:** ⭐ Easy  
**Concepts:** Boolean state, timestamps

**Problem Statement:**  
Create a `TodoItem` class with description, completion status, and due date.

**Requirements:**
- Constructor takes description and optional due date
- `mark_complete()` and `mark_incomplete()` toggle status
- `is_overdue()` checks if past due and not complete
- `days_until_due()` returns days remaining

**Test Cases:**
- New item → incomplete
- Mark complete → is_complete = true
- Past due date + incomplete → is_overdue = true

**Stretch:** Add priority levels (low/medium/high).

**Common Mistakes:**
- Timezone issues with dates
- Not handling null due dates

---

## B14: Dice Roller

**Difficulty:** ⭐ Easy  
**Concepts:** Randomness, configuration

**Problem Statement:**  
Create a `Dice` class representing an n-sided die with roll functionality.

**Requirements:**
- Constructor takes number of sides (default 6)
- `roll()` returns random value 1 to n
- `roll_multiple(times)` returns list of rolls
- `last_roll` property stores most recent result

**Test Cases:**
- 6-sided die: rolls always 1-6
- 20-sided die: rolls always 1-20

**Stretch:** Add `roll_with_modifier(bonus)` for RPG-style rolling.

**Common Mistakes:**
- Off-by-one in random range
- Not seeding random for testing

---

## B15: Password Strength Checker

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Validation, encapsulation, string analysis

**Problem Statement:**  
Create a `Password` class that evaluates password strength and enforces rules.

**Requirements:**
- Store password (consider hashing for real use)
- `strength()` returns weak/medium/strong based on rules
- Rules: length ≥8, has uppercase, lowercase, digit, special char
- `meets_requirements()` returns boolean

**Test Cases:**
- "abc" → weak
- "Password1" → medium
- "P@ssw0rd!" → strong

**Stretch:** Add `suggestions()` returning list of improvements needed.

**Common Mistakes:**
- Storing plain text passwords in production
- Missing edge cases in strength rules

---

## B16: Contact Card

**Difficulty:** ⭐ Easy  
**Concepts:** Multiple attributes, optional fields

**Problem Statement:**  
Create a `Contact` class with name, phone, email, and address. Handle optional fields gracefully.

**Requirements:**
- Name required, others optional
- `has_email()`, `has_phone()` methods
- `display_card()` formats non-null fields nicely
- `update_email(new_email)` with validation

**Test Cases:**
- Contact with only name → displays just name
- All fields → formatted multi-line card

**Stretch:** Add `vcard_format()` returning VCard string.

**Common Mistakes:**
- Null pointer exceptions on optional fields
- Inconsistent handling of empty vs null

---

## B17: Stack Implementation

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Data structure, LIFO behavior

**Problem Statement:**  
Implement a `Stack` class with push, pop, peek operations using OOP principles.

**Requirements:**
- `push(item)` adds to top
- `pop()` removes and returns top item
- `peek()` returns top without removing
- `is_empty()` and `size()` utility methods

**Test Cases:**
- Push 1, 2, 3 → pop returns 3, 2, 1
- Pop on empty → exception or None

**Stretch:** Add `clear()` and iteration support.

**Common Mistakes:**
- Not handling empty stack gracefully
- Memory leaks (in languages without GC)

---

## B18: Queue Implementation

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Data structure, FIFO behavior

**Problem Statement:**  
Implement a `Queue` class with enqueue, dequeue operations.

**Requirements:**
- `enqueue(item)` adds to back
- `dequeue()` removes from front
- `front()` peeks at front item
- `is_empty()` and `size()` methods

**Test Cases:**
- Enqueue 1, 2, 3 → dequeue returns 1, 2, 3
- Dequeue on empty → exception or None

**Stretch:** Implement circular queue with fixed capacity.

**Common Mistakes:**
- Confusing FIFO with LIFO
- Inefficient removal from front (array shifting)

---

## B19: Fraction Arithmetic

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Operator overloading, mathematical logic

**Problem Statement:**  
Create a `Fraction` class supporting addition, subtraction, multiplication, and division.

**Requirements:**
- Constructor takes numerator and denominator
- Automatically reduce to lowest terms (GCD)
- `add()`, `subtract()`, `multiply()`, `divide()` methods
- Handle zero denominator

**Test Cases:**
- 1/2 + 1/4 = 3/4
- 2/3 × 3/4 = 1/2 (simplified)
- Division by 0/n → error

**Stretch:** Implement comparison operators and mixed number conversion.

**Common Mistakes:**
- Not simplifying fractions
- Integer overflow with large numerators

---

## B20: Time Duration

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Complex internal representation, formatting

**Problem Statement:**  
Create a `Duration` class that stores time in hours, minutes, seconds with arithmetic operations.

**Requirements:**
- Multiple constructors: from seconds, from h/m/s
- `add(other)` and `subtract(other)` operations
- `to_seconds()` total conversion
- `format()` returns "HH:MM:SS"

**Test Cases:**
- 3661 seconds → "01:01:01"
- 1:30:00 + 0:45:30 = 2:15:30

**Stretch:** Add `from_string()` parser and comparison methods.

**Common Mistakes:**
- Overflow handling in seconds
- Off-by-one in carry operations

---

## B21: Playlist Manager

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Collections, ordering, uniqueness

**Problem Statement:**  
Create a `Playlist` class managing a list of song titles with add, remove, and shuffle operations.

**Requirements:**
- `add_song(title)` appends (no duplicates)
- `remove_song(title)` removes if exists
- `shuffle()` randomizes order
- `total_count()` and `current_song()` (first in list)

**Test Cases:**
- Add duplicate → ignored
- Remove non-existent → no error
- Shuffle → different order (statistically)

**Stretch:** Add `next_song()`, `previous_song()` navigation.

**Common Mistakes:**
- Modifying list while iterating
- Not handling empty playlist

---

## B22: Shopping Cart

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Nested objects, calculations

**Problem Statement:**  
Create a `ShoppingCart` class containing `CartItem` objects (product name, price, quantity).

**Requirements:**
- `add_item(name, price, quantity)`
- `remove_item(name)`
- `update_quantity(name, new_qty)`
- `total()` calculates sum of all items
- `item_count()` returns unique item count

**Test Cases:**
- Add 2 apples @$1 + 3 oranges @$1.5 → total = $6.50
- Update apples to qty 5 → total = $9.50

**Stretch:** Add `apply_discount(percent)` method.

**Common Mistakes:**
- Float precision in currency
- Not handling negative quantities

---

## B23: Car Rental Record

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Date calculations, business logic

**Problem Statement:**  
Create a `Rental` class tracking car rentals with start date, end date, and daily rate.

**Requirements:**
- `days_rented()` calculates duration
- `total_cost()` returns days × rate
- `is_active()` checks if currently rented
- `extend(additional_days)` updates end date

**Test Cases:**
- 5-day rental @$50/day → $250
- Extend by 2 days → 7 days, $350

**Stretch:** Add late return penalty calculation.

**Common Mistakes:**
- Off-by-one in day counting (inclusive vs exclusive)
- Timezone issues

---

## B24: Configuration Settings

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Key-value storage, type handling

**Problem Statement:**  
Create a `Config` class that stores application settings with type-safe getters.

**Requirements:**
- `set(key, value)` stores any value
- `get_string(key)`, `get_int(key)`, `get_bool(key)` typed getters
- `has(key)` checks existence
- Default values if key missing

**Test Cases:**
- set("port", 8080) → get_int("port") = 8080
- get_string("missing", "default") → "default"

**Stretch:** Add `load_from_file()` and `save_to_file()` methods.

**Common Mistakes:**
- Type casting errors
- Mutable default values

---

## B25: Movie Rating Aggregator

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Statistics, multiple data points

**Problem Statement:**  
Create a `Movie` class that collects ratings from multiple users and calculates statistics.

**Requirements:**
- `add_rating(user_id, score)` (score 1-5, one per user)
- `average_rating()` returns mean
- `rating_count()` returns number of ratings
- `rating_distribution()` returns count per score level

**Test Cases:**
- Ratings [5, 4, 4, 3] → avg=4.0, count=4
- Same user rates twice → updates, doesn't add

**Stretch:** Add `is_highly_rated(threshold)` method.

**Common Mistakes:**
- Duplicate user ratings
- Division by zero with no ratings

---

# 🟡 INTERMEDIATE LEVEL (I1–I25)
*Focus: Inheritance, polymorphism, interfaces, abstract classes, composition*

---

## I1: Shape Hierarchy with Inheritance

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Inheritance, abstract classes, method overriding

**Problem Statement:**  
Create an abstract `Shape` class with concrete subclasses `Circle`, `Rectangle`, and `Triangle`. Each must implement `area()` and `perimeter()`.

**Requirements:**
- Abstract `Shape` with abstract methods `area()`, `perimeter()`
- Each subclass stores necessary dimensions
- Add `describe()` method in base returning shape name
- Override `describe()` to include dimensions

**Test Cases:**
- Circle(r=5): area≈78.54, perimeter≈31.42
- Rectangle(4,6): area=24, perimeter=20
- Triangle(3,4,5): area=6, perimeter=12

**Stretch:** Add `scale(factor)` as base method calling abstract resize.

**Common Mistakes:**
- Forgetting to call `super()` in constructor
- Not marking methods as abstract/override

---

## I2: Employee Payroll System

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Inheritance hierarchy, different calculation strategies

**Problem Statement:**  
Create `Employee` base class with subclasses `SalariedEmployee`, `HourlyEmployee`, and `CommissionEmployee`. Each calculates pay differently.

**Requirements:**
- Base: name, id, `calculate_pay()` abstract
- SalariedEmployee: monthly salary
- HourlyEmployee: hours worked × hourly rate
- CommissionEmployee: base pay + (sales × commission rate)

**Test Cases:**
- Salaried($5000/month) → $5000
- Hourly(40hrs × $25) → $1000
- Commission($2000 base + $10000 sales × 10%) → $3000

**Stretch:** Add overtime calculation for hourly (1.5× after 40hrs).

**Common Mistakes:**
- Violating Liskov substitution with incompatible pay methods
- Not handling negative hours/sales

---

## I3: Vehicle Interface

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Interfaces, multiple implementations

**Problem Statement:**  
Define a `Driveable` interface with `start()`, `stop()`, `accelerate()`. Implement for `Car`, `Motorcycle`, and `ElectricScooter`.

**Requirements:**
- Interface defines contract only
- Each class implements differently (just print messages for now)
- Add `get_fuel_type()` → petrol/electric/diesel
- Store `current_speed` and update in accelerate

**Test Cases:**
- Car.start() → "Car engine started"
- ElectricScooter.accelerate() → silent acceleration message

**Stretch:** Add `Chargeable` interface for electric vehicles only.

**Common Mistakes:**
- Adding implementation in interface (pre-Java 8)
- Inconsistent method signatures

---

## I4: Payment Processing Polymorphism

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Runtime polymorphism, strategy pattern introduction

**Problem Statement:**  
Create a `PaymentMethod` interface with `process_payment(amount)`. Implement `CreditCard`, `PayPal`, `BankTransfer`, and `Crypto`.

**Requirements:**
- Each payment type has different validation rules
- Return success/failure with message
- Store transaction ID on success
- `get_fee()` returns processing fee (varies by type)

**Test Cases:**
- CreditCard: requires card number validation
- PayPal: requires email validation
- Crypto: requires wallet address format check

**Stretch:** Add `refund()` method with different refund policies.

**Common Mistakes:**
- Not handling payment failures gracefully
- Exposing sensitive data (card numbers)

---

## I5: Animal Kingdom Hierarchy

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Multi-level inheritance, method overriding chains

**Problem Statement:**  
Build inheritance: `Animal` → `Mammal`/`Bird`/`Fish` → specific species. Implement `speak()`, `move()`, `eat()`.

**Requirements:**
- Animal base: name, age, abstract methods
- Mammal adds `give_birth()`, Bird adds `lay_eggs()`
- Species: Dog, Cat, Eagle, Salmon
- Each overrides methods appropriately

**Test Cases:**
- Dog.speak() → "Woof"
- Eagle.move() → "Flying"
- Salmon.move() → "Swimming"

**Stretch:** Add `Habitat` association and dietary preferences.

**Common Mistakes:**
- Diamond problem awareness (if using multiple inheritance)
- Breaking the IS-A relationship logic

---

## I6: Notification Sender

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Interface segregation, multiple notification channels

**Problem Statement:**  
Create `NotificationChannel` interface with implementations for `EmailNotifier`, `SMSNotifier`, `PushNotifier`.

**Requirements:**
- Common: `send(message, recipient)`
- Each validates recipient format differently
- `supports_attachments()` varies by channel
- `max_message_length()` varies by channel

**Test Cases:**
- Email: supports attachments, no length limit
- SMS: 160 char limit, no attachments
- Push: 256 char limit, supports images

**Stretch:** Create `NotificationService` that routes to appropriate channel.

**Common Mistakes:**
- Fat interface with methods not all implementers need
- Not validating recipient format

---

## I7: Media Player Inheritance

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Template method pattern, common operations

**Problem Statement:**  
Create `MediaPlayer` base with `AudioPlayer` and `VideoPlayer` subclasses. Common: play, pause, stop. Different: rendering logic.

**Requirements:**
- Base handles state (playing/paused/stopped)
- `play()` calls abstract `render()` method
- AudioPlayer renders audio-only
- VideoPlayer renders audio + video frames

**Test Cases:**
- Play when stopped → starts from beginning
- Play when paused → resumes
- Stop → resets position to 0

**Stretch:** Add playlist support and shuffle mode.

**Common Mistakes:**
- Invalid state transitions (pause when stopped)
- Not resetting state properly

---

## I8: Document Export System

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Abstract class with concrete methods

**Problem Statement:**  
Create `DocumentExporter` abstract class with concrete `prepare()` and abstract `export()`. Implement `PDFExporter`, `HTMLExporter`, `MarkdownExporter`.

**Requirements:**
- `prepare()` validates document, gathers metadata (common)
- `export(document)` → format-specific string/bytes
- Add `get_file_extension()` and `get_mime_type()`

**Test Cases:**
- PDF: returns bytes, .pdf extension
- HTML: returns string with <html> tags
- Markdown: returns string with # headers

**Stretch:** Add `compress_output()` option.

**Common Mistakes:**
- Not calling `prepare()` before export
- Inconsistent encoding handling

---

## I9: Logging Framework

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Composition, multiple destinations

**Problem Statement:**  
Build a `Logger` that can write to multiple destinations using composition: `ConsoleLogger`, `FileLogger`, `DatabaseLogger`.

**Requirements:**
- `Log` interface: `log(level, message)`
- `CompositeLogger` holds multiple loggers
- Log levels: DEBUG, INFO, WARN, ERROR
- Each destination formats differently

**Test Cases:**
- Log to console + file simultaneously
- Filter by log level (only WARN+ to file)

**Stretch:** Add async logging capability.

**Common Mistakes:**
- Not handling destination failures gracefully
- Thread-safety issues in file writing

---

## I10: Game Character Composition

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Composition over inheritance, component-based design

**Problem Statement:**  
Create game character using composition: `Character` has `Weapon`, `Armor`, `Ability` components. Avoid deep inheritance.

**Requirements:**
- Character composes behavior from components
- `Weapon`: attack damage, range
- `Armor`: defense, weight
- `Ability`: special power, cooldown
- `calculate_stats()` aggregates component values

**Test Cases:**
- Character with Sword(10dmg) + Shield(5def) → attack=10, defense=5
- Swap weapon at runtime

**Stretch:** Add equipment slots limiting what can be equipped.

**Common Mistakes:**
- Using inheritance for equipment types
- Not handling null components

---

## I11: Restaurant Order System

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Association, aggregation relationships

**Problem Statement:**  
Model: `Restaurant` has `Menu` (aggregation), `Order` contains `OrderItems` (composition), `Customer` places `Orders`.

**Requirements:**
- Menu can exist without Restaurant
- OrderItems cannot exist without Order
- Order tracks status: pending/preparing/ready/delivered
- Calculate order total with tax

**Test Cases:**
- Add items, calculate subtotal + tax
- Change order status through lifecycle
- Customer views order history

**Stretch:** Add table assignment and waiter association.

**Common Mistakes:**
- Confusing aggregation vs composition semantics
- Not maintaining consistency between related objects

---

## I12: E-commerce Product Catalog

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Interface + abstract class combination

**Problem Statement:**  
Create `Sellable` interface and `Product` abstract class. Concrete: `PhysicalProduct`, `DigitalProduct`, `SubscriptionProduct`.

**Requirements:**
- Sellable: `get_price()`, `is_available()`
- Product: common attributes (name, description, sku)
- Physical: weight, dimensions, inventory count
- Digital: download link, file size
- Subscription: billing cycle, recurring price

**Test Cases:**
- Physical: check inventory before selling
- Digital: unlimited availability
- Subscription: price per billing cycle

**Stretch:** Add bundle products combining multiple items.

**Common Mistakes:**
- Physical-only attributes leaking to digital
- Not handling subscription renewal logic

---

## I13: School Management Classes

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Bidirectional associations, navigability

**Problem Statement:**  
Model: `School` → `Department` → `Teacher` and `Student`. Teachers teach `Courses`, Students enroll in Courses.

**Requirements:**
- Many-to-many: Students ↔ Courses
- One-to-many: Department → Teachers
- Teacher can access their courses
- Student can access their enrolled courses

**Test Cases:**
- Enroll student in course → appears in both student.courses and course.students
- Remove student → bidirectional cleanup

**Stretch:** Add prerequisites for courses.

**Common Mistakes:**
- Inconsistent bidirectional references
- Not handling enrollment limits

---

## I14: File System Composite

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Composite pattern, recursive structures

**Problem Statement:**  
Create `FileSystemItem` with `File` and `Folder` implementations. Folder contains FileSystemItems (recursive).

**Requirements:**
- `get_size()`: file returns size, folder sums children
- `get_path()`: returns full path from root
- `search(name)`: finds items matching name
- `display(indent)`: tree visualization

**Test Cases:**
- Folder with 3 files → size = sum of files
- Nested folders → correct path construction
- Search finds items at any depth

**Stretch:** Add file type filtering and modification timestamps.

**Common Mistakes:**
- Infinite loops in circular references
- Not handling empty folders

---

## I15: Plugin Architecture

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Interface-based extensibility, dependency inversion

**Problem Statement:**  
Design a plugin system where `Application` loads `Plugin` implementations dynamically. Plugins extend app functionality.

**Requirements:**
- `Plugin` interface: `initialize()`, `execute()`, `shutdown()`
- Application manages plugin lifecycle
- Plugins can access limited app context
- `PluginManager` loads/unloads plugins

**Test Cases:**
- Load plugin → initialize called
- Execute plugin action
- Shutdown gracefully

**Stretch:** Add plugin dependencies and load ordering.

**Common Mistakes:**
- Tight coupling between app and plugins
- Not handling plugin failures gracefully

---

## I16: Observer Pattern - Weather Station

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Observer pattern, decoupled notification

**Problem Statement:**  
Create `WeatherStation` (subject) that notifies `Display` observers when temperature/humidity changes.

**Requirements:**
- `Subject` interface: `attach()`, `detach()`, `notify()`
- `Observer` interface: `update(data)`
- Multiple displays: Current, Statistics, Forecast
- Each display formats data differently

**Test Cases:**
- Update weather → all displays notified
- Detach one display → no longer receives updates
- Multiple updates → latest data shown

**Stretch:** Add filtering (some displays only care about temperature).

**Common Mistakes:**
- Memory leaks from not detaching observers
- Notifying in inconsistent state

---

## I17: Strategy Pattern - Shipping Calculator

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Strategy pattern, runtime algorithm selection

**Problem Statement:**  
Create `ShippingCalculator` that uses different `ShippingStrategy` implementations: Standard, Express, Overnight, Pickup.

**Requirements:**
- Strategy interface: `calculate_cost(weight, distance)`
- Each strategy has different formula
- Pickup always returns 0
- Calculator can switch strategy at runtime

**Test Cases:**
- Standard: $5 base + $0.50/lb + $0.10/mile
- Express: 2× standard cost
- Overnight: 3× standard + $20 flat fee

**Stretch:** Add region-based pricing variations.

**Common Mistakes:**
- Hardcoding strategies instead of injecting
- Not validating weight/distance inputs

---

## I18: Decorator Pattern - Coffee Shop

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Decorator pattern, dynamic behavior extension

**Problem Statement:**  
Create `Beverage` abstract class with decorators for add-ons: Milk, Whip, Mocha, Soy. Each adds to cost and description.

**Requirements:**
- Base beverages: Espresso, HouseBlend, DarkRoast
- Each decorator wraps a beverage and modifies `cost()` and `description()`
- Multiple decorators can stack

**Test Cases:**
- Espresso → $1.99
- Espresso + Milk → $2.19
- DarkRoast + Mocha + Mocha + Whip → $1.49 + 0.20 + 0.20 + 0.10

**Stretch:** Add size multiplier (tall/grande/venti).

**Common Mistakes:**
- Breaking decorator chain
- Decorating wrong object (modify and return new)

---

## I19: Factory Pattern - Document Creator

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Factory method pattern, decoupled object creation

**Problem Statement:**  
Create `DocumentFactory` that produces `Document` objects (Resume, Report, Letter) based on type parameter.

**Requirements:**
- Factory method takes document type enum/string
- Returns appropriate Document subclass
- Each document type has different template structure
- Factory hides instantiation logic

**Test Cases:**
- create("resume") → Resume instance with sections
- create("report") → Report with title, body, summary
- create("unknown") → error or default

**Stretch:** Add document configuration options to factory.

**Common Mistakes:**
- Switch statements in factory (use registry instead)
- Returning wrong document type

---

## I20: Builder Pattern - Meal Builder

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Builder pattern, step-by-step construction

**Problem Statement:**  
Create `MealBuilder` that constructs `Meal` objects with burger, drink, side, and dessert. Different meal combos.

**Requirements:**
- `MealBuilder`: `add_burger()`, `add_drink()`, `add_side()`, `add_dessert()`, `build()`
- Fluent interface (method chaining)
- Director class with preset combos: KidsMeal, ValueMeal, DeluxeMeal
- Calculate total calories and price

**Test Cases:**
- KidsMeal: small burger, juice, fries → $4.99
- Empty meal → validation error or empty meal

**Stretch:** Add customization options (no pickles, extra cheese).

**Common Mistakes:**
- Not resetting builder after build()
- Missing required components validation

---

## I21: Liskov Substitution Violation Exercise

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** LSP violation detection and fixing

**Problem Statement:**  
Given a `Bird` class with `fly()` method, and `Penguin` (can't fly) inheriting from it - identify the LSP violation and refactor.

**Requirements:**
- Identify why Penguin extending Bird with fly() violates LSP
- Propose solution using interfaces: `Flyable`, `Swimmable`
- Refactor so Penguin doesn't falsely inherit fly()
- Ensure all birds can still be treated polymorphically for common behaviors

**Test Cases:**
- Original: penguin.fly() throws or returns error (violation)
- Fixed: Flyable interface only on flying birds

**Stretch:** Add more edge cases (Ostrich, Kiwi, Bat).

**Common Mistakes:**
- Making fly() return "can't fly" (still violation)
- Over-engineering with too many interfaces

---

## I22: Interface Segregation Refactoring

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** ISP violation detection and fixing

**Problem Statement:**  
Given a fat `Worker` interface with `work()`, `eat()`, `sleep()`, `code()`, `manage()` - refactor into smaller, focused interfaces.

**Requirements:**
- Identify which methods belong together
- Create focused interfaces: `Workable`, `Eatable`, `Developer`, `Manager`
- Implement classes that use only needed interfaces
- Robot worker doesn't need eat() or sleep()

**Test Cases:**
- HumanWorker implements Workable, Eatable
- RobotWorker implements only Workable
- Manager implements Workable, Manager (not Developer)

**Stretch:** Apply to a real-world multi-function device (printer/scanner/fax).

**Common Mistakes:**
- Creating too many micro-interfaces
- Breaking existing code that depends on original interface

---

## I23: Dependency Injection Container

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Dependency inversion, IoC container basics

**Problem Statement:**  
Create a simple `DIContainer` that registers and resolves dependencies. Classes declare dependencies in constructor.

**Requirements:**
- `register(interface, implementation)`
- `resolve(interface)` returns instance with dependencies injected
- Handle transient (new each time) vs singleton lifetimes
- Detect circular dependencies

**Test Cases:**
- Register ILogger → ConsoleLogger, resolve → instance
- UserService depends on ILogger → auto-injected
- A depends on B, B depends on A → error

**Stretch:** Add property injection and named registrations.

**Common Mistakes:**
- Infinite loops in circular dependencies
- Not handling missing registrations

---

## I24: Proxy Pattern - Image Loader

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Proxy pattern, lazy loading, access control

**Problem Statement:**  
Create `ImageProxy` that lazy-loads expensive `RealImage` objects only when `display()` is called.

**Requirements:**
- `Image` interface with `display()` method
- `RealImage` loads from disk in constructor (expensive)
- `ImageProxy` defers loading until first display()
- Both implement same interface

**Test Cases:**
- Create proxy → no loading yet
- First display() → loads and displays
- Second display() → uses cached image

**Stretch:** Add cache expiration and reload capability.

**Common Mistakes:**
- Loading in proxy constructor (defeats purpose)
- Not forwarding all interface methods

---

## I25: Adapter Pattern - Legacy Integration

**Difficulty:** ⭐⭐⭐ Medium-Hard  
**Concepts:** Adapter pattern, interface translation

**Problem Statement:**  
Adapt `LegacyPrinter` (with `printDocument(text)`) to work with new `ModernPrinter` interface (with `print(Document)`).

**Requirements:**
- Create adapter implementing ModernPrinter
- Internally delegates to LegacyPrinter
- Translate Document object to text for legacy
- Client code only knows about ModernPrinter

**Test Cases:**
- Create adapter wrapping legacy printer
- Call print(document) → legacy printDocument called
- Verify text conversion happens correctly

**Stretch:** Create two-way adapter for bidirectional compatibility.

**Common Mistakes:**
- Modifying legacy code directly
- Leaking legacy interface details through adapter

---

# 🟠 ADVANCED LEVEL (A1–A25)
*Focus: SOLID principles, design patterns, generics, collections, error handling, serialization*

---

## A1: Single Responsibility Principle Refactoring

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** SRP, code decomposition, cohesion

**Problem Statement:**  
Given a `UserManager` class that handles authentication, authorization, user CRUD, email notifications, and logging - refactor into focused classes.

**Requirements:**
- Identify 5+ distinct responsibilities in original class
- Extract: `AuthService`, `UserRepository`, `EmailService`, `Logger`, `AuthorizationPolicy`
- Each class has single reason to change
- Maintain original functionality via composition

**Test Cases:**
- All existing features still work after refactoring
- Changing email logic doesn't affect auth logic
- Each class can be tested independently

**Stretch:** Create façade that provides original API for backward compatibility.

**Common Mistakes:**
- Over-splitting into too many tiny classes
- Breaking dependencies without proper injection

---

## A2: Open-Closed Principle - Tax Calculator

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** OCP, extensibility without modification

**Problem Statement:**  
Create a tax calculator that can handle new tax rules without modifying existing code. Add regions: US, UK, Canada, Germany.

**Requirements:**
- `TaxCalculator` closed for modification
- Open for extension via `TaxRule` implementations
- Each rule knows its jurisdiction and calculation formula
- Register new rules without changing calculator code

**Test Cases:**
- Add new country tax rule → no existing code changes
- Calculate for product in US vs UK → different results
- Combine multiple rules (federal + state)

**Stretch:** Add date-effective tax rules (changes over time).

**Common Mistakes:**
- Modifying calculator when adding new tax types
- Hardcoding rule selection logic

---

## A3: Command Pattern - Undo/Redo Editor

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Command pattern, undo stack, memento

**Problem Statement:**  
Create a text editor with undo/redo functionality using command pattern. Support: insert, delete, replace, bold, italic.

**Requirements:**
- `Command` interface: `execute()`, `undo()`
- Each action creates a command object
- `CommandHistory` manages undo/redo stack
- Redo discarded on new action

**Test Cases:**
- Type, undo → text removed
- Undo, redo → text restored
- Type after undo → redo stack cleared

**Stretch:** Add macro recording (chain of commands).

**Common Mistakes:**
- Not storing enough state for undo
- Breaking redo on unrelated actions

---

## A4: State Pattern - Vending Machine

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** State pattern, finite state machine

**Problem Statement:**  
Model a vending machine with states: Idle, HasMoney, Dispensing, SoldOut. Transitions based on user actions.

**Requirements:**
- `VendingMachineState` interface
- Each state handles: `insertCoin()`, `selectProduct()`, `dispense()`
- Invalid actions in current state → appropriate response
- State transitions managed internally

**Test Cases:**
- Idle + insert coin → HasMoney
- HasMoney + select → Dispensing (if stocked)
- SoldOut + any action → "Machine empty" message

**Stretch:** Add refund functionality and multiple product slots.

**Common Mistakes:**
- Giant if-else instead of state objects
- Missing edge case transitions

---

## A5: Chain of Responsibility - Request Pipeline

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Chain of responsibility, middleware pattern

**Problem Statement:**  
Build an HTTP request pipeline with handlers: Authentication, Logging, Validation, RateLimiting, ActualProcessor.

**Requirements:**
- `Handler` interface with `handle()` and `setNext()`
- Each handler can process or pass to next
- Short-circuit on failure (401, 400, 429)
- Order matters: auth before validation

**Test Cases:**
- Valid request → all handlers pass → response
- Invalid auth → stops at auth handler, 401
- Rate limited → stops at rate limiter, 429

**Stretch:** Add async handler support and timeout handling.

**Common Mistakes:**
- Forgetting to call next handler
- Wrong handler order causing security issues

---

## A6: Generics - Type-Safe Container

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Generics, type parameters, constraints

**Problem Statement:**  
Create generic `Box<T>`, `Pair<K,V>`, and bounded `NumberBox<T: Number>` containers with type-safe operations.

**Requirements:**
- `Box<T>`: stores single item, get/set
- `Pair<K,V>`: stores key-value, swap operation
- `NumberBox<T>`: only numbers, add arithmetic methods
- Compare two boxes of same type

**Test Cases:**
- Box<String>.set("hello") works
- NumberBox<Int>.add(5) works
- Box<String> + Box<Int> comparison → compile error

**Stretch:** Implement covariance/contravariance examples.

**Common Mistakes:**
- Forgetting type bounds
- Generic array creation issues (Java)

---

## A7: Generic Repository Pattern

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Generics, repository pattern, CRUD abstraction

**Problem Statement:**  
Create `Repository<T, ID>` interface with implementations: `InMemoryRepository`, `FileRepository`. Type-safe CRUD for any entity.

**Requirements:**
- `save(entity)`, `findById(id)`, `findAll()`, `delete(id)`
- Entity must have ID property (constraint)
- InMemory uses dictionary/map
- File persists to JSON

**Test Cases:**
- UserRepository<User, UUID> works
- ProductRepository<Product, Long> works
- Find by ID returns correct type (not Object)

**Stretch:** Add query builder with type-safe filters.

**Common Mistakes:**
- Returning raw Object instead of T
- Not constraining T to have ID

---

## A8: Equality and HashCode

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** equals(), hashCode(), identity vs equality

**Problem Statement:**  
Create `Person` class with proper equals/hashCode based on id. Create `Money` value object with equals based on amount+currency.

**Requirements:**
- `Person`: entity equality (same id = same person)
- `Money`: value equality (same amount+currency)
- Implement both equals() and hashCode() correctly
- Test with HashSet and HashMap

**Test Cases:**
- Person(1) == Person(1) even with different names
- Money(100, "USD") == Money(100, "USD")
- HashSet effectively deduplicates

**Stretch:** Implement Comparable for sorting.

**Common Mistakes:**
- Implementing equals without hashCode (or vice versa)
- Using mutable fields in hashCode
- Violating equals contract (transitivity, symmetry)

---

## A9: Comparator and Sorting

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Comparable, Comparator, sorting strategies

**Problem Statement:**  
Create `Employee` that can be sorted by name, salary, hire date, or department with customizable comparators.

**Requirements:**
- Implement `Comparable` for natural ordering (by id)
- Create separate `Comparator` instances for each field
- Chain comparators (sort by department, then salary)
- Null-safe comparisons

**Test Cases:**
- Sort by salary descending
- Sort by department ASC, then name ASC
- Handle null department values

**Stretch:** Create ComparatorBuilder with fluent API.

**Common Mistakes:**
- NPE on null field comparison
- Inconsistent ordering causing sort instability

---

## A10: Custom Iterator

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Iterator pattern, lazy evaluation, fail-fast

**Problem Statement:**  
Create custom `LinkedList<T>` with `Iterator<T>` supporting traversal, removal during iteration, and fail-fast behavior.

**Requirements:**
- Implement Iterator interface fully
- `hasNext()`, `next()`, `remove()`
- Fail-fast: throw ConcurrentModificationException if list modified
- Use modification count tracking

**Test Cases:**
- Iterate through all elements
- Remove via iterator → works
- Modify list during iteration → exception

**Stretch:** Implement reverse iterator and indexed iterator.

**Common Mistakes:**
- Not tracking modifications
- Iterator invalidation after removal

---

## A11: Custom Exception Hierarchy

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Exception design, checked vs unchecked

**Problem Statement:**  
Design exception hierarchy for banking system: `BankingException` → `InsufficientFundsException`, `AccountNotFoundException`, `InvalidTransactionException`, `FraudDetectedException`.

**Requirements:**
- Custom base exception with error code and timestamp
- Each subtype carries relevant context data
- Include helpful error messages
- Proper use of checked vs unchecked pattern

**Test Cases:**
- InsufficientFunds carries balance and attempted amount
- AccountNotFound carries account number searched
- All exceptions can be caught by base type

**Stretch:** Add exception translation layer for external APIs.

**Common Mistakes:**
- Not preserving cause chain
- Missing serialVersionUID
- Using exceptions for flow control

---

## A12: Exception Handling Strategies

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Exception wrapping, retry, fallback patterns

**Problem Statement:**  
Create `RetryableOperation<T>` that retries on transient failures and `CircuitBreaker` that prevents calls to failing services.

**Requirements:**
- Retry with configurable attempts and backoff
- Circuit breaker states: Closed, Open, HalfOpen
- Fallback values on final failure
- Proper exception wrapping and logging

**Test Cases:**
- Transient failure, retry 3x → eventual success
- Permanent failure → fallback value
- Too many failures → circuit opens

**Stretch:** Add exponential backoff and jitter.

**Common Mistakes:**
- Retrying non-transient errors
- Not resetting circuit breaker properly

---

## A13: Singleton Variations

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Singleton patterns, thread safety, anti-patterns

**Problem Statement:**  
Implement Singleton in 4 ways: lazy, eager, double-checked locking, and enum-based (Java). Discuss trade-offs.

**Requirements:**
- Lazy: created on first access
- Eager: created at class load
- Double-checked: thread-safe lazy
- Enum: simplest, serialization-safe
- All must prevent multiple instantiation

**Test Cases:**
- Multiple threads request → same instance
- Serialization/deserialization → same instance
- Reflection attack → prevented (enum only)

**Stretch:** Make singleton testable with resettable hook.

**Common Mistakes:**
- Non-thread-safe lazy implementation
- Serialization creating new instance
- Making singleton a global mutable state holder

---

## A14: Abstract Factory - UI Themes

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Abstract factory, family of objects

**Problem Statement:**  
Create abstract factory for UI component families: `LightThemeFactory` and `DarkThemeFactory` producing Button, TextField, Checkbox.

**Requirements:**
- `UIFactory` interface with create methods
- Each theme produces consistent component family
- Components share interface but differ in appearance
- Client code theme-agnostic

**Test Cases:**
- LightFactory.createButton() → LightButton
- DarkFactory.createButton() → DarkButton
- Switch factory → entire UI theme changes

**Stretch:** Add high-contrast accessibility theme.

**Common Mistakes:**
- Mixing components from different factories
- Not maintaining consistency in factory output

---

## A15: Memento Pattern - Game Save System

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Memento pattern, state snapshots

**Problem Statement:**  
Create game save system using memento. `GameState` creates/restores mementos. `SaveManager` stores multiple save slots.

**Requirements:**
- `Memento` captures game state (position, inventory, health)
- `GameState` (originator) creates and restores mementos
- `SaveManager` (caretaker) stores list of mementos
- Mementos are opaque to SaveManager

**Test Cases:**
- Save game → memento created
- Load game → state restored exactly
- Multiple save slots → independent states

**Stretch:** Add save metadata (timestamp, thumbnail, description).

**Common Mistakes:**
- Exposing memento internals
- Breaking encapsulation of game state

---

## A16: Visitor Pattern - AST Evaluator

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Visitor pattern, double dispatch

**Problem Statement:**  
Create simple expression AST with `NumberNode`, `AddNode`, `SubtractNode`, `MultiplyNode`. Use visitor for evaluation, printing, and optimization.

**Requirements:**
- Each node accepts a visitor
- `EvaluatorVisitor` calculates result
- `PrintVisitor` generates string representation
- `OptimizerVisitor` simplifies constant expressions

**Test Cases:**
- Evaluate: (5 + 3) * 2 → 16
- Print: "((5 + 3) * 2)"
- Optimize: 3 + 5 → 8 (constant folding)

**Stretch:** Add variables and assignment nodes.

**Common Mistakes:**
- Forgetting to implement visit for all node types
- Breaking double dispatch mechanism

---

## A17: Flyweight Pattern - Character Rendering

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Flyweight pattern, memory optimization

**Problem Statement:**  
Create text rendering system where character glyphs are shared (flyweight) but positions are extrinsic.

**Requirements:**
- `CharacterGlyph` (intrinsic): font data shared
- `CharacterContext` (extrinsic): position, color per instance
- `GlyphFactory` caches and reuses glyphs
- Memory usage much lower than creating new glyph per character

**Test Cases:**
- Render 10000 'A' characters → only 1 'A' glyph
- Different fonts → separate glyphs
- Memory measurement shows savings

**Stretch:** Add glyph caching with LRU eviction.

**Common Mistakes:**
- Storing extrinsic state in flyweight
- Not properly separating concerns

---

## A18: JSON Serialization

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Serialization, DTOs, object mapping

**Problem Statement:**  
Create custom JSON serializer/deserializer using reflection. Support: primitives, lists, nested objects, custom formatters.

**Requirements:**
- `serialize(object)` → JSON string
- `deserialize(json, Class<T>)` → T instance
- Handle nested objects recursively
- Custom annotations for field names, date formats

**Test Cases:**
- Simple object → valid JSON
- Nested object → nested JSON
- Deserialize back → equal object

**Stretch:** Handle circular references with object ID.

**Common Mistakes:**
- Not handling null values
- Infinite recursion on circular references
- Date format inconsistencies

---

## A19: Repository with Unit of Work

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Unit of Work pattern, transaction management

**Problem Statement:**  
Implement `UnitOfWork` that tracks changes across multiple repositories and commits/rolls back atomically.

**Requirements:**
- Track inserted, updated, deleted entities
- `commit()` persists all changes
- `rollback()` discards changes
- Repositories obtained from UnitOfWork

**Test Cases:**
- Add user, add order → commit → both persisted
- Add user, add order → rollback → neither persisted
- Exception during commit → all changes rolled back

**Stretch:** Add change tracking with dirty checking.

**Common Mistakes:**
- Not rolling back on partial failure
- Orphaned entity references

---

## A20: Event Sourcing Basics

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Event sourcing, event store, projections

**Problem Statement:**  
Create simple event-sourced `BankAccount` where all changes are events: `AccountOpened`, `MoneyDeposited`, `MoneyWithdrawn`.

**Requirements:**
- State reconstructed from event history
- Append-only event store
- Aggregate root applies events
- Projection builds current balance from events

**Test Cases:**
- Apply 3 events → state matches
- Replay from empty → same final state
- Event history is immutable

**Stretch:** Add event versioning and schema evolution.

**Common Mistakes:**
- Mutating events after storage
- Inconsistent event ordering

---

## A21: Specification Pattern

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Specification pattern, composable business rules

**Problem Statement:**  
Create `Specification<T>` pattern for complex filtering: combine `AndSpec`, `OrSpec`, `NotSpec` with business rules.

**Requirements:**
- `isSatisfiedBy(candidate)` returns boolean
- `and()`, `or()`, `not()` combine specifications
- Business specs: `EligibleForDiscount`, `LivesInRegion`, `HasMinPurchases`
- Apply to customer filtering

**Test Cases:**
- Customer meets single spec → passes
- Customer meets AND of two specs → passes
- NOT(spec) inverts result

**Stretch:** Add specification repository for reusable queries.

**Common Mistakes:**
- Evaluating multiple times (cache results)
- Complex nested specs becoming unreadable

---

## A22: Null Object Pattern

**Difficulty:** ⭐⭐ Medium  
**Concepts:** Null object pattern, avoiding null checks

**Problem Statement:**  
Replace null checks for `Logger`, `TaxCalculator`, and `Notifier` with null object implementations that do nothing safely.

**Requirements:**
- `NullLogger` implements Logger, logs nothing
- `NoTaxCalculator` returns 0 tax
- `NullNotifier` sends no notifications
- Client code has no null checks

**Test Cases:**
- NullLogger.log("message") → no output, no error
- NoTaxCalculator.calculate() → 0
- Code works identically with null or real object

**Stretch:** Add logging to null objects for debugging.

**Common Mistakes:**
- Null object having side effects
- Returning null object where actual data expected

---

## A23: Template Method - Data Parser

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Template method pattern, hook methods

**Problem Statement:**  
Create `DataParser` base with template method `parse()`. Subclasses: `CSVParser`, `XMLParser`, `JSONParser` override specific steps.

**Requirements:**
- Template: `openFile()`, `readRaw()`, `parseRecords()`, `validate()`, `closeFile()`
- Subclasses override only parseRecords()
- Hook methods for optional preprocessing
- Common validation in base class

**Test Cases:**
- CSV parsing uses CSV-specific record parsing
- All parsers: open → read → parse → validate → close
- Invalid data caught in validation step

**Stretch:** Add error recovery hooks.

**Common Mistakes:**
- Making template method overridable
- Skipping steps in subclass overrides

---

## A24: Facade Pattern - Home Automation

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Facade pattern, simplified interface

**Problem Statement:**  
Create `HomeTheaterFacade` that coordinates: TV, SoundSystem, Lights, BlindsCurtains, StreamingDevice. Simplified operations.

**Requirements:**
- Complex subsystems with many individual controls
- Facade: `watchMovie()`, `endMovie()`, `playMusic()`, `goodnight()`
- Each facade method orchestrates multiple subsystems
- Subsystems still independentlywe usable

**Test Cases:**
- watchMovie() → dims lights, lowers blinds, turns on TV, sets surround sound
- endMovie() → reverses all
- Subsystem failure → graceful degradation

**Stretch:** Add scene presets and scheduling.

**Common Mistakes:**
- Facade becoming too complex
- Hiding useful subsystem functionality

---

## A25: Mediator Pattern - Chat Room

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Mediator pattern, decoupled communication

**Problem Statement:**  
Create `ChatRoom` mediator that manages communication between `User` objects. Users don't reference each other directly.

**Requirements:**
- Users only know about ChatRoom
- `sendMessage(user, message)` broadcasts to others
- Private message: `sendPrivate(from, to, message)`
- User join/leave tracked by room

**Test Cases:**
- User A sends → all others receive
- User B leaves → no longer receives
- Private message → only recipient sees

**Stretch:** Add chat rooms (multiple mediators) and user blocking.

**Common Mistakes:**
- Users directly referencing each other
- Mediator knowing too much about user internals

---

# 🔴 EXPERT TRACK (E1–E10)
*Focus: Concurrency, testing, architecture, domain modeling*

---

## E1: Thread-Safe Singleton

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Thread safety, double-checked locking, volatile

**Problem Statement:**  
Create a thread-safe lazy Singleton that works under high concurrency. Test with multiple threads requesting the instance simultaneously.

**Requirements:**
- Instance created only once even with 100 concurrent requests
- Proper use of synchronization/locks
- Double-checked locking pattern or language-specific idioms
- Performance: minimal lock contention after initialization

**Test Cases:**
- 100 threads → all get same instance
- Timing test: no race conditions
- Memory model correctness (happens-before)

**Stretch:** Create a thread-safe object pool with max size.

**Common Mistakes:**
- Non-volatile double-checked locking
- Excessive synchronization hurting performance

---

## E2: Producer-Consumer with Bounded Buffer

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Concurrency, blocking queues, wait/notify

**Problem Statement:**  
Implement a bounded buffer (`BlockingQueue`) with producer and consumer threads. Handle full/empty conditions correctly.

**Requirements:**
- `put(item)` blocks when buffer full
- `take()` blocks when buffer empty
- Multiple producers/consumers work safely
- No busy-waiting (use proper signaling)

**Test Cases:**
- Producer faster → blocks when full
- Consumer faster → blocks when empty
- Throughput test under load

**Stretch:** Add timeout versions of put/take.

**Common Mistakes:**
- Lost wakeups (check condition in loop)
- Spurious wakeups not handled
- Deadlock between producers and consumers

---

## E3: Read-Write Lock Implementation

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Reader-writer problem, concurrency primitives

**Problem Statement:**  
Create a read-write lock allowing multiple readers OR one writer. Writers have priority to prevent starvation.

**Requirements:**
- Multiple readers can hold lock simultaneously
- Writer gets exclusive access
- Writer priority: readers wait while writers pending
- Fair mode option (FIFO)

**Test Cases:**
- 10 readers, 1 writer → writer eventually gets lock
- Reader during write → waits
- Writer starvation prevented

**Stretch:** Add lock upgrade (reader to writer) capability.

**Common Mistakes:**
- Reader starvation in strict writer priority
- Deadlock when upgrading read to write lock

---

## E4: Unit Testing with Mocks

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** Unit testing, mocking, dependency injection, test isolation

**Problem Statement:**  
Test `OrderService` that depends on `InventoryService`, `PaymentGateway`, and `EmailService`. Mock all dependencies.

**Requirements:**
- Create mock implementations or use mocking framework
- Test happy path: order placed, payment processed, email sent
- Test failure: payment fails → no email, no inventory change
- Verify mock interactions (called with correct args)

**Test Cases:**
- Verify `chargeCard()` called with correct amount
- Verify `sendEmail()` called once on success
- Verify `deductStock()` not called on payment failure

**Stretch:** Add test coverage metrics and edge case tests.

**Common Mistakes:**
- Testing implementation instead of behavior
- Over-mocking (every object mocked)
- Brittle tests tied to method call counts

---

## E5: TDD Exercise - String Calculator Kata

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** TDD, red-green-refactor cycle

**Problem Statement:**  
Build a `StringCalculator.add(string)` using strict TDD. Start simple, add features incrementally with tests first.

**Requirements (grow incrementally):**
1. Empty string → 0
2. Single number → that number
3. Two numbers → sum
4. Handle unknown amount of numbers
5. Handle newlines as delimiters
6. Support custom delimiters: "//[delimiter]\n..."
7. Negative numbers throw exception listing all negatives

**Test Cases:**
- Write test first, then code, then refactor
- Each step adds 1-2 tests before implementation
- Final: "//;\n1;2" → 3

**Stretch:** Add multiple character and multiple delimiters support.

**Common Mistakes:**
- Writing code before test (defeats TDD)
- Giant leaps instead of baby steps
- Not refactoring in the refactor step

---

## E6: Layered Architecture Implementation

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Clean architecture, separation of concerns, dependency rule

**Problem Statement:**  
Build a small "User Registration" feature with proper layers: Domain, Application, Infrastructure, Presentation. Enforce dependency rule.

**Requirements:**
- Domain: User entity, UserRepository interface
- Application: RegisterUserUseCase
- Infrastructure: DatabaseUserRepository, EmailService
- Presentation: Controller/Handler
- Inner layers don't depend on outer

**Test Cases:**
- Domain compiles without infrastructure imports
- Use case testable with mock repository
- Infrastructure replaceable without domain changes

**Stretch:** Add anti-corruption layer for external API integration.

**Common Mistakes:**
- Domain depending on ORM/framework
- Application layer knowing about HTTP
- Circular dependencies between layers

---

## E7: Domain-Driven Design - Value Objects

**Difficulty:** ⭐⭐⭐ Hard  
**Concepts:** DDD, value objects, immutability, domain modeling

**Problem Statement:**  
Create value objects for e-commerce: `Money`, `Email`, `Address`, `PhoneNumber`. Enforce invariants in constructors.

**Requirements:**
- Value objects are immutable
- Equality based on attributes
- Factory methods for validation
- Operations return new instances (e.g., Money.add())

**Test Cases:**
- Money(100, "USD") == Money(100, "USD") → true
- Money(100, "USD") + Money(50, "USD") → Money(150, "USD")
- Invalid email format → exception

**Stretch:** Add conversion methods (Money currency conversion).

**Common Mistakes:**
- Mutable value objects
- Primitive obsession (using strings for email)
- Missing validation in constructor

---

## E8: Code Smells and Refactoring Kata

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Code smells, refactoring techniques, clean code

**Problem Statement:**  
Given deliberately bad code (long method, feature envy, God class, primitive obsession), identify smells and refactor systematically.

**Requirements:**
- Identify 5+ code smells in provided code
- Apply appropriate refactoring for each:
  - Extract Method, Extract Class
  - Replace conditional with polymorphism
  - Introduce Parameter Object
- Maintain behavior (tests pass throughout)

**Test Cases:**
- All existing tests still pass after each refactoring
- No single method over 10 lines
- Classes have single responsibility

**Stretch:** Add new feature to refactored code showing improved extensibility.

**Common Mistakes:**
- Refactoring without tests
- Too many changes at once
- Making code worse before making it better

---

## E9: Repository and Query Object

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** Repository pattern, specification/query objects

**Problem Statement:**  
Create rich `UserRepository` with `Query` object for complex queries: filter by status, sort by date, paginate, include relations.

**Requirements:**
- Repository interface with simple CRUD
- Query object for complex searches: `find(query)`
- Query builder: `Query.where(...).orderBy(...).limit(...)`
- Apply to in-memory and SQL implementations

**Test Cases:**
- Active users, sorted by name, page 2 → correct subset
- Query reusable: apply same query to different repos
- SQL implementation generates correct WHERE clause

**Stretch:** Add caching layer with query-based cache keys.

**Common Mistakes:**
- Leaking SQL into repository interface
- Query objects tied to specific persistence

---

## E10: Aggregate Root Design

**Difficulty:** ⭐⭐⭐⭐ Very Hard  
**Concepts:** DDD aggregates, invariants, transactional boundaries

**Problem Statement:**  
Design `Order` aggregate with `OrderLines`. Ensure invariants (max items, valid total) maintained. Only save via aggregate root.

**Requirements:**
- Order is aggregate root
- OrderLine accessible only through Order
- Invariants checked on any modification
- Repository saves entire aggregate transactionally

**Test Cases:**
- Add line → order total updated
- Add line exceeding max → rejected
- Cannot save OrderLine directly

**Stretch:** Add domain events for cross-aggregate communication.

**Common Mistakes:**
- Exposing internal collections
- Breaking invariants through direct child access
- Aggregate too large (performance issues)

---

# 🏆 CAPSTONE PROJECTS (C1–C5)
*End-to-end systems requiring object modeling, patterns, and clean design*

---

## C1: Library Management System

**Difficulty:** ⭐⭐⭐⭐⭐ Expert  
**Concepts:** Full OOP ecosystem, CRUD, relationships, business rules

**Problem Statement:**  
Build a library system: books, members, borrowing, returns, reservations, fines. Apply OOP throughout.

**Core Requirements:**
- **Entities:** Book, Member, Loan, Reservation, Fine
- **Features:** 
  - Borrow book (check availability, max loans per member)
  - Return book (calculate fine if late)
  - Reserve book (queue for unavailable books)
  - Search books by title, author, ISBN
  - Member history

**OOP Concepts to Apply:**
- Inheritance: MemberType (Student, Faculty, Public) with different limits
- Polymorphism: Fine calculation varies by member type
- Composition: Library contains Books, Members
- Interfaces: Searchable, Borrowable, Reservable
- State pattern: Book states (Available, Borrowed, Reserved, Lost)

**Design Patterns:**
- Factory: Create book/member instances
- Observer: Notify when reserved book available
- Strategy: Different fine calculation strategies

**Refactoring Journey:**
1. Start with basic procedural structure
2. Extract classes for each domain concept
3. Apply SOLID principles
4. Add design patterns where beneficial
5. Write comprehensive tests

**Acceptance Criteria:**
- [ ] All core features work
- [ ] No method over 20 lines
- [ ] Each class has single responsibility
- [ ] 80%+ test coverage
- [ ] Clean, documented code

---

## C2: Banking / Digital Wallet System

**Difficulty:** ⭐⭐⭐⭐⭐ Expert  
**Concepts:** Financial systems, transactions, audit trails, security

**Problem Statement:**  
Build a banking system: accounts, transfers, transaction history, statements, multi-currency support.

**Core Requirements:**
- **Entities:** Account, Transaction, Customer, Currency, Statement
- **Features:**
  - Account operations: deposit, withdraw, transfer
  - Transaction history with filtering
  - Monthly statement generation
  - Multi-currency with exchange rates
  - Fraud detection rules

**OOP Concepts to Apply:**
- Value Objects: Money (amount + currency), AccountNumber
- Aggregates: Account with transactions
- Interfaces: PaymentProcessor, FraudDetector
- Inheritance: AccountType (Savings, Checking, Business)
- Encapsulation: Balance never directly modified

**Design Patterns:**
- Command: Transaction as command (undoable transfers)
- Observer: Fraud alerts on suspicious activity
- Decorator: Add features to accounts (overdraft, interest)
- Factory: Create appropriate account types
- Event Sourcing: Transaction log is ground truth

**Refactoring Journey:**
1. Basic account with deposit/withdraw
2. Add transaction logging
3. Extract money as value object
4. Add transfer as aggregate operation
5. Implement fraud detection with strategy pattern

**Acceptance Criteria:**
- [ ] Money never uses float/double (use proper decimal)
- [ ] All operations are atomic
- [ ] Audit trail for all changes
- [ ] Thread-safe for concurrent operations
- [ ] Comprehensive exception handling

---

## C3: E-commerce Cart + Promotions Engine

**Difficulty:** ⭐⭐⭐⭐⭐ Expert  
**Concepts:** Pricing rules, composable discounts, extensibility

**Problem Statement:**  
Build shopping cart with complex promotions: percentage off, BOGO, bundle discounts, coupon codes, tiered pricing.

**Core Requirements:**
- **Entities:** Product, CartItem, Cart, Promotion, Coupon, Order
- **Features:**
  - Add/remove/update cart items
  - Apply multiple promotions (stackable or exclusive)
  - Coupon code validation and application
  - Calculate final price with tax
  - Checkout and order creation

**OOP Concepts to Apply:**
- Composition: Cart contains CartItems
- Polymorphism: Promotion types with different `apply()` logic
- Specification: Promotion eligibility rules
- Value Objects: Price, Quantity

**Design Patterns:**
- Strategy: Different promotion calculation strategies
- Decorator: Stack promotions on base price
- Composite: Combine promotions
- Chain of Responsibility: Apply promotions in order
- Builder: Construct complex orders

**Promotion Rules Example:**
- "Buy 2 get 1 free" on specific category
- "20% off orders over $100"
- "Free shipping on electronics"
- VIP members get extra 5% off

**Refactoring Journey:**
1. Basic cart with add/total
2. Add single promotion type
3. Refactor to support multiple promotion types
4. Add promotion stacking/exclusion logic
5. Implement coupon codes as special promotion

**Acceptance Criteria:**
- [ ] Promotions don't result in negative prices
- [ ] Order of promotion application is defined and consistent
- [ ] Adding new promotion type requires no existing code changes
- [ ] All edge cases tested (empty cart, expired coupons)

---

## C4: Ride Booking Simulation

**Difficulty:** ⭐⭐⭐⭐⭐ Expert  
**Concepts:** Real-time matching, state machines, location services

**Problem Statement:**  
Build ride-hailing system: riders, drivers, booking, matching, fare calculation, ratings.

**Core Requirements:**
- **Entities:** Rider, Driver, Ride, Vehicle, Location, Rating
- **Features:**
  - Request ride (specify pickup, destination)
  - Match nearest available driver
  - Driver accepts/rejects ride
  - Ride state tracking: Requested → Matched → InProgress → Completed
  - Fare calculation (distance, time, surge)
  - Two-way rating system

**OOP Concepts to Apply:**
- State Pattern: Ride lifecycle states
- Strategy: Different fare calculation (standard, premium, pool)
- Observer: Notify rider/driver of status changes
- Value Objects: Location (lat, lng), Money

**Design Patterns:**
- State: Ride transitions
- Strategy: Matching algorithm (nearest, highest-rated, random)
- Observer: Real-time notifications
- Factory: Create appropriate ride types
- Facade: Simple API for complex matching logic

**Matching Algorithm:**
- Find drivers within X km radius
- Filter by availability and vehicle type
- Sort by rating/distance
- Offer to best match, timeout → next

**Refactoring Journey:**
1. Basic ride request and manual assignment
2. Add driver matching logic
3. Implement state machine for ride lifecycle
4. Add fare calculation with multiple strategies
5. Implement rating and feedback system

**Acceptance Criteria:**
- [ ] No orphan rides (all requests eventually complete or cancel)
- [ ] Driver/rider state always consistent
- [ ] Concurrent requests handled correctly
- [ ] Surge pricing activates under high demand

---

## C5: Turn-Based Game Engine

**Difficulty:** ⭐⭐⭐⭐⭐ Expert  
**Concepts:** Game loop, entity-component, event systems, rules engine

**Problem Statement:**  
Build an extensible turn-based game engine that can power various games (chess, card games, strategy).

**Core Requirements:**
- **Entities:** Game, Player, Turn, Action, GameState, Rule
- **Features:**
  - Game initialization and player setup
  - Turn management (whose turn, available actions)
  - Action validation and execution
  - Win/lose/draw condition checking
  - Undo/redo moves
  - Save/load game state

**OOP Concepts to Apply:**
- Command: Actions as undoable commands
- Memento: Save/restore game state
- State: Game states (Setup, InProgress, Paused, Finished)
- Composition: Game contains players, board, rules

**Design Patterns:**
- Command: All game actions (Move, Attack, UseItem)
- Memento: Game state snapshots
- State: Game lifecycle
- Strategy: AI player strategies
- Observer: React to game events (damage, death, win)
- Template: Game loop with customizable steps
- Flyweight: Share common game assets

**Sample Game: Card Battle**
- Two players, deck of cards
- Draw, play, attack phases
- Health tracking
- Special abilities (card effects)

**Refactoring Journey:**
1. Basic game loop with hard-coded rules
2. Extract actions as command objects
3. Add undo/redo capability
4. Make rules configurable/pluggable
5. Add AI player using strategy pattern

**Acceptance Criteria:**
- [ ] Engine supports at least 2 different game types
- [ ] Adding new game requires no engine code changes
- [ ] Save/load works correctly
- [ ] AI can play against itself
- [ ] All game states have clear transitions

---

# 📊 Curriculum Summary

| Level | Assignments | Focus Areas |
|-------|-------------|-------------|
| 🟢 Beginner | B1–B25 | Classes, objects, methods, constructors, encapsulation |
| 🟡 Intermediate | I1–I25 | Inheritance, polymorphism, interfaces, composition, patterns |
| 🟠 Advanced | A1–A25 | SOLID, design patterns, generics, collections, exceptions |
| 🔴 Expert | E1–E10 | Concurrency, TDD, architecture, DDD, refactoring |
| 🏆 Capstone | C1–C5 | End-to-end systems with all concepts |

**Total: 90 assignments + 5 capstone projects**

---

*Happy coding! Remember: first make it work, then make it right, then make it fast.*
