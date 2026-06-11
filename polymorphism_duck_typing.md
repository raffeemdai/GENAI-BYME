# 🧠 Polymorphism in Python (with Duck Typing)

## 📌 1. What is Polymorphism?

**Polymorphism = “One thing, multiple behaviors”**

- *Poly* → many  
- *Morphism* → forms  

👉 Same object/method behaves differently depending on context.

### ✅ Real-life example:
- Same person:
  - At home → calm
  - At office → professional
  - With friends → fun  

✅ **Same person, different behavior → Polymorphism**

---

## 📌 2. Duck Typing Concept

### 🦆 Definition:
> “If it looks like a duck and quacks like a duck, it's a duck.”

### 💡 Meaning in Python:
- Python **does NOT care about the object type**
- It only cares if the object has the **required method**

✅ If object has required behavior → it works  
❌ If not → error

---

## 📌 3. Basic Syntax Idea

Instead of checking type like:

```python
if type(obj) == Laptop:
    ...
```

Python uses:

```python
obj.build()   # If method exists → OK
```

---

## 📌 4. Full Example

### ✅ Laptop class

```python
class Laptop:
    def build(self):
        print("Laptop builds")
```

### ✅ Alien class

```python
class Alien:
    def code(self, machine):
        print("Alien building")
        machine.build()
```

### ✅ Use Laptop

```python
l1 = Laptop()
a1 = Alien()

a1.code(l1)
```

✅ Output:
```
Alien building
Laptop builds
```

---

## 📌 5. Desktop Example

```python
class Desktop:
    def build(self):
        print("Desktop builds")
```

```python
d1 = Desktop()
a1.code(d1)
```

✅ Output:
```
Alien building
Desktop builds
```

---

## 📌 6. Failing Example

```python
class Tablet:
    def open_pdf(self):
        print("Opening PDF")
```

```python
t1 = Tablet()
a1.code(t1)
```

❌ Error because `build()` is missing

---

## 📌 7. Summary

### ✅ Polymorphism:
- Same method → different behavior

### ✅ Duck Typing:
- Behavior matters, not type

---

## 📌 8. Final Code

```python
class Laptop:
    def build(self):
        print("Laptop builds")


class Desktop:
    def build(self):
        print("Desktop builds")


class Tablet:
    def open_pdf(self):
        print("Opening PDF")


class Alien:
    def code(self, machine):
        print("Alien building")
        machine.build()


a1 = Alien()

l1 = Laptop()
d1 = Desktop()
t1 = Tablet()

# Working
a1.code(l1)
a1.code(d1)

# Failing
a1.code(t1)
```

---

## ✅ Final Takeaway

👉 Python uses **Duck Typing** to achieve polymorphism  
👉 “If it can do the job, Python accepts it.”
