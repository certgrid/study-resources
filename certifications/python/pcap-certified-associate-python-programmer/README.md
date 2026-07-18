# PCAP: Certified Associate Python Programmer - Study Guide

The PCAP (Certified Associate Python Programmer, exam code PCAP-31-03) from the OpenEDG Python Institute validates that you can write real Python 3 programs using modules and packages, exception handling, string processing, object-oriented programming, and the standard-library building blocks (iterators, generators, closures, comprehensions, and file I/O). It is a genuine step up from the entry-level PCEP: it expects working knowledge of classes, inheritance, and the method resolution order, not just syntax recall. It is aimed at people who already know Python basics and are moving into IT automation, scripting, DevOps, data, or security work where Python is the glue language. The exam is 65 minutes, has 40 questions across several formats (single- and multiple-choice, drag and drop, gap fill, code insertion, and code ordering), and requires 70% to pass.

## Exam at a glance

| Item             | Detail                                                                          |
| ---------------- | ------------------------------------------------------------------------------- |
| Exam code        | PCAP-31-03                                                                       |
| Credential       | PCAP - Certified Associate Python Programmer                                     |
| Vendor           | OpenEDG Python Institute                                                         |
| Level            | Associate (a step up from PCEP; real OOP and module depth)                       |
| Prerequisites    | None enforced; PCEP or equivalent Python basics strongly recommended            |
| Questions        | 40 (single/multi choice, drag and drop, gap fill, code insertion, ordering)     |
| Duration         | 65 minutes                                                                       |
| Passing score    | 70%                                                                              |
| Language version | Python 3                                                                         |
| Delivery         | OpenEDG testing service or Pearson VUE (test center or online proctored)         |
| Last verified    | 2026-07-18                                                                       |
| Official page    | https://pythoninstitute.org/pcap                                                 |

## Blocks

| #   | Block                                                            | Weight |
| --- | --------------------------------------------------------------- | ------ |
| 1   | Modules and Packages                                            | 12%    |
| 2   | Exceptions                                                      | 14%    |
| 3   | Strings                                                         | 18%    |
| 4   | Object-Oriented Programming                                     | 34%    |
| 5   | Miscellaneous (comprehensions, lambdas, closures, I/O)          | 22%    |

_These are the official PCAP-31-03 block weights published by the OpenEDG Python Institute. Weightings can shift between syllabus revisions, so confirm the current objectives on the vendor site before your exam. Note that Object-Oriented Programming alone is 34%, larger than any two other blocks combined, so it is where the exam is won or lost._

## How to use this guide

Work through the blocks top to bottom once for full coverage, then use the tables and the "Output-prediction traps" section as your revision layer. PCAP is a hands-on exam: many questions show you a short program and ask what it prints, whether it raises an error, or which line to insert, so reading the code carefully beats memorizing definitions. Budget your study time by weight. Object-Oriented Programming is the single biggest block at 34%, so plan for it to take roughly a third of your total effort, and make sure you can trace instance versus class variables, `super()`, the method resolution order (MRO), and the dunder methods without hesitation. Read the "Common confusions" and "Exam traps" notes at the end of each block closely, because most wrong answers come from two look-alike features (for example `find` versus `index`, `is` versus `==`, or `@classmethod` versus `@staticmethod`) rather than from a feature you have never seen. Finish with the readiness checklist and pair the guide with timed practice questions to expose gaps.

## Key concepts by block

### Block 1 - Modules and Packages

This block covers how Python code is organized into reusable files and folders, how the import machinery finds and loads them, the three standard-library modules the syllabus names explicitly (`math`, `random`, `platform`), and how to build your own module and package.

**Import variants**

