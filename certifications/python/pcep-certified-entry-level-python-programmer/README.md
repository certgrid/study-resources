# PCEP: Certified Entry-Level Python Programmer - Study Guide

The PCEP (Certified Entry-Level Python Programmer, exam code PCEP-30-02) from the OpenEDG Python Institute validates that you understand the fundamentals of computer programming and can read, write, and reason about basic Python 3 code: data types, operators, control flow, the core collection types, and simple functions with exception handling. It is a vendor-neutral, entry-level credential with no prerequisites, aimed at students, freshers, career changers, and anyone starting an automation, cloud, DevOps, data, or QA path where Python is the on-ramp language. The exam is 45 minutes, has 40 questions across several formats (single- and multiple-choice, drag-and-drop, gap fill, code insertion, and code ordering), and requires 70% to pass. It rewards careful reading of small code snippets and precise knowledge of what Python actually prints, so predicting output correctly matters more than writing large programs.

## Exam at a glance

| Item          | Detail                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------ |
| Exam code     | PCEP-30-02                                                                                 |
| Credential    | PCEP - Certified Entry-Level Python Programmer                                             |
| Vendor        | OpenEDG Python Institute (vendor-neutral, no prerequisites)                                |
| Level         | Entry / Beginner                                                                          |
| Questions     | 40 (single/multiple choice, drag-and-drop, gap fill, code insertion, code ordering)        |
| Duration      | 45 minutes                                                                                |
| Passing score | 70%                                                                                       |
| Delivery      | OpenEDG Testing Service (online proctored) or Pearson VUE                                  |
| Last verified | 2026-07-18                                                                                |
| Official page | https://pythoninstitute.org/pcep                                                          |

## Blocks

| #   | Block                                                                | Weight |
| --- | -------------------------------------------------------------------- | ------ |
| 1   | Computer Programming and Python Fundamentals                         | 18%    |
| 2   | Control Flow - Conditional Blocks and Loops                          | 29%    |
| 3   | Data Collections - Tuples, Dictionaries, Lists, and Strings          | 25%    |
| 4   | Functions and Exceptions                                             | 28%    |

_These are the official PCEP-30-02 exam-block weights. Percentages are approximate and the Python Institute can adjust them between exam revisions, so confirm the current syllabus on the vendor site before your exam. Note that Blocks 2 and 4 together are more than half the exam, so budget the most study time for loops, conditionals, functions, and exceptions._

## How to use this guide

Read top to bottom once for full coverage, then use the tables and the "Output-prediction traps" section as your revision layer. PCEP is a code-reading exam more than a code-writing one: most questions show you a short snippet and ask what it prints, what error it raises, or which line to insert. That means the highest-value skill is tracing execution by hand - tracking the value and type of each variable line by line. Type out and run every snippet in this guide in a real Python 3 interpreter (IDLE, the `python` REPL, or any online sandbox); watching the actual output cements the rules far faster than reading them. Pay close attention to each block's "Common confusions" and "Exam traps," because on PCEP the wrong answers are engineered around exactly those slips: an off-by-one slice, a mistaken operator precedence, a `str` where you expected an `int`. Finish with the readiness checklist and pair the guide with timed practice questions to expose gaps under the clock.

## Key concepts by block

### Block 1 - Computer Programming and Python Fundamentals

This block covers what a program is, how Python runs your code, and the basic building blocks: literals, variables, data types, operators, and the two functions you will use in almost every question, `print()` and `input()`.

**How Python runs your code**

- Python is an interpreted, high-level language. You write source code (a `.py` file); the Python interpreter reads it, compiles it to intermediate bytecode, and a virtual machine executes that bytecode. You do not compile to a standalone machine-code binary the way you would in C.
- CPython is the reference implementation (written in C). Other implementations exist (for example Jython, IronPython, PyPy), but PCEP assumes standard CPython 3 behavior.
- Python 3 is the current language. Python 2 is retired; know that `print` is a function in Python 3 (`print("hi")`), not a statement.
- Source code is plain text and is portable: the same script runs anywhere a compatible interpreter is installed.

**Keywords, literals, and comments**

