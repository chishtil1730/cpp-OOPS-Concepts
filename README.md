# C++ Object-Oriented Programming Concepts

## Overloading Methods

**Definition:** Method overloading allows multiple functions with the same name but different parameters (number, type, or order) to coexist in the same class. The compiler determines which function to call based on the arguments provided.

**Key Concepts:**
- **Function Overloading**: Multiple functions with the same name but different signatures
- **Compile-time Polymorphism**: The appropriate function is selected at compile time
- **Return Type**: Not considered in overloading; parameter list must differ

**Code Example:**
```bash
$ cat overloading.cpp
#include <iostream>
using namespace std;

class Calculator {
public:
    int add(int a, int b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
    double add(double a, double b) { return a + b; }
};

int main() {
    Calculator calc;
    cout << calc.add(2, 3) << endl;      // 5
    cout << calc.add(1, 2, 3) << endl;   // 6
    cout << calc.add(2.5, 3.5) << endl;  // 6.0
    return 0;
}

$ g++ overloading.cpp -o overloading
$ ./overloading
5
6
6
```

---

## Objects as Parameters

**Definition:** Objects can be passed as parameters to member functions, allowing one object to access and manipulate data from another object of the same class type.

**Key Concepts:**
- **Pass by Value**: The object is copied when passed (default behavior)
- **Pass by Reference**: Use `&` to pass the object reference for efficiency
- **Member Access**: The passed object's public members can be accessed within the function

**Code Example:**
```bash
$ cat objects_params.cpp
#include <iostream>
using namespace std;

class Example {
public:
    int a;
    void add(Example E) {
        a = a + E.a;
    }
};

int main() {
    Example E1, E2;
    E1.a = 50;
    E2.a = 100;
    E2.add(E1);
    cout << E2.a << endl; // 150
    return 0;
}

$ g++ objects_params.cpp -o objects_params
$ ./objects_params
150
```

---

## Returning Objects

**Definition:** Functions can return objects, enabling complex operations where new objects are created and returned as results of computations involving other objects.

**Key Concepts:**
- **Return by Value**: Returns a copy of the object
- **Constructor**: Used to initialize temporary objects
- **Return Value Optimization (RVO)**: Compiler optimization that eliminates unnecessary copying

**Code Example:**
```bash
$ cat returning_objects.cpp
#include <iostream>
using namespace std;

class Point {
private:
    int x, y;
public:
    Point(int x1 = 0, int y1 = 0) { x = x1; y = y1; }
    Point addPoint(Point p) {
        Point temp;
        temp.x = x + p.x;
        temp.y = y + p.y;
        return temp;
    }
    void display() { cout << x << ", " << y << endl; }
};

int main() {
    Point p1(5,3), p2(12,6), p3;
    p3 = p1.addPoint(p2);
    p3.display(); // 17, 9
    return 0;
}

$ g++ returning_objects.cpp -o returning_objects
$ ./returning_objects
17, 9
```

---

## Friend Function

**Definition:** A friend function is a non-member function that has access to the private and protected members of a class. It's declared inside the class using the `friend` keyword.

**Key Concepts:**
- **`friend` keyword**: Grants external function access to private members
- **Not a member**: Friend functions are not class members, so they don't have `this` pointer
- **Access privileges**: Can access private and protected data members

**Code Example:**
```bash
$ cat friend_function.cpp
#include <iostream>
using namespace std;

class Box {
    double width;
public:
    friend void printWidth(Box box);
    void setWidth(double wid) { width = wid; }
};

void printWidth(Box box) {
    cout << "Width of box : " << box.width << endl;
}

int main() {
    Box box;
    box.setWidth(10.0);
    printWidth(box);
    return 0;
}

$ g++ friend_function.cpp -o friend_function
$ ./friend_function
Width of box : 10
```

---

## Static Class Features

**Definition:** Static members belong to the class itself rather than to any specific object instance. They are shared among all objects of the class and can be accessed without creating an instance.

**Key Concepts:**
- **`static` keyword**: Declares class-level members
- **Static variables**: Must be defined outside the class
- **Static functions**: Can only access static members
- **Scope resolution operator (`::`)**: Used to access static members

**Code Example:**
```bash
$ cat static_features.cpp
#include <iostream>
using namespace std;

class Example {
public:
    static int a;
    static void func(int b) {
        cout << "Static func: " << b << endl;
    }
};
int Example::a = 28;

int main() {
    Example::func(8);
    cout << Example::a << endl; // 28
    return 0;
}

$ g++ static_features.cpp -o static_features
$ ./static_features
Static func: 8
28
```

---

## Nested & Inner Classes

**Definition:** A nested class is a class defined within another class. The inner class can access members of the outer class, and it helps in logical grouping of classes that are only used in one place.

**Key Concepts:**
- **Nested class**: Class defined inside another class
- **Scope resolution**: Use `OuterClass::InnerClass` to access from outside
- **Encapsulation**: Inner classes can be private to hide implementation details

