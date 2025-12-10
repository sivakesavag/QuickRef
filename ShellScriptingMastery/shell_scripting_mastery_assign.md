# Shell Scripting Mastery Curriculum

> **A comprehensive, self-contained progression from beginner to expert**
> 
> **200 Assignments | 340-470 Hours | Professional Shell Scripting Mastery**

---

## 📋 Curriculum Overview

| Level | Assignments | Focus Areas | Est. Hours |
|-------|-------------|-------------|------------|
| **🟢 Beginner** | B01-B50 | Fundamentals, syntax, I/O, conditions, loops, arrays | 50-70 |
| **🟡 Intermediate** | I01-I50 | Functions, grep/sed/awk, parallel processing, debugging | 70-100 |
| **🟠 Advanced** | A01-A50 | System admin, containers, CI/CD, security, deployment | 100-140 |
| **🔴 Expert** | E01-E50 | Optimization, DSLs, distributed patterns, cloud-native | 120-160 |

## 📚 Topics Covered by Level

### 🟢 Beginner (B01-B50)
- Variables, quoting, and command substitution
- User input and command-line arguments
- Arithmetic and string operations
- Conditional statements (if/else, case)
- Loops (for, while, until)
- Arrays and basic data structures
- File testing and permissions
- File reading and writing
- Environment variables
- Basic text search and filtering
- Color output and formatting
- Simple project management scripts

### 🟡 Intermediate (I01-I50)
- Functions and modular programming
- Variable scope and return values
- Recursive algorithms
- grep fundamentals and patterns
- sed stream editing
- awk text processing and reporting
- Regular expressions mastery
- Process substitution and subshells
- Signal handling and traps
- Parallel and background processing
- Error handling patterns
- Log parsing and analysis
- CSV/JSON/XML processing
- SSH and network operations
- Git automation
- Unit testing frameworks

### 🟠 Advanced (A01-A50)
- Process management deep dive
- System resource monitoring
- Security auditing
- Enterprise backup systems
- Container and Kubernetes automation
- CI/CD pipeline development
- Infrastructure provisioning
- Load testing frameworks
- Database migrations
- SSL certificate management
- Firewall automation
- Secrets management
- Compliance checking
- Rate limiting and queuing
- Workflow engines
- Anomaly detection

### 🔴 Expert (E01-E50)
- Performance optimization
- Memory-efficient processing
- High-performance text processing
- Plugin architectures
- Domain-specific languages (DSLs)
- REST API servers
- Event sourcing and CQRS
- Saga pattern implementation
- Distributed locks and consensus
- Schema validation engines
- Multi-tenancy frameworks
- GitOps controllers
- Self-healing infrastructure
- Kubernetes operators
- Terraform-like state management
- Cloud-native automation frameworks

## 🎯 Assignment Structure

Each assignment includes:
- **Objective**: Clear learning goal
- **Difficulty**: ⭐ to ⭐⭐⭐⭐⭐ rating
- **Time**: Expected completion time
- **Prerequisites**: Required prior assignments
- **Tasks**: 5 specific implementation requirements
- **Hints**: Tips for common pitfalls

## 📖 How to Use This Curriculum

1. **Start at your level** - Begin with Beginner if new to shell scripting
2. **Complete in order** - Assignments build on previous skills
3. **Practice each concept** - Don't rush; mastery requires repetition
4. **Use the cheatsheet** - Reference `shell_scripting_cheatsheet.md` for syntax help
5. **Build projects** - Capstone assignments (B50, I50, A50, E50) integrate all skills

---

# 🟢 LEVEL 1: BEGINNER

> **Goal**: Master shell fundamentals and write basic functional scripts

---

## B01: Hello Shell World
**Objective**: Create your first shell script with proper structure and permissions

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐ (1/5) |
| Time | 15-20 min |
| Prereqs | None |

**Learning Outcomes**:
- Understand shebang (`#!/bin/bash`) and its purpose
- Set executable permissions with `chmod`
- Execute scripts using different methods

**Task**: Create a script that:
1. Prints "Hello, Shell Scripting!"
2. Displays the current date and time
3. Shows the logged-in username
4. Prints the current working directory

**Hints**:
- Use `echo` for output
- Built-in commands: `date`, `whoami`, `pwd`
- Don't forget to make the script executable

---

## B02: Variable Playground
**Objective**: Declare, assign, and use variables effectively

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐ (1/5) |
| Time | 20-25 min |
| Prereqs | B01 |

**Learning Outcomes**:
- Declare string and numeric variables
- Use variable substitution
- Understand quoting rules (single vs double quotes)

**Task**: Create a script that:
1. Stores your name, age, and favorite color in variables
2. Prints a formatted introduction using these variables
3. Demonstrates the difference between single and double quotes
4. Uses command substitution to store today's date in a variable

**Hints**:
- No spaces around `=` in assignments
- `$variable` or `${variable}` for substitution
- Single quotes preserve literal text; double quotes allow expansion

---

## B03: User Input Handler
**Objective**: Accept and process user input interactively

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐ (1.5/5) |
| Time | 25-30 min |
| Prereqs | B02 |

**Learning Outcomes**:
- Use `read` command with various options
- Handle multiple inputs
- Create interactive prompts

**Task**: Create a script that:
1. Prompts for the user's first and last name
2. Asks for their birth year
3. Calculates and displays their approximate age
4. Greets them with a personalized message including all collected info

**Hints**:
- Use `read -p "prompt"` for inline prompts
- Arithmetic: `$((expression))` or `expr`
- Current year: `$(date +%Y)`

---

## B04: Command-Line Arguments
**Objective**: Process positional parameters passed to scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2/5) |
| Time | 30-35 min |
| Prereqs | B03 |

**Learning Outcomes**:
- Access arguments via `$1`, `$2`, etc.
- Use `$#`, `$@`, `$*`, and `$0`
- Handle missing arguments gracefully

**Task**: Create a script that:
1. Accepts a person's name and age as arguments
2. Prints the total number of arguments received
3. Displays all arguments in a formatted list
4. Shows a usage message if no arguments are provided

**Hints**:
- `$#` gives argument count
- Check for empty arguments before processing
- `$0` contains the script name itself

---

## B05: Basic Arithmetic Calculator
**Objective**: Perform mathematical operations in shell

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2/5) |
| Time | 30-40 min |
| Prereqs | B04 |

**Learning Outcomes**:
- Use arithmetic expansion `$(( ))`
- Handle integer division and modulo
- Work with `bc` for decimal operations

**Task**: Create a calculator script that:
1. Takes two numbers as command-line arguments
2. Displays results of: addition, subtraction, multiplication, division, modulo
3. Shows the average of both numbers (with decimals)
4. Handles division by zero gracefully

**Hints**:
- Integer arithmetic: `$((num1 + num2))`
- Decimal math requires `bc`: `echo "scale=2; $num1/$num2" | bc`
- Check if second number is zero before dividing

---

## B06: Simple Decision Maker
**Objective**: Implement conditional logic with if-else statements

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2/5) |
| Time | 35-45 min |
| Prereqs | B05 |

**Learning Outcomes**:
- Write `if`, `elif`, `else` statements
- Use test conditions with `[ ]` and `[[ ]]`
- Compare numbers and strings

**Task**: Create a grade calculator that:
1. Accepts a numeric score (0-100) as input
2. Outputs the letter grade (A: 90+, B: 80-89, C: 70-79, D: 60-69, F: <60)
3. Validates input is within valid range
4. Displays whether the student passed or failed

**Hints**:
- Numeric comparisons: `-eq`, `-ne`, `-lt`, `-le`, `-gt`, `-ge`
- String comparisons: `=`, `!=`, `-z` (empty), `-n` (not empty)
- Always quote variables in conditions: `[ "$score" -ge 90 ]`

---

## B07: Number Classifier
**Objective**: Work with compound and nested conditions

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 40-50 min |
| Prereqs | B06 |

**Learning Outcomes**:
- Combine conditions with AND (`&&`, `-a`) and OR (`||`, `-o`)
- Nest if statements effectively
- Use the NOT operator (`!`)

**Task**: Create a script that:
1. Accepts a number from the user
2. Determines if it's positive, negative, or zero
3. Checks if it's even or odd (for non-zero numbers)
4. Reports if the number is within a "safe range" (-100 to 100)
5. Identifies if it's a single, double, or multi-digit number

**Hints**:
- Modulo for even/odd: `$((num % 2))`
- Combine checks: `[[ $num -gt 0 && $num -lt 100 ]]`
- Use nested ifs or elif chains for multi-level classification

---

## B08: Case Statement Menu
**Objective**: Master the case statement for pattern matching

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B06 |

**Learning Outcomes**:
- Write case statements with multiple patterns
- Use wildcards in case patterns
- Handle default cases

**Task**: Create an interactive menu script that:
1. Displays a menu with options: Date, Calendar, Users, Uptime, Exit
2. Accepts user choice (number or first letter)
3. Executes the corresponding command
4. Shows "Invalid option" for unrecognized inputs
5. Loops until user chooses Exit

**Hints**:
- Case syntax: `case $var in pattern) commands;; esac`
- Multiple patterns: `1|d|D)`
- Default case: `*)`

---

## B09: For Loop Fundamentals
**Objective**: Iterate over lists using for loops

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2/5) |
| Time | 30-40 min |
| Prereqs | B06 |

**Learning Outcomes**:
- Use basic for loop syntax
- Iterate over lists, ranges, and command output
- Use C-style for loops

**Task**: Create a script that:
1. Prints numbers 1 to 10 using a range
2. Lists all .sh files in the current directory
3. Displays each word from a sentence on a new line
4. Creates a multiplication table for a given number (1-10)

**Hints**:
- Range syntax: `{1..10}` or `$(seq 1 10)`
- Command output: `for file in $(ls *.sh)`
- C-style: `for ((i=1; i<=10; i++))`

---