- Keywords are reserved words you cannot use as names (for example `if`, `else`, `while`, `for`, `def`, `return`, `True`, `False`, `None`, `and`, `or`, `not`, `in`, `is`, `import`, `break`, `continue`). Python is case-sensitive, so `True` is a keyword but `true` is not.
- A literal is a fixed value written directly in code: `10` (int), `3.14` (float), `"text"` (str), `True`/`False` (bool), `None` (the "no value" object).
- Comments start with `#` and run to the end of the line; the interpreter ignores them. Python has no dedicated multi-line comment syntax (a triple-quoted string is a string, not a true comment).

**Core data types**

| Type    | Example literals     | Notes                                                                 |
| ------- | -------------------- | --------------------------------------------------------------------- |
| `int`   | `0`, `42`, `-7`      | Whole numbers, unlimited size in Python 3                             |
| `float` | `3.14`, `1.0`, `2e3` | Numbers with a decimal point or exponent; `2e3` means 2000.0         |
| `str`   | `"hi"`, `'a'`        | Text; single or double quotes are equivalent                          |
| `bool`  | `True`, `False`      | A subclass of int: `True == 1` and `False == 0`                       |
| `None`  | `None`               | The single "no value" object; its type is `NoneType`                  |

**Numeral systems (integer literals)**

| Prefix | System      | Example  | Decimal value |
| ------ | ----------- | -------- | ------------- |
| none   | Decimal     | `255`    | 255           |
| `0b`   | Binary      | `0b1010` | 10            |
| `0o`   | Octal       | `0o17`   | 15            |
| `0x`   | Hexadecimal | `0xFF`   | 255           |

- All four are just different ways of writing the same `int`; `0b1010`, `0o12`, `0xA`, and `10` are equal.

**Operators and precedence**

- Arithmetic: `+`, `-`, `*`, `/` (true division, always returns a `float`), `//` (floor division, rounds toward negative infinity), `%` (modulo, remainder), `**` (exponentiation).
- `/` vs `//`: `7 / 2` is `3.5` (float); `7 // 2` is `3` (int); `7.0 // 2` is `3.0` (float, because one operand is a float).
- `%` gives the remainder: `7 % 2` is `1`, `10 % 3` is `1`. Useful for even/odd tests (`n % 2 == 0`).
- `**` is right-associative: `2 ** 3 ** 2` is `2 ** (3 ** 2)` = `2 ** 9` = `512`, not `(2 ** 3) ** 2` = `64`.
- Unary minus binds tighter than most operators but looser than `**`: `-2 ** 2` is `-(2 ** 2)` = `-4`.

| Precedence (high to low) | Operators                        | Associativity |
| ------------------------ | -------------------------------- | ------------- |
| Highest                  | `**`                             | Right         |
|                          | unary `+x`, `-x`, `~x`           | Right         |
|                          | `*`, `/`, `//`, `%`              | Left          |
|                          | `+`, `-` (binary)                | Left          |
|                          | `<`, `<=`, `>`, `>=`, `==`, `!=` | Left          |
|                          | `not`                            | -             |
|                          | `and`                            | Left          |
| Lowest                   | `or`                             | Left          |

**Variables and assignment**

- A variable is a name bound to a value; you create it by assigning to it: `x = 10`. There is no separate declaration step and no fixed type - the same name can later hold a different type (`x = "now a string"`).
- Names may contain letters, digits, and underscores, but cannot start with a digit and cannot be a keyword. Names are case-sensitive (`total` and `Total` are different).
- Shortcut (augmented) assignment: `x += 1` is `x = x + 1`; likewise `-=`, `*=`, `/=`, `//=`, `%=`, `**=`.

**print(), sep, and end**

```python
print("a", "b", "c")               # a b c        (default sep is a space)
print("a", "b", "c", sep="-")      # a-b-c
print("x", end="")                 # no newline after
print("y")                          # xy
print("1", "2", sep=", ", end="!") # 1, 2!
```

- `print()` separates its arguments with `sep` (default a single space) and finishes with `end` (default `"\n"`, a newline). Setting `end=""` keeps the next output on the same line.

**input() always returns a string**

```python
age = input("Enter age: ")   # user types 25
print(age + 5)               # TypeError: str + int
print(int(age) + 5)          # 30  (cast first)
```

- `input()` reads one line from the user and returns it as a `str`, always. To do math you must cast with `int()` or `float()` first. Forgetting this cast is one of the most common PCEP traps.

