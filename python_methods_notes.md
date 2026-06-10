# Python Types of Methods – Notes with Examples

## 1. Introduction

In Python classes, methods are mainly of 3 types:

1. Instance Method
2. Class Method
3. Static Method

These methods are used for different purposes depending on what data they work with.

---

# 2. Instance Variables vs Class Variables

## Instance Variable

Instance variables belong to an object (instance).

They are created using `self`.

## Example

```python
class Computer:

    def __init__(self, cpu, ram, ssd):
        self.cpu = cpu
        self.ram = ram
        self.ssd = ssd
```

### Creating Objects

```python
comp1 = Computer("i5", "16GB", "512GB")
comp2 = Computer("i9", "32GB", "1TB")
```

Each object has different values.

- `comp1.cpu` → i5
- `comp2.cpu` → i9

So these are called instance variables.

---

## Class Variable

A class variable belongs to the class itself, not individual objects.

## Example

```python
class Computer:

    brand = "TechCo"

    def __init__(self, cpu, ram, ssd):
        self.cpu = cpu
        self.ram = ram
        self.ssd = ssd
```

Here:

```python
brand = "TechCo"
```

is a class variable.

All objects share this value.

---

# 3. Accessing Class Variables

## Using Object

```python
print(comp1.brand)
```

## Using Class Name (Recommended)

```python
print(Computer.brand)
```

### Output

```python
TechCo
```

---

# 4. Instance Methods

Instance methods work with instance variables.

They use `self`.

## Example

```python
class Computer:

    brand = "TechCo"

    def __init__(self, cpu, ram):
        self.cpu = cpu
        self.ram = ram

    def config(self):
        print("CPU:", self.cpu)
        print("RAM:", self.ram)
```

### Calling Instance Method

```python
comp1 = Computer("i5", "16GB")

comp1.config()
```

### Output

```python
CPU: i5
RAM: 16GB
```

---

# 5. Class Methods

Class methods work with class variables.

They use `cls` instead of `self`.

To create a class method, use:

```python
@classmethod
```

## Example

```python
class Computer:

    brand = "TechCo AI"

    def __init__(self, cpu, ram):
        self.cpu = cpu
        self.ram = ram

    @classmethod
    def info(cls):
        return cls.brand
```

### Calling Class Method

```python
print(Computer.info())
```

### Output

```python
TechCo AI
```

---

# 6. Static Methods

Static methods are utility methods.

They do NOT work with:

- instance variables
- class variables

They are independent methods inside a class.

Use:

```python
@staticmethod
```

---

# 7. Static Method Examples

## Example 1 – Convert GB to Bytes

```python
class Computer:

    @staticmethod
    def gb_to_bytes(gb):
        return gb * 1024 * 1024 * 1024
```

### Calling Static Method

```python
print(Computer.gb_to_bytes(16))
```

### Output

```python
17179869184
```

---

## Example 2 – Check Even or Odd

```python
class MathUtility:

    @staticmethod
    def is_even(number):
        return number % 2 == 0
```

### Calling Static Method

```python
print(MathUtility.is_even(10))
print(MathUtility.is_even(7))
```

### Output

```python
True
False
```

---

## Example 3 – Celsius to Fahrenheit

```python
class Temperature:

    @staticmethod
    def celsius_to_fahrenheit(celsius):
        return (celsius * 9/5) + 32
```

### Calling Static Method

```python
print(Temperature.celsius_to_fahrenheit(30))
```

### Output

```python
86.0
```

---

## Example 4 – Find Maximum Number

```python
class Utility:

    @staticmethod
    def maximum(a, b):
        return a if a > b else b
```

### Calling Static Method

```python
print(Utility.maximum(10, 25))
```

### Output

```python
25
```

---

## Example 5 – Validate Email

```python
class Validator:

    @staticmethod
    def is_valid_email(email):
        return "@" in email and "." in email
```

### Calling Static Method

```python
print(Validator.is_valid_email("test@gmail.com"))
print(Validator.is_valid_email("hello123"))
```

### Output

```python
True
False
```

---

# 8. Complete Example

```python
class Computer:

    # Class Variable
    brand = "TechCo AI"

    # Constructor / Instance Method
    def __init__(self, cpu, ram, ssd):
        self.cpu = cpu
        self.ram = ram
        self.ssd = ssd

    # Instance Method
    def config(self):
        print("CPU:", self.cpu)
        print("RAM:", self.ram)
        print("SSD:", self.ssd)

    # Class Method
    @classmethod
    def get_brand(cls):
        return cls.brand

    # Static Method
    @staticmethod
    def gb_to_bytes(gb):
        return gb * 1024 * 1024 * 1024


# Objects
comp1 = Computer("i5", "16GB", "512GB")
comp2 = Computer("i9", "32GB", "1TB")

# Instance Method
comp1.config()

# Class Method
print("Brand:", Computer.get_brand())

# Static Method
print("16GB in bytes:", Computer.gb_to_bytes(16))
```

---

# 9. Summary Table

| Method Type | Uses | First Parameter | Decorator |
|---|---|---|---|
| Instance Method | Instance variables | `self` | No |
| Class Method | Class variables | `cls` | `@classmethod` |
| Static Method | Utility/helper functions | None required | `@staticmethod` |

---

# 10. Key Interview Points

## Instance Method

- Works with object data
- Requires object creation

## Class Method

- Works with class-level data
- Shared by all objects

## Static Method

- Independent utility function
- No access to `self` or `cls`

---

# 11. Real-Life Analogy

Imagine a class `Student`.

## Instance Variable

```python
name
marks
```

Different for every student.

---

## Class Variable

```python
school_name
```

Same for all students.

---

## Static Method

```python
def percentage_to_grade():
```

Just a helper function.

---

# 12. Final Understanding

- Use instance methods for object-specific data.
- Use class methods for class-wide shared data.
- Use static methods for utility operations related to the class.