## B10: While Loop Patterns
**Objective**: Control loop execution with while and until

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 40-50 min |
| Prereqs | B09 |

**Learning Outcomes**:
- Write while and until loops
- Use break and continue statements
- Prevent infinite loops

**Task**: Create a number guessing game that:
1. Generates a random number between 1 and 50
2. Prompts user to guess until correct
3. Provides "higher" or "lower" hints
4. Counts and displays total attempts
5. Allows user to quit by typing 'q'

**Hints**:
- Random number: `$((RANDOM % 50 + 1))`
- Infinite loop pattern: `while true; do ... done`
- Use `break` to exit loop on correct guess

---

## B11: Array Basics
**Objective**: Store and manipulate collections of data

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B09 |

**Learning Outcomes**:
- Declare and initialize arrays
- Access array elements and properties
- Loop through arrays

**Task**: Create a script that:
1. Stores a list of 5 fruits in an array
2. Prints all fruits on one line and each on separate lines
3. Displays the array length and specific elements (first, last, third)
4. Adds a new fruit and removes one
5. Searches for a specific fruit and reports if found

**Hints**:
- Array declaration: `fruits=("apple" "banana" "cherry")`
- All elements: `${fruits[@]}`, Length: `${#fruits[@]}`
- Element access: `${fruits[0]}` (zero-indexed)

---

## B12: File Existence Checker
**Objective**: Test file and directory properties

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B06 |

**Learning Outcomes**:
- Use file test operators
- Check permissions and file types
- Gather file metadata

**Task**: Create a file inspector script that:
1. Accepts a file/directory path as argument
2. Reports if the path exists
3. Identifies if it's a file, directory, or symbolic link
4. Shows readable, writable, executable permissions
5. For files: displays size, owner, and last modified date

**Hints**:
- Tests: `-e` (exists), `-f` (file), `-d` (directory), `-L` (symlink)
- Permissions: `-r`, `-w`, `-x`
- Use `stat` or `ls -l` for metadata

---

## B13: Basic File Reader
**Objective**: Read and display file contents

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B12 |

**Learning Outcomes**:
- Read files line by line
- Use cat, head, tail effectively
- Handle files with special characters

**Task**: Create a script that:
1. Accepts a filename as argument
2. Displays first 5 and last 5 lines
3. Shows total line count and word count
4. Reads and numbers each line
5. Searches for a user-specified word and shows matching lines

**Hints**:
- Line-by-line: `while IFS= read -r line`
- Redirect file: `< filename` or `done < filename`
- Count lines: `wc -l < filename`

---

## B14: Simple File Writer
**Objective**: Create and write content to files

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B13 |

**Learning Outcomes**:
- Write to files with redirection
- Append vs overwrite content
- Use here-documents

**Task**: Create a note-taking script that:
1. Prompts user for a note title
2. Accepts multi-line note content (end with empty line)
3. Saves to a file with timestamp
4. Supports append mode for existing files
5. Confirms save with filename and line count

**Hints**:
- Overwrite: `echo "text" > file`
- Append: `echo "text" >> file`
- Here-doc: `cat << EOF ... EOF`

---

## B15: Environment Explorer
**Objective**: Work with environment and shell variables

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 30-40 min |
| Prereqs | B02 |

**Learning Outcomes**:
- Access environment variables
- Set and export variables
- Understand variable scope

**Task**: Create a system info script that:
1. Displays key environment variables (HOME, USER, SHELL, PATH)
2. Creates a local and exported variable, demonstrating scope
3. Shows all environment variables matching a pattern
4. Modifies PATH temporarily within the script
5. Sources a configuration file and uses its variables

**Hints**:
- View all env vars: `env` or `printenv`
- Export: `export VAR=value`
- Source file: `source file` or `. file`
- Filter: `env | grep pattern`

---

## B16: String Manipulation Basics
**Objective**: Extract and modify string values

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B02 |

**Task**: Create a script that:
1. Accepts a string and extracts its length
2. Converts to uppercase and lowercase
3. Extracts substrings (first 5 chars, last 3 chars, middle portion)
4. Replaces a pattern within the string
5. Splits a sentence into words and counts them

**Hints**: `${#var}` for length, `${var^^}` uppercase, `${var:0:5}` substring

---

## B17: Exit Codes Explorer
**Objective**: Understand and use exit statuses

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2/5) |
| Time | 30-40 min |
| Prereqs | B06 |

**Task**: Create a script that:
1. Runs commands and captures their exit codes
2. Returns custom exit codes for different scenarios
3. Uses `$?` to check previous command success
4. Creates a wrapper that reports success/failure of any command

**Hints**: `exit 0` for success, `exit 1` for failure, check with `$?`

---

## B18: Logical Operators Deep Dive
**Objective**: Chain commands with && and ||

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B17 |

**Task**: Create a script that:
1. Uses `&&` to run commands only if previous succeeds
2. Uses `||` to run fallback commands
3. Combines both for complex conditional execution
4. Creates a backup with rollback on failure

**Hints**: `cmd1 && cmd2` runs cmd2 only if cmd1 succeeds

---

## B19: Temp File Management
**Objective**: Create and manage temporary files safely

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 30-40 min |
| Prereqs | B14 |

**Task**: Create a script that:
1. Creates temp files using `mktemp`
2. Uses trap to clean up on exit
3. Writes intermediate data to temp file
4. Processes and moves to final destination

**Hints**: `mktemp` creates unique temp files, `trap 'rm -f $tmpfile' EXIT`

---

## B20: Directory Operations
**Objective**: Navigate and manipulate directories

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 40-50 min |
| Prereqs | B12 |

**Task**: Create a script that:
1. Creates nested directory structures
2. Lists directories only (not files)
3. Counts items in each subdirectory
4. Finds empty directories
5. Creates a directory tree visualization

**Hints**: `mkdir -p` for nested, `find -type d`, `ls -d */`

---

## B21: File Copy and Move
**Objective**: Safely copy and relocate files

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B20 |

**Task**: Create a script that:
1. Copies files with progress indication
2. Moves files with backup of originals
3. Handles filename conflicts intelligently
4. Preserves file permissions and timestamps

**Hints**: `cp -p` preserves attributes, check existence before moving

---

## B22: Simple Backup Script
**Objective**: Create timestamped backups

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B21 |

**Task**: Create a backup script that:
1. Accepts source and destination directories
2. Creates dated backup folders (YYYY-MM-DD format)
3. Copies all files maintaining structure
4. Generates a backup manifest/log
5. Removes backups older than 7 days

**Hints**: `date +%Y-%m-%d` for format, `find -mtime +7` for old files

---

## B23: Input Validation Basics
**Objective**: Validate user input before processing

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B03, B06 |

**Task**: Create a registration form script that:
1. Validates name (letters only, min 2 chars)
2. Validates age (numeric, reasonable range)
3. Validates email format (contains @ and .)
4. Re-prompts on invalid input
5. Confirms all entries before saving

**Hints**: Use pattern matching with `[[ $var =~ pattern ]]`

---

## B24: Password Strength Checker
**Objective**: Evaluate password complexity

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B23 |

**Task**: Create a script that:
1. Accepts password input (hidden with `read -s`)
2. Checks minimum length (8 chars)
3. Verifies presence of uppercase, lowercase, numbers, symbols
4. Scores password strength (weak/medium/strong)
5. Suggests improvements

**Hints**: `read -s` for silent input, grep for character classes

---

## B25: Basic Text Search
**Objective**: Find patterns in text files

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B13 |

**Task**: Create a script that:
1. Searches for a word in a file (case-insensitive)
2. Counts occurrences
3. Shows line numbers of matches
4. Highlights the search term in output
5. Searches recursively in directories

**Hints**: `grep -i` case-insensitive, `-n` line numbers, `-r` recursive

---

## B26: Word Frequency Counter
**Objective**: Analyze text for word statistics

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B25 |

**Task**: Create a script that:
1. Reads a text file
2. Counts total words and unique words
3. Lists top 10 most frequent words
4. Ignores case and punctuation
5. Excludes common stop words (the, a, is, etc.)

**Hints**: `tr` for translation, `sort | uniq -c | sort -rn`

---

## B27: Select Menu Builder
**Objective**: Create user-friendly selection menus

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 30-40 min |
| Prereqs | B08 |

**Task**: Create a script that:
1. Uses `select` to build interactive menus
2. Displays numbered options automatically
3. Handles invalid selections
4. Supports nested submenus
5. Allows going back to previous menu

**Hints**: `select opt in options; do ... done`, `REPLY` contains input

---

## B28: Color and Formatting
**Objective**: Add visual enhancement to scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2/5) |
| Time | 30-40 min |
| Prereqs | B01 |

**Task**: Create a script that:
1. Displays text in different colors (red, green, blue, yellow)
2. Uses bold, underline, and blinking text
3. Creates a colored success/warning/error message function
4. Clears screen and positions cursor
5. Draws a simple colored box around text

**Hints**: ANSI codes: `\e[31m` red, `\e[0m` reset, `\e[1m` bold

---

## B29: Progress Indicators
**Objective**: Show visual progress in loops

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B28, B10 |

**Task**: Create a script that:
1. Displays a spinner animation during operations
2. Shows a percentage progress bar
3. Creates a visual progress bar with blocks (████░░░░)
4. Updates progress in-place (no scrolling)
5. Estimates time remaining

**Hints**: `\r` returns to line start, use loop with sleep

---

## B30: Simple Logger
**Objective**: Implement basic logging functionality

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B14 |

**Task**: Create a script with:
1. Log levels (DEBUG, INFO, WARN, ERROR)
2. Timestamps on each log entry
3. Output to both console and file
4. Color-coded console output by level
5. Configurable minimum log level

**Hints**: Define log functions, use tee for dual output

---

## B31: Arithmetic Sequence Generator
**Objective**: Generate number sequences programmatically

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 30-40 min |
| Prereqs | B09 |