| Statement                        | What it binds in the current namespace                     | How you then use it        |
| -------------------------------- | ---------------------------------------------------------- | -------------------------- |
| `import math`                    | The whole module object, named `math`                      | `math.sqrt(9)`             |
| `import math as m`               | The module object under the alias `m`                      | `m.sqrt(9)`                |
| `from math import sqrt`          | Only the `sqrt` name, directly                             | `sqrt(9)`                  |
| `from math import sqrt as s`     | The `sqrt` function under the alias `s`                    | `s(9)`                     |
| `from math import *`             | Every public name (those not starting with `_`, or the module's `__all__`) | `sqrt(9)`, `pi`, ... |

- `from module import *` is convenient but discouraged: it can silently overwrite names you already have and makes it unclear where a name came from. If a module defines `__all__`, only the names listed there are imported by the star form.
- A module is imported and its top-level code executed only once per interpreter session; later imports reuse the cached module object.

**The three named standard modules**

| Module     | Representative members                                                                                     |
| ---------- | --------------------------------------------------------------------------------------------------------- |
| `math`     | `pi`, `e`, `sqrt()`, `ceil()`, `floor()`, `trunc()`, `factorial()`, `hypot()`, `gcd()`, `log()`, `sin()`, `radians()`, `degrees()` |
| `random`   | `random()`, `randint(a, b)`, `randrange(start, stop, step)`, `choice(seq)`, `sample(pop, k)`, `shuffle(list)`, `seed()` |
| `platform` | `platform()`, `system()`, `machine()`, `processor()`, `version()`, `python_version()`, `python_implementation()` |

- `random.random()` returns a float in the half-open range 0.0 (inclusive) to 1.0 (exclusive). `random.randint(a, b)` returns an integer with both ends inclusive. `random.randrange(a, b)` excludes the upper bound, exactly like `range`.
- `math.ceil()`, `math.floor()`, and `math.trunc()` return integers in Python 3. `math.floor(-2.5)` is `-3` (toward negative infinity), while `math.trunc(-2.5)` is `-2` (toward zero) - a classic trap.
- `platform` values are strings, for example `platform.python_version()` returns something like `'3.12.4'`.

**Running as a script versus importing: `__name__`**

```python
def main():
    print("running")

if __name__ == "__main__":
    main()
```

- When a file is run directly (`python prog.py`), Python sets its `__name__` to the string `"__main__"`. When the same file is imported, `__name__` is the module's own name (for example `"prog"`).
- The `if __name__ == "__main__":` guard therefore lets a file act as both a runnable script and an importable module without executing the script part on import.

**The module search path, bytecode cache, and introspection**

| Feature        | What it is                                                                                        |
| -------------- | ------------------------------------------------------------------------------------------------- |
| `sys.path`     | A list of directory strings searched (in order) when importing; you can append to it at runtime   |
| `__pycache__`  | A folder where Python caches compiled bytecode as `.pyc` files to speed up later imports           |
| `.pyc` file    | Compiled bytecode, named like `module.cpython-312.pyc`; regenerated when the source changes        |
| `dir(obj)`     | Returns a sorted list of the names (attributes) an object or module exposes                         |
| `help(obj)`    | Prints the docstring-based help for a module, function, or object                                   |

- `sys.path` is seeded from the script's directory, the `PYTHONPATH` environment variable, and installation defaults. Because it is a normal list, `sys.path.append("/my/libs")` can add a location at runtime.
- A package is a directory of modules. Historically it needed an `__init__.py` file (which runs on package import and can expose a package-level API); since Python 3.3, namespace packages can omit it, but the exam still treats `__init__.py` as the standard marker.

**Common confusions:** `import module` (access as `module.name`) versus `from module import name` (access as bare `name`); `math.floor`/`ceil` (round toward negative/positive infinity) versus `trunc` (toward zero); `randint` (upper bound included) versus `randrange` (upper bound excluded).

**Exam traps:** `from module import *` skips names starting with an underscore unless `__all__` says otherwise. A module's top-level code runs once, on first import, not on every import. `sys.path` is an ordinary list you can modify. `__pycache__` and `.pyc` files are an optimization, not something you write by hand.

### Block 2 - Exceptions

This block covers structured error handling: the `try` compound statement, the built-in exception class hierarchy, raising and re-raising, writing your own exceptions, assertions, and reading the exception object.

**The `try` statement clauses**

| Clause         | Runs when...                                                          | Typical use                        |
| -------------- | -------------------------------------------------------------------- | ---------------------------------- |
| `try`          | Always; wraps the code that might fail                                | The protected operation            |
| `except`       | A matching exception was raised in `try`                              | Handle a specific error            |
| `else`         | The `try` block finished with no exception                            | Code that depends on success       |
| `finally`      | Always, whether or not an exception occurred, even on `return`        | Cleanup (close files, release locks) |

```python
try:
    x = int(data)
except ValueError:
    print("not a number")
else:
    print("parsed", x)   # only if no exception
finally:
    print("done")        # always
```

- Order your `except` clauses from most specific to most general. Python tries them top to bottom and stops at the first match, so if a base class like `Exception` comes before a subclass like `ValueError`, the subclass clause becomes unreachable.
- Catching a base class catches all of its subclasses. `except LookupError:` handles both `IndexError` and `KeyError`; `except Exception:` handles almost everything a normal program can raise.

**Built-in exception hierarchy (abridged)**

```
BaseException
 +-- SystemExit
 +-- KeyboardInterrupt
 +-- GeneratorExit
 +-- Exception
      +-- ArithmeticError
      |    +-- ZeroDivisionError
      |    +-- OverflowError
      +-- LookupError
      |    +-- IndexError
      |    +-- KeyError
      +-- ValueError
      +-- TypeError
      +-- OSError  (FileNotFoundError, PermissionError, ...)
      +-- ImportError  (ModuleNotFoundError)
```

- `SystemExit`, `KeyboardInterrupt`, and `GeneratorExit` inherit from `BaseException`, not `Exception`. A bare `except Exception:` deliberately does not catch them, which is why you should catch `Exception`, not `BaseException`, in normal code.
- Know the family names: division by zero is `ZeroDivisionError` (under `ArithmeticError`); a bad list index is `IndexError` and a missing dict key is `KeyError` (both under `LookupError`); `int("x")` raises `ValueError`; `"a" + 5` raises `TypeError`.

**Raising, re-raising, custom exceptions, and asserting**

| Construct                        | Effect                                                                     |
| -------------------------------- | -------------------------------------------------------------------------- |
| `raise ValueError("bad")`        | Raise a new exception with a message                                        |
| `raise` (bare, inside `except`)  | Re-raise the exception currently being handled, preserving its traceback    |
| `class MyError(Exception): ...`  | Define a custom exception by subclassing `Exception`                        |
| `assert cond, "msg"`             | Raise `AssertionError("msg")` if `cond` is false; do nothing if true        |

- A bare `raise` re-raises the active exception, which is useful for logging then letting it propagate. `raise` outside any active exception context raises `RuntimeError`.
- Custom exceptions should subclass `Exception` (or a more specific built-in), not `BaseException`. They inherit message handling for free.
- `assert` is for internal sanity checks, not for validating user input, because running Python with the `-O` (optimize) flag removes all `assert` statements.

**The exception object and `args`**

```python
try:
    raise ValueError("bad value", 42)
except ValueError as e:
    print(e.args)   # ('bad value', 42)
    print(str(e))   # ('bad value', 42) as text
```

- `except SomeError as e:` binds the exception instance to `e`. Its `args` attribute is the tuple of arguments passed to the constructor; `str(e)` gives the printable message.

**Common confusions:** `BaseException` (root of everything) versus `Exception` (root of normal, catchable errors); `IndexError` (bad sequence index) versus `KeyError` (missing mapping key); `assert` (a debugging aid, stripped by `-O`) versus `raise` (a real, always-present error).

**Exam traps:** A more general `except` placed before a specific one makes the specific one dead code. Catching `Exception` will not stop `KeyboardInterrupt` or `SystemExit`. `finally` runs even when `try` or `except` executes a `return`. `assert` disappears under `-O`, so never rely on it for control flow.

### Block 3 - Strings

This block covers the string type in depth: its methods, the three formatting styles, immutability, slicing (including reversal), character/code-point conversion, and lexicographic comparison.

**High-value string methods**

| Method                  | Returns                                                        | Note                                              |
| ----------------------- | ------------------------------------------------------------- | ------------------------------------------------- |
| `s.find(sub)`           | Lowest index of `sub`, or `-1` if absent                      | Safe: no exception when not found                 |
| `s.index(sub)`          | Lowest index of `sub`                                         | Raises `ValueError` if `sub` is not present       |
| `s.split(sep)`          | List of substrings                                            | No arg splits on any run of whitespace            |
| `sep.join(iterable)`    | Single string joined by `sep`                                 | Every item in the iterable must be a string       |
| `s.strip(chars)`        | Copy with leading/trailing `chars` removed                    | `lstrip`/`rstrip` do one side; default is whitespace |
| `s.replace(old, new)`   | Copy with all `old` replaced by `new`                         | Optional count argument limits replacements       |
| `s.center(w, fill)`     | Copy centered in width `w`                                    | Padded with `fill` (default space)                |
| `s.zfill(w)`            | Copy left-padded with `'0'` to width `w`                      | Keeps a leading sign: `"-9".zfill(4)` -> `"-009"` |

- The `is*` predicates test the whole string and return a boolean: `isalpha()`, `isdigit()`, `isalnum()`, `isspace()`, `islower()`, `isupper()`, `istitle()`, `isidentifier()`. On an empty string they return `False`.
- `find` versus `index` is the single most tested string pair: same result when the substring exists, but `find` returns `-1` on failure while `index` raises `ValueError`. The same holds for `rfind` versus `rindex`.

**The three formatting styles**

| Style        | Example                          | Result       |
| ------------ | -------------------------------- | ------------ |
| `%` operator | `"%d-%s" % (7, "ok")`            | `"7-ok"`     |
| `str.format` | `"{0}-{name}".format(7, name="ok")` | `"7-ok"`  |
| f-string     | `f"{7}-{'ok'}"`                  | `"7-ok"`     |

**Format specification mini-language**

| Spec        | Meaning                                | Example (`value = 42`)      |
| ----------- | -------------------------------------- | --------------------------- |
| `{:>8}`     | Right-align in width 8                  | `"      42"`                |
| `{:<8}`     | Left-align in width 8                   | `"42      "`                |
| `{:^8}`     | Center in width 8                       | `"   42   "`                |
| `{:08}`     | Zero-pad to width 8                     | `"00000042"`                |
| `{:.2f}`    | Fixed point, 2 decimals                 | `"42.00"`                   |
| `{:,}`      | Thousands separator                     | `"42"` (`1000000` -> `"1,000,000"`) |
| `{:x}` / `{:b}` | Hex / binary                        | `"2a"` / `"101010"`         |

- Strings are immutable. Every method that "changes" a string actually returns a new one, and you cannot assign to a character position: `s[0] = "X"` raises `TypeError`.
- Slicing is `s[start:stop:step]`, with `stop` excluded. `s[::-1]` reverses a string, `s[::2]` takes every other character, and negative indices count from the end.
- `ord(ch)` gives a character's Unicode code point (`ord("A")` is `65`) and `chr(n)` gives the character for a code point (`chr(97)` is `"a"`). They are inverses.
- String comparison is lexicographic by code point, character by character. Because `"A"` is 65 and `"a"` is 97, every uppercase letter sorts before every lowercase letter, so `"Z" < "a"` is `True`.

**Common confusions:** `find` (returns `-1`) versus `index` (raises `ValueError`); `split` (string to list) versus `join` (iterable to string); `zfill` (pads with zeros, keeps the sign) versus `rjust`/`center` (pad with spaces); slicing (returns a new string, never errors on out-of-range bounds) versus indexing (raises `IndexError`).

**Exam traps:** Strings are immutable, so item assignment fails. `"".join(...)` requires every element to already be a string, or it raises `TypeError`. An empty string makes every `is*` predicate return `False`. Out-of-range slice bounds are clamped silently, but an out-of-range single index raises `IndexError`. Uppercase sorts before lowercase.

### Block 4 - Object-Oriented Programming

This is the largest block at 34%. It covers classes and objects, instance versus class variables, encapsulation and name mangling, inheritance with `super()`, multiple inheritance and the method resolution order, polymorphism, type checks, the special (dunder) methods, `@classmethod` versus `@staticmethod`, and introspection.

**Classes, objects, `__init__`, and `self`**

```python
class Dog:
    species = "Canis"          # class variable, shared

    def __init__(self, name):
        self.name = name       # instance variable, per object

    def speak(self):           # self is the instance
        return f"{self.name} barks"
```

- `__init__` is the initializer (constructor) run when an object is created. `self` is the automatic first parameter of instance methods and refers to the instance the method was called on.

**Instance versus class variables (the shared-mutable trap)**

| Aspect          | Class variable                                | Instance variable                          |
| --------------- | --------------------------------------------- | ------------------------------------------ |
| Defined         | In the class body                             | On `self`, usually inside `__init__`        |
| Storage         | Once, shared by every instance                | Separately in each object's `__dict__`      |
| Read            | Found via the class if not on the instance    | Found directly on the instance              |
| Rebinding on `self` | Creates a new instance variable that shadows the class one | Just updates the instance      |

- Reading an attribute checks the instance first, then the class. Assigning `self.x = ...` always creates or updates an instance variable, even if a class variable of the same name exists.
- The trap: a mutable class variable (for example a list) is shared. If two objects both call `self.items.append(1)` without ever reassigning `self.items`, they mutate the one shared list and see each other's changes. Give each object its own list by assigning `self.items = []` in `__init__`.

**Encapsulation and name mangling**

- A single leading underscore (`_value`) is a convention meaning "internal, do not touch"; Python does not enforce it.
- A double leading underscore with at most one trailing underscore (`__value`) triggers name mangling: inside class `Account`, `self.__value` is stored as `self._Account__value`. This avoids accidental clashes in subclasses. From outside you can still reach it as `obj._Account__value`, so it is not true privacy.

**Inheritance, `super()`, multiple inheritance, and MRO**

```python
class A:
    def who(self): return "A"

class B(A):
    def who(self):
        return "B-" + super().who()   # calls A.who
```

- `super()` gives access to the next class in the MRO, most often to call a parent's `__init__` or method without naming the parent explicitly.
- With multiple inheritance, Python computes a single method resolution order (MRO) using C3 linearization. Inspect it with `ClassName.__mro__` or `ClassName.mro()`. Lookup walks the MRO left to right and uses the first match.
- For `class D(B, C)` where both `B` and `C` inherit `A`, the MRO is `D, B, C, A`. So `B` is checked before `C`, and the shared base `A` is visited only once, at the end.

**Polymorphism, duck typing, and type checks**

| Function                | Returns `True` when...                                          | Considers inheritance? |
| ----------------------- | -------------------------------------------------------------- | ---------------------- |
| `isinstance(obj, Cls)`  | `obj` is a `Cls` or any subclass of `Cls`                       | Yes                    |
| `issubclass(A, B)`      | `A` is `B` or a subclass of `B`                                 | Yes                    |
| `type(obj) is Cls`      | `obj`'s exact class is `Cls`                                    | No (exact match only)  |

- Duck typing: Python cares that an object has the method or attribute it needs, not what class it is. If it walks like a duck (has a `.quack()`), it works. Prefer `isinstance` over `type(...) is ...` when subclasses should also qualify.

**Special (magic / dunder) methods**

| Method            | Called by                          | Purpose                                        |
| ----------------- | ---------------------------------- | ---------------------------------------------- |
| `__init__`        | Object creation                    | Initialize a new instance                      |
| `__str__`         | `str(obj)`, `print(obj)`           | Readable, human-facing text                    |
| `__repr__`        | `repr(obj)`, the REPL, containers  | Unambiguous, developer-facing text             |
| `__len__`         | `len(obj)`                         | Report a length                                |
| `__eq__`          | `obj == other`                     | Define value equality                          |
| `__add__`         | `obj + other`                      | Operator overloading (also `__lt__`, `__mul__`, ...) |

- `__str__` is for a friendly display; `__repr__` is for an unambiguous representation aimed at developers. `print()` uses `__str__` and falls back to `__repr__` if `__str__` is not defined. Inside a list or other container, elements are always shown with `__repr__`, which is why defining only `__str__` leaves list output looking like `[<Point object at 0x...>]`.

**`@classmethod` versus `@staticmethod`**

| Decorator        | First parameter | Can access class state? | Typical use                          |
| ---------------- | --------------- | ----------------------- | ------------------------------------ |
| (plain method)   | `self`          | Via the instance        | Normal behavior on an instance       |
| `@classmethod`   | `cls`           | Yes (the class itself)  | Alternative constructors, class-wide factory |
| `@staticmethod`  | none            | No                      | A utility function grouped under the class |

**Introspection**

- `obj.__dict__` is the namespace dictionary of an object's (or class's) attributes. `Cls.__bases__` is the tuple of a class's immediate parents; `Cls.__name__` is its name.
- `hasattr(obj, "x")`, `getattr(obj, "x", default)`, `setattr(obj, "x", v)`, and `delattr(obj, "x")` read, fetch, set, and remove attributes by name at runtime.