**Type casting**

| Call          | Result                | Example                                  |
| ------------- | --------------------- | ---------------------------------------- |
| `int(x)`      | Integer               | `int("10")` -> `10`; `int(3.9)` -> `3` (truncates, does not round) |
| `float(x)`    | Float                 | `float("3.14")` -> `3.14`; `float(5)` -> `5.0` |
| `str(x)`      | String                | `str(42)` -> `"42"`                       |
| `bool(x)`     | Boolean               | `bool(0)` -> `False`; `bool("x")` -> `True` |

- `int("3.5")` raises `ValueError` (the string is not a valid integer). `int(3.9)` is fine and gives `3` because it truncates toward zero, not rounds.

**String `+` and `*`**

- `+` concatenates strings: `"ab" + "cd"` is `"abcd"`. Both operands must be strings; `"a" + 1` raises `TypeError`.
- `*` repeats a string: `"ab" * 3` is `"ababab"`; `"-" * 10` is `"----------"`. The other operand must be an int.

**Escape sequences**

| Sequence | Meaning        |
| -------- | -------------- |
| `\n`     | Newline        |
| `\t`     | Tab            |
| `\\`     | Backslash      |
| `\'`     | Single quote   |
| `\"`     | Double quote   |

- `print("line1\nline2")` prints on two lines. `len("a\nb")` is `3` - an escape sequence is a single character.

**Common confusions:** `/` (float division) vs `//` (floor division); a literal `10` vs the string `"10"`; `int(3.9)` truncating vs rounding; single vs double quotes (no difference in Python); `sep` (between items) vs `end` (after the last item).

**Exam traps:** `input()` always returns a `str`, so `input() + 1` raises `TypeError`. `2 ** 3 ** 2` is `512` because `**` is right-associative. `int("3.5")` raises `ValueError`, but `int(3.5)` returns `3`. `print("a", "b")` puts a space between them by default. `True + True` is `2` because `bool` is a subtype of `int`.

### Block 2 - Control Flow: Conditional Blocks and Loops

This is the heaviest block at 29%. It covers making decisions with `if`/`elif`/`else`, repeating work with `while` and `for`, the loop control statements `break` and `continue`, the loop `else` clause, logic and comparison operators, and bitwise operators. Indentation is not cosmetic in Python - it defines which statements belong to a block, and inconsistent indentation raises an error.

**Conditional statements**

```python
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
else:
    grade = "C"
```

- `if` runs its block when the condition is truthy. `elif` (any number allowed) checks further conditions only if the earlier ones were false. `else` (optional, at most one) runs when none matched.
- Only the first matching branch runs; the rest are skipped. Conditions are tested top to bottom.
- The colon `:` and the indented block are required. An empty block is a syntax error; use `pass` as a placeholder if you need to do nothing.

**Comparison operators**

| Operator | Meaning               | Example (result)     |
| -------- | --------------------- | -------------------- |
| `==`     | Equal to              | `3 == 3` -> `True`   |
| `!=`     | Not equal to          | `3 != 4` -> `True`   |
| `>`      | Greater than          | `5 > 2` -> `True`    |
| `<`      | Less than             | `5 < 2` -> `False`   |
| `>=`     | Greater than or equal | `5 >= 5` -> `True`   |
| `<=`     | Less than or equal    | `4 <= 3` -> `False`  |

- `==` compares values (do not confuse it with `=`, which assigns). Comparisons return a `bool`.

**while loops (and while-else)**

```python
n = 3
while n > 0:
    print(n)
    n -= 1
else:
    print("done")     # runs because the loop ended normally
```

- A `while` loop repeats while its condition is truthy. If the condition is false at the start, the body never runs.
- Always change something inside the loop that moves the condition toward false, or you create an infinite loop.
- The optional `else` on a loop runs once when the loop finishes normally (the condition became false), but is skipped if the loop is ended by `break`.

**for loops and range()**

```python
for i in range(5):        # 0 1 2 3 4
    print(i)

for i in range(2, 8):     # 2 3 4 5 6 7   (start inclusive, stop exclusive)
    print(i)

for i in range(10, 0, -2):  # 10 8 6 4 2  (step can be negative)
    print(i)
```