**Code Example:**
```bash
$ cat nested_classes.cpp
#include <iostream>
using namespace std;

class Outer {
public:
    class Inner {
        int val;
    public:
        void set(int v) { val = v; }
        void show() { cout << val << endl; }
    };
};

int main() {
    Outer::Inner obj;
    obj.set(42);
    obj.show(); // 42
    return 0;
}

$ g++ nested_classes.cpp -o nested_classes
$ ./nested_classes
42
```

---

## Inheritance: Basics

**Definition:** Inheritance is a mechanism where a new class (derived class) acquires properties and behaviors of an existing class (base class). It promotes code reusability and establishes a relationship between classes.

**Key Concepts:**
- **Base class**: The parent class being inherited from
- **Derived class**: The child class that inherits
- **Access specifier**: `public`, `protected`, or `private` inheritance
- **Code reusability**: Derived class inherits all public and protected members

**Code Example:**
```bash
$ cat inheritance_basics.cpp
#include <iostream>
using namespace std;

class Animal {
public:
    void eat() { cout << "I can eat!" << endl; }
    void sleep() { cout << "I can sleep!" << endl; }
};

class Dog : public Animal {
public:
    void bark() { cout << "Woof!" << endl; }
};

int main() {
    Dog d;
    d.eat(); d.sleep(); d.bark();
    return 0;
}

$ g++ inheritance_basics.cpp -o inheritance_basics
$ ./inheritance_basics
I can eat!
I can sleep!
Woof!
```

---

## Types of Inheritance

**Definition:** C++ supports various types of inheritance patterns that define how classes can inherit from one or more base classes.

**Key Concepts:**
- **Single Inheritance**: One derived class inherits from one base class
- **Multiple Inheritance**: One derived class inherits from multiple base classes
- **Multilevel Inheritance**: A derived class inherits from another derived class
- **Hierarchical Inheritance**: Multiple classes inherit from a single base class
- **Hybrid Inheritance**: Combination of multiple inheritance types

**Code Example:**
```bash
$ cat inheritance_types.cpp
// Single Inheritance
class A {};
class B : public A {};

// Multiple Inheritance
class C {};
class D : public B, public C {};

// Multilevel Inheritance
class E : public D {};

$ # This is a header-only demonstration showing syntax
```

---

## Method Overriding & Polymorphism

**Definition:** Method overriding allows a derived class to provide a specific implementation of a method already defined in its base class. Combined with virtual functions, it enables runtime polymorphism.

**Key Concepts:**
- **`virtual` keyword**: Enables dynamic binding for base class methods
- **`override` keyword**: (C++11) Explicitly indicates method overriding
- **Runtime polymorphism**: Function to execute is determined at runtime
- **Base class pointer**: Can point to derived class objects

**Code Example:**
```bash
$ cat polymorphism.cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show() { cout << "Base" << endl; }
};
class Derived : public Base {
public:
    void show() override { cout << "Derived" << endl; }
};

int main() {
    Base* ptr = new Derived();
    ptr->show(); // Derived
    delete ptr;
    return 0;
}

$ g++ polymorphism.cpp -o polymorphism
$ ./polymorphism
Derived
```

---

## Function Template

**Definition:** Function templates allow you to create generic functions that can work with different data types without rewriting the function for each type. The compiler generates the appropriate function version at compile time.

**Key Concepts:**
- **`template` keyword**: Declares a template
- **Template parameter (`typename` or `class`)**: Represents a generic type
- **Template instantiation**: Compiler creates specific versions for each type used
- **Type safety**: Maintains type checking while being generic

**Code Example:**
```bash
$ cat function_template.cpp
#include <iostream>
using namespace std;

template <typename T>
T add(T a, T b) { return a + b; }

int main() {
    cout << add<int>(3,4) << endl;    // 7
    cout << add<double>(2.5,3.6) << endl; // 6.1
    return 0;
}

$ g++ function_template.cpp -o function_template
$ ./function_template
7
6.1
```

---

## Class Template

**Definition:** Class templates enable creation of generic classes that can operate with different data types. The class definition is parameterized with template parameters that are specified when creating objects.

**Key Concepts:**
- **`template <class T>` or `template <typename T>`**: Class template declaration
- **Generic data members**: Can use template parameters for member variables
- **Template instantiation**: Must specify type when creating objects
- **Code reusability**: One class definition works for multiple types

**Code Example:**
```bash
$ cat class_template.cpp
#include <iostream>
using namespace std;

template <class T>
class TemplateClass {
    T data;
public:
    TemplateClass(T val) : data(val) {}
    void show() { cout << data << endl; }
};

int main() {
    TemplateClass<int> obj1(42);
    TemplateClass<double> obj2(3.14);
    obj1.show(); // 42
    obj2.show(); // 3.14
    return 0;
}

$ g++ class_template.cpp -o class_template
$ ./class_template
42
3.14
```