**Task**: Create a script that generates:
1. Fibonacci sequence up to N terms
2. Factorial of a given number
3. Prime numbers up to a limit
4. Sum of digits for any number

**Hints**: Use recursion or loops, `$((expression))` for math

---

## B32: Date and Time Operations
**Objective**: Work with dates and timestamps

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B01 |

**Task**: Create a script that:
1. Displays date in multiple formats
2. Calculates days until a future date
3. Determines day of week for any date
4. Converts between timezones
5. Creates countdown to an event

**Hints**: `date -d` for date parsing, `+%s` for epoch seconds

---

## B33: Simple To-Do List
**Objective**: Build a persistent task manager

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 50-60 min |
| Prereqs | B13, B14, B08 |

**Task**: Create a to-do script that:
1. Adds tasks with descriptions
2. Lists all pending tasks
3. Marks tasks as complete
4. Deletes tasks by number
5. Persists data between runs

**Hints**: Store tasks in a file, number lines for selection

---

## B34: Contact Book
**Objective**: Manage structured data with files

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 55-65 min |
| Prereqs | B33 |

**Task**: Create a contact book that:
1. Adds contacts (name, phone, email)
2. Searches contacts by name
3. Edits existing contacts
4. Deletes contacts
5. Exports to simple format

**Hints**: Use delimiter-separated format, grep for search

---

## B35: File Organizer
**Objective**: Sort files by type or date

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B20, B21 |

**Task**: Create a script that:
1. Organizes files by extension into folders
2. Groups files by modification date
3. Identifies and lists duplicate filenames
4. Moves old files to archive folder
5. Generates organization report

**Hints**: Extract extension: `${filename##*.}`, use find with -mtime

---

## B36: Disk Space Reporter
**Objective**: Monitor filesystem usage

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B01, B06 |

**Task**: Create a script that:
1. Shows disk usage for all partitions
2. Warns if any partition exceeds 80%
3. Lists largest files in a directory
4. Calculates folder sizes
5. Displays usage in human-readable format

**Hints**: `df -h` for disk info, `du -sh` for directory size

---

## B37: System Info Dashboard
**Objective**: Gather and display system information

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B28, B36 |

**Task**: Create a dashboard showing:
1. Hostname and OS information
2. CPU and memory usage
3. Uptime and load average
4. Currently logged-in users
5. Recent system messages

**Hints**: `uname -a`, `free -h`, `uptime`, `who`, `dmesg | tail`

---

## B38: File Permissions Manager
**Objective**: View and modify file permissions

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B12 |

**Task**: Create a script that:
1. Displays permissions in symbolic and octal format
2. Changes permissions based on user input
3. Sets permissions recursively on directories
4. Shows owner and group information
5. Identifies files with dangerous permissions

**Hints**: `stat -c %a` for octal, `chmod` for changing

---

## B39: Batch File Renamer
**Objective**: Rename multiple files with patterns

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B35 |

**Task**: Create a script that:
1. Adds prefix/suffix to filenames
2. Replaces patterns in filenames
3. Converts case of filenames
4. Adds sequential numbers
5. Previews changes before applying

**Hints**: Parameter expansion for renaming, preview with echo first

---

## B40: Simple HTTP Downloader
**Objective**: Download files from the web

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B17, B21 |

**Task**: Create a script that:
1. Downloads a file given URL
2. Shows download progress
3. Resumes interrupted downloads
4. Validates download with checksum
5. Organizes downloads by date

**Hints**: `curl -O` or `wget`, `-C -` for resume

---

## B41: Simple Quiz Game
**Objective**: Build an interactive quiz application

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 50-60 min |
| Prereqs | B10, B11 |

**Task**: Create a quiz script that:
1. Stores questions and answers in arrays
2. Presents questions randomly
3. Tracks score and percentage
4. Shows correct answer on wrong guess
5. Displays final results with grade

**Hints**: RANDOM for shuffling, associative arrays for Q&A pairs

---

## B42: Text-Based Calculator UI
**Objective**: Create an interactive calculator interface

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B05, B08, B28 |

**Task**: Create calculator with:
1. Menu for operations
2. Expression parsing (2+3*4)
3. Memory functions (store, recall)
4. History of calculations
5. Scientific operations (sqrt, power)

**Hints**: `bc -l` for advanced math, store history in array

---

## B43: Simple Alarm/Timer
**Objective**: Create countdown notifications

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B32, B29 |

**Task**: Create a timer script that:
1. Counts down from given minutes/seconds
2. Displays remaining time updating in place
3. Plays sound or shows notification when done
4. Supports pause and resume
5. Allows multiple named timers

**Hints**: `sleep 1` for delay, terminal bell `\a`

---

## B44: Random Data Generator
**Objective**: Generate test data for scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B14, B11 |

**Task**: Create a generator for:
1. Random numbers in range
2. Random strings of given length
3. Random names and emails (from word lists)
4. Random dates within range
5. CSV output with multiple random fields

**Hints**: `$RANDOM`, `/dev/urandom`, shuffle arrays

---

## B45: Argument Parser Template
**Objective**: Parse complex command-line options

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B04 |

**Task**: Create a template script that:
1. Accepts short options (-v, -h)
2. Accepts long options (--verbose, --help)
3. Handles options with values (--file=name)
4. Shows usage information on -h
5. Validates required options

**Hints**: Use `getopts` for short, while shift loop for long

---

## B46: Configuration File Reader
**Objective**: Parse and use config files

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 45-55 min |
| Prereqs | B13 |

