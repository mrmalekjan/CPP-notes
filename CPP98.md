# C++98

## 1. Classes

```cpp
class Person
{
private: //Encapsulation
 int id;
protected: //Encapsulation
public:
 Person(int id): id(id) // Constructor
 {
 }
 ~Person() // Destructor
 {
 }
    void SayHello()
    {
        std::cout << "Hello";
    }
};
```

---

## 2. Overloading

```cpp
void Print(int x);
void Print(double x);
```

---

## 3. Operator Overloading

```cpp
class Complex
{
public:
    int real;
    int imag;

    Complex(int r, int i): real(r), imag(i)
    {
    }

    Complex operator+(Complex other)
    {
        return Complex(
            real + other.real,
            imag + other.imag
        );
    }
};

void main()
{
    Complex a(2,3);
    Complex b(5,4);
    Complex c = a + b;
}
```

---

## 4. Inheritance

```cpp
class Animal
{
};

class Dog : public Animal
{
};
```

## 5. Multiple Inheritance

```cpp
class A {};
class B {};

class C : public A, public B
{
};
```

---

## 6. Virtual Function

```cpp
class Animal
{
public:
    virtual void Speak()
    {
        std::cout << "Animal\n";
    }
};

class Dog : public Animal
{
public:
    void Speak() // new definition for Speak is optional
    {
        std::cout << "Dog\n";
    }
};
```

---

## 7. Pure Virtual Function

```cpp
class Animal
{
public:
    virtual void Speak() = 0; // with this function, Animal is called an Abstract Class
};

class Dog : public Animal
{
public:
    void Speak() // new definition for Speak is mandatory
    {
        std::cout << "Dog\n";
    }
};
```

---

## 8. Runtime Polymorphism

```cpp
class Cat : public Animal
{
public:
    void Speak()
    {
        std::cout << "Meow\n";
    }
};

class Dog : public Animal
{
public:
    void Speak()
    {
        std::cout << "Bark\n";
    }
};

int main()
{
    Dog dog;
    Cat cat;

    Animal* a;

    a = &dog;
    a->Speak(); //"Bark\n"

    a = &cat;
    a->Speak(); //"Meow\n"
}
```

---

## 9. Virtual Destructor

```cpp
class Base
{
public:
    virtual ~Base()
    {
        std::cout << "Base Destructor\n";
    }
};

class Derived : public Base
{
public:
    ~Derived()
    {
        std::cout << "Derived Destructor\n";
    }
};

void main()
{
 Base* ptr = new Derived();
 delete ptr; // if ~Base was not virtual, only Base destructor would be called and ~Derived would not. So Derived would remain undeleted
}

```

---

## 10. Friend

```cpp
class BankAccount
{
private:
    int balance;
public:
    BankAccount(int b)
    {
        balance = b;
    }
    friend void PrintBalance(const BankAccount& account); // now PrintBalance can access all private and protected members of BankAccount
};

void PrintBalance(const BankAccount& account)
{
    std::cout << account.balance << std::endl;
}
```

---

## 11. static members

```cpp
class Car
{
public:
    static int count; // it is the same for all objects from the class
    static const int maximum_count = 100;

    Car()
    {
        count++;
    }
};

int main()
{
 int Car::count = 0;
    Car a;
    Car b;
    Car c;

    std::cout << Car::count; // output: 3
    std::cout << Car::maximum_count // output: 100
}
```

---

## 12 const Memeber Function

```cpp
class Person
{
private:

public:
    int age;

    Person(int a)
        : age(a)
    {
    }

    int GetAge() const // this "const" means that GetAge function can not change any parameter from the class
    {
        return age;
    }

    void SetAge(int a)
    {
        age = a;
    }
};
```

```cpp
const Person person(25); // We can only use GetAge function and not SetAge, because person object is define as constant
int age = person.GetAge();   // OK
person.SetAge(30);           // ERROR
```

---

## 13. const Object

```cpp
Person a(10);
Person b(10);

const Person p1(10);
Person* const p2 = &a;
const Person* p3 = &a;

p2 = &b; // ERROR
p3 = &b; // OK

p1.age = 3; // ERROR
p2->age = 3; // OK
p3->age = 3; // ERROR

p1.GetAge(); // OK
p2->GetAge(); // OK
p3->GetAge(); // OK

p1.SetAge(30); // ERROR
p2->SetAge(30); // OK
p3->SetAge(30); // ERROR
```

---

## 14. Reference

```cpp
int x = 10;

int* p = &x;
int& r = x;

//Changing Value
*p = 20;
std::cout << x;  // 20
r = 40;
std::cout << x;  // 40
```

