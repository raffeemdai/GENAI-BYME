# Python Asyncio Complete Guide

# Table of Contents
1. Introduction
2. What is Asynchronous Programming?
3. Why Asyncio Exists
4. Asyncio Core Concepts
5. Coroutines
6. async Keyword
7. await Keyword
8. Event Loop
9. Blocking vs Non-Blocking
10. asyncio.sleep()
11. Running Multiple Coroutines with gather()
12. Async HTTP Requests with aiohttp
13. Tasks and Event Loop Scheduling
14. Asyncio + Threading
15. ThreadPoolExecutor
16. run_in_executor()
17. Asyncio + Multiprocessing
18. ProcessPoolExecutor
19. Background Worker Example
20. Thread vs Process vs Asyncio
21. Interview Questions
22. Final Mental Model

---

# Introduction

Asyncio is Python's built-in framework for asynchronous programming. It allows applications to perform multiple I/O-bound operations efficiently without creating many threads or processes.

Modern frameworks such as FastAPI heavily rely on Asyncio, making them highly scalable and performant.

Examples of I/O-bound tasks:

- Database queries
- API calls
- Reading files
- Writing files
- HTTP requests
- Network communication

---

# What is Asynchronous Programming?

## Definition

Asynchronous programming is a programming model where a task can start, pause while waiting for an external operation, and allow other tasks to execute during that waiting period.

Instead of keeping the CPU idle, the application continues doing productive work.

## Real-Life Analogy: Tea Shop

Imagine you own a tea shop.

### Traditional (Synchronous)

```text
Customer 1 orders chai
Wait 3 minutes
Serve chai

Customer 2 orders chai
Wait 3 minutes
Serve chai
```

Total time = 6 minutes

### Asynchronous

```text
Start chai for Customer 1
Start chai for Customer 2
Start chai for Customer 3

All boil simultaneously
```

Total time ≈ 3 minutes

You are not speeding up the tea preparation itself.
You are simply avoiding wasted waiting time.

---

# Why Asyncio Exists

Many applications spend most of their time waiting.

For example:

```text
Database Response
API Response
File Read
Network Call
```

The CPU is mostly idle.

Asyncio efficiently handles this waiting period and allows thousands of tasks to progress concurrently.

---

# Asyncio Core Concepts

There are four foundational concepts:

```text
async
await
Event Loop
asyncio library
```

Everything else builds upon these concepts.

---

# What is a Coroutine?

## Definition

A coroutine is a special function that can:

```text
Start
Pause
Resume
Finish
```

Unlike normal functions, a coroutine does not need to run continuously from beginning to end.

## Normal Function

```python
def greet():
    print("Hello")
```

Execution:

```text
Start
Run
Finish
```

## Coroutine

```python
async def greet():
    print("Hello")
```

Execution:

```text
Start
Pause
Resume
Finish
```

## Real-Life Analogy

Suppose your manager asks for a report.

While preparing it, you realize you need data from another department.

Instead of sitting idle:

```text
Wait...
Wait...
Wait...
```

You start another task.

Once the data arrives, you continue the report.

That is exactly how a coroutine behaves.

---

# async Keyword

## Definition

The `async` keyword declares that a function is asynchronous.

```python
async def fetch_data():
    pass
```

Python understands that:

```text
This function can pause.
This function can use await.
This function is managed by the event loop.
```

## Important

Defining an async function does not execute it.

```python
async def hello():
    print("Hello")
```

Nothing happens until it is scheduled and executed.

---

# await Keyword

## Definition

The `await` keyword pauses the current coroutine until a result becomes available.

```python
await operation()
```

## What Happens Internally?

```text
Pause current coroutine
Allow others to execute
Resume when result is ready
```

## Real-Life Analogy: Pizza Restaurant

You order a pizza.

Bad approach:

```text
Stand at counter for 20 minutes.
```

Smart approach:

```text
Order pizza
Sit with friends
Pizza arrives
Eat pizza
```

You are still waiting.