**Task**: Create a script that:
1. Reads key=value config files
2. Handles sections [section_name]
3. Ignores comments (# lines)
4. Provides default values for missing keys
5. Validates required configuration

**Hints**: Source simple configs, parse complex ones with while read

---

## B47: Simple Search and Replace
**Objective**: Find and replace text in files

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B25 |

**Task**: Create a script that:
1. Replaces text in a single file
2. Replaces across multiple files
3. Creates backups before changes
4. Shows preview of changes
5. Supports case-insensitive replace

**Hints**: `sed -i` for in-place, `.bak` for backup

---

## B48: Line Counter Utility
**Objective**: Count various line patterns

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 35-45 min |
| Prereqs | B13 |

**Task**: Create a script that:
1. Counts total lines, blank lines, comment lines
2. Counts lines matching a pattern
3. Works on multiple files with totals
4. Identifies longest and shortest lines
5. Calculates average line length

**Hints**: `wc -l`, grep for counting patterns

---

## B49: File Comparison Tool
**Objective**: Compare files and directories

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B12, B13 |

**Task**: Create a script that:
1. Compares two files for differences
2. Shows which lines differ
3. Compares directories for missing files
4. Identifies identical files
5. Generates difference summary

**Hints**: `diff`, `cmp`, `comm` for comparisons

---

## B50: Beginner Capstone - Personal Assistant
**Objective**: Combine all beginner skills in one project

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 90-120 min |
| Prereqs | All B01-B49 |

**Task**: Create a personal assistant that:
1. Shows current date/time and weather (simulated)
2. Manages a to-do list
3. Tracks notes with categories
4. Sets reminders
5. Shows system status
6. Has colorful, menu-driven interface
7. Persists all data between runs
8. Includes help documentation

**Hints**: Combine previous scripts, modularize with files

---

# 🟡 LEVEL 2: INTERMEDIATE

> **Goal**: Master functions, text processing, and practical automation

---

## I01: Introduction to Functions
**Objective**: Create and call reusable functions

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 35-45 min |
| Prereqs | B01-B15 |

**Task**: Create a script that:
1. Defines functions with multiple syntaxes
2. Calls functions with arguments
3. Captures return values
4. Demonstrates function scope
5. Creates a library of utility functions

**Hints**: `function_name() { }` or `function name { }`

---

## I02: Function Return Values
**Objective**: Return data from functions effectively

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | I01 |

**Task**: Create a script demonstrating:
1. Exit codes as return values
2. Printing output for command substitution
3. Using global variables (carefully)
4. Returning arrays via reference
5. Error handling in functions

**Hints**: `return` for status, `echo` for values, capture with `$()`

---

## I03: Local Variables and Scope
**Objective**: Manage variable scope in functions

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 35-45 min |
| Prereqs | I02 |

**Task**: Create a script that:
1. Demonstrates local vs global variables
2. Uses `local` keyword properly
3. Shows variable shadowing
4. Passes by value vs reference
5. Creates pure functions (no side effects)

**Hints**: `local var=value`, variables without local are global

---

## I04: Recursive Functions
**Objective**: Implement recursion in shell

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 45-55 min |
| Prereqs | I03 |

**Task**: Create recursive functions for:
1. Directory tree traversal
2. Factorial calculation
3. Fibonacci sequence
4. File search by name
5. Sum of nested array elements

**Hints**: Base case essential, mind recursion depth limits

---

## I05: Function Libraries
**Objective**: Create sourceable function libraries

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | I03 |

**Task**: Create:
1. A math library with common operations
2. A string library for text manipulation
3. A file utility library
4. Main script that sources and uses libraries
5. Library documentation format

**Hints**: Source with `. library.sh`, use consistent naming

---

## I06: Grep Fundamentals
**Objective**: Master pattern searching with grep

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 40-50 min |
| Prereqs | B25 |

**Task**: Create a script that:
1. Uses basic and extended regex patterns
2. Combines multiple patterns
3. Excludes patterns (inverse match)
4. Searches with context lines
5. Creates a log analyzer using grep

**Hints**: `-E` extended, `-v` inverse, `-B/-A` context

---

## I07: Sed Stream Editor Basics
**Objective**: Transform text with sed

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 45-55 min |
| Prereqs | I06 |

**Task**: Create scripts that:
1. Substitute patterns (simple and global)
2. Delete specific lines
3. Insert and append text
4. Work with line ranges
5. Chain multiple sed commands

**Hints**: `s/old/new/g`, `d` delete, `-i` in-place editing

---

## I08: Sed Advanced Patterns
**Objective**: Complex text transformations with sed

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I07 |

**Task**: Create scripts that:
1. Use capture groups and backreferences
2. Transform multi-line patterns
3. Conditional commands
4. Hold and pattern space manipulation
5. Create a config file transformer

**Hints**: `\(\)` capture, `\1` reference, `N` multi-line

---

## I09: Awk Introduction
**Objective**: Process structured text with awk

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 45-55 min |
| Prereqs | I06 |

**Task**: Create scripts that:
1. Print specific columns from files
2. Use field separators
3. Apply conditions (patterns)
4. Use built-in variables (NR, NF, FS)
5. Process CSV data

**Hints**: `awk '{print $1}'`, `-F:` separator

---

## I10: Awk Programming
**Objective**: Write complete awk programs

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 55-65 min |
| Prereqs | I09 |

**Task**: Create awk scripts with:
1. BEGIN and END blocks
2. Variables and arithmetic
3. Arrays for aggregation
4. Conditional statements
5. Custom functions

**Hints**: `BEGIN{}` init, `END{}` finalize, associative arrays

---

## I11: Awk Report Generator
**Objective**: Create formatted reports with awk

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I10 |

**Task**: Create scripts that:
1. Parse log files and generate summaries
2. Calculate totals and averages
3. Group data by categories
4. Format output with printf
5. Generate HTML/Markdown tables

**Hints**: `printf` for formatting, arrays for grouping

---

## I12: Cut, Paste, and Join
**Objective**: Combine and extract column data

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 35-45 min |
| Prereqs | I09 |

**Task**: Create scripts that:
1. Extract columns with cut
2. Combine files side-by-side with paste
3. Join files on common fields
4. Rearrange column order
5. Process multi-character delimiters

**Hints**: `cut -d: -f1`, `paste -d,`, `join -1 1 -2 1`

---

## I13: Sort and Unique
**Objective**: Order and deduplicate data

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 35-45 min |
| Prereqs | I09 |

**Task**: Create scripts that:
1. Sort numerically and alphabetically
2. Sort by multiple fields
3. Reverse and random sort
4. Remove duplicates with counts
5. Find top-N items

**Hints**: `sort -k2 -n`, `uniq -c`, `head -n 10`

---

## I14: Tr and Character Translation
**Objective**: Transform characters in text streams

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐ (2.5/5) |
| Time | 30-40 min |
| Prereqs | B16 |

**Task**: Create scripts that:
1. Convert case (upper/lower)
2. Delete specific characters
3. Squeeze repeated characters
4. Translate character sets
5. Clean up messy text files

**Hints**: `tr 'a-z' 'A-Z'`, `tr -d`, `tr -s`

---

## I15: Regular Expression Mastery
**Objective**: Master regex patterns for shell

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 55-65 min |
| Prereqs | I06, I07 |

**Task**: Create a regex workbench that:
1. Tests patterns against input
2. Demonstrates all metacharacters
3. Shows character classes and quantifiers
4. Uses anchors and boundaries
5. Validates: emails, phones, IPs, dates

**Hints**: Basic vs Extended regex, `=~` in bash

---

## I16: Here Documents Advanced
**Objective**: Generate content with here-docs

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 35-45 min |
| Prereqs | B14 |

**Task**: Create scripts that:
1. Generate multi-line strings with variables
2. Create config files from templates
3. Execute remote commands via SSH
4. Build HTML documents dynamically
5. Use here-strings for single lines

**Hints**: `<<EOF`, `<<'EOF'` (no expansion), `<<<`

---

## I17: Process Substitution
**Objective**: Use process output as files

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 40-50 min |
| Prereqs | I12 |

**Task**: Create scripts that:
1. Compare outputs of two commands
2. Feed command output to programs expecting files
3. Use multiple process substitutions
4. Combine with tee for splitting output
5. Create pipelines with named pipes

**Hints**: `<(command)`, `>(command)`, `diff <(ls dir1) <(ls dir2)`

---

## I18: Subshells and Command Grouping
**Objective**: Control command execution context

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 40-50 min |
| Prereqs | I03 |

**Task**: Create scripts demonstrating:
1. Subshell execution `( )`
2. Current shell grouping `{ }`
3. Variable scope in subshells
4. Background subshell tasks
5. Exit status from grouped commands

**Hints**: `(cd /tmp && command)` doesn't change parent dir

---

## I19: Advanced Arrays
**Objective**: Master array manipulation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | B11, I03 |

**Task**: Create scripts that:
1. Use associative arrays (dictionaries)
2. Iterate with indices
3. Slice and splice arrays
4. Sort array elements
5. Pass arrays to functions

**Hints**: `declare -A`, `${array[@]:1:3}` slice

---

## I20: Signal Handling
**Objective**: Respond to system signals

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 45-55 min |
| Prereqs | B19 |

**Task**: Create scripts that:
1. Trap SIGINT (Ctrl+C)
2. Clean up on EXIT
3. Ignore signals selectively
4. Reset signal handlers
5. Create interruptible long-running tasks

**Hints**: `trap 'cleanup' EXIT INT TERM`, `trap '' SIGINT`

---

## I21: Background Processes
**Objective**: Run and manage background jobs

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 40-50 min |
| Prereqs | I20 |

**Task**: Create scripts that:
1. Start processes in background
2. Wait for background jobs
3. Manage multiple parallel tasks
4. Collect exit status from background jobs
5. Create a simple job manager

**Hints**: `command &`, `wait $pid`, `jobs`, `$!`

---

## I22: Parallel Processing
**Objective**: Run tasks concurrently

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I21 |

**Task**: Create scripts that:
1. Process files in parallel
2. Limit concurrent jobs
3. Collect results from parallel tasks
4. Use xargs for parallelization
5. Compare sequential vs parallel performance

**Hints**: `xargs -P 4`, job slot management

---

## I23: Named Pipes (FIFOs)
**Objective**: Create inter-process communication

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 45-55 min |
| Prereqs | I17 |

**Task**: Create scripts that:
1. Create and use named pipes
2. Implement producer-consumer pattern
3. Log to multiple destinations
4. Create a simple message queue
5. Handle pipe cleanup properly

**Hints**: `mkfifo`, read from one script, write from another

---

## I24: File Descriptor Manipulation
**Objective**: Advanced I/O redirection

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I18 |

**Task**: Create scripts that:
1. Open custom file descriptors
2. Redirect stderr separately
3. Duplicate and close file descriptors
4. Read and write simultaneously
5. Create logging with multiple outputs

**Hints**: `exec 3>file`, `>&2` stderr, `2>&1` combine

---

## I25: Error Handling Patterns
**Objective**: Robust error management

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I20, B17 |

**Task**: Create scripts with:
1. `set -e` for early exit on error
2. `set -u` for undefined variable errors
3. `set -o pipefail` for pipe errors
4. Custom error handling functions
5. Try-catch-like patterns

**Hints**: `set -euo pipefail`, `trap 'handle_error' ERR`

---

## I26: Debugging Techniques
**Objective**: Debug and troubleshoot scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 45-55 min |
| Prereqs | I25 |

**Task**: Create debugging utilities:
1. Use `set -x` for tracing
2. Create debug mode toggle
3. Add verbose output options
4. Log function entry/exit
5. Create a step-through debugger

**Hints**: `PS4='+ ${BASH_SOURCE}:${LINENO}: '`, conditional tracing

---

## I27: Input/Output Filters
**Objective**: Build text processing pipelines

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 40-50 min |
| Prereqs | I06-I14 |

**Task**: Create filter scripts that:
1. Read from stdin, write to stdout
2. Chain with other commands
3. Handle both file and pipe input
4. Process line by line efficiently
5. Build a custom text processing tool

**Hints**: Read from stdin or file: `${1:--}` pattern

---

## I28: Log File Analyzer
**Objective**: Parse and summarize log files

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 55-65 min |
| Prereqs | I06, I09, I13 |

**Task**: Create a log analyzer that:
1. Parses common log format
2. Counts requests by status code
3. Identifies top IPs and URLs
4. Detects error patterns
5. Generates daily/hourly summaries

**Hints**: Combine awk, sort, uniq for analysis

---

## I29: CSV Processor
**Objective**: Work with CSV data

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I09, I12 |

**Task**: Create a CSV tool that:
1. Reads and validates CSV format
2. Extracts specific columns
3. Filters rows by conditions
4. Joins multiple CSV files
5. Handles quoted fields properly

**Hints**: awk with FPAT for quoted CSV

---

## I30: JSON Parser (Basic)
**Objective**: Extract data from JSON

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I06, I07 |

**Task**: Create scripts that:
1. Extract values using jq or grep/sed
2. Navigate nested structures
3. Filter arrays by conditions
4. Transform JSON to other formats
5. Handle JSON from APIs

**Hints**: `jq '.key'`, `jq '.array[]'`, `-r` raw output

---

## I31: XML Processing
**Objective**: Parse XML in shell scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I07, I30 |

**Task**: Create scripts that:
1. Extract elements using xmllint or sed
2. Query with XPath expressions
3. Transform XML structure
4. Validate XML format
5. Convert XML to CSV

**Hints**: `xmllint --xpath`, `sed` for simple cases

---

## I32: Date Calculations Advanced
**Objective**: Complex date arithmetic

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 40-50 min |
| Prereqs | B32 |

**Task**: Create scripts that:
1. Calculate business days between dates
2. Find date of next/previous weekday
3. Handle timezone conversions
4. Parse various date formats
5. Generate date ranges

**Hints**: `date -d "+1 day"`, `TZ=UTC date`

---

## I33: Cron Job Basics
**Objective**: Schedule automated tasks

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 40-50 min |
| Prereqs | I25 |

**Task**: Create scripts that:
1. Parse cron expressions
2. Generate crontab entries
3. Handle script output and errors
4. Implement lock files for safety
5. Log cron job execution

**Hints**: Cron format: `m h dom mon dow command`

---

## I34: SSH Automation
**Objective**: Automate remote operations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I16 |

**Task**: Create scripts that:
1. Execute remote commands
2. Copy files with scp/rsync
3. Handle authentication gracefully
4. Run commands on multiple hosts
5. Capture and process remote output

**Hints**: `ssh host 'command'`, `ssh -o BatchMode=yes`

---

## I35: Network Information Gathering
**Objective**: Collect network statistics

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 40-50 min |
| Prereqs | B40 |

**Task**: Create scripts that:
1. Display network interfaces and IPs
2. Check port availability
3. Test connectivity to hosts
4. Measure latency
5. Monitor bandwidth usage

**Hints**: `ip addr`, `netstat`, `ping`, `ss`

---

## I36: User Management Scripts
**Objective**: Automate user administration

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | B38 |

**Task**: Create scripts that:
1. Create users from CSV file
2. Set up home directories
3. Manage group memberships
4. Enforce password policies
5. Audit user accounts

**Hints**: `useradd`, `usermod`, `chage`, parse /etc/passwd

---

## I37: Service Management
**Objective**: Control system services

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 40-50 min |
| Prereqs | I21 |

**Task**: Create scripts that:
1. Start/stop/restart services
2. Check service status
3. Wait for service readiness
4. Handle dependencies
5. Create system service wrapper

**Hints**: `systemctl`, `service`, check with `pidof`

---

## I38: Archive and Compression
**Objective**: Work with compressed archives

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 35-45 min |
| Prereqs | B22 |

**Task**: Create scripts that:
1. Create tar archives (gzip, bzip2, xz)
2. Extract with filtering
3. List archive contents
4. Add/remove files from archives
5. Compare compression ratios

**Hints**: `tar -czf`, `tar -tf`, different compression levels

---

## I39: Checksum and Verification
**Objective**: Validate file integrity

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3/5) |
| Time | 35-45 min |
| Prereqs | I38 |

