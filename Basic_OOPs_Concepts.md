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
