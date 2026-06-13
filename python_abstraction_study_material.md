# Python Abstraction — Study Material with Code and Simple Examples

## 1. What is Abstraction?

**Abstraction** means hiding complex internal implementation from the user and showing only the important required details.

In simple words:

> Abstraction means showing **what something does**, but hiding **how it does it**.

---

## 2. Real-World Example of Abstraction

Think about driving a car.

When you drive a car, you use:

- Steering
- Brake
- Accelerator
- Clutch
- Gear

But you do not need to know the internal working of:

- Engine
- Fuel system
- Braking mechanism
- Gearbox
- Electrical system

Still, you can drive the car.

This is abstraction.

The car hides complex implementation and gives you a simple interface to use.

---

## 3. Abstraction in Software

In software, abstraction is used to define a common structure or requirement.

For example, in a payment system:

- Every payment gateway should have a `pay()` method.
- Razorpay can implement `pay()` in its own way.
- PayPal can implement `pay()` in its own way.
- Stripe can implement `pay()` in its own way.

The user or application does not need to know the internal implementation of each payment gateway.

It only needs to call:

```python
gateway.pay()
```

This is abstraction.

---

## 4. Abstract Class and Abstract Method

In Python, abstraction is implemented using the `abc` module.

`abc` stands for:

> Abstract Base Class

To create abstraction, we use:

```python
from abc import ABC, abstractmethod
```

### Important Terms

#### Abstract Class

An **abstract class** is a class that cannot be directly instantiated.

That means we cannot create an object of an abstract class.

#### Abstract Method

An **abstract method** is a method that is declared in the abstract class but does not have full implementation.

The child class must implement this method.

---

## 5. Basic Syntax of Abstraction in Python

```python
from abc import ABC, abstractmethod


class A(ABC):
    @abstractmethod
    def show(self):
        pass
```

Here:

- `A` is an abstract class because it inherits from `ABC`.
- `show()` is an abstract method because it uses `@abstractmethod`.
- `pass` means no implementation is given here.

---

## 6. Simple Example Without Abstraction

First, let us create a normal class.

```python
class A:
    def show(self):
        print("In A show")


obj1 = A()
obj1.show()
```

### Output

```text
In A show
```

This is a normal class.

We can create an object of it:

```python
obj1 = A()
```

and we can call its method:

```python
obj1.show()
```

---

## 7. Creating an Abstract Class

Now let us convert the same class into an abstract class.

```python
from abc import ABC, abstractmethod


class A(ABC):
    @abstractmethod
    def show(self):
        pass


obj1 = A()
obj1.show()
```

### Output

```text
TypeError: Can't instantiate abstract class A with abstract method show
```

### Explanation

Here, class `A` is an abstract class.

```python
class A(ABC):
```

The method `show()` is an abstract method.

```python
@abstractmethod
def show(self):
    pass
```

So Python does not allow us to create an object of class `A`.

This line gives an error:

```python
obj1 = A()
```

Because abstract classes are only used to define requirements. They are not meant to be used directly.

---

## 8. Implementing Abstract Method in Child Class

To use an abstract class, we create a child class and implement the abstract method.

```python
from abc import ABC, abstractmethod


class A(ABC):
    @abstractmethod
    def show(self):
        pass


class B(A):
    def show(self):
        print("In B show")


obj1 = B()
obj1.show()
```

### Output

```text
In B show
```

### Explanation

Class `A` says:

> Any child class must have a `show()` method.

Class `B` follows that rule by implementing `show()`.

```python
class B(A):
    def show(self):
        print("In B show")
```

Now we can create an object of class `B`.

```python
obj1 = B()
```

This works because class `B` has implemented the abstract method.

---

## 9. Why Do We Need Abstraction?

Abstraction is useful when we want to define a common standard.

For example, suppose we are building an e-commerce application.

The application needs a payment gateway.

Today we may use:

- Razorpay

Tomorrow we may use:

- Stripe
- PayPal
- Another payment gateway

If our application is tightly connected to only one payment gateway, changing the gateway later becomes difficult.

Abstraction helps us create a common rule:

> Every payment gateway must have a `pay()` method.

Then our application can work with any payment gateway that follows this rule.

---