**Task**: Create scripts that:
1. Generate MD5/SHA checksums
2. Verify files against checksums
3. Create checksum manifests
4. Detect corrupted files
5. Compare directories by checksum

**Hints**: `md5sum`, `sha256sum`, `-c` to check

---

## I40: Environment Setup Script
**Objective**: Configure development environments

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | B15, I05 |

**Task**: Create scripts that:
1. Detect OS and shell type
2. Install dependencies conditionally
3. Set up PATH and environment
4. Configure shell profiles
5. Create development aliases

**Hints**: Check `$OSTYPE`, source appropriate configs

---

## I41: Template Engine
**Objective**: Generate files from templates

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I16, I07 |

**Task**: Create a template engine that:
1. Replaces variables in templates
2. Supports conditional sections
3. Handles loops for lists
4. Includes partial templates
5. Escapes special characters

**Hints**: Use sed/awk for substitution, `envsubst`

---

## I42: Git Automation
**Objective**: Automate Git operations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I34 |

**Task**: Create scripts that:
1. Parse git log output
2. Automate commits with messages
3. Check repository status
4. Switch branches conditionally
5. Create deployment hooks

**Hints**: `git log --format=`, `git status --porcelain`

---

## I43: Build Automation
**Objective**: Create build scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 55-65 min |
| Prereqs | I42 |

**Task**: Create a build system that:
1. Compiles source files
2. Tracks dependencies
3. Only rebuilds changed files
4. Runs tests after build
5. Creates release packages

**Hints**: Check file timestamps, use make or custom

---

## I44: Database CLI Wrapper
**Objective**: Script database operations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I29 |

**Task**: Create scripts that:
1. Execute SQL queries (MySQL/PostgreSQL/SQLite)
2. Format output as table/CSV/JSON
3. Handle connection parameters
4. Escape values safely
5. Export and import data

**Hints**: `mysql -e`, `psql -c`, `sqlite3`

---

## I45: HTTP API Client
**Objective**: Interact with REST APIs

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 55-65 min |
| Prereqs | B40, I30 |

**Task**: Create scripts that:
1. Make GET/POST/PUT/DELETE requests
2. Handle authentication headers
3. Parse JSON responses
4. Handle pagination
5. Implement retry logic

**Hints**: `curl -X POST -H -d`, capture status codes

---

## I46: Web Scraping
**Objective**: Extract data from web pages

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I45, I07 |

**Task**: Create scripts that:
1. Download web pages
2. Extract links and text
3. Follow pagination
4. Handle relative URLs
5. Save extracted data

**Hints**: `curl`, `grep` for patterns, `sed` for extraction

---

## I47: Notification System
**Objective**: Send alerts and notifications

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐ (3.5/5) |
| Time | 40-50 min |
| Prereqs | I45 |

**Task**: Create scripts that:
1. Send email alerts (mail/sendmail)
2. Post to Slack webhook
3. Send desktop notifications
4. Log notification history
5. Rate-limit notifications

**Hints**: `mail -s`, curl for webhooks, `notify-send`

---

## I48: Menu Framework
**Objective**: Create reusable menu system

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | B27, I05 |

**Task**: Create a framework with:
1. Dynamic menu generation
2. Keyboard navigation
3. Breadcrumb navigation
4. Help system integration
5. Configuration persistence

**Hints**: Combine arrays, select, and functions

---

## I49: Unit Testing Framework
**Objective**: Test shell scripts systematically

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 55-65 min |
| Prereqs | I02, I25 |

**Task**: Create a testing framework with:
1. Assert functions (equal, not equal, file exists)
2. Test case organization
3. Setup and teardown
4. Test result reporting
5. Exit codes for CI integration

**Hints**: Compare expected vs actual, count pass/fail

---

## I50: Intermediate Capstone - DevOps Toolkit
**Objective**: Build production-ready automation tools

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 120-150 min |
| Prereqs | All I01-I49 |

**Task**: Create a DevOps toolkit with:
1. Server health monitoring
2. Log analysis and alerting
3. Backup with rotation
4. Deployment automation
5. Configuration management
6. Comprehensive logging
7. Command-line interface
8. Documentation

**Hints**: Combine all intermediate skills, modular design

---

# 🟠 LEVEL 3: ADVANCED

> **Goal**: System administration, complex automation, and production-grade scripts

---

## A01: Process Management Deep Dive
**Objective**: Advanced process control

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I21, I22 |

**Task**: Create scripts that:
1. Monitor CPU/memory per process
2. Implement process pools
3. Handle zombie processes
4. Set process priorities
5. Create process hierarchies

**Hints**: `ps aux`, `nice`, `renice`, `/proc` filesystem

---

## A02: System Resource Monitoring
**Objective**: Comprehensive system monitoring

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 55-65 min |
| Prereqs | A01 |

**Task**: Create monitoring scripts for:
1. CPU, memory, disk usage trends
2. Alert thresholds with escalation
3. Historical data collection
4. Resource prediction
5. Visual dashboards (terminal)

**Hints**: `sar`, `vmstat`, `iostat`, track over time

---

## A03: Log Rotation and Management
**Objective**: Enterprise log handling

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I28 |

**Task**: Create log management with:
1. Size and time-based rotation
2. Compression of old logs
3. Retention policies
4. Log shipping to remote
5. Log integrity verification

**Hints**: `logrotate` style, size checks, find by age

---

## A04: Security Auditing Script
**Objective**: Audit system security

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | I36, B38 |

**Task**: Create audit scripts for:
1. Open ports and services
2. User permission anomalies
3. SUID/SGID files
4. Failed login attempts
5. Configuration compliance

**Hints**: `nmap`, `find -perm`, `/var/log/auth.log`

---

## A05: Automated Backup System
**Objective**: Enterprise backup solution

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-90 min |
| Prereqs | I38, I34 |

**Task**: Create backup system with:
1. Full and incremental backups
2. Multiple backup destinations
3. Encryption at rest
4. Verification and testing
5. Disaster recovery procedures

**Hints**: `rsync --link-dest`, `gpg` encryption

---

## A06: Configuration Management
**Objective**: Manage system configurations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | I41, A05 |

**Task**: Create config management with:
1. Version controlled configs
2. Template-based generation
3. Environment-specific values
4. Rollback capabilities
5. Validation before apply

**Hints**: Git for versioning, diff before apply

---

## A07: Container Management Scripts
**Objective**: Automate Docker operations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | I37 |

**Task**: Create scripts that:
1. Build and tag images
2. Manage container lifecycle
3. Monitor container resources
4. Clean up unused resources
5. Orchestrate multi-container apps

**Hints**: `docker` CLI, `docker-compose` commands

---

## A08: Kubernetes Automation
**Objective**: Script Kubernetes management

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-90 min |
| Prereqs | A07 |

**Task**: Create scripts that:
1. Manage deployments and services
2. Scale workloads
3. Monitor pod status
4. Roll back deployments
5. Manage secrets and configs

**Hints**: `kubectl` with `-o json/yaml`, `jq` for parsing

---

## A09: CI/CD Pipeline Scripts
**Objective**: Build continuous integration pipelines

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-95 min |
| Prereqs | I43, I49 |

**Task**: Create CI/CD scripts with:
1. Code checkout and validation
2. Automated testing
3. Build artifact creation
4. Deployment to environments
5. Rollback on failure

**Hints**: Exit codes for status, artifact staging

---

## A10: Infrastructure Provisioning
**Objective**: Automate infrastructure setup

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | I34, A06 |

**Task**: Create provisioning scripts for:
1. VM creation and configuration
2. Network setup
3. Storage provisioning
4. Software installation
5. Security hardening

**Hints**: Cloud CLI tools, SSH for remote config

---

## A11: Load Testing Framework
**Objective**: Performance testing automation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 60-75 min |
| Prereqs | I22, I45 |

**Task**: Create load testing scripts that:
1. Generate concurrent requests
2. Measure response times
3. Track error rates
4. Scale load gradually
5. Generate reports

**Hints**: `curl` in parallel, time measurements

---

## A12: Database Migration Manager
**Objective**: Automate database migrations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | I44 |