**Common confusions:** class variable (shared) versus instance variable (per object); `isinstance` (subclass-aware) versus `type(...) is` (exact class); `__str__` (friendly) versus `__repr__` (unambiguous, used in containers); `@classmethod` (gets `cls`) versus `@staticmethod` (gets nothing); single underscore (convention) versus double underscore (name-mangled).

**Exam traps:** A mutable class variable is shared across all instances until reassigned on `self`. `__x` becomes `_ClassName__x`, so `obj.__x` from outside fails but `obj._ClassName__x` works. In a diamond, `class D(B, C)` resolves `B` before `C` and the common base last. Assigning `self.attr = ...` never touches the class variable of the same name. Defining only `__str__` still shows the default `__repr__` inside a list.

### Block 5 - Miscellaneous

This block gathers the remaining building blocks: the iterator protocol, generators, closures and `nonlocal`, lambdas, the functional trio (`map`, `filter`, `sorted`), comprehensions, file processing, and four standard modules for the operating system and time.

**Iterators versus generators**

| Trait          | Iterator (class with `__iter__`/`__next__`)                | Generator (function with `yield`)               |
| -------------- | ---------------------------------------------------------- | ----------------------------------------------- |
| How you build it | Define a class implementing the protocol                  | Write a function that `yield`s, or a `(...)` expression |
| Ends by        | Raising `StopIteration` from `__next__`                     | Falling off the end of the function              |
| State          | You store it in attributes                                  | Python remembers it automatically at each `yield` |
| Reusable?      | Only if you make a fresh iterator                           | No: one-pass, exhausted after a full iteration   |

