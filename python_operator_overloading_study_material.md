# Python Operator Overloading — Study Material with Code Examples

## 1. What is Operator Overloading?

**Operator overloading** means giving a built-in operator, like `+`, `>`, `==`, etc., a custom meaning depending on the objects used with it.

In Python, the same operator can behave differently for different data types.

### Example: `+` with integers

```python
a = 5
b = 6

c = a + b
print(c)
```

### Output

```text
11
```

Here, `+` performs **addition** because both operands are integers.

---

### Example: `+` with strings

```python
a = "5"
b = "6"

c = a + b
print(c)
```

### Output

```text
56
```

Here, `+` performs **string concatenation** because both operands are strings.

So, the same `+` operator behaves differently:

| Operands | Operation | Output |
|---|---|---|
| `5 + 6` | Integer addition | `11` |
| `"5" + "6"` | String concatenation | `"56"` |

This is called **operator overloading**.

It is also related to **polymorphism**, because one operator can have many forms.

---

## 2. How `+` Works Behind the Scenes

In Python, everything is an object.

```python
a = 5
print(type(a))
```

### Output

```text
<class 'int'>
```

So `5` is an object of the `int` class.

When we write:

```python
c = a + b
```

Python internally calls a special method:

```python
c = int.__add__(a, b)
```

Example:

```python
a = 5
b = 6

c = int.__add__(a, b)
print(c)
```

### Output

```text
11
```

You can also write:

```python
a = 5
b = 6

c = a.__add__(b)
print(c)
```

### Output

```text
11
```

So these three statements are almost equivalent:

```python
a + b
int.__add__(a, b)
a.__add__(b)
```

But in real projects, we normally use:

```python
a + b
```

because it is more readable.

---

## 3. What are Dunder Methods?

Methods like `__add__()`, `__str__()`, and `__gt__()` are called **dunder methods** or **magic methods**.

Dunder means **double underscore**.

Example:

```python
__add__
__str__
__gt__
__lt__
__eq__
```

These methods allow us to define how operators should behave for our own classes.

| Operator | Dunder Method | Meaning |
|---|---|---|
| `+` | `__add__()` | Addition |
| `-` | `__sub__()` | Subtraction |
| `*` | `__mul__()` | Multiplication |
| `>` | `__gt__()` | Greater than |
| `<` | `__lt__()` | Less than |
| `==` | `__eq__()` | Equal to |
| `print(obj)` | `__str__()` | String representation |

---

## 4. Creating Our Own Class

Let us create a simple `Account` class.

Each account has:

1. `name`
2. `balance`

```python
class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance


user1 = Account("Naveen", 1000)
user2 = Account("Kiran", 2000)

print(user1)
print(user2)
```

### Output

```text
<__main__.Account object at 0x...>
<__main__.Account object at 0x...>
```

This output is not very useful.

Python prints the object memory location because we have not told Python how to display an `Account` object.

---

## 5. Using `__str__()` Method

When we write:

```python
print(user1)
```

Python internally calls:

```python
user1.__str__()
```

By default, Python gives object information like memory address.

But we can override `__str__()` to print meaningful information.

```python
class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    def __str__(self):
        return f"{self.name}: {self.balance}"


user1 = Account("Naveen", 1000)
user2 = Account("Kiran", 2000)

print(user1)
print(user2)
```

### Output

```text
Naveen: 1000
Kiran: 2000
```

Now, whenever we print the object, Python automatically calls `__str__()`.

---

## 6. Problem: Adding Two Account Objects

Now suppose we want to combine two account balances.

We may try this:

```python
class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    def __str__(self):
        return f"{self.name}: {self.balance}"


user1 = Account("Naveen", 1000)
user2 = Account("Kiran", 2000)

combined = user1 + user2
print(combined)
```

### Output

```text
TypeError: unsupported operand type(s) for +: 'Account' and 'Account'
```

Why?

Because Python does not know how to add two `Account` objects.

For integers, Python already has `__add__()` defined.

But for our custom `Account` class, we need to define it ourselves.

---

## 7. Overloading `+` Using `__add__()`

To use `+` with our objects, we define the `__add__()` method.

```python
class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    def __str__(self):
        return f"{self.name}: {self.balance}"

    def __add__(self, other):
        new_name = "Joint Account"
        new_balance = self.balance + other.balance
        return Account(new_name, new_balance)


user1 = Account("Naveen", 1000)
user2 = Account("Kiran", 2000)

combined = user1 + user2

print(combined)
```