**Task**: Create migration system with:
1. Sequential migration files
2. Up and down migrations
3. Migration tracking
4. Rollback capabilities
5. Data seeding

**Hints**: Track applied migrations, checksums

---

## A13: Multi-Server Command Executor
**Objective**: Run commands across server fleet

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | I34, I22 |

**Task**: Create executor that:
1. Reads server list from config
2. Runs commands in parallel
3. Collects and aggregates output
4. Handles failures gracefully
5. Reports success/failure per host

**Hints**: SSH with timeout, per-host logs

---

## A14: SSL Certificate Manager
**Objective**: Manage TLS certificates

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | I35, A04 |

**Task**: Create scripts that:
1. Check certificate expiration
2. Generate CSRs
3. Automate renewal (Let's Encrypt)
4. Deploy certificates
5. Alert on upcoming expiry

**Hints**: `openssl` commands, date comparison

---

## A15: DNS and Domain Management
**Objective**: Automate DNS operations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I45, I35 |

**Task**: Create scripts that:
1. Query DNS records
2. Update records via API
3. Verify propagation
4. Manage multiple domains
5. DNS failover handling

**Hints**: `dig`, `nslookup`, provider APIs

---

## A16: Firewall Rule Manager
**Objective**: Automated firewall configuration

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 60-75 min |
| Prereqs | A04, I35 |

**Task**: Create scripts that:
1. Read rules from config file
2. Apply iptables/nftables rules
3. Validate before applying
4. Save and restore rulesets
5. Audit rule changes

**Hints**: `iptables -L`, save/restore commands

---

## A17: Network Diagnostics Suite
**Objective**: Comprehensive network troubleshooting

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | I35 |

**Task**: Create diagnostic tools for:
1. Connectivity testing
2. Route tracing
3. Port scanning
4. Bandwidth measurement
5. Latency monitoring

**Hints**: `ping`, `traceroute`, `nc`, `iperf3`

---

## A18: Distributed Log Aggregator
**Objective**: Collect logs from multiple sources

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A03, A13 |

**Task**: Create aggregator that:
1. Collects logs from multiple servers
2. Normalizes log formats
3. Indexes for searching
4. Detects patterns/anomalies
5. Provides query interface

**Hints**: rsync or ssh for collection, grep for search

---

## A19: Automated Incident Response
**Objective**: Handle system incidents automatically

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-95 min |
| Prereqs | A02, I47 |

**Task**: Create incident handler that:
1. Detects anomalies
2. Executes response playbooks
3. Collects diagnostic data
4. Notifies on-call team
5. Logs incident timeline

**Hints**: Pattern matching, conditional actions

---

## A20: Canary Deployment System
**Objective**: Implement gradual rollouts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-90 min |
| Prereqs | A09, A02 |

**Task**: Create deployment system that:
1. Deploys to subset of servers
2. Monitors error rates
3. Gradual traffic shift
4. Automatic rollback triggers
5. Full deployment on success

**Hints**: Health checks, percentile deployment

---

## A21: Blue-Green Deployment
**Objective**: Zero-downtime deployments

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-90 min |
| Prereqs | A20 |

**Task**: Create blue-green system with:
1. Parallel environment management
2. Traffic switching
3. Environment validation
4. Quick rollback
5. Environment cleanup

**Hints**: Symlinks for switching, health validation

---

## A22: A/B Testing Framework
**Objective**: Feature flag management

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | I46 |

**Task**: Create framework that:
1. Defines feature flags
2. Assigns users to cohorts
3. Tracks metrics per variant
4. Enables/disables features
5. Reports results

**Hints**: Hash for consistent assignment, config files

---

## A23: Capacity Planning Tools
**Objective**: Resource planning automation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | A02 |

**Task**: Create planning tools that:
1. Collect historical metrics
2. Calculate growth trends
3. Project future needs
4. Identify bottlenecks
5. Generate recommendations

**Hints**: Store metrics in files, calculate averages

---

## A24: Performance Profiler
**Objective**: Profile script performance

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I26 |

**Task**: Create profiler that:
1. Times function execution
2. Counts function calls
3. Identifies slow sections
4. Profiles memory usage
5. Generates flame graphs (text)

**Hints**: `PS4` with timestamps, trap DEBUG

---

## A25: Static Analysis for Shell
**Objective**: Lint and analyze scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | I49, I15 |

**Task**: Create analysis tools that:
1. Check syntax errors
2. Detect common bugs
3. Enforce style guidelines
4. Find security issues
5. Generate reports

**Hints**: Use `shellcheck`, custom patterns

---

## A26: Documentation Generator
**Objective**: Generate docs from scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I06, I07 |

**Task**: Create doc generator that:
1. Extracts function comments
2. Documents parameters
3. Generates usage examples
4. Creates markdown output
5. Builds table of contents

**Hints**: Extract `##` comments, function headers

---

## A27: Interactive Installer
**Objective**: Create software installers

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | I48, I40 |

**Task**: Create installer that:
1. Checks prerequisites
2. Guides through options
3. Downloads dependencies
4. Configures application
5. Validates installation

**Hints**: Progress display, rollback on error

---

## A28: Self-Updating Scripts
**Objective**: Auto-update script mechanism

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 50-65 min |
| Prereqs | I45, I39 |

**Task**: Create update system that:
1. Checks for new versions
2. Downloads updates securely
3. Verifies checksums
4. Backs up current version
5. Applies and restarts

**Hints**: Version comparison, atomic replace

---

## A29: Secrets Management
**Objective**: Handle sensitive data securely

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 60-75 min |
| Prereqs | A04 |

**Task**: Create secrets handler that:
1. Encrypts secrets at rest
2. Decrypts on demand
3. Rotates secrets
4. Audits access
5. Integrates with external vaults

**Hints**: `gpg` encryption, avoid plaintext

---

## A30: Compliance Checker
**Objective**: Audit for compliance standards

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A04, A06 |

**Task**: Create compliance tools that:
1. Define compliance rules
2. Check system state
3. Report violations
4. Track remediation
5. Generate audit reports

**Hints**: Rules as config, check and report

---

## A31: Rate Limiting Implementation
**Objective**: Control request rates in scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 50-60 min |
| Prereqs | I22 |

**Task**: Create rate limiter that:
1. Tracks request counts
2. Implements sliding windows
3. Supports per-key limits
4. Handles burst allowance
5. Returns wait time on limit

**Hints**: File-based counters, timestamp tracking

---

## A32: Queueing System
**Objective**: Implement job queue in shell

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | I23, A31 |

**Task**: Create queue system with:
1. Add/remove jobs
2. Priority ordering
3. Worker processes
4. Job status tracking
5. Dead letter queue

**Hints**: File-based queue, flock for locking

---

## A33: Retry and Backoff Library
**Objective**: Robust retry mechanisms

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4/5) |
| Time | 45-55 min |
| Prereqs | I25 |

**Task**: Create retry library with:
1. Configurable retry counts
2. Exponential backoff
3. Jitter for distributed systems
4. Circuit breaker pattern
5. Timeout handling

**Hints**: Sleep with increasing delays, max wait

---

## A34: State Machine Framework
**Objective**: Implement state machines in shell

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 60-75 min |
| Prereqs | I19 |

**Task**: Create framework that:
1. Defines states and transitions
2. Handles events
3. Guards transitions with conditions
4. Persists state
5. Logs state changes

**Hints**: Associative arrays, case statements

---

## A35: Event-Driven Architecture
**Objective**: Pub/sub pattern implementation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | I23, A34 |

**Task**: Create event system with:
1. Event publishers
2. Multiple subscribers
3. Topic filtering
4. Event persistence
5. Replay capability

**Hints**: Named pipes or files for messages

---

## A36: Chaos Engineering Scripts
**Objective**: Test system resilience

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | A19, A01 |

**Task**: Create chaos tools that:
1. Kill random processes
2. Introduce network latency
3. Fill disk space
4. Stress CPU/memory
5. Log and recover

**Hints**: `tc` for network, `stress`, `dd`

---

## A37: Data Pipeline Orchestrator
**Objective**: ETL pipeline automation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-95 min |
| Prereqs | I29, A12 |

**Task**: Create pipeline that:
1. Extracts from multiple sources
2. Transforms data formats
3. Loads to destinations
4. Handles dependencies
5. Tracks data lineage

**Hints**: DAG execution, checkpoint files

---

## A38: Metric Collection Agent
**Objective**: Custom metrics gathering

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | A02, I45 |

**Task**: Create agent that:
1. Collects custom metrics
2. Aggregates values
3. Pushes to endpoints
4. Supports multiple formats
5. Handles buffering

**Hints**: JSON/InfluxDB format, curl for push

---

## A39: Health Check Framework
**Objective**: Comprehensive health checking

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 50-65 min |
| Prereqs | A02, I35 |

**Task**: Create framework with:
1. Multiple check types
2. Dependency mapping
3. Alerting thresholds
4. Historical tracking
5. API endpoint

**Hints**: Componentized checks, aggregate status

---

## A40: Resource Cleanup Automation
**Objective**: Clean orphaned resources

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 50-65 min |
| Prereqs | A07, A01 |

**Task**: Create cleanup scripts for:
1. Unused containers/images
2. Orphaned volumes
3. Stale temp files
4. Old log files
5. Abandoned processes

**Hints**: Age-based cleanup, dry-run mode

---

## A41: Environment Comparison Tool
**Objective**: Compare system configurations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | A06 |

**Task**: Create tool that:
1. Collects environment state
2. Compares across hosts
3. Highlights differences
4. Generates reports
5. Tracks drift over time

**Hints**: Serialize state, diff comparisons

---

## A42: Disaster Recovery Automation
**Objective**: Automated DR procedures

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | A05, A10 |

**Task**: Create DR scripts for:
1. Failover detection
2. DNS switching
3. Data synchronization
4. Service recovery
5. Validation and testing