```python
def countdown(n):
    while n > 0:
        yield n          # lazy: produces one value, then pauses
        n -= 1

nums = (x * x for x in range(5))   # generator expression, not a list
```

- The iterator protocol: `iter(obj)` returns an iterator (calls `__iter__`); `next(it)` returns the next value (calls `__next__`) and raises `StopIteration` when there is nothing left. A `for` loop does all of this for you.
- Generators are lazy and produce values on demand, so they use little memory even for huge or infinite sequences. They are single-pass: once consumed, a second loop over the same generator yields nothing.

**Closures, `nonlocal`, and lambdas**

```python
def make_counter():
    count = 0
    def step():
        nonlocal count      # rebind the enclosing variable
        count += 1
        return count
    return step             # step is a closure over count
```

- A closure is an inner function that remembers variables from the enclosing function even after that function has returned. `nonlocal` lets the inner function rebind an enclosing (but non-global) variable; `global` targets module-level names instead.
- A lambda is a small anonymous function limited to a single expression: `lambda x, y: x + y`. It is most useful as a throwaway `key` or callback.

**The functional trio and comprehensions**

| Tool                          | Produces                        | Note                                       |
| ----------------------------- | ------------------------------- | ------------------------------------------ |
| `map(func, iterable)`         | Lazy iterator of results        | Wrap in `list(...)` to materialize         |
| `filter(func, iterable)`      | Lazy iterator of kept items     | Keeps items where `func` is truthy         |
| `sorted(iterable, key=, reverse=)` | A new sorted list          | `key` is a function of one argument        |
| `[expr for x in it if cond]`  | A full list                     | List comprehension (eager)                 |
| `(expr for x in it if cond)`  | A generator                     | Generator expression (lazy, one-pass)      |

