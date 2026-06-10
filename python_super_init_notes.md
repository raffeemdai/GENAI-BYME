# Python `__init__()` and `super()` in Inheritance

# 1. Introduction

In this lesson, we learn:

- Every class inherits from `object`
- How `__init__()` behaves in inheritance
- How to use `super()`
- Calling parent constructors
- Calling parent methods

These concepts are very important in Python Object-Oriented Programming (OOP).

---

# 2. Every Class Inherits from `object`

In Python, every class automatically inherits from a built-in class called:

```python
object
```

Even if we don't write it explicitly.

---

# 3. Basic Example

```python
class A:

    def f1(self):
        print("F1 Works")
```

## Creating Object

```python
obj = A()
obj.f1()
```

## Output

```python
F1 Works
```

---

# 4. Hidden Inheritance from `object`

Python internally treats this class as:

```python
class A(object):

    def f1(self):
        print("F1 Works")
```

That means every class is already a child of `object`.

---

# 5. Why Do We See Many Methods?

When you type:

```python
obj.
```

You see many built-in methods like:

- `__str__`
- `__repr__`
- `__class__`
- `__dir__`

These methods come from the `object` class.

---

# 6. Understanding `__init__()`

`__init__()` is a constructor.

It automatically executes when an object is created.

---

# 7. Simple `__init__()` Example

```python
class A:

    def __init__(self):
        print("Inside A Init")

    def f1(self):
        print("F1 Works")
```

## Object Creation

```python
obj = A()
```

## Output

```python
Inside A Init
```

Because constructor executes automatically.

---

# 8. Inheritance with Constructor

## Parent Class

```python
class A:

    def __init__(self):
        print("Inside A Init")

    def f1(self):
        print("F1 Works")
```

## Child Class

```python
class B(A):

    def f2(self):
        print("F2 Works")
```

---

# 9. Creating Child Object

```python
obj = B()
```

## Output

```python
Inside A Init
```

Why?

Because:

- B does not have its own constructor
- Python searches in parent class A
- So A's `__init__()` gets executed

---

# 10. Child Class Constructor

Now let's define constructor inside B.

```python
class B(A):

    def __init__(self):
        print("Inside B Init")

    def f2(self):
        print("F2 Works")
```

## Object Creation

```python
obj = B()
```

## Output

```python
Inside B Init
```

---

# 11. Important Rule

Python calls only ONE constructor by default.

Search order:

1. Child class constructor
2. Parent class constructor

If child constructor exists, parent constructor is NOT automatically called.

---

# 12. What is `super()`?

`super()` refers to:

> Parent class object

It helps child classes access parent class methods and constructors.

---

# 13. Calling Parent Constructor Using `super()`

## Example

```python
class A:

    def __init__(self):
        print("Inside A Init")


class B(A):

    def __init__(self):

        super().__init__()

        print("Inside B Init")
```

## Object Creation

```python
obj = B()
```

## Output

```python
Inside A Init
Inside B Init
```

---

# 14. Constructor Chaining

Calling parent constructor from child constructor is called:

> Constructor Chaining

It is commonly done using:

```python
super().__init__()
```

---

# 15. Calling Parent Methods Using `super()`

## Example

```python
class A:

    def f1(self):
        print("F1 Works")


class B(A):

    def f2(self):

        super().f1()

        print("F2 Works")
```

## Object Creation

```python
obj = B()
obj.f2()
```

## Output

```python
F1 Works
F2 Works
```

---

# 16. Using `self` vs `super`

Both can call parent methods in many situations.

## Using `self`

```python
self.f1()
```

## Using `super`

```python
super().f1()
```

---

# 17. Difference Between `self` and `super()`

## `self`

- Refers to current object
- Can access child and parent methods

## `super()`

- Refers specifically to parent class
- Used mainly in inheritance

---

# 18. Complete Example

```python
class A:

    def __init__(self):
        print("Inside A Init")

    def f1(self):
        print("F1 Works")


class B(A):

    def __init__(self):

        super().__init__()

        print("Inside B Init")

    def f2(self):

        super().f1()

        print("F2 Works")


obj = B()
obj.f2()
```

## Output

```python
Inside A Init
Inside B Init
F1 Works
F2 Works
```

---

# 19. Real-Life Example – Employee System

## Parent Class

```python
class Employee:

    def __init__(self):
        print("Employee Created")

    def work(self):
        print("Employee Working")
```

## Child Class

```python
class Manager(Employee):

    def __init__(self):

        super().__init__()

        print("Manager Created")

    def manage(self):

        super().work()

        print("Manager Managing Team")
```

## Usage

```python
m = Manager()
m.manage()
```

## Output

```python
Employee Created
Manager Created
Employee Working
Manager Managing Team
```

---

# 20. Real-Life Example – Vehicle

```python
class Vehicle:

    def __init__(self):
        print("Vehicle Ready")

    def start(self):
        print("Vehicle Started")


class Car(Vehicle):

    def __init__(self):

        super().__init__()

        print("Car Ready")

    def music_system(self):

        super().start()

        print("Music System On")
```

## Usage

```python
c = Car()
c.music_system()
```

---

# 21. Advantages of `super()`

- Avoids duplicate code
- Helps reuse parent functionality
- Cleaner inheritance structure
- Easier maintenance
- Useful in multilevel inheritance

---

# 22. Important Notes

## Rule 1

If child constructor is absent:

- Parent constructor executes automatically

---

## Rule 2

If child constructor exists:

- Parent constructor does NOT execute automatically

Use:

```python
super().__init__()
```

---

## Rule 3

`super()` can call:

- Parent constructors
- Parent methods

---

# 23. Interview Questions

## What is `super()` in Python?

`super()` is used to access parent class methods and constructors.

---

## Why use `super()`?

To reuse parent class functionality inside child class.

---

## What happens if child class has its own constructor?

Parent constructor will not execute automatically.

---

## Does every Python class inherit from object?

Yes.

Every Python class is internally a child of `object`.

---

# 24. Summary Table

| Concept | Meaning |
|---|---|
| `object` class | Default parent class of all classes |
| `__init__()` | Constructor method |
| `super()` | Access parent class |
| Constructor chaining | Calling parent constructor from child |

---

# 25. Final Understanding

- Every Python class inherits from `object`.
- `__init__()` executes automatically during object creation.
- Child class constructors override parent constructors.
- `super()` helps call parent constructors and methods.
- `super()` is very important in inheritance-based designs.