## 10. Payment Gateway Example Without Abstraction

Let us first create a simple payment gateway class.

```python
class RazorPay:
    def pay(self):
        print("Paying using RazorPay")


class Purchase:
    def __init__(self, gateway):
        self.gateway = gateway

    def checkout(self):
        print("Checking out")
        self.gateway.pay()


gateway1 = RazorPay()

purchase = Purchase(gateway1)
purchase.checkout()
```

### Output

```text
Checking out
Paying using RazorPay
```

### Explanation

Here:

```python
gateway1 = RazorPay()
```

creates a RazorPay object.

Then we pass that object to `Purchase`.

```python
purchase = Purchase(gateway1)
```

Inside `checkout()`, we call:

```python
self.gateway.pay()
```

This works because `RazorPay` has a method called `pay()`.

---

## 11. Problem Without Abstraction

Suppose another payment gateway uses a different method name.

```python
class RazorPay:
    def make_payment(self):
        print("Paying using RazorPay")


class Purchase:
    def __init__(self, gateway):
        self.gateway = gateway

    def checkout(self):
        print("Checking out")
        self.gateway.pay()


gateway1 = RazorPay()

purchase = Purchase(gateway1)
purchase.checkout()
```

### Output

```text
AttributeError: 'RazorPay' object has no attribute 'pay'
```

### Explanation

The `Purchase` class expects every payment gateway to have a method called:

```python
pay()
```

But `RazorPay` has:

```python
make_payment()
```

So the code fails.

This is why we need a standard.

Abstraction helps us define that standard.

---

## 12. Payment Gateway Example Using Abstraction

Now let us create an abstract class called `PaymentGateway`.

```python
from abc import ABC, abstractmethod


class PaymentGateway(ABC):
    @abstractmethod
    def pay(self):
        pass
```

This abstract class says:

> Every payment gateway must implement the `pay()` method.

Now let us create different payment gateway classes.

```python
from abc import ABC, abstractmethod


class PaymentGateway(ABC):
    @abstractmethod
    def pay(self):
        pass


class RazorPay(PaymentGateway):
    def pay(self):
        print("Paying using RazorPay")


class TeleSkoPay(PaymentGateway):
    def pay(self):
        print("Paying using TeleSkoPay")


class Purchase:
    def __init__(self, gateway):
        self.gateway = gateway

    def checkout(self):
        print("Checking out")
        self.gateway.pay()


gateway1 = RazorPay()
purchase = Purchase(gateway1)
purchase.checkout()

gateway2 = TeleSkoPay()
purchase = Purchase(gateway2)
purchase.checkout()
```

### Output

```text
Checking out
Paying using RazorPay
Checking out
Paying using TeleSkoPay
```

### Explanation

Here, `PaymentGateway` is an abstract class.

```python
class PaymentGateway(ABC):
```

It has an abstract method:

```python
@abstractmethod
def pay(self):
    pass
```

Both `RazorPay` and `TeleSkoPay` inherit from `PaymentGateway`.

```python
class RazorPay(PaymentGateway):
```

```python
class TeleSkoPay(PaymentGateway):
```

So both classes must implement the `pay()` method.

This keeps the design standard.

---

## 13. What Happens If Child Class Does Not Implement Abstract Method?

Let us create a class that inherits from `PaymentGateway` but does not implement `pay()`.

```python
from abc import ABC, abstractmethod


class PaymentGateway(ABC):
    @abstractmethod
    def pay(self):
        pass


class RazorPay(PaymentGateway):
    pass


gateway1 = RazorPay()
```

### Output

```text
TypeError: Can't instantiate abstract class RazorPay with abstract method pay
```

### Explanation

Since `RazorPay` inherits from `PaymentGateway`, it must implement the `pay()` method.

But here, it does not implement it.

So Python does not allow object creation.

This is one of the main advantages of abstraction.

It forces child classes to follow a standard.

---

## 14. Complete Practical Example

