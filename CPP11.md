# C++11

## 1. auto

**Before C++11:**

```cpp
std::vector<std::string>::iterator it = names.begin();
```

**In C++11:**

```cpp
auto it = names.begin();
```

**Another example:**

```cpp
auto x = 10;        // int
auto y = 3.14;      // double
auto z = "Hello";   // const char*
```

```cpp
auto doubleValue = [](int x) // Just for lambdas not for functions
{
    return x * 2;
};
```

---

## 2. Range-based for

**Before C++11:**

```cpp
for (int i = 0; i < numbers.size(); i++)
{
    std::cout << numbers[i];
}
```

**In C++11:**

```cpp
for (auto n : numbers)
{
    std::cout << n;
}
```

**If you want to change value:**

```cpp
for (auto& n : numbers)
{
    n *= 2;
}
```

---

## 3. nullptr

**Before C++11:**

```cpp
int* ptr = NULL;
// OR
int* ptr = 0;
```

**In C++11:**

```cpp
int* ptr = nullptr;
```

---

## 4. Lambda Expression

**Before C++11:**

```cpp
bool compare(int a, int b)
{
    return a < b;
}

sort(v.begin(), v.end(), compare);
```

**In C++11:**

```cpp
sort(v.begin(), v.end(),
     [](int a, int b)
     {
         return a < b;
     });
```

**Capturing outer variables:**

```cpp
int limit = 10;

auto f = [limit](int x)
{
    return x > limit;
};
```

---

## 5. enum class

**Before C++11:**

```cpp
enum Color
{
    Red,
    Green
};
```

**In C++11:**

```cpp
enum class Color
{
    Red,
    Green
};

enum class ErrorCode : uint8_t // Strongly Typed Enum Underlying Type
{
    OK,
    FAIL
};
```

**Usage:**

```cpp
Color c = Color::Red;
```

**Pros:**

- Type Safe
- Separate Scope
- Prevents Type Interventions

---

## 6. Smart Pointer

**Before C++11:**

```cpp
Person* p = new Person();
// ...
delete p;
```

**In C++11:**

```cpp
auto p = std::make_unique<Person>();
// OR
auto p = std::make_shared<Person>();
```

**Pros:**

- Automatic Deletion
- Prevents Memory Leak

---

## 7. Move Semantics

**Before C++11:**

```cpp
std::string a = "Hello";
std::string b = a;  // whole string will be copied
```

**In C++11:**

```cpp
std::string b = std::move(a);  // Ownership transferred, not just a copy
```

---

## 8. Rvalue Reference

**Example:**

```cpp
void foo(std::string&& str)
{
}
```

---

## 9. Constructor Delegation

**Before C++11:**

```cpp
class A
{
public:
    A()
    {
        x = 0;
    }

    A(int n)
    {
        x = n;
    }

private:
    int x;
};
```

**In C++11:**

```cpp
class A
{
public:
    A()
        : A(0)
    {
    }

    A(int n)
    {
        x = n;
    }

private:
    int x;
};
```

---

## 10. Initializer List

**Before C++11:**

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);
v.push_back(3);
```

**In C++11:**

```cpp
std::vector<int> v = { 1, 2, 3 };
// OR
int a[] = { 1, 2, 3 };
```

---

## 11. Uniform Initialization

Everything can be initialized with `{}`.

```cpp
int a{10};
double b{3.5};
Person p{"Ali", 25};
```

---

## 12. override

**Before C++11:**

```cpp
class Base
{
public:
    virtual void print();
};

class Child : public Base
{
public:
    void pritn();  // it is a typo, but compiler will not catch it! (it will be compiled with no error)
};
```

**In C++11:**

```cpp
void print() override;   // compiles with no error

void pritn() override;   // compiler returns error
```

---

## 13. final

Prevents override:

```cpp
virtual void print() final;
```

Or prevents inheritation:

```cpp
class A final
{
};
```

---

## 14. constexpr

**Before C++11:**

```cpp
const int N = 10;
```

**In C++11:**

```cpp
constexpr int N = 10;  // compile-time constant
```

**Example:**

```cpp
const int a = 10;          // a is read-only, but also a compile-time constant (not always a compile-time constant)
constexpr int b = 10;      // b is definitely a compile-time constant
// Both work for array sizes:
int arr1[a];  // OK (a is compile-time constant)
int arr2[b];  // OK
// BUT:
int x = 5;
const int c = x;           // OK: c is read-only at runtime
constexpr int d = x;       // ERROR: x is not compile-time constant
int arr3[c];               // ERROR: c is NOT compile-time constant!
                           // Because c's value comes from runtime x
```

---

## 15. static_assert

**Before C++11:** There was no way to check for custom errors while compiling the code.

**In C++11:**

```cpp
static_assert(sizeof(int) == 4, "int must be 4 bytes");
```

If the condition does not meet, compilation will be stopped.

---

## 16. using

**Before C++11:**

```cpp
typedef std::vector<int> IntVector;
```

**In C++11:**

```cpp
using IntVector = std::vector<int>;
```

Both work exactly the same.

---

## 17. Thread Library

First multi-thread programming library for C++:

```cpp
void work()
{
}

int main()
{
    std::thread t(work);
    t.join();
}
```

---

## 18. mutex

```cpp
std::mutex m;
```

For controlling the threads accessing same sources simultaneously

---

## 19. chrono

For getting real time since starting the code:

```cpp
auto start = std::chrono::steady_clock::now();
```

---

## 20. Random Library

**Before C++11:**

```cpp
rand();
```

**In C++11:**

```cpp
std::mt19937 gen; // more standard and accurate random number
```

---

## 21. Unordered Map

**Before C++11:**

```cpp
std::map<int, std::string> m; // based on "Red-Black Tree"

m[5] = "Five";
m[1] = "One";
m[8] = "Eight";
m[3] = "Three";
```

**Pros:**

- All keys are sorted
Cons:
- Complexity of searching, inserting and deletion is equal to O(log n)

**In C++11:**

```cpp
std::unordered_map<int, std::string> // based on "Hash Table"

m[5] = "Five";
m[1] = "One";
m[8] = "Eight";
m[3] = "Three";
```

**Pros:**

- Most of the time, complexity of searching, inserting and deletion is equal to O(1) and in the worst case is O(n). So it is faster for larger maps
Cons:
- Keys are not sorted
- Takes more memory than "map"

---

## 22. Tuple

```cpp
std::tuple<int, double, std::string> t1 = std::make_tuple(42, 3.14, "hello");
//OR
std::tuple<int, double, std::string> t1(42, 3.14, "hello");
//OR
auto t1 = std::make_tuple(42, 3.14, "hello");

int i = std::get<0>(t1);        // 42
double d = std::get<1>(t1);     // 3.14
std::string s = std::get<2>(t1); // "hello"
```

---

## 23. Forward List

```cpp
std::forward_list<int> fl = {1, 2, 3, 4, 5, 3, 6};
fl.pop_front();  // fl: 2, 3, 4, 5, 3, 6
fl.remove(3);  // fl: 2, 4, 5, 6
```

---

## 24. Default/Delete Function

```cpp
class A
{
public:
    A() = default;
    A(const A&) = delete;
};

A a1;           // OK: default constructor works
A a2(a1);       // ERROR: copy constructor is deleted!
A a3 = a1;      // ERROR: copy constructor is deleted!
a1 = a2;        // Note: assignment still works! (more on this later)
```

---