- A list comprehension `[...]` builds the whole list immediately; the same code with parentheses `(...)` is a generator expression that yields lazily. Set (`{expr}`) and dict (`{k: v}`) comprehensions also exist.
- `sorted(data, key=lambda s: len(s))` sorts by length; `sorted(data, reverse=True)` sorts descending. `sorted` returns a new list, while `list.sort()` sorts in place and returns `None`.

**File processing and the `with` statement**

| Mode  | Meaning                                          | If file exists / missing                     |
| ----- | ------------------------------------------------ | -------------------------------------------- |
| `r`   | Read (default)                                   | Must exist, else `FileNotFoundError`         |
| `w`   | Write                                            | Truncates to empty / creates                 |
| `a`   | Append                                           | Writes at end / creates                      |
| `x`   | Exclusive create                                 | `FileExistsError` if it exists / creates     |
| `b`   | Binary modifier (`rb`, `wb`)                     | Reads/writes bytes, not text                 |
| `+`   | Read-and-write modifier (`r+`, `w+`)             | Opens for both reading and writing           |

```python
with open("data.txt") as f:      # auto-closes, even on error
    for line in f:               # iterates line by line
        print(line.rstrip())
```

- Read methods: `read()` returns the whole file (or n characters); `readline()` returns the next single line; `readlines()` returns a list of all lines. Write with `write(text)` or `writelines(list_of_strings)`.
- The `with` statement is a context manager that guarantees the file is closed when the block ends, whether it finishes normally or raises an exception. Prefer it over manual `open`/`close`.

