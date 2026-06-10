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