```cpp
void Decrease(int x) // x is a copy of the input
{
    x-= 100;
}
void Increase(int& x) // x is the actual the input
{
    x += 100;
}

int a = 200;
Increase(a);
std::cout << a; // 300
Decrease(a);
std::cout << a; // 300

```

```cpp
int x = 10;
int y = 20;

int* p = &x;
int& r = x;

//Changing Variable Reference
p = &y; // Now p points at y
std::cout << x; // 10
r = y; // r does not point at y. It is still pointing at x
std::cout << x; // 20
```

A useful case:

```cpp
void Print(const std::string& s)
{
    std::cout << s; // It does not need the input string to be copied. It is much more efficient if the input is a large string.
}
```

---

## 15. Pointer Function

```cpp
int Add(int x1, int x2)
{
    return x1+x2;
}
int Subtract(int x1, int x2)
{
    return x1 - x2;
}

int (*ptr)(int, int) = Add;
//OR
int (*ptr)(int, int) = &Add;

int result = ptr(1, 2); // 3

int (*operation)(int, int);
operation = Add;
result = operation(1,2); //3
operation = Subtract;
result = operation(2,1); //1

```

---

## 16. namespace

```cpp
namespace LibraryA
{
    void print()
    {
        std::cout << "Hello"
    }
    //...
}

namespace LibraryB
{
    void print() // No inference with the other "print" function
    {
        std::cout << "Goodbye";
    }
    //...
}

int main()
{
    LibraryA::print(); //"Hello"
    LibraryB::print(); //"Goodbye"
}
```

```cpp
int main()
{
    using namespace LibraryA;
    //OR
    using LibraryA::print;

    print(); //"Hello"
}
```

---

## 16. template

```cpp
template<typename T>
T Max(T a, T b)
{
    return a > b ? a : b;
}

int a = Max(10, 20); // OK
double b = Max(3.14, 2.71); // OK
char c = Max('a', 'z'); // OK
```

```cpp
template<typename T>
class Box
{
public:
    T value;
};

Box<int> box;
```

```cpp
template<typename T>
class Box
{
public:
    void Print()
    {
        std::cout << "Generic Box";
    }
};

template<>
class Box<bool> // We can write a specific class "Box" for a specific typename (for example in this case, bool)
{
public:
    void Print()
    {
        std::cout << "Boolean Box";
    }
};

Box<int> a;
a.Print();        // Generic Box

Box<bool> b;
b.Print();        // Boolean Box
```

```cpp
class Printer
{
public:
    template<typename T>
    void Print(T value)
    {
        std::cout << value << std::endl;
    }
};

int main()
{
    Printer p;

    p.Print(10);
    p.Print(3.14);
    p.Print("Hello");
    //OR
    p.Print<int>(10);
    p.Print<float>(3.14);
    p.Print<std::string>("Hello");

    return 0;
}
```

```cpp
template<typename T, typename U>
class Pair
{
public:
    void Print()
    {
        std::cout << "General";
    }
};

template<typename T>
class Pair<T, T>
{
public:
    void Print()
    {
        std::cout << "Same types";
    }
};

Pair<int, double> a; // "General"
Pair<int, int> b; // "Same types"
Pair<float, float> c; // "Same types"
```

```cpp
template<typename T>
class A
{
public:
    void Print()
    {
        std::cout << "General";
    }
};

template<typename T>
class A<T*> // It says if the typename was a pointer, class "A" is defined as below
{
public:
    void Print()
    {
        std::cout << "Pointer";
    }
};

A<int> a;
A<int*> b;
A<double*> c;

a.Print();   // General
b.Print();   // Pointer
c.Print();   // Pointer
```

---

## 17. try & catch

```cpp
int Divide(int a, int b)
{
    if (b == 0)
        throw "Division by zero";
    return a / b;
}

int main()
{
    try
    {
        int result = Divide(10, 0);
    }
    catch (const char* message)
    {
        std::cout << "Error: " << message; // comes here!
    }
    catch (int x)
    {
        std::cout << "Integer exception";
    }
    catch(...)
    {
        std::cout << "Any kind of exception";
    }
    return 0;

    try
    {
        throw 10; // The input of catch
    }
    catch (const char* message)
    {
        std::cout << "Error: " << message;
    }
    catch (int x)
    {
        std::cout << "Integer exception"; // comes here!
    }
    catch(...)
    {
        std::cout << "Any kind of exception";
    }
}
```

## 18. RTTI

```cpp
class Animal
{
public:
    virtual ~Animal() {}
};

class Dog : public Animal
{
};

class Cat : public Animal
{
};

int main()
{
    Animal* animal = new Dog();
    if (typeid(*animal) == typeid(Dog))
    {
        std::cout << "It is a Dog";
    }
    return 0;
}
```

## 19. enum

```cpp
enum Color
{
    Red,
    Green,
    Blue
};
```

## 20. explicit