**Standard modules for OS and time**

| Module     | Representative members                                                                            |
| ---------- | ------------------------------------------------------------------------------------------------- |
| `os`       | `getcwd()`, `listdir()`, `mkdir()`, `remove()`, `rename()`, `os.path.join()`, `environ`            |
| `time`     | `time()` (seconds since the epoch), `sleep()`, `localtime()`, `strftime()`                         |
| `datetime` | `datetime`, `date`, `time`, `timedelta`; `strftime()` (to text), `strptime()` (from text)         |
| `calendar` | `isleap(year)`, `weekday()`, `month()`, `setfirstweekday()`                                        |

- `strftime` formats a date/time object into a string with directives like `%Y` (year), `%m` (month), `%d` (day), `%H:%M:%S` (time). `strptime` does the reverse, parsing a string into a `datetime` given a matching format.
- `timedelta` represents a duration; adding one to a `datetime` shifts it (`now + timedelta(days=7)`). `calendar.isleap(2024)` returns `True`, `calendar.isleap(2100)` returns `False`.

**Common confusions:** iterator (reusable if rebuilt, needs a class) versus generator (one-pass, uses `yield`); list comprehension `[...]` (eager list) versus generator expression `(...)` (lazy generator); `sorted()` (returns a new list) versus `list.sort()` (in place, returns `None`); `nonlocal` (enclosing scope) versus `global` (module scope); mode `w` (truncates) versus `a` (appends) versus `x` (fails if the file exists).