**Hints**: Health checks trigger failover

---

## A43: Multi-Cloud Abstraction
**Objective**: Cross-platform cloud scripts

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-95 min |
| Prereqs | A10, I45 |

**Task**: Create abstraction layer for:
1. Compute provisioning
2. Storage operations
3. Network management
4. Provider detection
5. Unified interface

**Hints**: Provider-specific modules, common API

---

## A44: Service Mesh Scripts
**Objective**: Service discovery and routing

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A17, I45 |

**Task**: Create scripts for:
1. Service registration
2. Health-based routing
3. Load balancing
4. Circuit breaking
5. Request tracing

**Hints**: Registry file, health checks

---

## A45: Distributed Lock Manager
**Objective**: Coordinate across processes

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | I20, A32 |

**Task**: Create lock manager with:
1. Acquire/release locks
2. Lock timeouts
3. Lock renewal
4. Deadlock detection
5. Distributed coordination

**Hints**: `flock`, temp files, cleanup

---

## A46: Workflow Engine
**Objective**: Complex workflow automation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | A34, A37 |

**Task**: Create workflow engine with:
1. Step definitions
2. Conditional branching
3. Parallel execution
4. Error handling/retry
5. Workflow state persistence

**Hints**: DAG execution, step status files

---

## A47: Anomaly Detection System
**Objective**: Detect unusual patterns

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A38, I28 |

**Task**: Create detector for:
1. Baseline establishment
2. Statistical deviation
3. Pattern matching
4. Alert generation
5. Historical analysis

**Hints**: Moving averages, threshold deviation

---

## A48: SLA Monitoring and Reporting
**Objective**: Track service levels

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | A39, A38 |

**Task**: Create SLA tracker for:
1. Uptime calculation
2. Response time metrics
3. Error rate tracking
4. SLA violation alerts
5. Monthly reporting

**Hints**: Track incidents, calculate percentages

---

## A49: Cost Optimization Scripts
**Objective**: Identify cost savings

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐ (4.5/5) |
| Time | 55-70 min |
| Prereqs | A23, A40 |

**Task**: Create optimizer for:
1. Unused resource detection
2. Right-sizing recommendations
3. Scheduled shutdown
4. Reserved instance analysis
5. Cost allocation reports

**Hints**: Usage patterns, idle detection

---

## A50: Advanced Capstone - Enterprise Automation Platform
**Objective**: Production-ready automation suite

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 180-240 min |
| Prereqs | All A01-A49 |

**Task**: Create enterprise platform with:
1. Multi-server management
2. Configuration deployment
3. Monitoring and alerting
4. Automated remediation
5. Audit logging
6. Role-based access
7. API interface
8. Comprehensive documentation

**Hints**: Modular architecture, plugins

---

# 🔴 LEVEL 4: EXPERT

> **Goal**: Production-grade scripts, optimization, and enterprise solutions

---

## E01: Performance Optimization Deep Dive
**Objective**: Optimize script performance

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | A24 |

**Task**: Create optimized scripts that:
1. Minimize process spawning
2. Use built-ins over externals
3. Optimize regex patterns
4. Reduce I/O operations
5. Profile and benchmark

**Hints**: `time`, avoid subshells in loops

---

## E02: Memory Efficient Processing
**Objective**: Handle large data efficiently

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 60-75 min |
| Prereqs | E01 |

**Task**: Create scripts that:
1. Process files line by line
2. Stream without loading full file
3. Use temp files strategically
4. Handle unlimited file sizes
5. Monitor memory usage

**Hints**: Avoid $(), use while read

---

## E03: High-Performance Text Processing
**Objective**: Optimized text transformations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 60-75 min |
| Prereqs | I08, I10, E01 |

**Task**: Create processors that:
1. Combine multiple passes
2. Use awk over sed when faster
3. Leverage mawk/gawk differences
4. Optimize regex patterns
5. Benchmark alternatives

**Hints**: Single pass processing, awk -b

---

## E04: Concurrent Processing Mastery
**Objective**: Maximize parallel efficiency

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | I22, E01 |

**Task**: Create scripts with:
1. Optimal worker counts
2. Work stealing
3. Lock-free coordination
4. Load balancing
5. Graceful scaling

**Hints**: Dynamic worker adjustment

---

## E05: Shell Script Compiler
**Objective**: Create script bundler/compiler

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-90 min |
| Prereqs | A28, E01 |

**Task**: Create compiler that:
1. Bundles dependencies
2. Minifies scripts
3. Obfuscates code
4. Creates standalone executables
5. Optimizes for size/speed

**Hints**: Inline sourced files, shc

---

## E06: Plugin Architecture
**Objective**: Create extensible plugin systems

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | I05, A27 |

**Task**: Create plugin system with:
1. Plugin discovery
2. Dependency resolution
3. API versioning
4. Plugin lifecycle
5. Hot reload capability

**Hints**: Source directory scan, naming conventions

---

## E07: DSL (Domain Specific Language)
**Objective**: Create configuration DSL

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | I07, A34 |

**Task**: Create DSL that:
1. Parses custom syntax
2. Validates structure
3. Compiles to shell
4. Provides error messages
5. Supports includes

**Hints**: Tokenize input, generate code

---

## E08: Database Abstraction Layer
**Objective**: Unified database interface

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-90 min |
| Prereqs | I44, A12 |

**Task**: Create abstraction with:
1. Connection pooling (simulated)
2. Query builder
3. Transaction support
4. Migration integration
5. Multiple backend support

**Hints**: Backend-specific modules, common interface

---

## E09: REST API Server
**Objective**: HTTP server in shell

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | I45, E06 |

**Task**: Create API server with:
1. Request parsing
2. Route handling
3. JSON responses
4. Authentication
5. Rate limiting

**Hints**: `nc` or `socat` for sockets

---

## E10: GraphQL-like Query Engine
**Objective**: Flexible data querying

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 90-110 min |
| Prereqs | I30, E09 |

**Task**: Create query engine with:
1. Query parsing
2. Field selection
3. Nested queries
4. Filtering and sorting
5. Schema validation

**Hints**: Recursive parsing, jq integration

---

## E11: Event Sourcing Pattern
**Objective**: Event-based state management

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-90 min |
| Prereqs | A35 |

**Task**: Create system with:
1. Event store
2. Event replay
3. Snapshots
4. Event versioning
5. Projections

**Hints**: Append-only log, state reconstruction

---

## E12: CQRS Pattern Implementation
**Objective**: Command Query separation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | E11, A32 |

**Task**: Create system with:
1. Command handlers
2. Query handlers
3. Read model sync
4. Command validation
5. Async processing

**Hints**: Separate write/read paths

---

## E13: Saga Pattern for Distributed Transactions
**Objective**: Manage distributed workflows

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | A46, E11 |

**Task**: Create saga manager with:
1. Step orchestration
2. Compensating actions
3. Timeout handling
4. State persistence
5. Recovery mechanisms

**Hints**: Step logs, rollback chains

---

## E14: Idempotency Framework
**Objective**: Ensure operation safety

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 60-75 min |
| Prereqs | A45 |

**Task**: Create framework that:
1. Generates idempotency keys
2. Tracks completed operations
3. Returns cached results
4. Handles expiration
5. Concurrent access safety

**Hints**: Hash-based keys, lock files

---

## E15: Cache Layer Implementation
**Objective**: High-performance caching

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | E02 |

**Task**: Create cache with:
1. Multiple eviction policies
2. TTL support
3. Cache warming
4. Invalidation strategies
5. Statistics tracking

**Hints**: File-based cache, LRU with timestamps

---

## E16: Consensus Algorithm (Simplified)
**Objective**: Distributed agreement

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 90-110 min |
| Prereqs | A45, E11 |

**Task**: Create consensus system with:
1. Leader election
2. Proposal mechanism
3. Quorum calculation
4. Split-brain handling
5. Recovery protocol

**Hints**: Heartbeats, voting files

---

## E17: Schema Validation Engine
**Objective**: Validate data structures

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | I30, E07 |

**Task**: Create validator for:
1. Type checking
2. Required fields
3. Pattern matching
4. Nested structures
5. Custom validators

**Hints**: Schema as config, recursive validation

---

## E18: Template Compilation Engine
**Objective**: High-performance templates

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | I41, E01 |

**Task**: Create template engine that:
1. Pre-compiles templates
2. Caches compiled output
3. Supports inheritance
4. Handles partials
5. Escapes output safely

**Hints**: Generate shell functions

---

## E19: Dependency Injection Container
**Objective**: Manage script dependencies

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 65-80 min |
| Prereqs | E06, I05 |

**Task**: Create DI container with:
1. Service registration
2. Automatic resolution
3. Lifecycle management
4. Lazy loading
5. Scoped instances

**Hints**: Function references, lazy sourcing

---

## E20: ORM-like Data Mapper
**Objective**: Object-like data handling

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | E08, I19 |

**Task**: Create data mapper with:
1. Model definitions
2. CRUD operations
3. Relationship handling
4. Query chaining
5. Validation integration

**Hints**: Associative arrays as objects

---

## E21: Reactive Data Binding
**Objective**: Observable data patterns

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A35, E11 |

**Task**: Create reactive system with:
1. Observable values
2. Computed properties
3. Watch triggers
4. Dependency tracking
5. Batched updates

**Hints**: File watchers, inotify

---

## E22: Configuration Hot Reload
**Objective**: Runtime config changes

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 55-70 min |
| Prereqs | E21 |

**Task**: Create system that:
1. Watches config files
2. Validates new config
3. Applies atomically
4. Notifies components
5. Rollback on failure

**Hints**: inotifywait, signal handlers

---

## E23: Multi-Tenancy Framework
**Objective**: Isolated tenant environments

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-90 min |
| Prereqs | A29, E19 |

**Task**: Create framework with:
1. Tenant isolation
2. Config per tenant
3. Data partitioning
4. Resource limits
5. Tenant switching

