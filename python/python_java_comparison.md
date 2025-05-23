
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