**Exam traps:** A generator is exhausted after one full pass, so a second loop yields nothing. `map` and `filter` return lazy iterators in Python 3, not lists. `list.sort()` returns `None`, so `x = mylist.sort()` sets `x` to `None`. Opening a file in `w` mode erases its contents immediately. `strftime` formats to text while `strptime` parses from text - do not swap them.

## Output-prediction traps

PCAP loves "what does this print" questions built on these seven behaviors. Learn to spot the pattern instantly.

| Trap                       | Minimal example                                                        | What surprises people                                                                             |
| -------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| MRO order                  | `class D(B, C)`, both from `A`; call an inherited method               | Resolves `D, B, C, A`. `B` wins over `C`, and the shared base `A` runs last, not right after `B`.  |
| Shared mutable class var   | `items = []` in the class body, then `a.items.append(1)`               | `b.items` also shows `[1]` because both objects share the one class-level list.                    |
| Mutable default argument   | `def f(x, acc=[]): acc.append(x); return acc`                          | The default list is created once at definition, so it keeps growing across calls: `[1]`, `[1, 2]`. |
| Generator exhaustion       | `g = (i for i in range(3))`; loop over `g` twice                       | The first loop prints `0 1 2`; the second prints nothing, because the generator is spent.          |
| `__str__` vs `__repr__`    | Define only `__str__`, then `print([obj])`                             | The list uses `__repr__`, so you see `[<Cls object at 0x...>]`, not your friendly string.           |
| Name-mangling access       | `self.__x = 1` in class `C`, then `C().__x`                            | `obj.__x` raises `AttributeError`; the attribute really lives at `obj._C__x`.                       |
| `is` vs `==`               | `a = [1, 2]; b = [1, 2]`; compare with `==` and `is`                   | `a == b` is `True` (equal values) but `a is b` is `False` (different objects in memory).            |