### Output

```text
Joint Account: 3000
```

Here:

```python
combined = user1 + user2
```

internally means:

```python
combined = user1.__add__(user2)
```

In this method:

```python
def __add__(self, other):
```

- `self` refers to `user1`
- `other` refers to `user2`

So this line:

```python
new_balance = self.balance + other.balance
```

means:

```python
new_balance = user1.balance + user2.balance
```

That is:

```python
1000 + 2000
```

So the final balance is:

```text
3000
```

---

## 8. Overloading `>` Using `__gt__()`

Now suppose we want to compare two accounts.

Example:

```python
if user1 > user2:
    print("Naveen pays the bill")
else:
    print("Kiran pays the bill")
```

By default, Python does not know how to compare two `Account` objects.

So we define the `__gt__()` method.

`gt` means **greater than**.

```python
class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    def __str__(self):
        return f"{self.name}: {self.balance}"

    def __add__(self, other):
        new_name = "Joint Account"
        new_balance = self.balance + other.balance
        return Account(new_name, new_balance)

    def __gt__(self, other):
        return self.balance > other.balance


user1 = Account("Naveen", 1000)
user2 = Account("Kiran", 2000)

if user1 > user2:
    print("Naveen pays the bill")
else:
    print("Kiran pays the bill")
```

### Output

```text
Kiran pays the bill
```

Because:

```python
1000 > 2000
```

is `False`.

So the `else` block runs.

---

### Changing the Balance

Now let us increase Naveen’s balance.

```python
class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    def __str__(self):
        return f"{self.name}: {self.balance}"

    def __add__(self, other):
        new_name = "Joint Account"
        new_balance = self.balance + other.balance
        return Account(new_name, new_balance)

    def __gt__(self, other):
        return self.balance > other.balance


user1 = Account("Naveen", 4000)
user2 = Account("Kiran", 2000)

if user1 > user2:
    print("Naveen pays the bill")
else:
    print("Kiran pays the bill")
```

### Output

```text
Naveen pays the bill
```

Because:

```python
4000 > 2000
```

is `True`.

---

## 9. Complete Example

```python
class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    def __str__(self):
        return f"{self.name}: {self.balance}"

    def __add__(self, other):
        return Account("Joint Account", self.balance + other.balance)

    def __gt__(self, other):
        return self.balance > other.balance


user1 = Account("Naveen", 1000)
user2 = Account("Kiran", 2000)

print("User 1:", user1)
print("User 2:", user2)

combined = user1 + user2
print("Combined:", combined)

if user1 > user2:
    print("Naveen pays the bill")
else:
    print("Kiran pays the bill")
```

### Output

```text
User 1: Naveen: 1000
User 2: Kiran: 2000
Combined: Joint Account: 3000
Kiran pays the bill
```

---

## 10. Simple Explanation of the Flow

When we write:

```python
print(user1)
```

Python calls:

```python
user1.__str__()
```

When we write:

```python
user1 + user2
```

Python calls:

```python
user1.__add__(user2)
```

When we write:

```python
user1 > user2
```

Python calls:

```python
user1.__gt__(user2)
```

So operator overloading means we are giving our own meaning to operators for custom objects.

---

## 11. Key Points to Remember

1. Operator overloading allows the same operator to behave differently for different objects.
2. It is an example of polymorphism.
3. Python uses special dunder methods for operator overloading.
4. `+` internally uses `__add__()`.
5. `>` internally uses `__gt__()`.
6. `print()` internally uses `__str__()`.
7. We can define these methods in our own classes to change operator behavior.

---

## 12. Practice Example

Try this small example with a `Student` class.

We will compare students based on marks.

```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def __str__(self):
        return f"{self.name}: {self.marks}"

    def __gt__(self, other):
        return self.marks > other.marks


student1 = Student("Rahul", 85)
student2 = Student("Priya", 92)

print(student1)
print(student2)

if student1 > student2:
    print("Rahul scored more marks")
else:
    print("Priya scored more marks")
```

### Output

```text
Rahul: 85
Priya: 92
Priya scored more marks
```

Here, we overloaded the `>` operator to compare students based on their marks.

---

## Final Definition

**Operator overloading in Python means defining special methods inside a class so that built-in operators like `+`, `>`, `<`, `==`, etc., can work with custom objects using our own logic.**