But your time is being used efficiently.

That is what `await` does.

---

# Event Loop

## Definition

The Event Loop is the heart of Asyncio.

Its responsibilities:

- Execute coroutines
- Schedule tasks
- Pause tasks
- Resume tasks
- Monitor asynchronous operations

## Real-Life Analogy: Call Center Manager

Imagine 100 customers calling a support center.

The manager notices:

```text
Caller 1 waiting for OTP
Caller 2 waiting for Database
Caller 3 asking a question
```

Instead of waiting:

```text
Handle Caller 3
Resume Caller 1 when OTP arrives
Resume Caller 2 when database responds
```

The manager is the Event Loop.

---

# Basic Async Program

```python
import asyncio

async def brew_chai():
    print("Brewing chai...")

    await asyncio.sleep(2)

    print("Chai is ready!")

asyncio.run(brew_chai())
```

Output:

```text
Brewing chai...
(wait 2 seconds)
Chai is ready!
```

---

# Blocking vs Non-Blocking

## Blocking Operation

```python
import time

time.sleep(3)
```

Behavior:

```text
Program stops
CPU waits
Nothing else executes
```

## Real-Life Analogy

Start washing machine.

Then stand and watch it for 30 minutes.

That is blocking.

---

## Non-Blocking Operation

```python
await asyncio.sleep(3)
```

Behavior:

```text
Current task pauses
Others continue executing
```

### Real-Life Analogy

Start washing machine.

Then:

```text
Read a book
Cook food
Answer emails
```

Return when washing is complete.

---

# asyncio.sleep()

## Definition

A non-blocking sleep operation.

```python
await asyncio.sleep(3)
```

Difference:

```python
time.sleep(3)
```

Blocks the entire thread.

```python
await asyncio.sleep(3)
```

Only pauses the current coroutine.

---

# Running Multiple Coroutines with gather()

## Definition

`asyncio.gather()` runs multiple coroutines concurrently.

```python
import asyncio

async def brew(name):
    print(f"Brewing {name}")

    await asyncio.sleep(3)

    print(f"{name} Ready")

async def main():

    await asyncio.gather(
        brew("Masala Chai"),
        brew("Green Chai"),
        brew("Ginger Chai")
    )

asyncio.run(main())
```

## Real-Life Analogy

Three customers order:

```text
Masala Chai
Green Chai
Ginger Chai
```

Without gather:

```text
3 + 3 + 3 = 9 sec
```

With gather:

```text
All start together
≈3 sec total
```

---

# Async HTTP Requests using aiohttp

Install:

```bash
pip install aiohttp
```

Example:

```python
import asyncio
import aiohttp

async def fetch_url(session, url):
    async with session.get(url) as response:
        print(response.status)

async def main():

    urls = [
        "https://httpbin.org/delay/2"
    ] * 3

    async with aiohttp.ClientSession() as session:

        tasks = [
            fetch_url(session, url)
            for url in urls
        ]

        await asyncio.gather(*tasks)

asyncio.run(main())
```

## Real-Life Analogy

Instead of calling your friends one by one:

```text
Call Friend 1
Call Friend 2
Call Friend 3
```

You send messages to everyone simultaneously and wait for replies.

---

# Understanding *tasks

Suppose:

```python
tasks = [task1, task2, task3]
```

Using:

```python
asyncio.gather(*tasks)
```

means:

```python
asyncio.gather(
    task1,
    task2,
    task3
)
```

## Analogy

A basket contains:

```text
Apple
Banana
Orange
```

Using `*` unpacks everything from the basket.

---

# Tasks in Asyncio

## Definition

A Task is a scheduled coroutine managed by the Event Loop.

Think:

```text
Coroutine = Work Description
Task = Scheduled Work
```

The Event Loop executes tasks.

---

# Asyncio + Threading

Asyncio does not replace threading.

Both can work together.

## Example

