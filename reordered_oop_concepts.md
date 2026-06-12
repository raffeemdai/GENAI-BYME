
# Reordered Python OOP Concepts (Topic-wise)

## 1. Basics: Class and Object

# Basic OOP Concepts Explained Simply

## Table of Contents
1. [What is a Class?](#1-what-is-a-class)
2. [What is an Object?](#2-what-is-an-object)
3. [Class Attributes vs Instance Attributes](#3-class-attributes-vs-instance-attributes)
4. [Instance Methods vs Class Methods](#4-instance-methods-vs-class-methods)
5. [The self Parameter](#5-the-self-parameter-explained-simply)
6. [Complete Example](#complete-example-putting-it-all-together)
7. [Quick Reference](#quick-reference-cheat-sheet)

---

## 1. What is a Class?

A **class** is like a **blueprint** or **template** for creating objects.

**Real-World Analogy:**
- Think of a class as a **cookie cutter** 🍪
- The cookie cutter defines the **shape and design**
- But it's not a cookie itself!

```python
class BankAccount:
    """This is a blueprint for creating bank accounts"""
    pass  # Empty for now
```

**What does a class contain?**
- **Attributes** (data/properties) - What it HAS
- **Methods** (functions/behaviors) - What it CAN DO

---

## 2. What is an Object?

An **object** is a **specific instance** created from a class blueprint.

**Real-World Analogy:**
- If the class is a **cookie cutter**, the object is an **actual cookie** 🍪
- You can make many cookies from one cookie cutter
- Each cookie is separate and independent

```python
class BankAccount:
    pass

# Create objects (instances)
user1_account = BankAccount()  # First cookie
user2_account = BankAccount()  # Second cookie

# Check their types
print(type(user1_account))  # <class '__main__.BankAccount'>
print(type(user2_account))  # <class '__main__.BankAccount'>

# They are different objects
print(user1_account is user2_account)  # False - different cookies!
```

**Key Points:**
- Each object is **independent** - changes to one don't affect others
- All objects created from the same class have the **same structure**
- But each can have **different data**

---
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

## 3. Class Attributes vs Instance Attributes

### Class Attributes (Shared by All)

**Class attributes** are like **family traits** - shared by everyone.

```python
class BankAccount:
    # CLASS ATTRIBUTE - Shared by ALL accounts
    bank_name = "SBI"  # All accounts belong to SBI bank
    
    def __init__(self, customer_name, balance):
        # INSTANCE ATTRIBUTES - Unique to each account
        self.customer_name = customer_name
        self.balance = balance
```

**Visual Explanation:**

```
           SBI Bank (Class)
           bank_name = "SBI"  ← Shared by all
                 ↓
    ┌────────────┼────────────┐
    ↓            ↓            ↓
  Alice       Bob         Charlie
balance=1000  balance=500  balance=2000  ← Unique to each
```

**Example:**

```python
class BankAccount:
    bank_name = "SBI"  # Class attribute
    
    def __init__(self, customer_name, balance):
        self.customer_name = customer_name  # Instance attribute
        self.balance = balance              # Instance attribute

# Create two accounts
alice = BankAccount("Alice", 1000)
bob = BankAccount("Bob", 500)

# Instance attributes are different
print(alice.customer_name)  # Alice
print(bob.customer_name)    # Bob

# Class attribute is shared
print(alice.bank_name)      # SBI
print(bob.bank_name)        # SBI


# Class attribute is accessed via class itself
print(BankAccount.bank_name)    # Output: "SBI"


# Change class attribute - affects ALL instances
BankAccount.bank_name = "HDFC"
print(alice.bank_name)      # HDFC
print(bob.bank_name)        # HDFC
```

### Comparison Table

| Feature | Class Attribute | Instance Attribute |
|---------|----------------|-------------------|
| **Where defined** | Outside `__init__`, in class body | Inside `__init__` with `self.` |
| **Who owns it** | The class itself | Each individual object |
| **Shared or unique** | Shared by all instances | Unique to each instance |
| **Access** | `ClassName.attribute` | `self.attribute` or `object.attribute` |
| **Example** | Bank name (same for all) | Account balance (different for each) |

---

## 4. Instance Methods vs Class Methods

### Instance Methods (Work on Individual Objects)

**Instance methods** operate on a **specific object's data**.

**Real-World Analogy:**
- Like **personal actions**: "Alice withdraws money from HER account"
- Each person (object) performs actions on their own data

```python
class BankAccount:
    def __init__(self, customer_name, balance):
        self.customer_name = customer_name
        self.balance = balance
    
    # INSTANCE METHOD - Works on THIS specific account
    def withdraw(self, amount):
        """Withdraw money from THIS account"""
        if amount <= self.balance:
            self.balance -= amount
            print(f"{self.customer_name} withdrew {amount}")
            return True
        else:
            print("Insufficient funds!")
            return False
    
    def get_balance(self):
        """Get balance of THIS account"""
        return self.balance

# Create accounts
alice = BankAccount("Alice", 1000)
bob = BankAccount("Bob", 500)

# Instance methods work on specific objects
alice.withdraw(200)  # Alice's balance: 1000 - 200 = 800
bob.withdraw(100)    # Bob's balance: 500 - 100 = 400

print(alice.get_balance())  # 800
print(bob.get_balance())    # 400
```

**Key Features:**
- First parameter is always `self` (refers to the object itself)
- Access using: `object.method()`
- Operate on instance attributes (`self.attribute`)

### Class Methods (Work on the Class Itself)

**Class methods** operate on **class-level data**, not individual objects.

**Real-World Analogy:**
- Like **company-wide actions**: "Change the bank's name for everyone"
- Affects the entire class, not individual objects

```python
class BankAccount:
    bank_name = "SBI"  # Class attribute
    
    def __init__(self, balance):
        self.balance = balance
    
    # CLASS METHOD - Works on class-level data
    @classmethod
    def get_bank_name(cls):
        """Get the bank name (same for all accounts)"""
        return cls.bank_name
    
    @classmethod
    def change_bank_name(cls, new_name):
        """Change bank name for ALL accounts"""
        cls.bank_name = new_name
    
    # INSTANCE METHOD - Works on individual account
    def withdraw(self, amount):
        """Withdraw from THIS account"""
        if amount <= self.balance:
            self.balance -= amount
            return True
        return False

# Create accounts
alice = BankAccount(1000)
bob = BankAccount(500)

# CLASS METHOD - Call on the class itself
print(BankAccount.get_bank_name())  # SBI

# Change bank name for everyone
BankAccount.change_bank_name("HDFC")

# Affects all instances
print(alice.get_bank_name())  # HDFC
print(bob.get_bank_name())    # HDFC

# INSTANCE METHOD - Call on specific object
alice.withdraw(200)  # Only affects Alice's account
```

**Key Features:**
- Decorated with `@classmethod`
- First parameter is `cls` (refers to the class itself)
- Access using: `ClassName.method()` or `object.method()`
- Operate on class attributes (`cls.attribute`)

### Comparison Table

| Feature | Instance Method | Class Method |
|---------|----------------|--------------|
| **Decorator** | None | `@classmethod` |
| **First parameter** | `self` (the object) | `cls` (the class) |
| **Called on** | Individual objects | The class itself |
| **Access** | `object.method()` | `ClassName.method()` |
| **Purpose** | Work with object's data | Work with class-level data |
| **Example** | `alice.withdraw(100)` | `BankAccount.get_bank_name()` |

---

## 5. The `self` Parameter - Explained Simply

**What is `self`?**
- `self` is a reference to **"this specific object"**
- It's how Python knows **which object** you're talking about

**Real-World Analogy:**
- When you say **"MY phone"**, "MY" refers to you specifically
- `self` is like saying **"THIS object's attribute"**

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # THIS person's name
        self.age = age    # THIS person's age
    
    def introduce(self):
        # "self" refers to the specific person object
        print(f"Hi, I'm {self.name} and I'm {self.age} years old")

# Create two people
alice = Person("Alice", 25)
bob = Person("Bob", 30)

# When you call alice.introduce():
# Python automatically passes alice as "self"
alice.introduce()  # Hi, I'm Alice and I'm 25 years old

# When you call bob.introduce():
# Python automatically passes bob as "self"
bob.introduce()    # Hi, I'm Bob and I'm 30 years old
```

**Behind the Scenes:**

```python
# What you write:
alice.introduce()

# What Python actually does:
Person.introduce(alice)  # Passes alice as "self"
```

---

## Complete Example: Putting It All Together

```python
class BankAccount:
    """A simple bank account class"""
    
    # CLASS ATTRIBUTE - Shared by all accounts
    bank_name = "SBI"
    total_accounts = 0
    
    def __init__(self, customer_name, balance):
        """Constructor - Initialize a new account"""
        # INSTANCE ATTRIBUTES - Unique to each account
        self.customer_name = customer_name
        self.balance = balance
        
        # Update class attribute
        BankAccount.total_accounts += 1
    
    # INSTANCE METHOD - Works on individual account
    def deposit(self, amount):
        """Deposit money into THIS account"""
        self.balance += amount
        print(f"{self.customer_name} deposited ₹{amount}")
        print(f"New balance: ₹{self.balance}")
    
    def withdraw(self, amount):
        """Withdraw money from THIS account"""
        if amount <= self.balance:
            self.balance -= amount
            print(f"{self.customer_name} withdrew ₹{amount}")
            print(f"Remaining balance: ₹{self.balance}")
            return True
        else:
            print(f"Sorry {self.customer_name}, insufficient funds!")
            return False
    
    def show_balance(self):
        """Display THIS account's balance"""
        print(f"{self.customer_name}'s balance: ₹{self.balance}")
    
    # CLASS METHOD - Works on class-level data
    @classmethod
    def get_bank_info(cls):
        """Get bank information"""
        print(f"Bank: {cls.bank_name}")
        print(f"Total accounts: {cls.total_accounts}")
    
    @classmethod
    def change_bank_name(cls, new_name):
        """Change bank name for ALL accounts"""
        cls.bank_name = new_name
        print(f"Bank name changed to: {new_name}")

# ========================================
# Usage Examples
# ========================================

# Create accounts (objects)
print("=== Creating Accounts ===")
alice = BankAccount("Alice", 5000)
bob = BankAccount("Bob", 3000)
charlie = BankAccount("Charlie", 10000)

# Instance methods - work on specific accounts
print("\n=== Alice's Transactions ===")
alice.show_balance()    # Alice's balance: ₹5000
alice.deposit(2000)     # Alice deposited ₹2000
alice.withdraw(1000)    # Alice withdrew ₹1000
alice.show_balance()    # Alice's balance: ₹6000

print("\n=== Bob's Transactions ===")
bob.show_balance()      # Bob's balance: ₹3000
bob.withdraw(500)       # Bob withdrew ₹500

# Class methods - work on class-level data
print("\n=== Bank Information ===")
BankAccount.get_bank_info()
# Bank: SBI
# Total accounts: 3

print("\n=== Changing Bank Name ===")
BankAccount.change_bank_name("HDFC")

print("\n=== Checking All Accounts ===")
print(f"Alice's bank: {alice.bank_name}")      # HDFC
print(f"Bob's bank: {bob.bank_name}")          # HDFC
print(f"Charlie's bank: {charlie.bank_name}")  # HDFC
```

**Output:**

```
=== Creating Accounts ===

=== Alice's Transactions ===
Alice's balance: ₹5000
Alice deposited ₹2000
New balance: ₹7000
Alice withdrew ₹1000
Remaining balance: ₹6000
Alice's balance: ₹6000

=== Bob's Transactions ===
Bob's balance: ₹3000
Bob withdrew ₹500
Remaining balance: ₹2500

=== Bank Information ===
Bank: SBI
Total accounts: 3

=== Changing Bank Name ===
Bank name changed to: HDFC

=== Checking All Accounts ===
Alice's bank: HDFC
Bob's bank: HDFC
Charlie's bank: HDFC
```

---

## Quick Reference Cheat Sheet

### Class vs Object

```python
# Class = Blueprint
class Dog:
    species = "Canine"  # Class attribute
    
    def __init__(self, name):
        self.name = name  # Instance attribute

# Objects = Actual instances
buddy = Dog("Buddy")
max_dog = Dog("Max")
```

### Class Attribute vs Instance Attribute

```python
class MyClass:
    class_var = "Shared"  # Class attribute (outside __init__)
    
    def __init__(self, value):
        self.instance_var = value  # Instance attribute (inside __init__)
```

### Instance Method vs Class Method

```python
class MyClass:
    # Instance method
    def instance_method(self):
        return f"Working on {self}"
    
    # Class method
    @classmethod
    def class_method(cls):
        return f"Working on {cls}"
```

---

## Summary

| Concept | What It Is | Example |
|---------|-----------|---------|
| **Class** | Blueprint/template | `class BankAccount:` |
| **Object** | Instance created from class | `alice = BankAccount()` |
| **Class Attribute** | Data shared by all objects | `bank_name = "SBI"` |
| **Instance Attribute** | Data unique to each object | `self.balance = 1000` |
| **Instance Method** | Function that works on an object | `def withdraw(self, amount):` |
| **Class Method** | Function that works on the class | `@classmethod def get_bank_name(cls):` |
| **self** | Reference to the current object | `self.name` |
| **cls** | Reference to the class itself | `cls.bank_name` |

---

## Key Takeaways

1. **Classes** are blueprints, **objects** are actual instances
2. **Class attributes** are shared, **instance attributes** are unique
3. **Instance methods** use `self`, **class methods** use `cls`
4. Use **instance methods** for object-specific operations
5. Use **class methods** for class-level operations

---

# @classmethod Explained in Simple Way

Let me explain `@classmethod` with the simplest possible examples.

---

## **What is @classmethod?**

`@classmethod` is a **decorator** that lets you create methods that work on the **entire class** (not just one object).

### **Simple Analogy:**

```
Imagine a school:

┌─────────────────────────────────┐
│     School (Class)              │
│  Principal's Office (Important) │
└─────────────────────────────────┘
         │
    ┌────┴────┬─────────┐
    │          │         │
  Room 1     Room 2    Room 3
 (Students) (Students) (Students)

- Regular Method = Something a teacher does IN a classroom
- @classmethod = Something the Principal does for ENTIRE school
```

---

## **Example 1: Bank Account (Simplest)**

```python
class BankAccount:
    bank_name = "SBI"  # Class variable - SHARED
    
    def __init__(self, balance):
        self.balance = balance  # Instance variable - UNIQUE
    
    # REGULAR METHOD - Works on ONE account
    def withdraw(self, amount):
        self.balance -= amount
        print(f"Withdrew ${amount}")
    
    # @classmethod - Works on ENTIRE class
    @classmethod
    def change_bank_name(cls, new_name):
        cls.bank_name = new_name
        print(f"Bank name changed to {new_name}")

# Create 2 accounts
alice_account = BankAccount(1000)
bob_account = BankAccount(500)

# Regular method - works on ONE account
alice_account.withdraw(100)  # Only Alice's balance changes

# @classmethod - works on ENTIRE class
BankAccount.change_bank_name("HDFC")
# NOW BOTH alice and bob see the new name!

print(alice_account.bank_name)  # HDFC
print(bob_account.bank_name)    # HDFC
```

**Output:**
```
Withdrew $100
Bank name changed to HDFC
HDFC
HDFC
```

---

## **Example 2: Student Class Counter**

```python
class Student:
    total_students = 0  # Class variable - count all students
    
    def __init__(self, name):
        self.name = name  # Instance variable - individual name
        Student.total_students += 1
    
    @classmethod
    def get_total_students(cls):
        """Get total number of students"""
        return cls.total_students
    
    @classmethod
    def reset_counter(cls):
        """Reset counter for entire class"""
        cls.total_students = 0

# Create students
s1 = Student("Alice")
s2 = Student("Bob")
s3 = Student("Charlie")

# Use @classmethod
print(Student.get_total_students())  # 3

# Create more
s4 = Student("David")
print(Student.get_total_students())  # 4

# Reset for entire class
Student.reset_counter()
print(Student.get_total_students())  # 0
```

**Output:**
```
3
4
0
```

---

## **Example 3: Creating Objects from Different Data (Factory Pattern)**

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    # Regular method
    def introduce(self):
        return f"Hi, I'm {self.name}, {self.age} years old"
    
    # @classmethod - Create Person from different format
    @classmethod
    def from_birth_year(cls, name, birth_year):
        """Create person using birth year instead of age"""
        age = 2024 - birth_year
        return cls(name, age)
    
    @classmethod
    def from_string(cls, person_string):
        """Create person from string like 'Alice-25'"""
        name, age = person_string.split('-')
        return cls(name, int(age))

# Normal way
p1 = Person("Alice", 30)
print(p1.introduce())  # Hi, I'm Alice, 30 years old

# Using @classmethod - different ways to create
p2 = Person.from_birth_year("Bob", 1999)
print(p2.introduce())  # Hi, I'm Bob, 25 years old

p3 = Person.from_string("Charlie-28")
print(p3.introduce())  # Hi, I'm Charlie, 28 years old
```

**Output:**
```
Hi, I'm Alice, 30 years old
Hi, I'm Bob, 25 years old
Hi, I'm Charlie, 28 years old
```

---

## **Example 4: Configuration Settings (Real-World)**

```python
class AppSettings:
    debug = False  # Class variable
    timeout = 30   # Class variable
    
    def __init__(self, app_name):
        self.app_name = app_name  # Instance variable
    
    @classmethod
    def enable_debug(cls):
        """Enable debug for ENTIRE app"""
        cls.debug = True
        print("Debug mode ON for entire app")
    
    @classmethod
    def disable_debug(cls):
        """Disable debug for ENTIRE app"""
        cls.debug = False
        print("Debug mode OFF for entire app")
    
    @classmethod
    def set_timeout(cls, seconds):
        """Set timeout for ENTIRE app"""
        cls.timeout = seconds
        print(f"Timeout set to {seconds} seconds for all apps")
    
    def show_settings(self):
        """Show settings for THIS app"""
        print(f"{self.app_name}: Debug={AppSettings.debug}, Timeout={AppSettings.timeout}")

# Create different apps
auth_app = AppSettings("Auth")
db_app = AppSettings("Database")
api_app = AppSettings("API")

# Show default settings
auth_app.show_settings()  # Auth: Debug=False, Timeout=30
db_app.show_settings()    # Database: Debug=False, Timeout=30

# Use @classmethod to change for ENTIRE app
AppSettings.enable_debug()
AppSettings.set_timeout(60)

# NOW all apps see the changes
auth_app.show_settings()  # Auth: Debug=True, Timeout=60
db_app.show_settings()    # Database: Debug=True, Timeout=60
api_app.show_settings()   # API: Debug=True, Timeout=60
```

**Output:**
```
Auth: Debug=False, Timeout=30
Database: Debug=False, Timeout=30
Debug mode ON for entire app
Timeout set to 60 seconds for all apps
Auth: Debug=True, Timeout=60
Database: Debug=True, Timeout=60
API: Debug=True, Timeout=60
```

---

## **Example 5: Logger System**

```python
class Logger:
    log_level = "INFO"  # Class variable - shared
    
    def __init__(self, module_name):
        self.module_name = module_name  # Instance variable - unique
    
    @classmethod
    def set_log_level(cls, level):
        """Change log level for ENTIRE system"""
        cls.log_level = level
    
    def log(self, message):
        """Instance method - log for THIS module"""
        print(f"[{self.module_name}] [{Logger.log_level}] {message}")

# Create loggers for different modules
auth_logger = Logger("AUTH")
db_logger = Logger("DATABASE")
api_logger = Logger("API")

# All use default log level
auth_logger.log("User login")      # [AUTH] [INFO] User login
db_logger.log("Query executed")    # [DATABASE] [INFO] Query executed
api_logger.log("Request received") # [API] [INFO] Request received

print("--- Changing log level for entire system ---")

# Change for ENTIRE system using @classmethod
Logger.set_log_level("DEBUG")

# Now all loggers use new level
auth_logger.log("User login")      # [AUTH] [DEBUG] User login
db_logger.log("Query executed")    # [DATABASE] [DEBUG] Query executed
api_logger.log("Request received") # [API] [DEBUG] Request received
```

**Output:**
```
[AUTH] [INFO] User login
[DATABASE] [INFO] Query executed
[API] [INFO] Request received
--- Changing log level for entire system ---
[AUTH] [DEBUG] User login
[DATABASE] [DEBUG] Query executed
[API] [DEBUG] Request received
```

---

## **Example 6: @classmethod vs Regular Method - Side by Side**

```python
class Car:
    total_cars = 0  # Class variable
    
    def __init__(self, brand, model):
        self.brand = brand        # Instance variable
        self.model = model        # Instance variable
        Car.total_cars += 1
    
    # REGULAR METHOD - Works on ONE car
    def drive(self):
        print(f"Driving {self.brand} {self.model}")
    
    # @classmethod - Works on ENTIRE class
    @classmethod
    def get_total_cars(cls):
        return cls.total_cars

# Create cars
car1 = Car("Toyota", "Camry")
car2 = Car("Honda", "Civic")
car3 = Car("Ford", "Mustang")

# Regular method - works on ONE car
car1.drive()  # Output: Driving Toyota Camry
car2.drive()  # Output: Driving Honda Civic

# @classmethod - works on ENTIRE class
print(Car.get_total_cars())  # Output: 3

# You can also call @classmethod on instance (but don't do this)
print(car1.get_total_cars())  # Output: 3 (same result)
```

**Output:**
```
Driving Toyota Camry
Driving Honda Civic
3
3
```

---

## **Key Differences - Quick Table**

| Feature | Regular Method | @classmethod |
|---------|----------------|-------------|
| **Syntax** | `def method(self)` | `@classmethod` `def method(cls)` |
| **First Parameter** | `self` (one object) | `cls` (entire class) |
| **What it touches** | One object's data | Class's shared data |
| **Call on** | `object.method()` | `ClassName.method()` |
| **Example** | `car.drive()` | `Car.get_total_cars()` |
| **Affects** | Only that object | ENTIRE class |

---

## **When to Use @classmethod**

```python
Use @classmethod when you need to:

✅ Count total objects created
✅ Change shared settings for entire app
✅ Create objects from different data formats
✅ Access shared resources (database, config)
✅ Reset/initialize class-wide data
✅ Implement singleton pattern (only one instance)

❌ Don't use @classmethod for:
❌ Working on individual object data
❌ Methods that only affect one instance
```

---

## **Real-World Comparison**

```python
class BankAccount:
    bank_name = "SBI"
    
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance
    
    # Regular method - Personal action
    def withdraw(self, amount):
        self.balance -= amount
        return f"{self.owner} withdrew ${amount}"
    
    # @classmethod - Company-wide action
    @classmethod
    def merge_banks(cls, new_name):
        cls.bank_name = new_name
        return f"Merged into {new_name}"

# Create accounts
alice = BankAccount("Alice", 1000)
bob = BankAccount("Bob", 500)

# Regular method - Personal
print(alice.withdraw(100))  # Alice withdrew $100

# @classmethod - Company-wide
print(BankAccount.merge_banks("HDFC"))  # Merged into HDFC

# Both accounts now show new bank
print(alice.bank_name)  # HDFC
print(bob.bank_name)    # HDFC
```

**Output:**
```
Alice withdrew $100
Merged into HDFC
HDFC
HDFC
```

---

## **Summary** ✅

| Point | Explanation |
|-------|-------------|
| **What is it?** | A method that works on the CLASS, not individual objects |
| **How to use?** | Add `@classmethod` before the method, use `cls` instead of `self` |
| **Call it on** | The CLASS itself: `ClassName.method()` |
| **Use when** | You need to change/access shared data for ENTIRE app |
| **Real examples** | Logging, config, database, counters, factory methods |

**Think of it like this:**
- **Regular method** = Something YOU do (personal action)
- **@classmethod** = Something the ORGANIZATION does (affects everyone)

Does this make sense? Let me know if you want more examples! 😊

## Practice Exercises

### Exercise 1: Create a Student Class

Create a `Student` class with:
- Class attribute: `school_name = "ABC High School"`
- Instance attributes: `name`, `age`, `grade`
- Instance method: `display_info()` - prints student details
- Class method: `change_school_name(new_name)` - changes school name

```python
# Your solution here
class Student:
    pass

# Test your code
student1 = Student("Alice", 15, 10)
student2 = Student("Bob", 16, 11)
```

### Exercise 2: Create a Product Class

Create a `Product` class for an e-commerce store:
- Class attribute: `total_products = 0`
- Instance attributes: `name`, `price`, `quantity`
- Instance method: `apply_discount(percentage)` - reduces price
- Class method: `get_total_products()` - returns total products created

```python
# Your solution here
class Product:
    pass

# Test your code
laptop = Product("Laptop", 50000, 10)
phone = Product("Phone", 20000, 25)
```

---

## Solutions

### Solution 1: Student Class

```python
class Student:
    school_name = "ABC High School"  # Class attribute
    
    def __init__(self, name, age, grade):
        self.name = name      # Instance attributes
        self.age = age
        self.grade = grade
    
    def display_info(self):
        """Display student information"""
        print(f"Name: {self.name}")
        print(f"Age: {self.age}")
        print(f"Grade: {self.grade}")
        print(f"School: {self.school_name}")
    
    @classmethod
    def change_school_name(cls, new_name):
        """Change school name for all students"""
        cls.school_name = new_name
        print(f"School name changed to: {new_name}")

# Test
student1 = Student("Alice", 15, 10)
student2 = Student("Bob", 16, 11)

student1.display_info()
Student.change_school_name("XYZ High School")
student2.display_info()
```

### Solution 2: Product Class

```python
class Product:
    total_products = 0  # Class attribute
    
    def __init__(self, name, price, quantity):
        self.name = name          # Instance attributes
        self.price = price
        self.quantity = quantity
        Product.total_products += 1
    
    def apply_discount(self, percentage):
        """Apply discount to product price"""
        discount = self.price * (percentage / 100)
        self.price -= discount
        print(f"Discount applied! New price: ₹{self.price}")
    
    @classmethod
    def get_total_products(cls):
        """Get total number of products"""
        return cls.total_products

# Test
laptop = Product("Laptop", 50000, 10)
phone = Product("Phone", 20000, 25)

print(f"Total products: {Product.get_total_products()}")  # 2
laptop.apply_discount(10)  # 10% discount
```

---

## Next Steps

Now that you understand the basics, explore:
1. **Inheritance** - Creating child classes from parent classes
2. **Polymorphism** - Same method, different behaviors
3. **Encapsulation** - Hiding data with properties
4. **Abstraction** - Defining contracts with abstract classes

Happy coding! 🚀


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



# Python Inheritance – Complete Notes with Examples

# 1. Introduction to Inheritance

Inheritance is one of the most important concepts in Object-Oriented Programming (OOP).

Inheritance means:

> One class can use properties and methods of another class.

Real-life example:

- Parents → Child inherits property
- Grandparents → Parents → Child = Multilevel inheritance
- Mother + Father → Child = Multiple inheritance

In Python, inheritance helps us:

- Reuse code
- Avoid duplication
- Build relationships between classes

---

# 2. Basic Class Example

## Parent Class

```python
class A:

    def f1(self):
        print("Feature 1 works")

    def f2(self):
        print("Feature 2 works")
```

## Creating Object

```python
obj1 = A()

obj1.f1()
obj1.f2()
```

## Output

```python
Feature 1 works
Feature 2 works
```

---

# 3. Another Class

```python
class B:

    def f3(self):
        print("Feature 3 works")

    def f4(self):
        print("Feature 4 works")
```

## Object of B

```python
obj2 = B()

obj2.f3()
obj2.f4()
```

---

# 4. Problem Without Inheritance

Suppose we want class `B` to use methods of class `A`.

Without inheritance, we would need to copy code:

```python
# Not recommended
```

Code duplication is not good practice.

---

# 5. Single Inheritance

Single inheritance means:

> One child class inherits from one parent class.

## Syntax

```python
class Child(Parent):
```

## Example

```python
class A:

    def f1(self):
        print("Feature 1 works")

    def f2(self):
        print("Feature 2 works")


class B(A):

    def f3(self):
        print("Feature 3 works")

    def f4(self):
        print("Feature 4 works")
```

## Creating Object

```python
obj = B()

obj.f1()
obj.f2()
obj.f3()
obj.f4()
```

## Output

```python
Feature 1 works
Feature 2 works
Feature 3 works
Feature 4 works
```

---

# 6. Understanding Parent and Child Class

In the example:

```python
class B(A):
```

- `A` → Parent class
- `B` → Child class

Child class gets all features of parent class.

---

# 7. Multilevel Inheritance

Multilevel inheritance means:

> One class inherits from another child class.

## Structure

```python
A → B → C
```

- A = Grandparent
- B = Parent
- C = Child

---

# 8. Multilevel Inheritance Example

```python
class A:

    def f1(self):
        print("Feature 1 works")


class B(A):

    def f2(self):
        print("Feature 2 works")


class C(B):

    def f3(self):
        print("Feature 3 works")
```

## Creating Object

```python
obj = C()

obj.f1()
obj.f2()
obj.f3()
```

## Output

```python
Feature 1 works
Feature 2 works
Feature 3 works
```

---

# 9. Important Point

Parent can NOT access child methods.

## Example

```python
obj = B()

obj.f3()   # Error
```

Because `f3()` belongs to class `C`.

Child can access parent methods.

Parent cannot access child methods.

---

# 10. Multiple Inheritance

Multiple inheritance means:

> One child class inherits from multiple parent classes.

## Structure

```python
class C(A, B)
```

Here:

- A = Parent 1
- B = Parent 2
- C = Child

---

# 11. Multiple Inheritance Example

```python
class A:

    def f1(self):
        print("Feature 1 works")


class B:

    def f2(self):
        print("Feature 2 works")


class C(A, B):

    def f3(self):
        print("Feature 3 works")
```

## Creating Object

```python
obj = C()

obj.f1()
obj.f2()
obj.f3()
```

## Output

```python
Feature 1 works
Feature 2 works
Feature 3 works
```

---

# 12. Method Resolution Order (MRO)

MRO stands for:

> Method Resolution Order

Python follows a specific order to search methods.

Order:

1. Current class
2. First parent class
3. Second parent class

---

# 13. MRO Example

```python
class A:

    def show(self):
        print("In A Show")


class B:

    def show(self):
        print("In B Show")


class C(A, B):
    pass
```

## Creating Object

```python
obj = C()

obj.show()
```

## Output

```python
In A Show
```

Why?

Because Python searches:

1. C
2. A
3. B

A comes first.

---

# 14. Changing MRO Sequence

```python
class C(B, A):
    pass
```

## Output

```python
In B Show
```

Now Python searches:

1. C
2. B
3. A

---

# 15. Calling Parent Class Method Directly

You can directly call a parent class method.

## Example

```python
class A:

    def show(self):
        print("In A Show")


class B:

    def show(self):
        print("In B Show")


class C(A, B):
    pass


obj = C()

B.show(obj)
```

## Output

```python
In B Show
```

---

# 16. Real-Life Example – Vehicle

## Parent Class

```python
class Vehicle:

    def start(self):
        print("Vehicle Started")
```

## Child Class

```python
class Car(Vehicle):

    def music(self):
        print("Music Playing")
```

## Usage

```python
c = Car()

c.start()
c.music()
```

## Output

```python
Vehicle Started
Music Playing
```

---

# 17. Real-Life Example – Employee

```python
class Employee:

    def work(self):
        print("Employee Working")


class Manager(Employee):

    def meeting(self):
        print("Manager attends meeting")
```

## Usage

```python
m = Manager()

m.work()
m.meeting()
```

---

# 18. Advantages of Inheritance

- Code reusability
- Less duplication
- Better organization
- Easier maintenance
- Real-world relationship modeling

---

# 19. Summary Table

| Inheritance Type | Description |
|---|---|
| Single Inheritance | One child inherits one parent |
| Multilevel Inheritance | Chain inheritance |
| Multiple Inheritance | One child inherits multiple parents |

---

# 20. Key Interview Questions

## What is inheritance?

Inheritance allows one class to acquire properties and methods of another class.

---

## What is parent class?

The class being inherited.

---

## What is child class?

The class that inherits from another class.

---

## What is MRO?

Method Resolution Order determines the order in which Python searches methods.

---

# 21. Complete Combined Example

```python
class A:

    def f1(self):
        print("Feature 1")

    def show(self):
        print("Inside A")


class B:

    def f2(self):
        print("Feature 2")

    def show(self):
        print("Inside B")


class C(A, B):

    def f3(self):
        print("Feature 3")


obj = C()

obj.f1()
obj.f2()
obj.f3()
obj.show()
```

## Output

```python
Feature 1
Feature 2
Feature 3
Inside A
```

Because A comes before B in inheritance order.

---

# 22. Final Understanding

- Inheritance helps reuse code.
- Child classes can access parent methods.
- Python supports:
  - Single inheritance
  - Multilevel inheritance
  - Multiple inheritance
- MRO decides which method Python executes first.



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

# Duck Typing and Polymorphism in Python - Complete Guide

Let me explain both concepts with simple examples, real-world analogies, and diagrams.

---

## **Part 1: Duck Typing**

### **What is Duck Typing?**

**"If it walks like a duck and quacks like a duck, then it's a duck"**

Duck typing means: **If an object behaves like what you need, you can use it - regardless of its actual type.**

You don't check **what it is**, you check **what it can do**.

---

### **Simple Analogy: Restaurant Kitchen**

```
┌─────────────────────────────────────────────────────────┐
│          Restaurant Kitchen                             │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Chef says: "I need something that can CUT"            │
│                                                         │
│  ✓ Knife can cut    → Use it!                          │
│  ✓ Scissors can cut → Use it!                          │
│  ✓ Saw can cut      → Use it!                          │
│                                                         │
│  Chef doesn't ask "What TYPE are you?"                 │
│  Chef only asks "Can you CUT?"                         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

### **Example 1: Duck Typing - Simple**

```python
# NO class hierarchy needed!

class Dog:
    def speak(self):
        return "Woof! Woof!"

class Cat:
    def speak(self):
        return "Meow! Meow!"

class Robot:
    def speak(self):
        return "Beep! Boop!"

# Function that uses duck typing
def make_animal_speak(animal):
    """Doesn't care WHAT it is, only that it can speak()"""
    print(animal.speak())

# Use with any object that has speak()
dog = Dog()
cat = Cat()
robot = Robot()

make_animal_speak(dog)      # Woof! Woof!
make_animal_speak(cat)      # Meow! Meow!
make_animal_speak(robot)    # Beep! Boop!
```

**Output:**
```
Woof! Woof!
Meow! Meow!
Beep! Boop!
```

**Key Point:** `make_animal_speak()` doesn't care if it's a Dog, Cat, or Robot. It only cares that the object has a `speak()` method.

---

### **Example 2: Duck Typing - Different Types**

```python
class Bird:
    def fly(self):
        return "Flying high!"

class Airplane:
    def fly(self):
        return "Taking off!"

class Superman:
    def fly(self):
        return "Faster than a bullet!"

# Function works with ANYTHING that can fly()
def launch(flying_object):
    print(flying_object.fly())

# All work with same function!
bird = Bird()
plane = Airplane()
hero = Superman()

launch(bird)       # Flying high!
launch(plane)      # Taking off!
launch(hero)       # Faster than a bullet!
```

**Output:**
```
Flying high!
Taking off!
Faster than a bullet!
```

---

### **Example 3: Real-World - File Operations**

```python
class TextFile:
    def read(self):
        return "Reading text file"
    
    def write(self, data):
        return f"Writing to text: {data}"

class ImageFile:
    def read(self):
        return "Reading image file"
    
    def write(self, data):
        return f"Writing to image: {data}"

class PDFFile:
    def read(self):
        return "Reading PDF file"
    
    def write(self, data):
        return f"Writing to PDF: {data}"

# Function that works with ANY file type
def save_and_read(file_object):
    print(file_object.write("Important data"))
    print(file_object.read())

# Works with all file types!
text = TextFile()
image = ImageFile()
pdf = PDFFile()

save_and_read(text)    # No inheritance needed!
save_and_read(image)
save_and_read(pdf)
```

**Output:**
```
Writing to text: Important data
Reading text file
Writing to image: Important data
Reading image file
Writing to PDF: Important data
Reading PDF file
```

---

### **Diagram: Duck Typing Flow**

```
┌────────────────────────────────────────────────────────┐
│              Duck Typing (No Inheritance)              │
├────────────────────────────────────────────────────────┤
│                                                        │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐            │
│  │  Dog     │  │  Cat     │  │  Robot   │            │
│  │----------|  |----------|  |----------|            │
│  │ speak()  │  │ speak()  │  │ speak()  │            │
│  └──────────┘  └──────────┘  └──────────┘            │
│       │              │              │                 │
│       └──────────────┼──────────────┘                 │
│                      │                                │
│              All implement speak()                    │
│              (No parent class needed!)                │
│                                                        │
│    make_animal_speak(any_object_with_speak)          │
│                                                        │
└────────────────────────────────────────────────────────┘
```

---

---

## **Part 2: Polymorphism**

### **What is Polymorphism?**

**"Many forms"** - Same function/method, different behaviors based on the object type.

There are 3 types:
1. **Method Overriding** (Inheritance)
2. **Method Overloading** (Not supported in Python directly)
3. **Operator Overloading**

---

### **Simple Analogy: Vehicle Payment**

```
┌──────────────────────────────────────────────┐
│          "Pay Toll" (Same action)            │
├──────────────────────────────────────────────┤
│                                              │
│  Car:       pays $5                          │
│  Truck:     pays $10                         │
│  Bike:      pays $2                          │
│  Bus:       pays $15                         │
│                                              │
│  Same method (pay_toll), different amounts! │
│                                              │
└──────────────────────────────────────────────┘
```

---

### **Example 1: Method Overriding (Inheritance)**

```python
# Base class (Parent)
class Animal:
    def speak(self):
        return "Some sound"

# Derived classes (Children)
class Dog(Animal):
    def speak(self):  # Override parent's speak()
        return "Woof!"

class Cat(Animal):
    def speak(self):  # Override parent's speak()
        return "Meow!"

class Cow(Animal):
    def speak(self):  # Override parent's speak()
        return "Moo!"

# Same function call, different results!
animals = [Dog(), Cat(), Cow()]

for animal in animals:
    print(animal.speak())  # Same method, different behavior!
```

**Output:**
```
Woof!
Meow!
Moo!
```

**Key Point:** All inherit from `Animal`, but each `speak()` works differently.

---

### **Example 2: Real-World - Payment Processing**

```python
class PaymentMethod:
    def process_payment(self, amount):
        return "Payment processed"

class CreditCard(PaymentMethod):
    def process_payment(self, amount):
        return f"Processing ${amount} via Credit Card"

class Bitcoin(PaymentMethod):
    def process_payment(self, amount):
        return f"Processing {amount} BTC via Bitcoin"

class PayPal(PaymentMethod):
    def process_payment(self, amount):
        return f"Processing ${amount} via PayPal"

class ApplePay(PaymentMethod):
    def process_payment(self, amount):
        return f"Processing ${amount} via Apple Pay"

# Polymorphism in action!
def checkout(payment_method, amount):
    print(payment_method.process_payment(amount))

# Different payment methods, same function!
card = CreditCard()
crypto = Bitcoin()
paypal = PayPal()
apple = ApplePay()

checkout(card, 100)      # Processing $100 via Credit Card
checkout(crypto, 0.5)    # Processing 0.5 BTC via Bitcoin
checkout(paypal, 100)    # Processing $100 via PayPal
checkout(apple, 100)     # Processing $100 via Apple Pay
```

**Output:**
```
Processing $100 via Credit Card
Processing 0.5 BTC via Bitcoin
Processing $100 via PayPal
Processing $100 via Apple Pay
```

---

### **Example 3: Shape Polymorphism**

```python
import math

# Base class
class Shape:
    def area(self):
        pass

# Derived classes
class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return math.pi * self.radius ** 2

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    def area(self):
        return self.side ** 2

class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height
    
    def area(self):
        return 0.5 * self.base * self.height

# Polymorphism in action!
def print_area(shape):
    print(f"Area: {shape.area():.2f}")

shapes = [
    Circle(5),
    Square(4),
    Triangle(3, 4)
]

for shape in shapes:
    print_area(shape)  # Same function, different calculation!
```

**Output:**
```
Area: 78.50
Area: 16.00
Area: 6.00
```

---

### **Example 4: Operator Overloading (Special Methods)**

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    # Overload + operator
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    # Overload - operator
    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)
    
    # Overload * operator
    def __mul__(self, scalar):
        return Vector(self.x * scalar, self.y * scalar)
    
    # Overload == operator
    def __eq__(self, other):
        return self.x == other.x and self.y == other.y
    
    # String representation
    def __str__(self):
        return f"({self.x}, {self.y})"

# Using overloaded operators
v1 = Vector(2, 3)
v2 = Vector(1, 4)

print(v1 + v2)      # (3, 7)
print(v1 - v2)      # (1, -1)
print(v1 * 2)       # (4, 6)
print(v1 == v2)     # False
```

**Output:**
```
(3, 7)
(1, -1)
(4, 6)
False
```

---

### **Diagram: Polymorphism (Method Overriding)**

```
┌─────────────────────────────────────────────┐
│       Polymorphism (Inheritance)            │
├─────────────────────────────────────────────┤
│                                             │
│              Animal (Base Class)            │
│              ┌────────────────┐             │
│              │ speak()        │             │
│              └────────────────┘             │
│                      ▲                      │
│         ┌────────────┼────────────┐         │
│         │            │            │         │
│      Dog          Cat          Cow          │
│      ─────────    ─────────    ─────────    │
│   Woof!         Meow!        Moo!          │
│                                             │
│  Same method name, different implementation│
│                                             │
└─────────────────────────────────────────────┘
```

---

---

## **Part 3: Duck Typing vs Polymorphism**

### **Comparison Table**

| Feature | Duck Typing | Polymorphism |
|---------|------------|--------------|
| **Inheritance** | ❌ Not needed | ✅ Needed |
| **Type Checking** | No type checking | Type checking via inheritance |
| **Flexibility** | Very flexible | Structured |
| **Example** | Any object with `speak()` | Animal → Dog, Cat |
| **Philosophy** | "What can it do?" | "What is it?" |
| **When to use** | General behavior | Related objects |

---

### **Side-by-Side Comparison**

**Duck Typing Approach:**
```python
# No parent class needed
class TextProcessor:
    def process(self):
        return "Processing text"

class ImageProcessor:
    def process(self):
        return "Processing image"

def run_processor(processor):
    print(processor.process())  # Works with ANY object that has process()
```

**Polymorphism Approach:**
```python
# Parent class required
class Processor:
    def process(self):
        pass

class TextProcessor(Processor):
    def process(self):
        return "Processing text"

class ImageProcessor(Processor):
    def process(self):
        return "Processing image"

def run_processor(processor: Processor):  # Type checked
    print(processor.process())
```

---

---

## **Part 4: Real-World Example - E-Commerce**

```python
# DUCK TYPING APPROACH
class CreditCard:
    def charge(self, amount):
        return f"Charged ${amount} to credit card"

class Bitcoin:
    def charge(self, amount):
        return f"Charged {amount} BTC"

class AppleGiftCard:
    def charge(self, amount):
        return f"Charged ${amount} to gift card"

# Works with ANY object that has charge() method
def checkout(payment, amount):
    print(payment.charge(amount))

checkout(CreditCard(), 100)
checkout(Bitcoin(), 0.5)
checkout(AppleGiftCard(), 50)
```

```python
# POLYMORPHISM APPROACH
class Payment:
    def charge(self, amount):
        pass

class CreditCard(Payment):
    def charge(self, amount):
        return f"Charged ${amount} to credit card"

class Bitcoin(Payment):
    def charge(self, amount):
        return f"Charged {amount} BTC"

class AppleGiftCard(Payment):
    def charge(self, amount):
        return f"Charged ${amount} to gift card"

# Type checked - payment must be Payment subclass
def checkout(payment: Payment, amount):
    print(payment.charge(amount))

checkout(CreditCard(), 100)
checkout(Bitcoin(), 0.5)
checkout(AppleGiftCard(), 50)
```

---

---

## **Complete Diagram: Both Concepts**

```
┌───────────────────────────────────────────────────────────┐
│                   Python Concepts                         │
├───────────────────────────────────────────────────────────┤
│                                                           │
│  DUCK TYPING                 POLYMORPHISM                │
│  ─────────────               ──────────────              │
│                                                           │
│  No inheritance      ◄──►    Requires inheritance        │
│  Flexible            ◄──►    Structured                  │
│  "Behavior-based"    ◄──►    "Type-based"                │
│                                                           │
│  Example:                    Example:                    │
│  ┌──────────────┐           ┌──────────────┐            │
│  │ Dog          │           │ Animal       │            │
│  │ speak()      │           │ speak()      │            │
│  └──────────────┘           └──────────────┘            │
│                                    ▲                     │
│  ┌──────────────┐                  │                     │
│  │ Cat          │           ┌──────┴──────┐              │
│  │ speak()      │           │             │              │
│  └──────────────┘        ┌──────┐    ┌──────┐           │
│                          │ Dog  │    │ Cat  │           │
│  ┌──────────────┐        └──────┘    └──────┘           │
│  │ Robot        │                                       │
│  │ speak()      │        speak() inherited              │
│  └──────────────┘        and overridden                 │
│                                                           │
│  All have speak()         All inherit from Animal        │
│  (No parent class)        (Type checking possible)       │
│                                                           │
└───────────────────────────────────────────────────────────┘
```

---

## **Summary Table** ✅

| Concept | What | How | Use Case |
|---------|------|-----|----------|
| **Duck Typing** | If it walks like a duck... | Check behavior, not type | Generic functions |
| **Polymorphism** | One interface, many forms | Inheritance + method override | Related objects |
| **Method Overriding** | Child changes parent method | `class Child(Parent): def method()` | Customization |
| **Operator Overloading** | Change operator behavior | `def __add__(self, other)` | Mathematical operations |

---

## **Which One to Use?**

```python
✅ USE DUCK TYPING when:
   - Objects don't have common parent
   - You only care about behavior
   - Maximum flexibility needed
   - Example: read(), write() on different file types

✅ USE POLYMORPHISM when:
   - Objects are related (is-a relationship)
   - You want type safety
   - Building a framework
   - Example: Dog is-a Animal
```

Does this make sense? Let me know if you want more examples or diagrams! 😊
# 🧠 Polymorphism in Python – Deep Dive (with Duck Typing)

## 📌 1. What is Polymorphism?

**Polymorphism = Same interface, different behavior**

- *Poly* → many  
- *Morphism* → forms  

👉 One function or method can work with different objects and behave differently.

### ✅ Why Polymorphism?
- Improves code reusability
- Reduces complexity
- Makes applications scalable
- Avoids unnecessary conditional logic

---

## 📌 2. Real-Time Analogies

### 🎭 Analogy 1: Play Button
- Spotify → plays music
- YouTube → plays video
- Game → starts game

✅ Same button → different behavior

---

### 🧑‍💼 Analogy 2: Same Person, Multiple Roles
- Office → employee
- Home → parent
- Gym → trainee

✅ Same person → different behavior

---

### 🔌 Analogy 3: Power Socket (Duck Typing)
- Mobile charger
- Laptop charger
- Fan plug

👉 Socket doesn’t care about type
👉 It only cares if it fits

✅ Behavior matters, not type

---

## 📌 3. Types of Polymorphism in Python

### ✅ Function Polymorphism
```python
print(len("hello"))
print(len([1, 2, 3]))
```

---

### ✅ Operator Polymorphism
```python
print(5 + 3)
print("Hi " + "All")
```

---

## 📌 4. Duck Typing Concept

### 🦆 Definition:
> If it behaves like a duck, treat it as a duck

### ✅ Rule:
- Python checks behavior
- Not object type

---

## 📌 5. Basic Example

```python
class Dog:
    def sound(self):
        print("Dog barks")

class Cat:
    def sound(self):
        print("Cat meows")


def make_sound(animal):
    animal.sound()


d = Dog()
c = Cat()

make_sound(d)
make_sound(c)
```

✅ Output:
```
Dog barks
Cat meows
```

---

## 📌 6. Machine Example (Duck Typing)

```python
class Laptop:
    def build(self):
        print("Building project using Laptop")

class Desktop:
    def build(self):
        print("Building project using Desktop")

class Alien:
    def code(self, machine):
        print("Coding started...")
        machine.build()
```

### ✅ Usage

```python
a = Alien()

l = Laptop()
d = Desktop()

a.code(l)
a.code(d)
```

✅ Output:
```
Coding started...
Building project using Laptop

Coding started...
Building project using Desktop
```

---

## 📌 7. Failure Case

```python
class Tablet:
    def read(self):
        print("Reading book")


t = Tablet()

# This will fail
#a.code(t)
```

❌ Error: build() method missing

---

## 📌 8. Real-World Example: Payment System

```python
class CreditCard:
    def pay(self, amount):
        print(f"Paid {amount} using Credit Card")

class PayPal:
    def pay(self, amount):
        print(f"Paid {amount} using PayPal")

class UPI:
    def pay(self, amount):
        print(f"Paid {amount} using UPI")


def make_payment(method, amount):
    method.pay(amount)


cc = CreditCard()
pp = PayPal()
upi = UPI()

make_payment(cc, 100)
make_payment(pp, 200)
make_payment(upi, 300)
```

---

## 📌 9. With vs Without Polymorphism

### ❌ Without Polymorphism
```python
if type(method) == CreditCard:
    pass
elif type(method) == PayPal:
    pass
```

### ✅ With Polymorphism
```python
method.pay()
```

---

## 📌 10. Key Rules

✅ Same method, different behavior  
✅ Focus on behavior, not type  
✅ Improves flexibility

---

## ✅ Final Takeaway

👉 Python uses Duck Typing to achieve polymorphism  
👉 "If it can do the job, Python accepts it" 