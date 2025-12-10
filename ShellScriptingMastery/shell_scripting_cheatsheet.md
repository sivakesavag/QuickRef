# Shell Scripting Cheatsheet

> **Comprehensive reference for solving the 200 Shell Scripting Mastery assignments**

---

## Table of Contents
1. [Basics & Syntax](#1-basics--syntax)
2. [Variables & Data Types](#2-variables--data-types)
3. [Input/Output](#3-inputoutput)
4. [Operators](#4-operators)
5. [Conditionals](#5-conditionals)
6. [Loops](#6-loops)
7. [Arrays](#7-arrays)
8. [Functions](#8-functions)
9. [String Operations](#9-string-operations)
10. [File Operations](#10-file-operations)
11. [Text Processing](#11-text-processing)
12. [Regular Expressions](#12-regular-expressions)
13. [Process Management](#13-process-management)
14. [Error Handling](#14-error-handling)
15. [Debugging](#15-debugging)
16. [Networking](#16-networking)
17. [Advanced Patterns](#17-advanced-patterns)

---

# 1. Basics & Syntax

## Script Structure
```bash
#!/bin/bash
# Shebang - specifies interpreter

# Comments start with #

# Your code here
echo "Hello, World!"

exit 0  # Exit with success status
```

## Running Scripts
```bash
# Make executable
chmod +x script.sh

# Execute methods
./script.sh          # Direct execution
bash script.sh       # Using bash explicitly
source script.sh     # Run in current shell (also: . script.sh)
```

## Command Separators
```bash
cmd1 ; cmd2          # Run sequentially
cmd1 && cmd2         # Run cmd2 only if cmd1 succeeds
cmd1 || cmd2         # Run cmd2 only if cmd1 fails
cmd1 & cmd2          # Run cmd1 in background, then cmd2
cmd1 | cmd2          # Pipe output of cmd1 to cmd2
```

---

# 2. Variables & Data Types

## Variable Declaration
```bash
# Assignment (NO spaces around =)
name="John"
age=25
readonly PI=3.14159  # Constant

# Access
echo $name
echo ${name}         # Preferred (safer)
echo "${name}"       # Preserves whitespace
```

## Special Variables
```bash
$0          # Script name
$1 to $9    # Positional parameters
${10}       # 10th parameter and beyond
$#          # Number of arguments
$@          # All arguments (as separate words)
$*          # All arguments (as single string)
$?          # Exit status of last command
$$          # Current process ID
$!          # PID of last background process
$_          # Last argument of previous command
```

## Variable Expansion
```bash
${var:-default}      # Use default if var unset/empty
${var:=default}      # Set and use default if var unset/empty
${var:+alternate}    # Use alternate if var is set
${var:?error_msg}    # Error if var unset/empty

# String length
${#var}

# Substrings
${var:start}         # From position to end
${var:start:length}  # From position for length chars
${var: -n}           # Last n characters (note space)
```

## Environment Variables
```bash
export VAR=value     # Export to child processes
env                  # Show all environment variables
printenv VAR         # Print specific variable
unset VAR            # Remove variable
```

---

# 3. Input/Output

## Reading Input
```bash
read name                        # Read into variable
read -p "Enter name: " name      # With prompt
read -s password                 # Silent (for passwords)
read -t 5 response               # Timeout in seconds
read -n 1 char                   # Read single character
read -a array                    # Read into array
read -r line                     # Raw mode (no backslash interpretation)

# Read from file line by line
while IFS= read -r line; do
    echo "$line"
done < filename.txt
```

## Output
```bash
echo "Hello"                     # Print with newline
echo -n "No newline"             # Without newline
echo -e "Tab:\t Newline:\n"      # Enable escape sequences
printf "Name: %s, Age: %d\n" "$name" $age  # Formatted output
```

## Redirection
```bash
cmd > file           # Redirect stdout (overwrite)
cmd >> file          # Redirect stdout (append)
cmd 2> file          # Redirect stderr
cmd 2>&1             # Redirect stderr to stdout
cmd &> file          # Redirect both stdout and stderr
cmd < file           # Redirect stdin from file
cmd << EOF           # Here document
content
EOF
cmd <<< "string"     # Here string
```

## File Descriptors
```bash
exec 3> file         # Open fd 3 for writing
exec 4< file         # Open fd 4 for reading
echo "text" >&3      # Write to fd 3
read line <&4        # Read from fd 4
exec 3>&-            # Close fd 3
```

---

# 4. Operators

## Arithmetic Operators
```bash
# Arithmetic expansion
result=$((5 + 3))
result=$((a * b))
result=$((10 / 3))   # Integer division
result=$((10 % 3))   # Modulo
result=$((2 ** 8))   # Exponentiation

# Increment/Decrement
((count++))
((count--))
((count += 5))

# Using expr (older style)
result=$(expr 5 + 3)

# Floating point with bc
result=$(echo "scale=2; 10/3" | bc)
```

## Comparison Operators (Numeric)
```bash
[ $a -eq $b ]        # Equal
[ $a -ne $b ]        # Not equal
[ $a -lt $b ]        # Less than
[ $a -le $b ]        # Less than or equal
[ $a -gt $b ]        # Greater than
[ $a -ge $b ]        # Greater than or equal
```

## Comparison Operators (String)
```bash
[ "$a" = "$b" ]      # Equal
[ "$a" != "$b" ]     # Not equal
[ -z "$a" ]          # Empty (zero length)
[ -n "$a" ]          # Not empty (non-zero length)
[[ "$a" < "$b" ]]    # Less than (alphabetically)
[[ "$a" > "$b" ]]    # Greater than (alphabetically)
[[ "$a" =~ regex ]]  # Regex match
```

## Logical Operators
```bash
[ ! expr ]           # NOT
[ expr1 -a expr2 ]   # AND (in single brackets)
[ expr1 -o expr2 ]   # OR (in single brackets)
[[ expr1 && expr2 ]] # AND (in double brackets)
[[ expr1 || expr2 ]] # OR (in double brackets)
```

---

# 5. Conditionals

## If Statement
```bash
if [ condition ]; then
    commands
elif [ condition2 ]; then
    commands
else
    commands
fi

# One-liner
[ condition ] && command_if_true || command_if_false
```

## File Test Operators
```bash
[ -e file ]    # Exists
[ -f file ]    # Is regular file
[ -d file ]    # Is directory
[ -L file ]    # Is symbolic link
[ -r file ]    # Is readable
[ -w file ]    # Is writable
[ -x file ]    # Is executable
[ -s file ]    # Size > 0
[ -O file ]    # Owned by current user
[ file1 -nt file2 ]  # file1 newer than file2
[ file1 -ot file2 ]  # file1 older than file2
```

## Case Statement
```bash
case $variable in
    pattern1)
        commands
        ;;
    pattern2|pattern3)
        commands
        ;;
    *)
        default_commands
        ;;
esac

# Pattern matching examples
case $input in
    [Yy]|[Yy][Ee][Ss])
        echo "Yes"
        ;;
    [Nn]|[Nn][Oo])
        echo "No"
        ;;
    [0-9]*)
        echo "Number"
        ;;
esac
```

---

# 6. Loops

## For Loop
```bash
# List iteration
for item in item1 item2 item3; do
    echo "$item"
done

# Range
for i in {1..10}; do
    echo "$i"
done

# Range with step
for i in {0..100..5}; do
    echo "$i"
done

# C-style
for ((i=0; i<10; i++)); do
    echo "$i"
done

# Files in directory
for file in *.txt; do
    echo "$file"
done

# Command output
for user in $(cat users.txt); do
    echo "$user"
done
```

## While Loop
```bash
while [ condition ]; do
    commands
done

# Infinite loop
while true; do
    commands
    [ condition ] && break
done

# Counter example
count=0
while [ $count -lt 10 ]; do
    echo $count
    ((count++))
done

# Read file
while IFS= read -r line; do
    echo "$line"
done < file.txt
```

## Until Loop
```bash
until [ condition ]; do
    commands
done

# Example
count=0
until [ $count -ge 10 ]; do
    echo $count
    ((count++))
done
```

## Loop Control
```bash
break        # Exit loop
break 2      # Exit nested loop (2 levels)
continue     # Skip to next iteration
continue 2   # Continue in outer loop
```

## Select Menu
```bash
PS3="Choose option: "
select opt in "Option 1" "Option 2" "Quit"; do
    case $opt in
        "Option 1") echo "Selected 1" ;;
        "Option 2") echo "Selected 2" ;;
        "Quit") break ;;
        *) echo "Invalid" ;;
    esac
done
```

---

# 7. Arrays

## Indexed Arrays
```bash
# Declaration
arr=(one two three)
arr[0]="first"
declare -a arr

# Access
echo ${arr[0]}         # Single element
echo ${arr[@]}         # All elements
echo ${arr[*]}         # All as single string
echo ${#arr[@]}        # Length
echo ${!arr[@]}        # All indices

# Slice
echo ${arr[@]:1:2}     # From index 1, 2 elements

# Add elements
arr+=("four")

# Delete element
unset arr[1]

# Iterate
for item in "${arr[@]}"; do
    echo "$item"
done

# Iterate with index
for i in "${!arr[@]}"; do
    echo "$i: ${arr[$i]}"
done
```

## Associative Arrays
```bash
# Declaration (required)
declare -A dict

# Assignment
dict[key]="value"
dict=([name]="John" [age]="30")

# Access
echo ${dict[name]}
echo ${dict[@]}        # All values
echo ${!dict[@]}       # All keys

# Iterate
for key in "${!dict[@]}"; do
    echo "$key: ${dict[$key]}"
done
```

---

# 8. Functions

## Basic Functions
```bash
# Definition style 1
function_name() {
    commands
    return 0
}

# Definition style 2
function function_name {
    commands
}

# Calling
function_name
function_name arg1 arg2
```

## Parameters & Return
```bash
greet() {
    local name=$1      # Local variable
    local age=$2
    echo "Hello, $name! Age: $age"
    return 0           # Return status (0-255)
}

# Call and capture output
result=$(greet "John" 30)

# Check return status
greet "John" 30
if [ $? -eq 0 ]; then
    echo "Success"
fi
```

## Local Variables
```bash
my_func() {
    local local_var="local"
    global_var="global"    # Affects outside scope
}
```

## Returning Values
```bash
# Method 1: Echo and capture
get_value() {
    echo "result"
}
value=$(get_value)

# Method 2: Global variable
get_value() {
    RESULT="value"
}

# Method 3: Return code (0-255 only)
is_valid() {
    [ "$1" -gt 0 ] && return 0 || return 1
}
```

---

# 9. String Operations

## String Manipulation
```bash
str="Hello World"

# Length
${#str}                      # 11

# Substring
${str:0:5}                   # Hello
${str:6}                     # World
${str: -5}                   # World (last 5 chars, note space)

# Case conversion (Bash 4+)
${str^^}                     # HELLO WORLD (uppercase)
${str,,}                     # hello world (lowercase)
${str^}                      # Hello world (first char upper)

# Search and Replace
${str/World/Universe}        # Replace first occurrence
${str//o/0}                  # Replace all occurrences
${str/#Hello/Hi}             # Replace if at start
${str/%World/Universe}       # Replace if at end

# Remove pattern
${str#Hello }                # Remove shortest match from start
${str##*/}                   # Remove longest match from start
${str%World}                 # Remove shortest match from end
${str%%/*}                   # Remove longest match from end

# Example: Extract filename/extension
filepath="/path/to/file.txt"
filename="${filepath##*/}"   # file.txt
dirname="${filepath%/*}"     # /path/to
extension="${filename##*.}"  # txt
basename="${filename%.*}"    # file
```

## String Comparison
```bash
[[ $str == *"pattern"* ]]    # Contains pattern
[[ $str == pattern* ]]       # Starts with pattern
[[ $str == *pattern ]]       # Ends with pattern
[[ $str =~ ^[0-9]+$ ]]       # Regex match (numbers only)
```

---

# 10. File Operations

## Reading Files
```bash
# Entire file into variable
content=$(cat file.txt)
content=$(<file.txt)

# Line by line
while IFS= read -r line; do
    echo "$line"
done < file.txt

# With line numbers
nl=1
while IFS= read -r line; do
    echo "$nl: $line"
    ((nl++))
done < file.txt

# First/last lines
head -n 5 file.txt
tail -n 5 file.txt
tail -f file.txt     # Follow file updates
```

## Writing Files
```bash
# Overwrite
echo "text" > file.txt
cat > file.txt << EOF
Line 1
Line 2
EOF

# Append
echo "text" >> file.txt

# Write array
printf "%s\n" "${arr[@]}" > file.txt
```

## File Information
```bash
stat file.txt              # Detailed file info
file file.txt              # File type
wc -l file.txt             # Line count
wc -w file.txt             # Word count
wc -c file.txt             # Byte count
du -h file.txt             # File size
ls -la file.txt            # Permissions, owner, size
```

## Directory Operations
```bash
mkdir -p path/to/dir       # Create with parents
rmdir dir                  # Remove empty directory
rm -rf dir                 # Remove recursively (dangerous!)
cp -r src dest             # Copy recursively
mv src dest                # Move/rename
ls -la                     # List with details
pwd                        # Current directory
cd /path                   # Change directory
find . -name "*.txt"       # Find files
```

## Temporary Files
```bash
tmpfile=$(mktemp)          # Create temp file
tmpdir=$(mktemp -d)        # Create temp directory

# Cleanup on exit
trap "rm -f $tmpfile" EXIT
```

---

# 11. Text Processing

## grep - Pattern Matching
```bash
grep "pattern" file            # Basic search
grep -i "pattern" file         # Case insensitive
grep -v "pattern" file         # Inverse (non-matching)
grep -n "pattern" file         # Show line numbers
grep -c "pattern" file         # Count matches
grep -l "pattern" *.txt        # List matching files
grep -r "pattern" dir/         # Recursive search
grep -E "regex" file           # Extended regex
grep -o "pattern" file         # Only matching part
grep -A 2 "pattern" file       # 2 lines after match
grep -B 2 "pattern" file       # 2 lines before match
grep -C 2 "pattern" file       # 2 lines context
grep -w "word" file            # Whole word match
```

## sed - Stream Editor
```bash
# Substitution
sed 's/old/new/' file          # Replace first occurrence
sed 's/old/new/g' file         # Replace all occurrences
sed 's/old/new/gi' file        # Case insensitive
sed -i 's/old/new/g' file      # In-place edit
sed -i.bak 's/old/new/g' file  # Backup before edit

# Line operations
sed -n '5p' file               # Print line 5
sed -n '5,10p' file            # Print lines 5-10
sed '5d' file                  # Delete line 5
sed '5,10d' file               # Delete lines 5-10
sed '/pattern/d' file          # Delete matching lines

# Insert/Append
sed '5i\New line' file         # Insert before line 5
sed '5a\New line' file         # Append after line 5
sed '1s/^/Header\n/' file      # Add header

# Multiple commands
sed -e 's/a/b/' -e 's/c/d/' file
sed 's/a/b/; s/c/d/' file

# Using capture groups
sed 's/\(.*\)/[\1]/' file      # Wrap each line in brackets
sed 's/\([a-z]*\) \([a-z]*\)/\2 \1/' file  # Swap words
```

## awk - Text Processing
```bash
# Basic syntax: awk 'pattern {action}' file

# Print columns
awk '{print $1}' file          # First column
awk '{print $1, $3}' file      # First and third columns
awk '{print $NF}' file         # Last column
awk '{print $(NF-1)}' file     # Second to last column

# Field separator
awk -F: '{print $1}' /etc/passwd
awk -F',' '{print $1}' file.csv
awk 'BEGIN{FS=":"} {print $1}' file

# Patterns
awk '/pattern/ {print}' file   # Print matching lines
awk '$1 > 100' file            # Numeric comparison
awk 'NR==5' file               # Line 5
awk 'NR>=5 && NR<=10' file     # Lines 5-10

# Built-in variables
awk '{print NR, NF, $0}' file  # Line number, field count, full line
awk 'BEGIN{OFS=","} {print $1,$2}' file  # Output separator

# Calculations
awk '{sum += $1} END {print sum}' file
awk '{sum += $1; count++} END {print sum/count}' file

# Formatting
awk '{printf "%-10s %5d\n", $1, $2}' file

# BEGIN and END blocks
awk 'BEGIN {print "Header"} {print} END {print "Footer"}' file

# Associative arrays
awk '{count[$1]++} END {for (word in count) print word, count[word]}' file

# Conditionals
awk '{if ($1 > 100) print "High"; else print "Low"}' file
```

## Other Text Tools
```bash
# cut - extract columns
cut -d: -f1 /etc/passwd        # First field, colon delimiter
cut -c1-10 file                # Characters 1-10

# sort
sort file                      # Alphabetical
sort -n file                   # Numeric
sort -r file                   # Reverse
sort -k2 file                  # By field 2
sort -u file                   # Unique only

# uniq
uniq file                      # Remove consecutive duplicates
uniq -c file                   # Count occurrences
uniq -d file                   # Only duplicates

# tr - translate characters
tr 'a-z' 'A-Z' < file          # Uppercase
tr -d '0-9' < file             # Delete digits
tr -s ' ' < file               # Squeeze spaces
tr '\n' ' ' < file             # Newlines to spaces

# paste - merge files
paste file1 file2              # Side by side
paste -d',' file1 file2        # With delimiter

# join - join files on common field
join file1 file2

# comm - compare sorted files
comm file1 file2
```

---

# 12. Regular Expressions

## Basic Patterns
```regex
.           Any single character
*           Zero or more of previous
+           One or more of previous (ERE)
?           Zero or one of previous (ERE)
^           Start of line
$           End of line
[]          Character class
[^]         Negated character class
\           Escape special character
```

## Character Classes
```regex
[abc]       a, b, or c
[a-z]       Any lowercase letter
[A-Z]       Any uppercase letter
[0-9]       Any digit
[a-zA-Z]    Any letter
[^0-9]      Not a digit

# POSIX classes
[[:alpha:]] Letters
[[:digit:]] Digits
[[:alnum:]] Alphanumeric
[[:space:]] Whitespace
[[:upper:]] Uppercase
[[:lower:]] Lowercase
[[:punct:]] Punctuation
```

## Extended Regex (ERE)
```regex
{n}         Exactly n times
{n,}        n or more times
{n,m}       Between n and m times
|           Alternation (OR)
()          Grouping
\1, \2      Backreferences
```

## Common Patterns
```bash
# Email (simplified)
[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}

# IP address (simplified)
[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}

# Phone number
[0-9]{3}[-.]?[0-9]{3}[-.]?[0-9]{4}

# Date (YYYY-MM-DD)
[0-9]{4}-[0-9]{2}-[0-9]{2}

# URL (simplified)
https?://[A-Za-z0-9.-]+\.[A-Za-z]{2,}(/[A-Za-z0-9._~:/?#@!$&'()*+,;=-]*)?
```

## Bash Regex Matching
```bash
if [[ $string =~ ^[0-9]+$ ]]; then
    echo "All digits"
fi

# Capture groups
if [[ $string =~ ([0-9]+)-([0-9]+) ]]; then
    echo "First: ${BASH_REMATCH[1]}"
    echo "Second: ${BASH_REMATCH[2]}"
fi
```

---

# 13. Process Management

## Process Information
```bash
ps aux                     # All processes
ps -ef                     # Full format
pgrep -f "pattern"         # Find by name
pidof process_name         # Get PID
top                        # Interactive monitor
htop                       # Better interactive monitor
```

## Background Processes
```bash
command &                  # Run in background
jobs                       # List background jobs
fg %1                      # Bring job 1 to foreground
bg %1                      # Resume job 1 in background
disown %1                  # Detach job from shell
nohup command &            # Run immune to hangups
wait $pid                  # Wait for process
wait                       # Wait for all background jobs
```

## Process Control
```bash
kill $pid                  # Send SIGTERM
kill -9 $pid               # Send SIGKILL (force)
kill -0 $pid               # Check if process exists
killall process_name       # Kill by name
pkill -f "pattern"         # Kill by pattern
```

## Signals
```bash
trap 'cleanup' EXIT        # Run on exit
trap 'handler' SIGINT      # Handle Ctrl+C
trap '' SIGINT             # Ignore signal
trap - SIGINT              # Reset to default

# Common signals
SIGHUP (1)   - Hangup
SIGINT (2)   - Interrupt (Ctrl+C)
SIGQUIT (3)  - Quit
SIGKILL (9)  - Kill (cannot be caught)
SIGTERM (15) - Terminate
SIGUSR1 (10) - User defined
SIGUSR2 (12) - User defined
```

## Parallel Execution
```bash
# Using &
for file in *.txt; do
    process "$file" &
done
wait  # Wait for all

# Limiting concurrency
max_jobs=4
for file in *.txt; do
    ((i++ >= max_jobs)) && wait -n
    process "$file" &
done
wait

# Using xargs
find . -name "*.txt" | xargs -P 4 -I {} process {}
```

---

# 14. Error Handling

## Exit Status
```bash
# Check exit status
command
if [ $? -eq 0 ]; then
    echo "Success"
else
    echo "Failed"
fi

# Short form
command && echo "Success" || echo "Failed"

# Exit with status
exit 0    # Success
exit 1    # General error
exit 2    # Misuse of command
```

## Strict Mode
```bash
set -e              # Exit on error
set -u              # Error on undefined variable
set -o pipefail     # Fail on pipe errors
set -x              # Debug mode (print commands)

# Combined (recommended for scripts)
set -euo pipefail
```

## Error Handling Patterns
```bash
# Try-catch pattern
{
    command1
    command2
} || {
    echo "Error occurred"
    exit 1
}

# Custom error function
die() {
    echo "ERROR: $1" >&2
    exit "${2:-1}"
}
[ -f "$file" ] || die "File not found: $file"

# Trap ERR
trap 'echo "Error on line $LINENO"' ERR
```

## Validation
```bash
# Check argument count
if [ $# -lt 2 ]; then
    echo "Usage: $0 arg1 arg2"
    exit 1
fi

# Check if file exists
[ -f "$file" ] || { echo "File not found"; exit 1; }

# Check if command exists
command -v git >/dev/null 2>&1 || { echo "git required"; exit 1; }
```

---

# 15. Debugging

## Debug Options
```bash
bash -x script.sh          # Trace execution
bash -n script.sh          # Syntax check only
bash -v script.sh          # Print lines as read

# In script
set -x                     # Enable trace
set +x                     # Disable trace
```

## Debug Output
```bash
# Custom debug function
DEBUG=${DEBUG:-0}
debug() {
    [ "$DEBUG" -eq 1 ] && echo "DEBUG: $*" >&2
}

# Verbose PS4
export PS4='+ ${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]}: '
```

## Common Issues
```bash
# Quote variables
file="my file.txt"
cat "$file"                # Correct
cat $file                  # WRONG - breaks on spaces

# Check empty variables
[ -z "$var" ]              # True if empty
[ -n "$var" ]              # True if not empty

# Use [[ ]] for safety
[[ $var == pattern ]]      # No quotes needed
```

---

# 16. Networking

## HTTP Requests
```bash
# curl
curl http://example.com              # GET request
curl -o file.html http://example.com # Save to file
curl -O http://example.com/file.zip  # Save with original name
curl -I http://example.com           # Headers only
curl -X POST -d "data" http://example.com  # POST
curl -H "Content-Type: application/json" -d '{"key":"value"}' URL
curl -s http://example.com           # Silent mode
curl -L http://example.com           # Follow redirects
curl -u user:pass http://example.com # Basic auth

# wget
wget http://example.com/file
wget -O output.html http://example.com
wget -c http://example.com/file      # Resume download
wget -r http://example.com           # Recursive
```

## Network Commands
```bash
ping -c 4 host                       # Test connectivity
nc -zv host port                     # Test port
netstat -tuln                        # List listening ports
ss -tuln                             # Modern netstat alternative
dig domain                           # DNS lookup
nslookup domain                      # DNS lookup
host domain                          # DNS lookup
ip addr                              # Show IP addresses
ifconfig                             # Show interfaces
```

## SSH Operations
```bash
ssh user@host                        # Connect
ssh user@host 'command'              # Run remote command
ssh -o BatchMode=yes user@host       # Non-interactive
scp file user@host:/path             # Copy to remote
scp user@host:/path/file .           # Copy from remote
rsync -avz source user@host:/dest    # Sync files
```

---

# 17. Advanced Patterns

## Subshells and Groups
```bash
# Subshell - runs in child process
(cd /tmp && ls)            # Directory change doesn't affect parent

# Command group - runs in current shell
{ cd /tmp && ls; }         # Directory change affects parent

# Process substitution
diff <(cmd1) <(cmd2)       # Compare outputs
```

## Coprocesses
```bash
coproc { while read line; do echo "Got: $line"; done; }
echo "Hello" >&${COPROC[1]}
read response <&${COPROC[0]}
```

## Named Pipes (FIFO)
```bash
mkfifo mypipe
cmd1 > mypipe &
cmd2 < mypipe
rm mypipe
```

## Lock Files
```bash
LOCKFILE="/tmp/script.lock"

acquire_lock() {
    exec 200>"$LOCKFILE"
    flock -n 200 || { echo "Already running"; exit 1; }
}

release_lock() {
    rm -f "$LOCKFILE"
}

trap release_lock EXIT
acquire_lock
```

## Configuration Files
```bash
# Source config file
[ -f config.sh ] && source config.sh

# Parse key=value
while IFS='=' read -r key value; do
    # Skip comments and empty lines
    [[ $key =~ ^#.*$ || -z $key ]] && continue
    declare "$key=$value"
done < config.ini
```

## Command-Line Parsing
```bash
# Using getopts (short options)
while getopts "hv:f:" opt; do
    case $opt in
        h) show_help; exit 0 ;;
        v) VERBOSE=$OPTARG ;;
        f) FILE=$OPTARG ;;
        \?) echo "Invalid option"; exit 1 ;;
    esac
done
shift $((OPTIND-1))

# Long options (manual parsing)
while [[ $# -gt 0 ]]; do
    case $1 in
        --help) show_help; exit 0 ;;
        --file=*) FILE="${1#*=}"; shift ;;
        --file) FILE="$2"; shift 2 ;;
        --verbose) VERBOSE=1; shift ;;
        *) echo "Unknown: $1"; exit 1 ;;
    esac
done
```

## JSON Processing with jq
```bash
# Parse JSON
echo '{"name":"John"}' | jq '.name'
echo '{"users":[{"name":"John"}]}' | jq '.users[0].name'

# Extract raw value (without quotes)
jq -r '.name' file.json

# Filter arrays
jq '.users[] | select(.age > 30)' file.json

# Create JSON
jq -n --arg name "John" '{"name": $name}'
```

## Date/Time Operations
```bash
date                              # Current date/time
date +%Y-%m-%d                    # Formatted date
date +%s                          # Unix timestamp
date -d "2024-01-01"              # Parse date
date -d "+1 day"                  # Relative date
date -d "@1704067200"             # From timestamp
TZ="UTC" date                     # Specific timezone

# Calculate difference
start=$(date +%s)
# ... operations ...
end=$(date +%s)
diff=$((end - start))
echo "Took $diff seconds"
```

---

# Quick Reference Tables

## Comparison Operators Summary
| Numeric | String | Meaning |
|---------|--------|---------|
| -eq | = | Equal |
| -ne | != | Not equal |
| -lt | < | Less than |
| -le | | Less than or equal |
| -gt | > | Greater than |
| -ge | | Greater than or equal |
| | -z | Is empty |
| | -n | Is not empty |

## File Test Operators
| Operator | Meaning |
|----------|---------|
| -e | Exists |
| -f | Regular file |
| -d | Directory |
| -L | Symbolic link |
| -r | Readable |
| -w | Writable |
| -x | Executable |
| -s | Size > 0 |

## Common Exit Codes
| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error |
| 2 | Misuse of command |
| 126 | Cannot execute |
| 127 | Command not found |
| 128+n | Killed by signal n |
| 130 | Interrupted (Ctrl+C) |

---

*This cheatsheet covers all concepts needed for the 200 Shell Scripting Mastery curriculum assignments.*