```python
import asyncio
from concurrent.futures import ThreadPoolExecutor
import time


def check_stock(item):
    time.sleep(3)
    return f"{item}: 42"

async def main():

    loop = asyncio.get_running_loop()

    with ThreadPoolExecutor() as pool:

        result = await loop.run_in_executor(
            pool,
            check_stock,
            "Masala Chai"
        )

    print(result)

asyncio.run(main())
```

---

# ThreadPoolExecutor

## Definition

A pool that manages multiple worker threads.

Useful for:

- Legacy code
- Blocking libraries
- File operations
- Logging

## Real-Life Analogy

You hire assistants.

Instead of personally checking inventory, assistants handle it while you continue serving customers.

---

# run_in_executor()

## Definition

Allows Asyncio to run a normal blocking function in a separate thread or process.

```python
await loop.run_in_executor(...)
```

## Benefit

Blocking code does not freeze the event loop.

---

# Asyncio + Multiprocessing

When work becomes CPU intensive:

```text
Encryption
Machine Learning
Video Processing
Image Processing
Analytics
```

Use processes.

Example:

```python
import asyncio
from concurrent.futures import ProcessPoolExecutor


def encrypt(data):
    return f"Encrypted {data}"

async def main():

    loop = asyncio.get_running_loop()

    with ProcessPoolExecutor() as pool:

        result = await loop.run_in_executor(
            pool,
            encrypt,
            "1234"
        )

    print(result)

if __name__ == "__main__":
    asyncio.run(main())
```

---

# ProcessPoolExecutor

## Definition

Runs tasks in separate processes.

Processes have:

```text
Separate memory
Separate interpreter
Separate CPU utilization
```

## Real-Life Analogy

Thread:

```text
Two workers in the same office.
```

Process:

```text
Two independent offices.
```

---

# Background Worker Example

```python
import asyncio
import threading
import time


def background_worker():

    while True:
        time.sleep(1)
        print("Logging System Health")

async def fetch_order():

    await asyncio.sleep(3)

    print("Order Fetched")

thread = threading.Thread(
    target=background_worker,
    daemon=True
)

thread.start()

asyncio.run(fetch_order())
```

Both run simultaneously.

---

# When to Use What?

## Use Asyncio

- APIs
- Database queries
- File operations
- Web scraping
- FastAPI
- Network services

## Use Threading

- Background jobs
- Logging
- Legacy libraries
- Existing blocking code

## Use Multiprocessing

- AI/ML
- Encryption
- Compression
- Image processing
- Video rendering

---

# Common Interview Questions

## What is Asyncio?

A framework for asynchronous programming using coroutines and an event loop.

## What is a Coroutine?

A special function that can pause and resume execution.

## What is await?

A keyword used to pause a coroutine until an operation completes.

## What is Event Loop?

The scheduler responsible for running and resuming asynchronous tasks.

## Difference between time.sleep() and asyncio.sleep()?

```text
time.sleep()      -> Blocking
asyncio.sleep()   -> Non-Blocking
```

## Does Asyncio Create Threads?

No.

Asyncio typically runs on a single thread using an Event Loop.

## What does asyncio.gather() do?

Runs multiple coroutines concurrently and waits for all to complete.

---

# Final Mental Model

Think of a restaurant.

## Coroutine

Waiter taking orders.

## await

Waiter leaves while food cooks.

## Event Loop

Restaurant manager coordinating everyone.

## gather()

Multiple waiters serving multiple tables simultaneously.

## ThreadPoolExecutor

Assistant workers helping with side jobs.

## ProcessPoolExecutor

Additional kitchens handling heavy workloads.

---

# Key Takeaway

Asyncio is not about making work itself faster.

It is about:

> Avoiding wasted waiting time and efficiently utilizing system resources while tasks wait for external operations.

Remember:

```text
async  -> Creates coroutine
await  -> Pauses coroutine efficiently
Event Loop -> Runs and resumes tasks
asyncio -> Framework managing everything
```

Understanding these four concepts gives you a strong foundation for FastAPI, modern web development, scalable APIs, and advanced asynchronous Python programming.