```cpp
class NumberOld
{
public:
    Number(int x)
    {
    }
};

class NumberNew
{
public:
    explicit Number(int x)
    {
    }
};

int main()
{
    NumberOld n = 10;   // OK
    Print(10);       // OK
    NumberOld n(10);        // OK
    NumberOld n = NumberOld(10); // OK
    Print(NumberOld(10));  // OK

    NumberNew n = 10;   // ERROR
    Print(10);       // ERROR
    NumberNew n(10);        // OK
    NumberNew n = NumberNew(10); // OK
    Print(NumberNew(10));  // OK
}
```

## 21. mutable

```cpp
class CounterOld
{
private:
    int count;
public:
    void Increment() const
    {
        count++;   // ERROR
    }
};

class CounterNew
{
private:
    mutable int count;
public:
    void Increment() const
    {
        count++;   // OK: mutable neutralizes the const function
    }
};
```

## 22. inline

If a function is defined (and not just declared), we should define it "inline".

```cpp
inline int Square(int x)
{
    return x * x;
}
```

Note: any function in a class is considered an inline function by compiler.

## 23. Default Arguments

```cpp
void Print(int x = 10);
```

## 24. Function Objects

```cpp
struct Add
{
    int operator()(int a, int b)
    {
        return a + b;
    }
};

int main()
{
    int result = add(10, 20);
    //OR
    int result = add.operator()(10, 20);
}
```

## 25. Nested Class

```cpp
class Outer
{
public:
    class Inner
    {
    public:
        void Hello()
        {
            std::cout << "Hello";
        }
    };
};

int main()
{
    Outer::Inner obj;
    obj.Hello();
}
```

## 26. Nested namespace

```cpp
namespace A
{
    namespace B
    {
    }
}
```

## 27. Cast Operators

```cpp
float x = 10.5;
double y = static_cast<double>(x);
//OR
double y = (double)x; // like normal casting in C

class Base {};
class Derived : public Base {};
Derived d;
Base* b = static_cast<Base*>(&d); // an upcast
```

```cpp
class Base
{
public:
    virtual ~Base() {}
};

class Derived : public Base
{
public:
    void Hello()
    {
        std::cout << "Hello";
    }
};

int main()
{
    Base* base = new Derived;
    Derived* derived = dynamic_cast<Derived*>(base); // because "base" is actually a Derived class

    Base* base = new Base;
    Derived* derived = dynamic_cast<Derived*>(base); // Wrong! (no error but pointer will be null)
    Derived* derived = dynamic_cast<Derived*>(base); // Wrong! (no error, but undefined behavior)
}

```

The difference between static and dynamic cast is that in dynamic cast compiler does a runtime check, but in static cast there is non, but it is faster

```cpp
const int x = 10;
int* p = const_cast<int*>(&x);
*p = 20;       // Wrong! (undefined behavior)
```

```cpp
int x = 10;
const int* p = &x;
int* q = const_cast<int*>(p);
*q = 20;       // OK
```

```cpp
uint32_t x = 0x12345678;
uint8_t* p = reinterpret_cast<uint8_t*>(&x);
//OR
uint8_t* p = (uint8_t *)&x;
```

## 28. new & delete

```cpp
int x = new int(42);
delete x;

int* array = new int[10];
array[0] = 100;
array[1] = 200;
delete[] array;
```

```cpp
class Motor
{
public:
    Motor()
    {
        std::cout << "Motor created\n";
    }

    ~Motor()
    {
        std::cout << "Motor destroyed\n";
    }
};

int main()
{
    Motor* motor = new Motor; // Constructor executes and dynamic memory is taken for Motor size class
    delete motor; // Destructor exectues and memory taken for motor is freed

    Motor* m = (Motor*)malloc(sizeof(Motor)); // constructor does not execute, but memory is taken of Motor size class
    free(motor); // Destructor does not exectue, but memory taken for motor is freed
}
```

Note: only use new & delete with pointers.

## 29. Anonymous union

```cpp
union Data // regular union
{
    int i;
    float f;
};

Data data;
data.i = 10;
```

```cpp
union // anonymous union
{
    int i;
    float f;
};

i = 10;
```

## 30. Bit-field

```cpp
struct S
{
    uint8_t x : 3; // only takes 3 bit space for x
    uint32_t y : 10; // only takes 10 bit space for x
};
```

## 31. Covariant Return Type

```cpp
class Animal
{
public:
    virtual Animal* Clone()
    {
        return new Animal();
    }
};

class Dog : public Animal
{
public:
    virtual Dog* Clone()
    {
        return new Dog();
    }
};
```

## 32. Declaration in if/while

```cpp
if (Widget* widget = GetWidget())
{
    widget->Run();
}

if (int x = Foo())
{
    std::cout << x;
}
```
