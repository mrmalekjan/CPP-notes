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