- `for` iterates over each item of a sequence (a range, list, tuple, string, and so on).
- `range(stop)` goes from `0` up to but not including `stop`. `range(start, stop)` starts at `start`. `range(start, stop, step)` adds `step` each time. The stop value is always excluded.
- `range(5)` produces five values `0..4`. Iterating a string yields one character at a time; iterating a dict yields its keys.

**for-else, break, and continue**

| Statement | Effect                                                                 |
| --------- | ---------------------------------------------------------------------- |
| `break`   | Exits the nearest enclosing loop immediately (skips the loop `else`)   |
| `continue`| Skips the rest of the current iteration and goes to the next one       |
| `else`    | On a loop, runs only if the loop finished without hitting a `break`    |

```python
for n in [4, 7, 9]:
    if n == 7:
        break
else:
    print("no 7 found")   # NOT printed, because break fired
```

- `break` inside a loop cancels the loop `else`. This "search" pattern (loop with `break` on found, `else` for not-found) is a favourite PCEP question.
- `continue` does not exit the loop; it jumps straight to the next iteration.

**Nesting**

- Loops and conditionals can be nested inside each other. `break` and `continue` affect only the innermost loop that contains them, not any outer loop.

**Logic operators and truthiness**

| Operator | Result                                                              |
| -------- | ------------------------------------------------------------------ |
| `and`    | True only if both sides are truthy; returns the deciding operand    |
| `or`     | True if either side is truthy; returns the first truthy operand     |
| `not`    | Inverts the boolean value (`not True` is `False`)                   |

- Falsy values in Python: `False`, `None`, `0`, `0.0`, `""` (empty string), `[]`, `()`, `{}` (empty collections). Everything else is truthy.
- Short-circuiting: `and` stops at the first falsy operand; `or` stops at the first truthy operand. The rest is never evaluated, so `x != 0 and 10 / x > 1` safely avoids dividing by zero.
- `and`/`or` return one of their operands, not necessarily `True`/`False`: `2 or 0` is `2`; `0 or "hi"` is `"hi"`; `3 and 4` is `4`; `0 and 4` is `0`.

**Bitwise operators**

| Operator | Name        | Example       | Result |
| -------- | ----------- | ------------- | ------ |
| `&`      | AND         | `6 & 3`       | `2`    |
| `\|`     | OR          | `6 \| 3`      | `7`    |
| `^`      | XOR         | `6 ^ 3`       | `5`    |
| `~`      | NOT (invert)| `~6`          | `-7`   |
| `<<`     | Left shift  | `1 << 3`      | `8`    |
| `>>`     | Right shift | `16 >> 2`     | `4`    |

