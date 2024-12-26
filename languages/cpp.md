# C++

## Overview
C++ is a general-purpose programming language created as an extension of C. It provides high-level abstractions while maintaining low-level memory manipulation capabilities, making it ideal for system programming and performance-critical applications.

## Core Concepts

### Basic Syntax
```cpp
#include <iostream>
#include <string>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

### Data Types and Variables
```cpp
// Primitive types
int integer = 42;
double decimal = 3.14159;
float floatNum = 3.14f;
char character = 'A';
bool boolean = true;
long long bigNum = 9223372036854775807LL;

// Auto type deduction
auto x = 42;        // int
auto y = 3.14;      // double
auto z = "hello";   // const char*

// Constants
const int MAX_SIZE = 100;
constexpr int SQUARE(int x) { return x * x; }

// References
int& ref = integer;

// Pointers
int* ptr = &integer;
int* nullPtr = nullptr;
```

### Control Flow
```cpp
// If-else
if (condition) {
    // code
} else if (another) {
    // code
} else {
    // code
}

// Switch
switch (value) {
    case 1:
        break;
    case 2:
        [[fallthrough]];
    default:
        break;
}

// Loops
for (int i = 0; i < 10; i++) { }
for (const auto& item : container) { }
while (condition) { }
do { } while (condition);

// Range-based for with structured bindings
for (const auto& [key, value] : map) { }
```

### Functions
```cpp
// Basic function
int add(int a, int b) {
    return a + b;
}

// Default parameters
void greet(const std::string& name = "World") {
    std::cout << "Hello, " << name << std::endl;
}

// Function overloading
int max(int a, int b) { return a > b ? a : b; }
double max(double a, double b) { return a > b ? a : b; }

// Inline functions
inline int square(int x) { return x * x; }

// Lambda expressions
auto lambda = [](int x, int y) { return x + y; };
auto capture = [&]() { return captured_var; };

// Function templates
template<typename T>
T maximum(T a, T b) {
    return a > b ? a : b;
}
```

### Object-Oriented Programming
```cpp
class Animal {
private:
    std::string name;
    int age;
    
protected:
    std::string species;

public:
    // Constructor
    Animal(const std::string& n, int a) : name(n), age(a) {}
    
    // Destructor
    virtual ~Animal() = default;
    
    // Copy constructor
    Animal(const Animal& other) = default;
    
    // Move constructor
    Animal(Animal&& other) noexcept = default;
    
    // Getters
    const std::string& getName() const { return name; }
    int getAge() const { return age; }
    
    // Virtual method
    virtual void speak() const {
        std::cout << name << " makes a sound" << std::endl;
    }
};

// Inheritance
class Dog : public Animal {
private:
    std::string breed;
    
public:
    Dog(const std::string& name, int age, const std::string& breed)
        : Animal(name, age), breed(breed) {}
    
    void speak() const override {
        std::cout << getName() << " barks!" << std::endl;
    }
};

// Abstract class
class Shape {
public:
    virtual double area() const = 0;  // Pure virtual
    virtual ~Shape() = default;
};
```

### Memory Management
```cpp
// Raw pointers (avoid when possible)
int* ptr = new int(42);
delete ptr;

int* arr = new int[10];
delete[] arr;

// Smart pointers
#include <memory>

// Unique pointer (exclusive ownership)
std::unique_ptr<int> uptr = std::make_unique<int>(42);

// Shared pointer (shared ownership)
std::shared_ptr<int> sptr = std::make_shared<int>(42);
std::shared_ptr<int> sptr2 = sptr;  // Reference count: 2

// Weak pointer (non-owning reference)
std::weak_ptr<int> wptr = sptr;
if (auto locked = wptr.lock()) {
    // Use locked
}
```

### STL Containers
```cpp
#include <vector>
#include <map>
#include <set>
#include <unordered_map>
#include <queue>
#include <stack>

// Vector
std::vector<int> vec = {1, 2, 3};
vec.push_back(4);
vec.emplace_back(5);

// Map
std::map<std::string, int> map;
map["key"] = 1;
map.insert({"key2", 2});

// Unordered map (hash map)
std::unordered_map<std::string, int> hashMap;

// Set
std::set<int> set = {3, 1, 2};  // Ordered

// Queue and Stack
std::queue<int> queue;
std::stack<int> stack;

// Priority Queue
std::priority_queue<int> maxHeap;
std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;
```

### STL Algorithms
```cpp
#include <algorithm>
#include <numeric>

std::vector<int> v = {5, 2, 8, 1, 9};

// Sorting
std::sort(v.begin(), v.end());
std::sort(v.begin(), v.end(), std::greater<int>());

// Searching
auto it = std::find(v.begin(), v.end(), 8);
bool found = std::binary_search(v.begin(), v.end(), 8);

// Transform
std::transform(v.begin(), v.end(), v.begin(), [](int x) {
    return x * 2;
});

// Accumulate
int sum = std::accumulate(v.begin(), v.end(), 0);

// For each
std::for_each(v.begin(), v.end(), [](int x) {
    std::cout << x << " ";
});
```

### Modern C++ Features (C++11/14/17/20)

```cpp
// Structured bindings (C++17)
auto [x, y] = std::make_pair(1, 2);

// If with initializer (C++17)
if (auto it = map.find(key); it != map.end()) {
    // use it
}

// constexpr if (C++17)
template<typename T>
void process(T value) {
    if constexpr (std::is_integral_v<T>) {
        // Integer processing
    } else {
        // Other processing
    }
}

// std::optional (C++17)
std::optional<int> maybeValue = getValue();
if (maybeValue.has_value()) {
    int val = maybeValue.value();
}

// std::variant (C++17)
std::variant<int, std::string> var = "hello";

// Concepts (C++20)
template<typename T>
concept Numeric = std::is_arithmetic_v<T>;

template<Numeric T>
T add(T a, T b) { return a + b; }
```

### Multithreading
```cpp
#include <thread>
#include <mutex>
#include <future>

// Basic thread
std::thread t([]() {
    std::cout << "In thread" << std::endl;
});
t.join();

// Mutex
std::mutex mtx;
{
    std::lock_guard<std::mutex> lock(mtx);
    // Critical section
}

// Async and futures
std::future<int> future = std::async(std::launch::async, []() {
    return computeValue();
});
int result = future.get();
```

## Best Practices

1. Use **RAII** (Resource Acquisition Is Initialization)
2. Prefer **smart pointers** over raw pointers
3. Use **const** wherever possible
4. Prefer **references** over pointers for non-null params
5. Use **move semantics** for efficiency
6. Prefer **range-based for loops**
7. Enable **compiler warnings** (-Wall -Wextra)

## Resources
- cppreference.com
- C++ Core Guidelines
- Effective Modern C++ (book)