## 4-week study plan

Typical PCAP prep is a few weeks at roughly 1 to 2 hours a day. This is a revision-paced plan for people who already know Python basics; complete beginners should slow down and add extra hands-on coding. Time is weighted by block, with Object-Oriented Programming getting the most because it is 34% of the exam.

| Week | Focus                                                                                                   | Blocks                    |
| ---- | ------------------------------------------------------------------------------------------------------- | ------------------------- |
| 1    | Import variants, `math`/`random`/`platform`, `__name__`, `sys.path`, building modules and packages; then the `try` statement, exception hierarchy, `raise`, custom exceptions, `assert` | Block 1 + Block 2         |
| 2    | String methods (`find` vs `index`, `split`/`join`, `is*`, `strip`/`zfill`), all three formatting styles, slicing and reversal, `ord`/`chr`, comparison; then begin OOP: classes, `__init__`, `self`, instance vs class variables | Block 3 + start of Block 4 |
| 3    | OOP in full: encapsulation and name mangling, inheritance and `super()`, multiple inheritance and the MRO, polymorphism and duck typing, `isinstance`/`issubclass`/`type`, dunder methods, `@classmethod` vs `@staticmethod`, introspection | Block 4 (the biggest)     |
| 4    | Iterators and generators, closures and `nonlocal`, lambdas, `map`/`filter`/`sorted`, comprehensions, file I/O with `with`, `os`/`time`/`datetime`/`calendar`; then full timed mock exams and review of the output-prediction traps | Block 5 + full review     |

## Readiness checklist

You are ready when you can...

- Predict what each import form binds, and explain why `from module import *` skips underscore names and respects `__all__`.
- Recall the behavior differences among `randint`, `randrange`, and `random`, and among `math.floor`, `ceil`, and `trunc`.
- Explain how `__name__ == "__main__"` lets one file be both a script and an importable module.
- Order multiple `except` clauses correctly and place any exception in the hierarchy (`ZeroDivisionError`, `IndexError`, `KeyError`, `ValueError`, `TypeError`).
- Write a custom exception, use a bare `raise` to re-raise, and read an exception's `args`, and say why `assert` is unsafe for input validation.
- Tell `find` from `index` and `split` from `join`, and format a value with alignment, zero-padding, and fixed decimals using f-strings, `format`, and `%`.
- Slice and reverse strings, convert with `ord`/`chr`, and predict lexicographic comparison results (uppercase before lowercase).
- Distinguish instance from class variables and explain the shared-mutable trap.
- Trace the MRO of a diamond hierarchy and use `super()` correctly.
- Choose `isinstance` versus `type(...) is`, and predict `__str__` versus `__repr__` output inside and outside a container.
- State the difference between `@classmethod` and `@staticmethod`, and access a name-mangled `__attr`.
- Explain the iterator protocol and `StopIteration`, and why a generator is one-pass.
- Write closures with `nonlocal`, use `map`/`filter`/`sorted(key=...)`, and tell a list comprehension from a generator expression.
- Pick the right file mode (`r`/`w`/`a`/`x`/`b`/`+`), use `with`, and format dates with `strftime` versus `strptime`.

---

Want the full breakdown? See the complete **[PCAP study guide](https://certgrid.app/study-guide/pcap-certified-associate-python-programmer)** and **[free practice questions](https://certgrid.app/practice/pcap-certified-associate-python-programmer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_
