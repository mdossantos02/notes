
# 🔄 Advanced Python Concepts with Java Equivalents

This guide provides a comparison of key Python concepts and how they relate to similar ideas in Java.

---

## 1. Iterators and Iterables

**Python:**
```python
nums = [1, 2, 3]
it = iter(nums)
print(next(it))
```

**Java:**
```java
List<Integer> nums = Arrays.asList(1, 2, 3);
Iterator<Integer> it = nums.iterator();
System.out.println(it.next());
```

---

## 2. Generators with `yield`

**Python:**
```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1
```

**Java:**
No direct equivalent; would require custom Iterator or Stream API with lazy evaluation.

---

## 3. `*args` and `**kwargs`

**Python:**
```python
def func(*args, **kwargs):
    print(args)
    print(kwargs)
```

**Java:**
```java
void func(String... args) {
    for (String arg : args) {
        System.out.println(arg);
    }
}
```

No native support for keyword arguments; simulate with Map<String, Object>.

---

## 4. Data Classes

**Python:**
```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int
```

**Java:**
```java
public class Point {
    public int x;
    public int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

}
```

---

## 5. `with` Statement (Context Managers)

**Python:**
```python
with open("file.txt") as f:
    data = f.read()
```

**Java:**
```java
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String data = reader.readLine();
}
```

---

## 6. Descriptors and Properties

**Python:**
```python
class MyClass:
    def __init__(self):
        self._x = 0

    @property
    def x(self):
        return self._x

    @x.setter
    def x(self, value):
        self._x = value
```

**Java:**
```java
public class MyClass {
    private int x;

    public int getX() { return x; }
    public void setX(int value) { this.x = value; }
}
```

---

## 7. Pattern Matching

**Python (3.10+):**
```python
match command.split():
    case ["load", filename]:
        print(f"Loading {filename}")
    case ["quit"]:
        print("Quitting")
    case _:
        print("Unknown command")
```

**Java (17+):**
```java
switch (command) {
    case "load" -> System.out.println("Loading");
    case "quit" -> System.out.println("Quitting");
    default -> System.out.println("Unknown command");
}
```

Java pattern matching is still evolving with type-based matching in newer versions.

---

## 8. Modules and Packages

**Python:**
- Use directories with `__init__.py` for packages.
- Import with `import module` or `from package import module`.

**Java:**
- Use packages and import statements.
- File structure reflects package structure: `com/example/MyClass.java`.

---

## 9. File and Path Handling

**Python:**
```python
from pathlib import Path
p = Path("my_file.txt")
print(p.exists())
```

**Java:**
```java
import java.nio.file.*;

Path path = Paths.get("my_file.txt");
boolean exists = Files.exists(path);
```

---

## 10. Mocking and Testing Tools

**Python:**
- Use `unittest`, `pytest`, `unittest.mock`, etc.

**Java:**
- Use `JUnit`, `Mockito` for mocking, `Hamcrest` for assertions.

---

This table should help you draw clear parallels between Python and Java's capabilities and idioms.

# 🧠 Advanced Python vs Java Concepts (Extended Guide)

This guide compares powerful Python concepts with their Java counterparts, including detailed usage examples.

---

## 🧱 1. Classes and Inheritance

**Python:**
```python
class Animal:
    def speak(self):
        return "..."

class Dog(Animal):
    def speak(self):
        return "Woof"
```
- Classes are dynamic. You can add methods or attributes at runtime.
- Multiple inheritance is supported (but use with caution).

**Java:**
```java
class Animal {
    String speak() {
        return "...";
    }
}

class Dog extends Animal {
    @Override
    String speak() {
        return "Woof";
    }
}
```
- Java is statically typed and supports single inheritance.

---

## 🧰 2. Abstract Base Classes and Interfaces

**Python:**
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```
- Use `abc` to define interfaces.
- Helps enforce method implementation.

**Java:**
```java
interface Shape {
    double area();
}
```
- Java interfaces define contracts.
- You can implement multiple interfaces.

---

## 🪞 3. Reflection and Introspection

**Python:**
```python
class MyClass:
    def greet(self): print("Hello")

obj = MyClass()
print(hasattr(obj, 'greet'))  # True
getattr(obj, 'greet')()       # Calls greet
```
- Easy to inspect and manipulate objects at runtime.
- Common in decorators and dynamic frameworks.

**Java:**
```java
Method m = obj.getClass().getMethod("greet");
m.invoke(obj);
```
- Java reflection is powerful but verbose.
- Used in frameworks like Spring and Hibernate.

---

## 📦 4. Decorators vs Annotations

**Python:**
```python
def log(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@log
def greet():
    print("Hello")
```
- Functions wrapping functions.
- Used for logging, access control, timing, etc.

**Java:**
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Log {}

@Log
public void greet() {
    System.out.println("Hello");
}
```
- Annotations are metadata.
- Behavior must be implemented via reflection.

---

## 🧪 5. Testing Frameworks

**Python:**
```python
import pytest

def test_add():
    assert 1 + 1 == 2
```
- `pytest` supports fixtures, parametrize, mocking.
- Minimal boilerplate and very readable.

**Java:**
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

@Test
void testAdd() {
    assertEquals(2, 1 + 1);
}
```
- JUnit is robust and often used with Mockito.

---

## ⛓️ 6. Concurrency

**Python:**
```python
import asyncio

async def fetch_data():
    await asyncio.sleep(1)
    return "Done"
```
- `asyncio` is ideal for I/O-bound tasks.
- Python also has `threading`, `multiprocessing`.

**Java:**
```java
CompletableFuture.supplyAsync(() -> {
    Thread.sleep(1000);
    return "Done";
});
```
- Java concurrency uses threads, executors, and newer reactive models.

---

## 🔀 7. Enums

**Python:**
```python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
```
- You can add methods and properties.
- Useful for constant sets with behavior.

**Java:**
```java
enum Color {
    RED, GREEN;
}
```
- Enums are type-safe and can have methods.

---

## 📋 8. Exception Handling

**Python:**
```python
try:
    1 / 0
except ZeroDivisionError as e:
    print("Cannot divide by zero!")
finally:
    print("Cleanup")
```
- Use `try/except/finally`.
- Avoid catching `Exception` unless necessary.

**Java:**
```java
try {
    int result = 1 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero!");
} finally {
    System.out.println("Cleanup");
}
```
- Very similar in concept.
- Must declare or catch checked exceptions.

---

These concepts form the backbone of writing idiomatic, maintainable code in both Python and Java.