**Hints**: Environment prefixes, namespacing

---

## E24: Distributed Tracing
**Objective**: Request tracing across services

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A44, E11 |

**Task**: Create tracing system with:
1. Trace ID propagation
2. Span creation
3. Context injection
4. Trace collection
5. Visualization (text)

**Hints**: UUID generation, header passing

---

## E25: Feature Toggle System
**Objective**: Runtime feature management

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 60-75 min |
| Prereqs | A22, E22 |

**Task**: Create toggle system with:
1. Toggle definitions
2. Percentage rollouts
3. User targeting
4. Override rules
5. Toggle analytics

**Hints**: Config-driven, hash for consistency

---

## E26: API Gateway Implementation
**Objective**: Route and manage API traffic

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | E09, A44 |

**Task**: Create gateway with:
1. Request routing
2. Authentication/authorization
3. Rate limiting
4. Request transformation
5. Response caching

**Hints**: Proxy requests, header manipulation

---

## E27: Service Registry and Discovery
**Objective**: Dynamic service management

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A44, E16 |

**Task**: Create registry with:
1. Service registration
2. Health monitoring
3. DNS-based discovery
4. Load balancing
5. Failover handling

**Hints**: File-based registry, heartbeats

---

## E28: Chaos Monkey Framework
**Objective**: Systematic resilience testing

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-90 min |
| Prereqs | A36, E13 |

**Task**: Create framework that:
1. Schedules chaos experiments
2. Defines failure injection
3. Monitors impact
4. Automatic recovery
5. Reports findings

**Hints**: Random selection, controlled blast radius

---

## E29: Self-Healing Infrastructure
**Objective**: Automatic problem resolution

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | A19, E27 |

**Task**: Create self-healing with:
1. Problem detection
2. Root cause analysis
3. Remediation playbooks
4. Service restart/failover
5. Prevention learning

**Hints**: Pattern matching, remediation actions

---

## E30: GitOps Controller
**Objective**: Git-driven operations

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | I42, A09 |

**Task**: Create controller that:
1. Watches git repository
2. Detects changes
3. Applies configurations
4. Validates deployments
5. Rollback on failure

**Hints**: Git polling, diff detection

---

## E31: Immutable Infrastructure Manager
**Objective**: Replace-don't-modify approach

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | A10, E30 |

**Task**: Create manager with:
1. Image building
2. Version management
3. Atomic deployments
4. Traffic draining
5. Rollback capability

**Hints**: Symlink switching, image tags

---

## E32: Policy Engine
**Objective**: Define and enforce policies

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-90 min |
| Prereqs | A30, E07 |

**Task**: Create engine that:
1. Defines policies in DSL
2. Evaluates against state
3. Enforces automatically
4. Reports violations
5. Supports exceptions

**Hints**: Rule evaluation, action triggers

---

## E33: Data Lake Scripts
**Objective**: Manage large-scale data

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | A37, E02 |

**Task**: Create data lake tools for:
1. Ingestion from sources
2. Schema evolution
3. Partitioning strategies
4. Compaction jobs
5. Query optimization

**Hints**: Directory structures, metadata files

---

## E34: Stream Processing Framework
**Objective**: Real-time data processing

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | I23, A35 |

**Task**: Create framework with:
1. Event streaming
2. Windowed aggregation
3. Late data handling
4. Exactly-once processing
5. Checkpointing

**Hints**: Named pipes, sliding windows

---

## E35: ML Pipeline Orchestrator
**Objective**: Automate ML workflows

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | A37, A46 |

**Task**: Create orchestrator for:
1. Data preparation steps
2. Training execution
3. Model evaluation
4. Deployment automation
5. A/B model comparison

**Hints**: Step execution, artifact management

---

## E36: Observability Platform
**Objective**: Full-stack monitoring

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 90-120 min |
| Prereqs | A38, E24, A18 |

**Task**: Create platform with:
1. Metrics collection
2. Log aggregation
3. Trace correlation
4. Unified dashboard
5. Alert management

**Hints**: Combine monitoring approaches

---

## E37: Runbook Automation
**Objective**: Executable documentation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A26, A46 |

**Task**: Create system with:
1. Runbook definitions
2. Interactive execution
3. Variable injection
4. Approval workflows
5. Execution logging

**Hints**: Markdown with code blocks, step execution

---

## E38: Compliance as Code
**Objective**: Automated compliance checks

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | A30, E32 |

**Task**: Create compliance framework:
1. Standard definitions (CIS, SOC2)
2. Automatic scanning
3. Evidence collection
4. Report generation
5. Remediation tracking

**Hints**: Control checks as functions

---

## E39: Kubernetes Operator (Shell-based)
**Objective**: Custom resource controller

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 90-120 min |
| Prereqs | A08, E27 |

**Task**: Create operator that:
1. Watches custom resources
2. Reconciles state
3. Handles updates
4. Reports status
5. Manages lifecycle

**Hints**: kubectl watch, reconciliation loops

---

## E40: Terraform-like State Manager
**Objective**: Infrastructure state tracking

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 95-120 min |
| Prereqs | A10, E11 |

**Task**: Create state manager with:
1. State file handling
2. Resource graph
3. Plan/Apply workflow
4. Drift detection
5. State locking

**Hints**: JSON state files, dependency ordering

---

## E41: Secrets Rotation Framework
**Objective**: Automated credential management

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | A29, E14 |

**Task**: Create framework that:
1. Rotates credentials
2. Distributes securely
3. Updates services
4. Validates access
5. Audits operations

**Hints**: Sequential rotation, rollback

---

## E42: Zero-Trust Network Implementation
**Objective**: Security-first networking

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | A16, E26 |

**Task**: Create implementation with:
1. Service authentication
2. Certificate management
3. Policy enforcement
4. Traffic encryption
5. Continuous verification

**Hints**: mTLS concepts, token validation

---

## E43: Incident Management System
**Objective**: Full incident lifecycle

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 80-100 min |
| Prereqs | A19, E37 |

**Task**: Create system with:
1. Incident creation
2. Severity classification
3. Escalation management
4. Communication automation
5. Post-mortem generation

**Hints**: Status tracking, timeline logging

---

## E44: Capacity Autoscaler
**Objective**: Dynamic resource scaling

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-95 min |
| Prereqs | A23, E27 |

**Task**: Create autoscaler with:
1. Metric-based scaling
2. Predictive scaling
3. Scale-up/down policies
4. Cooldown periods
5. Cost awareness

**Hints**: Threshold-based decisions

---

## E45: Deployment Strategy Library
**Objective**: Multiple deployment methods

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | A20, A21 |

**Task**: Create library supporting:
1. Rolling deployments
2. Canary releases
3. Blue-green switching
4. Feature flags
5. Shadow deployments

**Hints**: Unified interface, strategy pattern

---

## E46: FinOps Automation
**Objective**: Cloud cost management

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 75-90 min |
| Prereqs | A49, E36 |

**Task**: Create FinOps tools for:
1. Cost visibility
2. Anomaly detection
3. Budget alerts
4. Optimization recommendations
5. Chargeback/showback

**Hints**: Parse billing data, trend analysis

---

## E47: Disaster Simulation Framework
**Objective**: DR testing automation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 85-105 min |
| Prereqs | A42, E28 |

**Task**: Create framework that:
1. Defines failure scenarios
2. Executes simulations
3. Measures recovery time
4. Validates data integrity
5. Reports findings

**Hints**: Controlled failures, metrics tracking

---

## E48: Platform Engineering Toolkit
**Objective**: Developer experience automation

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 90-120 min |
| Prereqs | E06, E30 |

**Task**: Create toolkit with:
1. Project scaffolding
2. Environment provisioning
3. CI/CD templates
4. Documentation generation
5. Self-service portals

**Hints**: Templates, interactive setup

---

## E49: Production Readiness Checker
**Objective**: Validate production deployments

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 70-85 min |
| Prereqs | E38, E36 |

**Task**: Create checker for:
1. Security requirements
2. Monitoring coverage
3. Documentation completeness
4. Performance baselines
5. Runbook availability

**Hints**: Checklist validation, scoring

---

## E50: Expert Capstone - Cloud-Native Automation Framework
**Objective**: Enterprise-grade automation platform

| Attribute | Value |
|-----------|-------|
| Difficulty | ⭐⭐⭐⭐⭐ (5/5) |
| Time | 300-400 min |
| Prereqs | All E01-E49 |

**Task**: Create comprehensive framework with:
1. Multi-cloud infrastructure management
2. Container orchestration
3. GitOps-driven deployments
4. Full observability stack
5. Self-healing capabilities
6. Policy-based governance
7. Secrets and security management
8. Cost optimization
9. Disaster recovery
10. API and CLI interfaces
11. Plugin extensibility
12. Comprehensive documentation

**Hints**: Modular architecture, combine all expert skills

---

# 📚 CURRICULUM COMPLETION

## Congratulations!

After completing all 200 assignments, you will have mastered:

### Technical Skills
- ✅ Shell scripting fundamentals to expert patterns
- ✅ Text processing with grep, sed, awk
- ✅ Process management and parallel execution
- ✅ System administration automation
- ✅ Network operations and API interactions
- ✅ Database operations and data processing
- ✅ Security and compliance automation
- ✅ Container and Kubernetes management
- ✅ CI/CD pipeline development
- ✅ Monitoring and observability
- ✅ Performance optimization

### Professional Capabilities
- ✅ Production-grade error handling
- ✅ Comprehensive debugging skills
- ✅ Documentation and testing practices
- ✅ Modular and maintainable code
- ✅ Enterprise automation patterns
- ✅ DevOps and SRE practices

## Estimated Total Learning Time

| Level | Hours |
|-------|-------|
| Beginner | 50-70 |
| Intermediate | 70-100 |
| Advanced | 100-140 |
| Expert | 120-160 |
| **Total** | **340-470 hours** |

---

*This curriculum is self-contained and designed for professional shell scripting mastery.*
