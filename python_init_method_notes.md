# Python `__init__()` Method Explained

## What is a Dunder Method?

**Dunder** means **Double UNDERscore**.

Example:

```python
__init__
```

It has:

- Two underscores before `init`
- Two underscores after `init`

These special methods in Python are called **dunder methods** or **magic methods**.

---

# Why Do We Need `__init__()`?

Suppose we create a class called `Computer`.

## Basic Class Example

```python
class Computer:

    def config(self):
        print("i5, 16GB, 1TB")
```

## Creating Objects

```python
comp1 = Computer()
comp2 = Computer()

comp1.config()
comp2.config()
```

### Output

```python
i5, 16GB, 1TB
i5, 16GB, 1TB
```

---

## Problem

Every object gives the **same configuration**.

But in real life:

- One computer may have i5
- Another may have i9
- RAM and storage can also differ

So we need a way to give **different values to different objects**.

---

# Object Attributes

## Trying to Access a Variable

```python
print(comp1.cpu)
```

### Error

```python
AttributeError: 'Computer' object has no attribute 'cpu'
```

Because the class has no `cpu` variable.

---

# Creating Attribute Outside the Class

```python
comp1.cpu = "i5"

print(comp1.cpu)
```

### Output

```python
i5
```

This works.

But only for `comp1`.

```python
print(comp2.cpu)
```

### Error Again

```python
AttributeError
```

Because `cpu` belongs only to `comp1`.

---

# Class Variable

We can create variables inside the class.

```python
class Computer:
    cpu = "i5"

    def config(self):
        print("Computer config")
```

Now all objects can access it.

```python
comp1 = Computer()
comp2 = Computer()

print(comp1.cpu)
print(comp2.cpu)
```

### Output

```python
i5
i5
```

---

## Why This is Called Class Variable

Because it belongs to the **class**, not individual objects.

All objects share the same value.

Good example:

```python
brand = "Dell"
```

Every computer can belong to the same brand.

---

# Instance Variable

Sometimes every object needs its own data.

Example:

- Different CPU
- Different RAM
- Different SSD

For that we use `__init__()`.

---

# Introducing `__init__()`

```python
class Computer:

    def __init__(self):
        print("Init called")
```

---

# Important Point

Whenever an object is created:

```python
comp1 = Computer()
```

Python automatically calls:

```python
__init__()
```

---

## Example

```python
class Computer:

    def __init__(self):
        print("Init called")


comp1 = Computer()
comp2 = Computer()
```

### Output

```python
Init called
Init called
```

Because two objects were created.

---

# Why `self` is Needed

Incorrect:

```python
def __init__():
```

This gives error.

Correct:

```python
def __init__(self):
```

`self` represents the current object.

---

# Creating Instance Variables

```python
class Computer:

    def __init__(self):
        self.cpu = "i5"
```

Now every object gets its own `cpu`.

---

## Example

```python
class Computer:

    def __init__(self):
        self.cpu = "i5"

comp1 = Computer()

print(comp1.cpu)
```

### Output

```python
i5
```

---

# Multiple Instance Variables

```python
class Computer:

    def __init__(self):
        self.cpu = "i5"
        self.ram = "16GB"
        self.ssd = "1TB"
```

---

# Accessing Variables in Methods

```python
class Computer:

    def __init__(self):
        self.cpu = "i5"
        self.ram = "16GB"
        self.ssd = "1TB"

    def config(self):
        print("Config:", self.cpu, self.ram, self.ssd)
```

---

## Example

```python
comp1 = Computer()

comp1.config()
```

### Output

```python
Config: i5 16GB 1TB
```

---

# Problem with Static Values

All objects still get same values.

We need dynamic values.

---

# Passing Values During Object Creation

```python
comp1 = Computer("i5", "16GB", "512GB")
comp2 = Computer("i9", "64GB", "2TB")
```

Now we must accept these values in `__init__()`.

---

# Final Dynamic Example

```python
class Computer:

    def __init__(self, cpu, ram, ssd):
        self.cpu = cpu
        self.ram = ram
        self.ssd = ssd

    def config(self):
        print("Config:", self.cpu, self.ram, self.ssd)


comp1 = Computer("i5", "16GB", "512GB")
comp2 = Computer("i9", "64GB", "2TB")

comp1.config()
comp2.config()
```

---

# Output

```python
Config: i5 16GB 512GB
Config: i9 64GB 2TB
```

---

# Simple Real-Life Analogy

Think of a `Computer` class like a **factory design**.

The class defines:

- What a computer should have

Objects are:

- Actual computers made from that design

`__init__()` helps initialize each computer with its own configuration.

---

# Key Concepts Summary

## 1. Dunder Method

```python
__init__
```

Double underscore method.

---

## 2. `self`

Represents current object.

---

## 3. Class Variable

Shared by all objects.

```python
brand = "Dell"
```

---

## 4. Instance Variable

Different for each object.

```python
self.cpu
```

---

## 5. `__init__()`

Automatically called when object is created.

Used to initialize object data.

---

# Mini Practice Exercise

Try this yourself:

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def show(self):
        print(self.name, self.marks)


s1 = Student("Ravi", 85)
s2 = Student("Aisha", 92)

s1.show()
s2.show()
```

### Expected Output

```python
Ravi 85
Aisha 92
```

---

# Final Note

In the transcript, an important point was mentioned:

- `__init__()` is often called a constructor informally
- But technically in Python it is mainly an initializer method

Its purpose is to initialize object values automatically when objects are created.