```python
from abc import ABC, abstractmethod


class PaymentGateway(ABC):
    @abstractmethod
    def pay(self, amount):
        pass


class RazorPay(PaymentGateway):
    def pay(self, amount):
        print(f"Paying {amount} using RazorPay")


class StripePay(PaymentGateway):
    def pay(self, amount):
        print(f"Paying {amount} using Stripe")


class PayPal(PaymentGateway):
    def pay(self, amount):
        print(f"Paying {amount} using PayPal")


class Purchase:
    def __init__(self, gateway):
        self.gateway = gateway

    def checkout(self, amount):
        print("Checking out")
        self.gateway.pay(amount)


gateway1 = RazorPay()
purchase1 = Purchase(gateway1)
purchase1.checkout(500)

gateway2 = StripePay()
purchase2 = Purchase(gateway2)
purchase2.checkout(800)

gateway3 = PayPal()
purchase3 = Purchase(gateway3)
purchase3.checkout(1200)
```

### Output

```text
Checking out
Paying 500 using RazorPay
Checking out
Paying 800 using Stripe
Checking out
Paying 1200 using PayPal
```

---

## 15. How This Example Uses Abstraction

The abstract class is:

```python
class PaymentGateway(ABC):
    @abstractmethod
    def pay(self, amount):
        pass
```

It defines the requirement:

> Every payment gateway must have a `pay(amount)` method.

The implementation classes are:

```python
class RazorPay(PaymentGateway):
```

```python
class StripePay(PaymentGateway):
```

```python
class PayPal(PaymentGateway):
```

Each class gives its own implementation of `pay()`.

The `Purchase` class does not care which payment gateway is used.

It only calls:

```python
self.gateway.pay(amount)
```

So we can easily switch from RazorPay to Stripe or PayPal.

This is called **loose coupling**.

---

## 16. Object Creation Restriction

An abstract class cannot be instantiated directly.

Example:

```python
from abc import ABC, abstractmethod


class PaymentGateway(ABC):
    @abstractmethod
    def pay(self):
        pass


gateway = PaymentGateway()
```

### Output

```text
TypeError: Can't instantiate abstract class PaymentGateway with abstract method pay
```

### Why?

Because `PaymentGateway` is only a blueprint.

It says what should be done, but it does not say how it should be done.

The actual implementation is done in child classes like:

```python
RazorPay
StripePay
PayPal
```

---

## 17. Abstraction vs Implementation

### Abstraction

Abstraction defines the requirement.

Example:

```python
class PaymentGateway(ABC):
    @abstractmethod
    def pay(self, amount):
        pass
```

It says:

> Every payment gateway should have a `pay()` method.

### Implementation

Implementation provides the actual logic.

Example:

```python
class RazorPay(PaymentGateway):
    def pay(self, amount):
        print(f"Paying {amount} using RazorPay")
```

It says:

> This is how RazorPay performs payment.

---

## 18. Key Points to Remember

1. Abstraction means hiding internal implementation and showing only important details.
2. In Python, abstraction is implemented using the `abc` module.
3. `ABC` is used to create an abstract class.
4. `@abstractmethod` is used to create an abstract method.
5. Abstract classes cannot be instantiated directly.
6. A child class must implement all abstract methods.
7. Abstraction helps define common rules or standards.
8. It helps reduce tight coupling.
9. It makes code flexible and easier to change.
10. Payment gateways are a good real-world example of abstraction.

---

## 19. Simple Final Example

```python
from abc import ABC, abstractmethod


class Car(ABC):
    @abstractmethod
    def start_engine(self):
        pass


class Ford(Car):
    def start_engine(self):
        print("Ford engine started")


class Tesla(Car):
    def start_engine(self):
        print("Tesla motor started")


car1 = Ford()
car1.start_engine()

car2 = Tesla()
car2.start_engine()
```

### Output

```text
Ford engine started
Tesla motor started
```

### Explanation

`Car` is an abstract class.

It says every car must have a `start_engine()` method.

`Ford` and `Tesla` implement that method in their own way.

The user only calls:

```python
car.start_engine()
```

The internal working is hidden.

That is abstraction.

---

## Final Definition

**Abstraction in Python means hiding complex implementation details and exposing only the required functionality. It is implemented using abstract classes and abstract methods from the `abc` module.**

Example syntax:

```python
from abc import ABC, abstractmethod


class MyAbstractClass(ABC):
    @abstractmethod
    def my_method(self):
        pass
```
