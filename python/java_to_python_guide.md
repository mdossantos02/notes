
# 🐍 Java Developer's Guide to Python

A quick reference for Java developers adapting to Python's syntax, features, and philosophy.

---

## 📏 Syntax & Structure

- **No Semicolons or Braces**:
  - Python uses **indentation** (4 spaces) instead of `{}`.
  - No semicolons at line ends.

- **Dynamic Typing**:
  - Variables are not typed explicitly.
  - Example: `x = 5`

- **Duck Typing**:
  - Types are inferred from behavior, not declared.

- **No Main Method**:
  ```python
  if __name__ == "__main__":
      main()
  ```

---

## 📚 Language Features

- **List, Dict, Set Comprehensions**:
  ```python
  squares = [x*x for x in range(10)]
  ```

- **First-Class Functions & Lambdas**:
  ```python
  doubled = map(lambda x: x * 2, [1, 2, 3])
  ```

- **Multiple Return Values**:
  ```python
  def get_coordinates(): return (10, 20)
  x, y = get_coordinates()
  ```

- **Everything is an Object**:
  - Including functions and types.

---

## 📦 Standard Library & Ecosystem

- **Batteries Included**:
  - Includes `datetime`, `json`, `os`, `re`, etc.

- **Package Management**:
  - Use `pip`, `venv`, `poetry`, or `pipenv`.

---

## ✅ Testing & Tooling

- **Testing**:
  - Use `pytest`, `unittest`, or `nose2`.

- **Linting & Formatting**:
  - Tools: `black`, `ruff`, `flake8`, `mypy`

- **Typing (Optional)**:
  ```python
  def greet(name: str) -> str:
      return f"Hello {name}"
  ```

---

## 🧠 Philosophy

- **"There should be one — and preferably only one — obvious way to do it."**

- **Readability > Verbosity**

- **Zen of Python**:
  ```python
  >>> import this
  ```

---

Adapt with curiosity and enjoy Python's flexibility!
