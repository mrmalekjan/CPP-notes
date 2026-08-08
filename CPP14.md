# C++14

## 1. Improved auto

**In C++11:**

```cpp
auto doubleValue = [](int x) // Could not use auto in input
{
    return x * 2;
};
```

**In C++14:**

```cpp
auto doubleValue = [](double x)
{
    return x * 2;
};
```

---

## 2. Lambda Init-Capture

**In C++11:**

```cpp
int x = 10;

auto f = [x]() // x should had been defined before
{
    return x * 2;
};
```

**In C++14:**

```cpp
auto f = [x = 10]()
{
    return x * 2;
};
```

---

## 3. Return Type Deduction

**In C++11:**

```cpp
int add(int a, int b)
{
    return a + b;
}
```

**In C++14:**

```cpp
auto add(int a, int b)
{
    return a + b; //OK
     // Compiler figures out the output type automatically
}
```

```cpp
template <typename T, typename U>
auto add(T a, U b)
{
    return a + b; //OK
}
```

```cpp
auto test(bool condition)
{
    if (condition)
        return 10; // ERROR: not a single type output

    return 3.14; // ERROR: not a single type output
}
```

## 4. Variable Templates

```cpp
template <typename T> // Now in C++14 it can be written for variables too.
constexpr T zero = T(0);

int x = zero<int>;
double y = zero<double>;
```

## 5. Relaxed constexpr

In C++11 it was not allowed to have local variables, loops, if, switch, etc in constexpr functions. but in C++14 it is possible:

```cpp
constexpr int factorial(int n)
{
    int result = 1; //OK in C++14

    for (int i = 2; i <= n; ++i) //OK in C++14
        result *= i;

    return result;
}
```

## 6. Binary Literals

**Before C++14:**

```cpp
int a = 42;        // decimal // OK
int b = 0b101010;  // binary // OK
int c = 052;       // octal // OK
int d = 0x2A;      // hexadecimal // OK
```

**In C++14:**

```cpp
int a = 42;        // decimal // OK
int b = 0b101010;  // binary // Not OK
int c = 052;       // octal // OK
int d = 0x2A;      // hexadecimal // OK
```

## 7. Digit Separators

```cpp
int x = 1'000'000;
uint32_t value = 0xFF'00'AA'55;
long long n = 1'234'567'890;
```

## 8. Default Member Initializer with Aggregate

```cpp
struct Point
{
    int x = 0;
    int y = 0;
};

Point p; // OK in C++14 and C++11
Point p{10, 20}; // OK in C++14 and not OK in C++11
Point p{10}; // OK in C++14 and not OK in C++11
```
