# Python

## Overview
Python is a high-level, interpreted, general-purpose programming language known for its readability and versatility. It supports multiple programming paradigms including procedural, object-oriented, and functional programming.

## Core Concepts

### Variables and Data Types
```python
# Variables (dynamically typed)
name = "John"
age = 30
height = 5.9
is_active = True

# Data Types
string = "Hello, World!"
integer = 42
floating = 3.14159
boolean = True
none_value = None

# Collections
my_list = [1, 2, 3, 4, 5]          # Mutable, ordered
my_tuple = (1, 2, 3)                # Immutable, ordered
my_set = {1, 2, 3}                  # Mutable, unordered, unique
my_dict = {"key": "value"}          # Mutable, key-value pairs
```

### Control Flow
```python
# Conditionals
if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")

# Loops
for item in my_list:
    print(item)

for i in range(5):
    print(i)

while condition:
    # do something
    break  # or continue

# Comprehensions
squares = [x**2 for x in range(10)]
even_squares = [x**2 for x in range(10) if x % 2 == 0]
dict_comp = {k: v for k, v in items}
set_comp = {x for x in range(10)}
```

### Functions
```python
# Basic function
def greet(name: str) -> str:
    """Return a greeting message."""
    return f"Hello, {name}!"

# Default arguments
def power(base: int, exp: int = 2) -> int:
    return base ** exp

# *args and **kwargs
def flexible(*args, **kwargs):
    for arg in args:
        print(arg)
    for key, value in kwargs.items():
        print(f"{key}: {value}")

# Lambda functions
square = lambda x: x ** 2

# Decorators
def timer(func):
    def wrapper(*args, **kwargs):
        import time
        start = time.time()
        result = func(*args, **kwargs)
        print(f"Elapsed: {time.time() - start:.2f}s")
        return result
    return wrapper

@timer
def slow_function():
    import time
    time.sleep(1)
```

### Object-Oriented Programming
```python
class Animal:
    # Class variable
    kingdom = "Animalia"
    
    def __init__(self, name: str, species: str):
        # Instance variables
        self.name = name
        self.species = species
        self._protected = "accessible but private by convention"
        self.__private = "name mangled"
    
    def speak(self) -> str:
        return f"{self.name} makes a sound"
    
    @property
    def info(self) -> str:
        return f"{self.name} ({self.species})"
    
    @classmethod
    def from_dict(cls, data: dict):
        return cls(data["name"], data["species"])
    
    @staticmethod
    def is_animal(obj) -> bool:
        return isinstance(obj, Animal)


class Dog(Animal):
    def __init__(self, name: str, breed: str):
        super().__init__(name, "Canis familiaris")
        self.breed = breed
    
    def speak(self) -> str:
        return f"{self.name} says Woof!"
```

### Error Handling
```python
try:
    result = risky_operation()
except ValueError as e:
    print(f"Value error: {e}")
except (TypeError, KeyError) as e:
    print(f"Type or Key error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
else:
    print("No errors occurred")
finally:
    cleanup()

# Custom exceptions
class CustomError(Exception):
    def __init__(self, message: str, code: int):
        super().__init__(message)
        self.code = code

# Context managers
with open("file.txt", "r") as f:
    content = f.read()

# Custom context manager
from contextlib import contextmanager

@contextmanager
def managed_resource():
    resource = acquire()
    try:
        yield resource
    finally:
        release(resource)
```

### Generators and Iterators
```python
# Generator function
def fibonacci(n: int):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

# Generator expression
squares = (x**2 for x in range(10))

# Iterator protocol
class Counter:
    def __init__(self, max_val: int):
        self.max = max_val
        self.current = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current >= self.max:
            raise StopIteration
        self.current += 1
        return self.current
```

### Async Programming
```python
import asyncio

async def fetch_data(url: str) -> dict:
    await asyncio.sleep(1)  # Simulate network delay
    return {"url": url, "data": "..."}

async def main():
    # Sequential
    result1 = await fetch_data("url1")
    result2 = await fetch_data("url2")
    
    # Parallel
    results = await asyncio.gather(
        fetch_data("url1"),
        fetch_data("url2"),
        fetch_data("url3")
    )

asyncio.run(main())
```

### Type Hints
```python
from typing import List, Dict, Optional, Union, Callable, TypeVar

def process_items(items: List[str]) -> Dict[str, int]:
    return {item: len(item) for item in items}

def get_user(user_id: int) -> Optional[User]:
    ...

def handle_input(value: Union[str, int]) -> str:
    return str(value)

T = TypeVar('T')

def first(items: List[T]) -> T:
    return items[0]
```

## Best Practices

1. Follow **PEP 8** style guide
2. Use **type hints** for better code clarity
3. Write **docstrings** for functions and classes
4. Use **virtual environments** (venv, conda)
5. Prefer **list comprehensions** over map/filter
6. Use **context managers** for resource management
7. **Don't use mutable default arguments**

## Common Libraries
- requests, httpx (HTTP)
- pandas, numpy (Data)
- pytest (Testing)
- flask, fastapi, django (Web)
- sqlalchemy (ORM)
- pydantic (Validation)

## Resources
- Python.org documentation
- Real Python
- Fluent Python (book)
