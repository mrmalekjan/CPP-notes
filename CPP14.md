# C++14

## 1. auto

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