- Bitwise operators work on the binary bits of integers (for example `6` is `0b110`, `3` is `0b011`, so `6 & 3` is `0b010` = `2`).
- `~x` equals `-(x + 1)` (two's complement), so `~6` is `-7`.
- Left shift by `n` multiplies by `2**n`; right shift by `n` is integer division by `2**n`. Do not confuse bitwise `&`/`|` with the logical `and`/`or`.

**Common confusions:** `=` (assignment) vs `==` (comparison); logical `and`/`or` vs bitwise `&`/`|`; `break` (leave the loop) vs `continue` (skip to next iteration); `range(1, 5)` producing `1,2,3,4` (stop excluded); the loop `else` running on normal completion vs being skipped by `break`.

**Exam traps:** `range(a, b)` excludes `b`, so `range(2, 8)` yields `2..7`. A loop `else` is skipped whenever `break` fires. `and`/`or` return an operand, not always a boolean (`5 or 0` is `5`). Empty collections and `0` are falsy. `~6` is `-7`, not `-6`. `break` only exits the innermost loop.

### Block 3 - Data Collections: Tuples, Dictionaries, Lists, and Strings

This block (25%) is about the four core sequence and collection types. The single most important idea is mutability: lists and dictionaries can be changed in place, while tuples and strings cannot. Indexing and slicing rules are shared across the sequence types and are heavily tested.

**Collection types at a glance**

| Type    | Literal example        | Mutable? | Ordered?              | Indexed by        | Duplicates? |
| ------- | ---------------------- | -------- | --------------------- | ----------------- | ----------- |
| `list`  | `[1, 2, 3]`            | Yes      | Yes                   | Integer position  | Yes         |
| `tuple` | `(1, 2, 3)`            | No       | Yes                   | Integer position  | Yes         |
| `dict`  | `{"a": 1, "b": 2}`     | Yes      | Yes (insertion order) | Key               | Keys unique |
| `str`   | `"abc"`                | No       | Yes                   | Integer position  | Yes         |

- "Mutable" means you can change contents in place after creation. Lists and dicts are mutable; tuples and strings are not. Any "change" to a string or tuple actually builds a new object.

**Indexing and slicing (shared by lists, tuples, strings)**

```python
s = "python"
s[0]      # 'p'   (first item, index starts at 0)
s[-1]     # 'n'   (last item; negative counts from the end)
s[1:4]    # 'yth' (start inclusive, stop exclusive)
s[:3]     # 'pyt' (omitted start means 0)
s[3:]     # 'hon' (omitted stop means end)
s[::2]    # 'pto' (step of 2)
s[::-1]   # 'nohtyp' (reversed)
```

- Indexing is zero-based. `s[0]` is the first item; the last item is `s[len(s)-1]` or `s[-1]`.
- A slice `s[start:stop]` includes `start` but excludes `stop`, so its length is `stop - start` (when both are in range). This off-by-one is a top PCEP trap.
- An out-of-range index raises `IndexError`, but an out-of-range slice does not - it just clips to what exists.

**Lists**

```python
nums = [10, 20, 30]
nums.append(40)        # [10, 20, 30, 40]
nums.insert(1, 15)     # [10, 15, 20, 30, 40]
nums.remove(20)        # removes first 20
last = nums.pop()      # removes and returns the last item
nums[0] = 99           # in-place change (lists are mutable)
len(nums)              # number of items
squares = [x * x for x in range(5)]   # [0, 1, 4, 9, 16]  (comprehension)
grid = [[1, 2], [3, 4]]               # 2D list; grid[1][0] is 3
```

| Method / op        | Effect                                              |
| ------------------ | --------------------------------------------------- |
| `append(x)`        | Add `x` to the end                                  |
| `insert(i, x)`     | Insert `x` before index `i`                         |
| `remove(x)`        | Remove the first occurrence of value `x`            |
| `pop([i])`         | Remove and return item at `i` (default last)        |
| `sort()`           | Sort in place; `sorted(lst)` returns a new list     |
| `reverse()`        | Reverse in place                                    |
| `len(lst)`         | Count of items                                      |
| `x in lst`         | Membership test, returns a bool                     |

- Aliasing vs copying: `b = a` makes `b` another name for the same list, so changing one changes both. To get an independent copy use `b = a[:]`, `b = a.copy()`, or `b = list(a)`.

```python
a = [1, 2, 3]
b = a          # alias: same object
b.append(4)
print(a)       # [1, 2, 3, 4]  <- a changed too

c = a[:]       # copy: new object
c.append(9)
print(a)       # [1, 2, 3, 4]  <- a unaffected
```

**Tuples**

```python
t = (1, 2, 3)
t[0]              # 1
one = (5,)        # single-element tuple NEEDS the trailing comma
not_tuple = (5)   # this is just the int 5
a, b, c = t       # unpacking: a=1, b=2, c=3
packed = 1, 2, 3  # packing: parentheses optional -> (1, 2, 3)
```

- Tuples are immutable: `t[0] = 9` raises `TypeError`. They have no `append`, `insert`, or `remove`.
- A one-element tuple requires the trailing comma: `(5,)` is a tuple, but `(5)` is just the integer `5`.
- Packing bundles values into a tuple; unpacking spreads a tuple's items into separate variables (the counts must match).

**Dictionaries**

```python
d = {"name": "Ann", "age": 30}
d["name"]            # 'Ann'   (index by key)
d["city"] = "Pune"   # add a new key (dicts are mutable)
d["age"] = 31        # update an existing key
d.get("email")       # None    (no KeyError, returns default)
d.get("email", "n/a")# 'n/a'
"age" in d           # True    (membership tests keys)
d.keys()             # dict_keys(['name', 'age', 'city'])
d.values()           # the values
d.items()            # key/value pairs, good for looping
```

- Access a value by its key with `d[key]`. A missing key with `d[key]` raises `KeyError`; `d.get(key)` returns `None` (or a default you supply) instead of raising.
- Keys must be unique and hashable (strings, numbers, tuples work; lists cannot be keys). Assigning to an existing key overwrites its value.
- `in` on a dict tests the keys, not the values. Looping `for k in d:` gives keys; `for k, v in d.items():` gives both.

**Strings**

```python
s = "Hello"
len(s)          # 5
s.upper()       # 'HELLO'   (returns a NEW string; s is unchanged)
s.lower()       # 'hello'
s.replace("l", "L")  # 'HeLLo'
"a,b,c".split(",")   # ['a', 'b', 'c']
"-".join(["a", "b"]) # 'a-b'
"Hello".find("l")    # 2   (index of first match, -1 if none)
ord("A")        # 65   (character to its code point)
chr(66)         # 'B'  (code point back to a character)
```

- Strings are immutable: `s[0] = "h"` raises `TypeError`. Methods like `upper()` and `replace()` return a new string and leave the original untouched.
- Index and slice strings exactly like lists. `"abc"[1]` is `"b"`.
- `ord(c)` gives the Unicode code point of a single character; `chr(n)` converts a code point back to a character. They are inverses: `chr(ord("A"))` is `"A"`.

| Method            | Returns                                       |
| ----------------- | --------------------------------------------- |
| `upper()`/`lower()` | New string in that case                     |
| `strip()`         | New string with leading/trailing whitespace removed |
| `replace(a, b)`   | New string with all `a` replaced by `b`       |
| `split(sep)`      | List of substrings                            |
| `join(iterable)`  | Single string joined by the separator         |
| `find(sub)`       | Index of first match, or `-1`                 |

**Common confusions:** list (mutable) vs tuple (immutable); `d[key]` (raises `KeyError` if missing) vs `d.get(key)` (returns `None`); `(5)` (an int) vs `(5,)` (a tuple); aliasing (`b = a`) vs copying (`b = a[:]`); `in` on a dict testing keys not values; string methods returning a new string rather than editing in place.

**Exam traps:** A slice `s[1:4]` has length 3 and excludes index 4. Strings and tuples are immutable, so item assignment raises `TypeError`. `(5)` is not a tuple; you need the trailing comma. `d[key]` on a missing key raises `KeyError`. `b = a` aliases the same list, so mutating through `b` is visible through `a`. Negative indexes count from the end (`s[-1]` is the last item).

### Block 4 - Functions and Exceptions

This block (28%) covers defining and calling functions, how arguments are passed, variable scope, and handling runtime errors with `try`/`except`. Together with Block 2 it makes up most of the exam.

**Defining and calling functions**

```python
def greet(name):
    return "Hi " + name

message = greet("Sam")   # call; "Sam" is the argument
print(message)           # Hi Sam
```

- `def` defines a function; the code runs only when you call the function with `name(...)`. Defining is not calling.
- Parameters are the names in the definition (`name`); arguments are the actual values you pass in the call (`"Sam"`).
- A function ends when it hits `return` or reaches the end of its body.

**return and None**

```python
def add(a, b):
    return a + b        # sends a value back

def show(x):
    print(x)            # no return -> returns None

r = show(5)             # prints 5
print(r)                # None
```

- `return value` ends the function and hands `value` back to the caller. A function with no `return` (or a bare `return`) returns `None`.
- Any code after a `return` that runs is unreachable within that call.

**Parameters: positional, keyword, and default**

```python
def power(base, exp=2):        # exp has a default value
    return base ** exp

power(3)                        # 9   (exp defaults to 2)
power(3, 3)                     # 27  (positional)
power(exp=3, base=2)            # 8   (keyword args, order free)
```

- Positional arguments are matched by position; keyword arguments are matched by name (`base=2`) and can appear in any order.
- Default parameter values are used when the caller omits that argument. Parameters with defaults must come after parameters without defaults in the definition.
- You cannot supply a positional argument after a keyword argument in the same call.

**Scope: local vs global**

```python
x = 10                # global

def f():
    x = 5             # a NEW local x, does not touch the global
    print(x)          # 5

f()
print(x)              # 10  (global unchanged)

def g():
    global x
    x = 99            # now rebinds the global

g()
print(x)              # 99
```

- A name assigned inside a function is local to that function by default and disappears when the function returns.
- Code inside a function can read a global variable, but to reassign (rebind) a global name you must declare `global name` first.
- A local name shadows a global of the same name within that function only.

**Passing collections: mutation vs rebinding**

```python
def add_item(lst):
    lst.append(99)      # mutates the caller's list (same object)

def rebind(lst):
    lst = [0, 0, 0]     # rebinds the local name only; caller unaffected

data = [1, 2, 3]
add_item(data)
print(data)             # [1, 2, 3, 99]
rebind(data)
print(data)             # [1, 2, 3, 99]  (unchanged by rebind)
```

- Arguments are passed by object reference. If you mutate a mutable argument in place (for example `list.append`), the caller sees the change. If you rebind the parameter to a new object, only the local name changes and the caller's object is untouched.
- Immutable arguments (int, str, tuple) cannot be changed in place at all, so a function can never alter the caller's original value for those.

**Exceptions: try / except / else / finally**

```python
try:
    x = int(input("number: "))
    print(10 / x)
except ValueError:
    print("not a valid number")
except ZeroDivisionError:
    print("cannot divide by zero")
else:
    print("worked")        # runs only if no exception was raised
finally:
    print("always runs")   # runs no matter what
```

| Clause    | Runs when                                                         |
| --------- | ---------------------------------------------------------------- |
| `try`     | Always; contains the code that might fail                         |
| `except`  | Only if a matching exception was raised in `try`                  |
| `else`    | Only if the `try` block finished with no exception                |
| `finally` | Always, whether or not an exception occurred (cleanup)            |

- Order matters: put more specific exceptions before broader ones. A bare `except:` (or `except Exception:`) catches everything, so place it last.
- Once an exception is caught by a matching `except`, remaining `except` clauses are skipped.

**raise and assert**

```python
def withdraw(amount):
    if amount < 0:
        raise ValueError("amount must be non-negative")

assert 2 + 2 == 4          # passes silently
assert 1 == 2, "math broke" # raises AssertionError: math broke
```

- `raise` deliberately triggers an exception; you can re-raise inside an `except` or raise a fresh one to signal an error.
- `assert condition, message` raises `AssertionError` if the condition is falsy; it is a sanity check, not a substitute for normal error handling.

**Common built-in exceptions**

| Exception           | Typical cause                                                    |
| ------------------- | --------------------------------------------------------------- |
| `ValueError`        | Right type, wrong value: `int("abc")`                            |
| `TypeError`         | Wrong type for the operation: `"a" + 1`, `len(5)`               |
| `ZeroDivisionError` | Dividing or modulo by zero: `10 / 0`, `5 % 0`                    |
| `IndexError`        | Sequence index out of range: `[1, 2][5]`                         |
| `KeyError`          | Missing dictionary key: `{"a": 1}["b"]`                          |

- Match the error to the cause: a bad conversion is a `ValueError`, mixing incompatible types is a `TypeError`, an out-of-range list index is an `IndexError`, and a missing dict key is a `KeyError`.

**Common confusions:** defining a function (`def`) vs calling it (`name()`); parameter (definition) vs argument (call); positional vs keyword arguments; local vs global scope and when `global` is needed; mutating a list argument in place vs rebinding the parameter; `except` (only on error) vs `finally` (always) vs `else` (only when no error).

**Exam traps:** a function with no `return` returns `None`. Assigning to a name inside a function makes it local unless you declare `global`. `list.append` inside a function changes the caller's list; reassigning the parameter does not. `int("abc")` is a `ValueError`, `"a" + 1` is a `TypeError`, `d["missing"]` is a `KeyError`. `finally` runs even if the `try` or `except` block returns or raises. Parameters with defaults must follow those without.

## Output-prediction traps

PCEP loves "what does this print?" questions built on a handful of rules. Memorize these outcomes.

| Snippet                          | Output / result | Why                                                                       |
| -------------------------------- | --------------- | ------------------------------------------------------------------------- |
| `print(2 ** 3 ** 2)`             | `512`           | `**` is right-associative: `2 ** (3 ** 2)` = `2 ** 9`                     |
| `print(-2 ** 2)`                 | `-4`            | `**` binds tighter than unary minus: `-(2 ** 2)`                         |
| `print(7 / 2)`                   | `3.5`           | `/` is true division, always a float                                     |
| `print(7 // 2)`                  | `3`             | `//` floors toward negative infinity                                     |
| `print(7 % 3)`                   | `1`             | Modulo returns the remainder                                             |
| `print(int(3.9))`                | `3`             | `int()` truncates toward zero, it does not round                         |
| `print("ab" * 3)`                | `ababab`        | `*` repeats a string                                                     |
| `print("py"[1:4])`               | `y`             | Slice stops before index 4, and the string is only 2 chars, so clips     |
| `print([1, 2, 3][-1])`           | `3`             | Negative index counts from the end                                       |
| `print(len(range(2, 10, 2)))`    | `4`             | `range(2,10,2)` is `2,4,6,8` - stop excluded                            |
| `print(5 or 0)`                  | `5`             | `or` returns the first truthy operand, not a bool                        |
| `print(0 and 5)`                 | `0`             | `and` short-circuits and returns the first falsy operand                 |
| `print(bool(""), bool("0"))`     | `False True`    | Empty string is falsy; a non-empty string (even `"0"`) is truthy         |
| `print(1 == 1.0)`                | `True`          | `==` compares value across int and float                                 |
| `a=[1,2]; b=a; b.append(3)`      | `a` is `[1,2,3]`| `b = a` aliases the same list, so `a` sees the append                     |
| `print(True + True)`             | `2`             | `bool` is a subclass of `int`                                            |

## 5-day study plan

This is a revision-paced plan for someone who has written a little Python already. Complete beginners should stretch it over two to three weeks and spend extra time typing and running every snippet in a real interpreter.

| Day | Focus                                                                                                   | Blocks              |
| --- | ------------------------------------------------------------------------------------------------------- | ------------------- |
| 1   | How Python runs, data types, literals, numeral systems, operators and precedence, `print`/`input`, casting | Block 1             |
| 2   | `if`/`elif`/`else`, comparisons, `while`/`for`, `range`, `break`/`continue`, loop `else`                 | Block 2 (part 1)    |
| 3   | Logic operators, truthy/falsy, short-circuiting, bitwise operators, nested loops                        | Block 2 (part 2)    |
| 4   | Lists, tuples, dictionaries, strings, indexing/slicing, mutability, aliasing vs copy                    | Block 3             |
| 5   | Functions, arguments, scope and `global`, exceptions (`try`/`except`/`else`/`finally`), then a full timed mock and review | Block 4 + full review |

## Readiness checklist

You are ready when you can...

- Explain how Python runs a program (interpreter, bytecode, virtual machine) and that Python 3 `print` is a function.
- Read `0b`, `0o`, `0x` literals and tell an `int` from a `float` from a `str`.
- Predict operator-precedence outcomes, including `**` being right-associative and the difference between `/`, `//`, and `%`.
- Use `print()` with `sep` and `end`, and remember that `input()` returns a `str` that must be cast for math.
- Trace `if`/`elif`/`else`, `while`, and `for` with `range(start, stop, step)`, and know that `stop` is excluded.
- Explain `break` vs `continue`, and when a loop `else` runs versus when it is skipped.
- Evaluate `and`/`or`/`not` with truthy/falsy values and short-circuiting, and distinguish them from bitwise `&`, `|`, `^`, `~`, `<<`, `>>`.
- Index and slice lists, tuples, and strings correctly, including negative indexes and the slice off-by-one.
- Say which of list, tuple, dict, and string are mutable, and tell aliasing (`b = a`) from copying (`b = a[:]`).
- Use dictionary access safely (`d[key]` vs `d.get(key)`) and know that `in` on a dict tests keys.
- Define and call functions, use positional/keyword/default arguments, and explain local vs global scope and the `global` keyword.
- Predict whether a function mutates or leaves a passed-in collection unchanged.
- Structure `try`/`except`/`else`/`finally`, use `raise` and `assert`, and match `ValueError`, `TypeError`, `ZeroDivisionError`, `IndexError`, and `KeyError` to their causes.

---

Want the full breakdown? See the complete **[PCEP study guide](https://certgrid.app/study-guide/pcep-certified-entry-level-python-programmer)** and **[free practice questions](https://certgrid.app/practice/pcep-certified-entry-level-python-programmer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_
