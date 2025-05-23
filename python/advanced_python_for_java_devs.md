
# 🧠 Advanced Python Concepts for Java Developers

A deeper look at Python features that are powerful but can feel more complex coming from Java.

---

## 🔁 1. List Comprehensions

A concise way to generate lists.

**Syntax**:
```python
[expression for item in iterable if condition]
```

**Example**:
```python
squares = [x * x for x in range(10) if x % 2 == 0]
```

**Equivalent Java** (roughly):
```java
List<Integer> squares = new ArrayList<>();
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) squares.add(i * i);
}
```

---

## ⚙️ 2. Generator Expressions

Similar to list comprehensions but lazily evaluated (saves memory).

**Syntax**:
```python
(expression for item in iterable if condition)
```

**Example**:
```python
gen = (x * x for x in range(1000000))
next(gen)
```

---

## 🧱 3. Decorators

Wrap or modify function behavior.

**Example**:
```python
def decorator(func):
    def wrapper(*args, **kwargs):
        print("Before")
        result = func(*args, **kwargs)
        print("After")
        return result
    return wrapper

@decorator
def say_hello():
    print("Hello")
```

---

## 🧪 4. Context Managers

Manage resources with the `with` statement (similar to Java's try-with-resources).

**Built-in Example**:
```python
with open("file.txt") as f:
    data = f.read()
```

**Custom Context Manager**:
```python
from contextlib import contextmanager

@contextmanager
def my_resource():
    print("Setup")
    yield
    print("Cleanup")

with my_resource():
    print("Inside block")
```

---

## 📦 5. Unpacking and Tuple Assignment

**Example**:
```python
a, b = (1, 2)
a, b, *rest = [1, 2, 3, 4]  # rest = [3, 4]
```

Allows multiple assignments in one line and cleaner code patterns.

---

## 🧠 6. Lambda & Functional Tools

**Lambda Example**:
```python
squared = list(map(lambda x: x**2, [1, 2, 3]))
evens = list(filter(lambda x: x % 2 == 0, [1, 2, 3, 4]))
```

**Also useful**:
- `map()`, `filter()`, `reduce()` (from `functools`)
- Often clearer with list comprehensions

---

Explore these patterns to write more Pythonic, efficient, and readable code.
