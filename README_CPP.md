## Table of contents

<table><tr><td>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [🌍 Summary of C++ and Programming World](#-summary-of-c-and-programming-world)
  - [✨ Object-Oriented Programming](#-object-oriented-programming)
    - [Encapsulation](#encapsulation)
    - [Data Hiding](#data-hiding)
    - [Inheritance](#inheritance)
    - [Polymorphism](#polymorphism)
  - [⌨️ Syntax and Structure](#-syntax-and-structure)
    - [Weak vs Strong typing](#weak-vs-strong-typing)
    - [Semicolons in C++](#semicolons-in-c)
    - [Curly Braces in C++](#curly-braces-in-c)
    - [Comments in C++](#comments-in-c)
      - [Single-line comments](#single-line-comments)
      - [Multi-line comments](#multi-line-comments)
    - [Headers vs source files](#headers-vs-source-files)
    - [Includes](#includes)
  - [🔥 Standard Library](#-standard-library)
  - [🔢 Data types](#-data-types)
    - [Char](#char)
    - [Booleans](#booleans)
    - [Integers](#integers)
      - [Modifiers](#modifiers)
    - [Floating points (floats and doubles)](#floating-points-floats-and-doubles)
  - [🙋‍♂️ Typedefs](#-typedefs)
  - [🍂 Members](#-members)
    - [Variables](#variables)
      - [Assignments](#assignments)
    - [Functions](#functions)
  - [🧬 Classes](#-classes)
    - [Structs](#structs)
  - [💔 Accessibility](#-accessibility)
  - [🤔 If-statements](#-if-statements)
  - [🔣 Comparisons and Boolean Operators](#-comparisons-and-boolean-operators)
    - [❓ Conditional Expressions (Ternary operator)](#-conditional-expressions-ternary-operator)
  - [🔀 Switches](#-switches)
  - [🔁 Loops](#-loops)
    - [♾️ While Loop](#-while-loop)
    - [🔃 Do-While Loop](#-do-while-loop)
    - [🔂 For Loop](#-for-loop)
    - [🗂️ Foreach Loop](#-foreach-loop)
  - [🦋 Immutable vs Mutable](#-immutable-vs-mutable)
    - [Mutable](#mutable)
    - [Immutable](#immutable)
  - [🪝 Try Catch](#-try-catch)
  - [🪞 Casting](#-casting)
    - [Static casting](#static-casting)
    - [Const casting](#const-casting)
    - [Dynamic casting](#dynamic-casting)
    - [Reinterpret Casting](#reinterpret-casting)
  - [🛼 Inlining](#-inlining)
  - [📇 Namespace](#-namespace)
  - [🌐 Static members](#-static-members)
  - [`auto` keyword](#auto-keyword)
  - [🌱 Polymorphism (In Depth)](#-polymorphism-in-depth)
      - [Operator Overloading](#operator-overloading)
      - [Function Overloading](#function-overloading)
      - [Virtual functions](#virtual-functions)
  - [🧙‍♂️ Generic Programming](#-generic-programming)
  - [😵 Recursion](#-recursion)
  - [⚙️ Linker](#-linker)
    - [Static Library](#static-library)
    - [Dynamic Library](#dynamic-library)
  - [🫀 Lambda](#-lambda)
  - [🦾 Binary code](#-binary-code)
    - [Logic gates](#logic-gates)
    - [Hexadecimal](#hexadecimal)
    - [Bitwise Operators](#bitwise-operators)
  - [💥 Stack vs Heap](#-stack-vs-heap)
    - [Stack Memory Allocation](#stack-memory-allocation)
    - [Heap Memory Allocation](#heap-memory-allocation)
  - [Design Patterns And Principles](#design-patterns-and-principles)
    - [SOLID Principle](#solid-principle)
    - [KISS (Keep It Simple, Stupid)](#kiss-keep-it-simple-stupid)
    - [Singleton](#singleton)
    - [Observer](#observer)
    - [Factory](#factory)
    - [Strategy](#strategy)
    - [MVC (Model-View-Controller)](#mvc-model-view-controller)
  - [💯 Structures](#-structures)
    - [Array](#array)
    - [List](#list)
    - [Queue](#queue)
    - [Hash Set (Lookup table)](#hash-set-lookup-table)
    - [Dictionary (Map)](#dictionary-map)
    - [Linked List](#linked-list)
  - [⏰ Time Complexity](#-time-complexity)
    - [Constant](#constant)
    - [Logarithmic](#logarithmic)
    - [Linear](#linear)
    - [Quadratic](#quadratic)
    - [Exponential](#exponential)
    - [Factorial](#factorial)
- [📍 Footnotes](#-footnotes)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

</td></tr></table>

<!-- prettier-ignore-start -->

## 🌍 Summary of C++ and Programming World

### ✨ Object-Oriented Programming

<details open>
  <summary>Click to expand</summary>

Object-Oriented Programming (**OOP**) organizes code around **objects** — bundles of data (attributes) and the functions that work with that data (methods). Think of a game character: it has properties like `Health`, `Position`, and `Speed`, plus behaviors like `TakeDamage()`, `Move()`, and `Attack()`. OOP keeps all of this together in one place instead of scattering it across unrelated functions.

#### Encapsulation

Encapsulation bundles data (variables) and the functions that operate on that data into one unit — a class. Think of it like a car dashboard: you interact with buttons and gauges (the public interface), but you don't need to know how the engine's fuel injection system works internally. The engine encapsulates its complexity behind a simple interface.

In code, this means you put your data as `private` and expose only the functions that should be used to modify it. This prevents other code from putting your object into an invalid state.

#### Data Hiding

Data hiding is a direct consequence of encapsulation — it means keeping your class's internal data private so external code can't read or modify it directly. Instead, they must go through your public methods, which can validate input and enforce rules.

Example: If a `Health` variable were public, someone could set it to `-9999` or `1000000`. By making it private and providing `TakeDamage(amount)` and `Heal(amount)` functions, you control what values are valid and can trigger side effects (like playing a damage animation) every time health changes.

#### Inheritance

![Inheritance](static/img/Inheritance.png)

Inheritance lets a new class (derived class) reuse code from an existing class (base class). Think of it like family traits: a child inherits eye color and hair type from their parents, but can also have unique features of their own.

In code, you might have a base class `ACharacter` with common properties like `Health`, `Speed`, and `Position`. Then `APawn`, `APlayerCharacter`, and `ANPC` all inherit those properties automatically — you don't rewrite them. Each derived class can add its own stuff (like `Weapon` for `APlayerCharacter`) or override existing behavior (like how `ANPC` handles damage differently from `APlayerCharacter`).

In Unreal Engine, inheritance is everywhere: every Actor, Component, and GameMode in your project inherits from a base class provided by the engine.

#### Polymorphism

![Polymorphism](static/img/Polymorphism.png)

Polymorphism lets you treat derived class objects through a common base class pointer or reference. Derived classes override base methods, and the correct version is called at runtime (via `virtual` functions).

Think of a universal remote: it has buttons labeled "Volume Up," "Volume Down," and "Power." These buttons work on your TV, stereo, and soundbar — even though each device implements those buttons differently. You don't need a different remote for each device. That's polymorphism: one interface (`Remote`), many implementations (`TV`, `Stereo`, `Soundbar`).

In Unreal, this is how you can loop through all Actors in a level and call `Tick()` on each one without knowing their specific types — they all inherit from `AActor`, which has a virtual `Tick()` function.

</details>

### ⌨️ Syntax and Structure

Syntax refers to the set of rules that define the structure, format and grammar of a programming language. It dictates how statements and expressions should be written to form valid code.

C++ follows a structured syntax that includes elements such as keywords[^1], identifiers, operators and control structures. Think of syntax like grammar in English: just as "the cat sat" makes sense but "sat the cat on" doesn't, C++ has strict rules about how code must be written for the compiler to understand it.

#### Weak vs Strong typing

Type safety determines how strictly a language prevents you from treating data as a type it isn't.

C++ is **strongly typed**: you can't accidentally treat an `int` as a `float` or a pointer as an integer without explicitly telling the compiler to do so. This catches bugs at compile time instead of letting them crash your game at runtime.

Weak Typing (Python[^11] code):

```python3
a = 5 # Compiled! Because Python is a weak typing language.
```

Strong Typing (C++ code):

```cpp
a = 5; // Error!
int a = 5; // Compiled!
```

#### Semicolons in C++

A semicolon (`;`) marks the end of a statement. Think of it like a period at the end of a sentence — without it, the compiler doesn't know where one statement ends and the next begins.

```cpp
int a = 5; // Compiled!
int b = 5  // Error! Semicolon missing.
```

Languages like Python[^11] use newlines and indentation instead, but C++ requires explicit semicolons because it allows multiple statements on one line and gives you more control over formatting.

```cpp
int a = 5; // Compiled!
int b = 5 // Error! Semicolon missing.
```

#### Curly Braces in C++

Curly braces (<kbd>{}</kbd>) define **blocks of code** — the body of functions, classes, if-statements, loops, and namespaces. Everything inside braces shares the same **scope**: variables declared inside are invisible outside.

Think of braces like a room in a house: people (variables) inside the room can see each other, but people in the hallway can't.

```cpp
class Car
{

};
```

```cpp
namespace MyNamespace
{

}
```

```cpp
void MyFunction()
{
    {
        // Scope inside a function
    }
}
```

#### Comments in C++

Comments are ignored by the compiler — they're for humans only. Use them to explain *why* you did something, not *what* the code does (good code should be self-explanatory).

##### Single-line comments

Single-line comments start with two forward slashes `//` and continue until the end of the line.

They are typically used for brief comments or explanations on a single line.

```cpp
// This is a single-line comment in C++
```

##### Multi-line comments

Multi-line comments, also known as block comments, start with a forward slash (`/`) followed by an asterisk (`*`) and end with an asterisk (`*`) followed by a forward slash (`/`).

Multi-line comments can span multiple lines and are used for more extensive comments or documentation.

```cpp
/*
    This is a multi-line comment
    It can span multiple lines
*/
```

#### Headers vs source files

Think of a header file as a **menu** at a restaurant — it tells you what's available (function names, class structures). The source file is the **kitchen** — where the actual cooking happens.

<table><tr><td>

Header Files (.h / .hpp)

* Contain: declarations (function prototypes, class definitions, type aliases)
* Told the compiler: "these things exist"
* Included by other files via `#include`

Source Files (.cpp)

* Contain: implementations (actual function bodies, class method definitions)
* Compiled into object files (.obj), then linked into your executable

---

Why Separate Them?

Separation keeps builds fast. When you change a function's implementation, only that `.cpp` file needs recompiling. Other files that `#include` the header don't need to touch — they already know the interface hasn't changed.

---

History of Single File Extensions

In the early days of computing, languages like [Fortran](https://en.wikipedia.org/wiki/Fortran) and [COBOL](https://en.wikipedia.org/wiki/COBOL) used single file extensions because of the limitations of the operating systems and compilers at the time. Each file had to adhere to a specific format defined by the language and its compiler, and the extension represented that format.

</td></tr></table>

Other languages, like C#[^12], Java[^13], and Python[^11], continued to use single file extensions because they adopted a more integrated approach to handling both declarations and implementations within a single file.

In modern programming, the choice of using single file extensions or separate header and source files depends on the language's design philosophy and the needs of the development community. Both approaches have their strengths and weaknesses, and different languages adopt the one that best aligns with their goals and use cases.

#### Includes

The `#include` directive copies the contents of a header file directly into your source file at compile time. It's like pasting a recipe into your cookbook — now you have access to those function declarations.

The `include` directive is typically written as:

```cpp
#include "filename.h"   // Using double quotes for user-defined headers
#include <filename.h>   // Using angular brackets for standard library headers
```

Here's the difference between using double quotes and angular brackets:

1. **Double Quotes (`"filename.h")**: When you use double quotes, the preprocessor searches for the header file in the current directory first. If it doesn't find the file there, it will look in the additional include directories specified in the project settings.

   Example: `#include "MyHeader.h"`

2. **Angular Brackets (`<filename.h>`)**: When you use angular brackets, the preprocessor only searches for the header file in the standard library directories specified for the compiler.

   Example: `#include <iostream>`

In general, you use double quotes for your own header files (which may be part of your project) and angular brackets for standard library headers (like `iostream`, `vector`, etc.) or headers from external libraries.

### 🔥 Standard Library

The standard library in C++ is a collection of pre-built tools — classes, functions, and utilities — that handle common tasks so you don't have to write them from scratch. It's part of the [C++ Standard Template Library (STL)](https://en.wikipedia.org/wiki/Standard_Template_Library) and is officially known as the [C++ Standard Library](https://en.wikipedia.org/wiki/C%2B%2B_Standard_Library).

Think of it like a toolbox: instead of building your own hammer, screwdriver, and wrench for every project, you grab them from the box. The standard library gives you ready-made containers (`std::vector`, `std::map`), algorithms (`std::sort`, `std::find`), string handling, I/O operations, and more. It works the same way on Windows, Mac, or Linux — that's what "platform-independent" means.

The C++ Standard Library is organized into several header files, each of which contains declarations for specific classes and functions. Some of the key components of the standard library include containers (like vectors, lists, maps, etc.), algorithms (sorting, searching, etc.), iterators, input/output operations, strings, and more.

To use the standard library in C++, you include the appropriate header files in your code, and then you can directly use the classes and functions provided by the library. For example, to use the `std::vector` class, you include the `<vector>` header file and then create instances of the vector and use its methods.

The name "std" comes from the fact that all the classes, functions, and other elements of the standard library are part of the `std` namespace. The namespace `std` is used to avoid naming conflicts with other libraries and user-defined code. By using the `std::` prefix before any element from the standard library, you explicitly specify that you are referring to the elements in the `std` namespace.

Here's a simple example of how to use the standard library in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

std::vector<int> numbers = {5, 2, 9, 1, 7};

// Use standard library algorithm to sort the vector
std::sort(numbers.begin(), numbers.end());

// Use standard library to print the sorted vector
for (int num : numbers)
{
    std::cout << num << " ";
}
```

### 🔢 Data types

<table><tr><td>

Native Types

* `bool` - Represents a logical value, either `true` or `false`
* `char` - Represents a single character in the ASCII[^3] character set
* `int` - Represents a integer (whole number)
* `float` - Represents a floating-point number, which is a real number with a fractional component
* `double` - Represents a double-precision floating-point number, which has twice the precision of a float

<br>

</td></tr></table>

Table from [Microsoft Learn about Data Type Ranges](https://learn.microsoft.com/en-us/cpp/cpp/data-type-ranges?view=msvc-170).

| Type Name           | Bytes | Other Names                          | Range of Values                                       |
|---------------------|-------|--------------------------------------|-------------------------------------------------------|
| `int`                 | 4     | `signed`                               | -2,147,483,648 to 2,147,483,647                       |
| `unsigned int`        | 4     | `unsigned`                             | 0 to 4,294,967,295                                   |
| `__int8`              | 1     | `char`                                 | -128 to 127                                          |
| `unsigned __int8`     | 1     | `unsigned char`                        | 0 to 255                                             |
| `__int16`             | 2     | `short`, `short int`, `signed short int`   | -32,768 to 32,767                                    |
| `unsigned __int16`    | 2     | `unsigned short`, `unsigned short int`   | 0 to 65,535                                          |
| `__int32`             | 4     | `signed`, `signed int`, `int`              | -2,147,483,648 to 2,147,483,647                      |
| `unsigned __int32`    | 4     | `unsigned`, `unsigned int`               | 0 to 4,294,967,295                                  |
| `__int64`             | 8     | `long long`, `signed long long`          | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `unsigned __int64`    | 8     | `unsigned long long`                   | 0 to 18,446,744,073,709,551,615                      |
| `bool`                | 1     | none                                 | `false` or `true`                                        |
| `char`                | 1     | none                                 | -128 to 127 by default; 0 to 255 when compiled by using /J |
| `signed char`         | 1     | none                                 | -128 to 127                                          |
| `unsigned char`       | 1     | none                                 | 0 to 255                                             |
| `short`               | 2     | `short int`, `signed short int`          | -32,768 to 32,767                                    |
| `unsigned short`      | 2     | `unsigned short int`                   | 0 to 65,535                                          |
| `long`                | 4     | `long int`, `signed long int`            | -2,147,483,648 to 2,147,483,647                      |
| `unsigned long`       | 4     | `unsigned long int`                    | 0 to 4,294,967,295                                  |
| `long long`           | 8     | none (but equivalent to `__int64`)     | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `unsigned long long`  | 8     | none (but equivalent to `unsigned __int64`) | 0 to 18,446,744,073,709,551,615                      |
| `enum`                | varies| none                                 |                                                       |
| `float`               | 4     | none                                 | 3.4E +/- 38 (7 digits)                               |
| `double`              | 8     | none                                 | 1.7E +/- 308 (15 digits)                             |
| `long double`         | same as `double` | none                        | Same as `double`                                       |
| `wchar_t`             | 2     | `__wchar_t`                            | 0 to 65,535                                          |

If its name begins with two underscores (`__`), a data type is non-standard.

> [!WARNING]
> C++ lacks explicitness about data types size, leading to potential variation. For instance, the `int` type can manifest as either 16-bits or 32-bits, depending on the context.

Here is a summary of the explicit data sizes:

<table><tr><td>

* `char`, `signed char` and `unsigned char` are at least 8 bits
* `signed short`, `unsigned short`, `signed int` and `unsigned int` are at least 16 bits
* `signed long` and `unsigned long` are at least 32 bits
* `signed long long` and `unsigned long long` are at least 64 bits

</td></tr></table>

#### Char

```cpp
char myChar = 'a';
```

#### Booleans

```cpp
bool isDead = true;
```

#### Integers

```cpp
int health = 10;
```

##### Modifiers

C++ allows the char, int, and double data types to have modifiers preceding them. A modifier is used to alter the meaning of the base type so that it more precisely fits the needs of various situations.

<table><tr><td>

List of modifiers

* `signed`
* `unsigned`
* `long`
* `short`

<br>

</td></tr></table>

The modifiers `signed`, `unsigned`, `long` and `short` can be applied to integer base types. In addition, `signed` and `unsigned` can be applied to `char`, and `long` can be applied to `double`.

The modifiers `signed` and `unsigned` can also be used as prefix to `long` or `short` modifiers.

For example:

```cpp
unsigned long int // Same as unsigned 32-bit integer (unsigned int)
```

> [!NOTE]
> The default behavior for all integer types is `signed`.

Here is a list of modifiers for **integer** data type:

| Declare            | Size (bits) | Size (bytes) | Min Value                   | Max Value                     |
|--------------------|-------------|--------------|-----------------------------|------------------------------|
| `unsigned char`    | 8           | 1            | 0                           | 255                          |
| `unsigned short int` | 16          | 2            | 0                           | 65,535                       |
| `unsigned int`     | 32          | 4            | 0                           | 4,294,967,295                |
| `unsigned long long` | 64          | 8            | 0                           | 18,446,744,073,709,551,615   |
| `signed char`      | 8           | 1            | -128                        | 127                          |
| `signed short int` | 16          | 2            | -32,768                     | 32,767                       |
| `signed int`       | 32          | 4            | -2,147,483,648              | 2,147,483,647                |
| `signed long long` | 64          | 8            | -9,223,372,036,854,775,808  | 9,223,372,036,854,775,807    |

#### Floating points (floats and doubles)

```cpp
float speedInMetersPerSecond = 5.5f; // C++ always uses 'f' or 'F' literal for defining a float variable.
```

```cpp
double speedInMetersPerSecond = 5.5; // C++ never uses a literal for defining a double variable.
```

### 🙋‍♂️ Typedefs

A `typedef` creates an alias — a new name for an existing type. It's like giving your friend a nickname: everyone still knows them by their real name, but calling them "Tex" is faster to say.

```cpp
typedef int myInt; // Declare our alias for custom type

myInt x = 5;  // Equivalent to: int x = 5;
```

**Modern C++ (C++11 and later)** prefers the `using` keyword instead of `typedef`. It does the same thing but reads more naturally:

```cpp
using myInt = int; // Same result, clearer syntax
```

> [!WARNING]
> UHT[^2] doesn't support typedefs. Meaning, you can't expose to Blueprint.

### 🍂 Members

Members are variables or functions that are part of a class or object. They define the properties and behaviors of the class.

There are two main types of members: `variables` and `functions`.

#### Variables

Members that store data. They can be of different types such as numbers, strings, booleans, or custom data types. Variables hold values that can be accessed and manipulated within the class or object.

##### Assignments

There are abbreviations for frequently done kinds of assignments. Here are a few:

| Abbreviation  | Meaning | Note |
| ------------- | ------------- | ------------- |
| `n += k`  | `n = n + k`  | |
| `n -= k`  | `n = n - k`  | |
| `++n`  | `n = n + 1`  | Where the value of expression `++n` is the value of `n` after the assignment |
| `n++`  | `n = n + 1`  | But the value of expression `n++` is the value of `n` before the assignment |
| `--n`  | `n = n - 1`  | Where the value of expression `--n` is the value of `n` after the assignment |
| `n--`  | `n = n - 1`  | But the value of expression `n--` is the value of `n` before the assignment |

#### Functions

Functions are blocks of code that perform a specific task or set of tasks. They encapsulate a series of instructions and can be called and executed from various parts of a program. Functions can accept input parameters (arguments) and can also return a value as a result.

Functions can be defined outside of classes as standalone functions or can be defined within classes as member functions. Standalone functions are typically used for common tasks that are not specific to any particular class or object.

Here's an example:

```cpp
/// @brief Calculates the factorial of a number using recursion.
/// @param n Number of times.
/// @result A number.
int Factorial(int n)
{
    if (n == 0 || n == 1)
        return 1;
    else
        return n * Factorial(n - 1);
}
```

### 🧬 Classes

Classes are the building blocks of object-oriented programming (OOP). They are a blueprint for creating objects, which are instances of a class. A class defines the structure and behavior of objects by specifying the members it contains.

A class can have variables (members) to store data and functions (methods) to perform actions. The variables defined within a class are often referred to as attributes, while the functions are referred to as methods.

Objects created from a class can access and modify the class's members. They provide a way to create multiple instances that share the same structure and behavior defined by the class. Objects can be thought of as individual entities that represent real-world objects or abstract concepts.

Classes allow for code reusability, encapsulation (hiding internal details), and the ability to model complex systems by organizing related data and behavior together.

Here's an example:

```cpp
class Person
{
public:
    Person(std::string name, int age)
        : name(name)
        , age(age)
    { }

    void DisplayInfo()
    {
        // ...
    }

private:
    std::string name;
    int age;
};
```

#### Structs

A `struct` groups multiple variables of different types under one name — like a record or a form. Think of a player stats card: it holds `Name`, `Score`, `Level`, and `Health` all in one package.

It's similar to a `class`, but with one key difference: **struct members are public by default**, while class members are private by default. Use `struct` for simple data containers (like `FVector` or `FColor` in Unreal) and `class` when you need encapsulation and complex behavior.

**Usage of `struct` in C++**
- Structs are used to create lightweight data structures to hold related data elements.
- They are commonly used to represent simple data objects or records that do not require complex behavior or methods.

**Difference between `class` and `struct`**
In C++, the main difference between a `class` and a `struct` is the default access level. In a `class`, the default access level for its members is private, while in a `struct`, the default access level is public. This means that members of a `struct` are accessible outside the struct without the need for access specifiers.

For example:

```cpp
struct Vector3
{
    float x;
    float y;
    float z;

    Vector3(float _x = 0.0f, float _y = 0.0f, float _z = 0.0f)
        : x(_x)
        , y(_y)
        , z(_z)
    { }
};

Vector3 v1(1.0f, 2.0f, 3.0f);
Vector3 v2(4.0f, 5.0f, 6.0f);

float dx = v1.x - v2.x;
float dy = v1.y - v2.y;
float dz = v1.z - v2.z;

float dist = std::sqrt(dx * dx + dy * dy + dz * dz);
```

**Historical difference with C language**
In C, there was no concept of classes, and `struct` was the primary way to define user-defined data types. In C++, the `struct` keyword was retained to maintain compatibility with C, but it gained additional features and behavior, such as the ability to have member functions and access specifiers.

In modern C++, the distinction between `class` and `struct` has become more a matter of convention and coding style rather than a strict rule. Many developers prefer to use `struct` for simple data containers with public data members and `class` for more complex objects with private data members and member functions. However, you can use either `class` or `struct` based on your design preferences.

### 💔 Accessibility

| Keyword	    | Access ability | Description                                                                                          |
| ----------- | -------------- | ---------------------------------------------------------------------------------------------------- |
| `public`    | All	           | Members and functions are accessible from anywhere, including outside the class.                     |
| `protected` |	Subclasses     | Members and functions are accessible from within the class and any subclasses, but not from outside. |
| `private`   |	Class	         | Members and functions are only accessible from within the class itself.                              |
| `mutable`   |	Class	         | Specifies that a member variable can be modified even if the owning object is const.                 |
| `friend`    | Class          | Allows a non-member function or class to access the private and protected members of a class.        |

```cpp
class MyClass
{
public:
    int publicVar; // Public member variable

    // Public member function
    void publicFunction()
    {
        // ...
    }

protected:
    int protectedVar; // Protected member variable

    // Protected member function
    void protectedFunction()
    {
        // ...
    }

private:
    int privateVar; // Private member variable

    // Private member function
    void privateFunction()
    {
        // ...
    }

    mutable int mutableVar; // Mutable member variable

    friend void friendFunction(MyClass& obj); // Friend function declaration
};

void friendFunction(MyClass& obj)
{
    obj.privateVar = 42; // Friend function can access private member variable
}

MyClass obj;

// Accessing public members
obj.publicVar = 10; // Compiled!
obj.publicFunction(); // Compiled!

// Accessing private members via friend function
friendFunction(obj); // Compiled!

// Accessing private members directly (only possible within the class)
obj.privateVar = 20; // Error!
obj.privateFunction(); // Error!
```

### 🤔 If-statements

An if-statement lets your code make decisions: "if this is true, do that." It's the simplest way to control what your program does based on conditions — like checking if a player has enough health before letting them attack.

```cpp
if (condition)
{
    // Code to be executed if the condition is true
}
else if (secondCondition)
{
    // Code to be executed if the secondCondition is true, but condition was false
}
else
{
    // Code to be executed if the condition and secondCondition is both false
}
```

```cpp
if (condition)
{
    // Code to be executed if the condition is true
}
else if (secondCondition)
{
    // Code to be executed if the secondCondition is true, but condition was false
}
else
{
    // Code to be executed if the condition and secondCondition is both false
}
```

### 🔣 Comparisons and Boolean Operators

Here are some operations for creating conditions:

* `==` 	- Equality check
* `!=` 	- Inequality check
* `>` 	- Check for greater
* `<` 	- Check for less
* `>=`	- Check for greater or equal
* `<=`	- Check for less or equal
* `&&` 	- Expression A && B is evaluated by first evaluating A. A has value 0, then A && B also has value 0, and B is not evaluated. Otherwise, B is evaluated; if B has value 0, then A && B has the same value 0, and otherwise has value 1. Also called `AND` operator.
* `||`	- Expression A || B is evaluated by first evaluating A. If A has a nonzero value, then A || B has value 1, and B is not evaluated. Otherwise, A || B has value 1 if B is nonzero and value 0 if B is zero. Also called `OR` operator.
* `!` 	- Expression !A is 0 if A is nonzero, and is 1 if A is 0. Also called `NOT` operator.

#### ❓ Conditional Expressions (Ternary operator)

Conditional expressions in C++ are statements that evaluate a condition and return a value based on the result of the condition. They provide a concise way to express simple conditions and perform different actions or assignments based on the outcome.

The basic syntax of a conditional expression in C++ is as follows:

```cpp
int value = isDead ? 100 : -100; // condition ? value_if_true : value_if_false;
```

* 1\. The condition within the parentheses is evaluated.

* 2\. If the condition is true, the value or expression before the colon (<kbd>:</kbd>) is returned as the result of the conditional expression.

* 3\. If the condition is false, the value or expression after the colon is returned as the result.

### 🔀 Switches

In C++, a switch statement is a control flow construct used to select one of many possible execution paths based on the value of a given expression. It provides an alternative to using multiple if-else statements when checking a variable against different values.

The basic syntax of a switch statement in C++ is as follows:

```cpp
switch (expression)
{
    case value1:
        // Code to be executed if expression matches value1
        break;
    case value2:
        // Code to be executed if expression matches value2
        break;
    // Add more case statements as needed
    default:
        // Code to be executed if none of the cases match
        break;
}
```

* 1\. The expression is evaluated, and its value is compared against the cases specified in the switch statement.

* 2\. If a case matches the value of the expression, the code block associated with that case is executed. The execution then continues until a break statement is encountered, which exits the switch statement.

* 3\. If no case matches, the `default` block runs (if present).

### 🔁 Loops

Loops execute a block of code repeatedly while a condition is true. C++ provides three loop types:

#### ♾️ While Loop

**While loop** — runs while a condition is true. Evaluates before each iteration.

Here's an example of finding the first power of 2 greater than 100:

```cpp
int num = 1;

while (num <= 100)
{
    num *= 2;
}

std::cout << "First power of 2 greater than 100: " << num << std::endl;

// Output: First power of 2 greater than 100: 128
```

#### 🔃 Do-While Loop

**Do-while loop** — like `while` but checks the condition *after* running the block. Guarantees at least one execution.

Here's an example of printing numbers from 1 to 5 using a do-while loop:

```cpp
int i = 1;

do
{
    std::cout << i << " ";
    i++;
} while (i <= 5);

// Output: 1 2 3 4 5
```

#### 🔂 For Loop

**For loop** — use when you know the iteration count upfront. Combines initialization, condition, and update in one line.

Here's an example of printing numbers from 1 to 5:

```cpp
for (int i = 1; i <= 5; i++)
{
    std::cout << i << " ";
}

// Output: 1 2 3 4 5
```

#### 🗂️ Foreach Loop

**Range-based for loop** — iterates over any collection (array, vector, etc.) without manual indexing. Cleanest syntax for simple iteration.

Here's an example of printing each character of a string:

```cpp
std::string message = "Hello";

for (char c : message)
{
    std::cout << c << " ";
}

// Output: H e l l o
```

---

In summary:

| Loop Type    | Purpose                                        |
|--------------|------------------------------------------------|
| while loop   | Executes the block of code while the condition is true. |
| do-while loop| Executes the block of code first, then checks the condition. It guarantees that the loop will execute at least once. |
| for loop     | Executes the block of code based on the initialization, condition, and update expressions. |
| foreach loop | Iterates over the elements of a container (e.g., arrays, vectors) and executes the block of code for each item. |

### 🦋 Immutable vs Mutable

`Mutable` variables can be changed after creation. `Immutable` (via `const`) cannot — their value is fixed at initialization.

#### Mutable

The `mutable` keyword lets a class member change even when the object is `const`. Useful for caches, locks, or counters that don't affect logical state.

Usage of `mutable` for variables:

```cpp
class MyClass
{
public:
    MyClass(int value) : constantValue(value) {}

    void IncrementValue() const
    {
        mutableValue++; // Modifying the mutable member inside a const member function
    }

    // This function is const and cannot modify constantValue
    int GetConstantValue() const { return constantValue; }

    // This function is const, but mutableValue can still be modified.
    int GetMutableValue() const { return mutableValue; }

private:
    const int constantValue; // Regular constant member
    mutable int mutableValue; // Mutable member
};
```

When to use `mutable`:
- Caching computed results
- Thread-safe counters (e.g., reference counts)
- Lazy initialization inside `const` methods

Don't overuse it — only for members that don't affect the object's logical state.

> [!WARNING]
> Don't overuse `mutable` — modifying members inside `const` methods can make code harder to reason about and cause thread-safety issues.

#### Immutable

A `const` member variable can't be changed after initialization. Any attempt to modify it causes a compilation error.

The `const` keyword declares a constant variable — its value can't be changed after assignment. On member functions, it means the function won't modify the object's state (except `mutable` members). The compiler enforces this.

Usage of `const` for variables:

```cpp
const int immutableValue = 10; // Immutable variable
// immutableValue = 20; // Error: Cannot modify an immutable variable
```

---

| Property                   | Immutable                   | Mutable                      |
|----------------------------|-----------------------------|------------------------------|
| State                      | Cannot be changed           | Can be changed               |
| Modification               | Creates a new object        | Modifies the original object |
| Data Sharing               | Thread-safe (no synchronization needed) | Requires synchronization for thread-safety |
| Memory Overhead            | Additional memory allocation for each update | Direct modification, no additional memory overhead |
| Performance Characteristics | Generally more memory-efficient but slower for frequent updates | May be less memory-efficient but faster for frequent updates |

### 🪝 Try Catch

`try-catch` handles runtime errors gracefully instead of crashing. Wrap risky code in `try`, catch specific exceptions in `catch`.

How it works:

1\. Wrap risky code in a `try` block. If an exception occurs, execution jumps to the nearest matching `catch`.

2\. The `catch` block specifies which exception type it handles. Only matching exceptions are caught.

Here's a simple example in C++:

```cpp
try
{
    int numA = 5;
    int numB = 0;
    int result = numA / numB;
}
catch (const char* errorMessage)
{
    // Caught "Floating point exception"
}
```

Using `try-catch` blocks handles exceptional situations gracefully — provides error messages or logs for debugging instead of crashing. Makes your programs more robust and user-friendly.

### 🪞 Casting

Casting converts one data type into another — changing how the compiler interprets the underlying bits. You'll use casting when you need to pass data between types that don't naturally match.

#### Static casting

The most basic cast. Converts between related types (int ↔ float, base ↔ derived). Safe for numeric conversions, but doesn't check at runtime — if you cast a `float` to an `int`, you lose the decimal part silently.

Example:

```cpp
int num1 = 10;
double num2 = static_cast<double>(num1); // Static cast from int to double
```

#### Const casting

Adds or removes `const` from a variable. Rarely needed — prefer `const_cast` only when interfacing with legacy APIs that weren't written with `const` correctness in mind.

Example:

```cpp
const int x = 5;
const_cast<int&>(x) = 10; // Const cast to remove const and modify the value of x
```

#### Dynamic casting

Casts pointers/references within a class hierarchy. Only works with polymorphic classes (has virtual functions). Returns `nullptr` on failure — safe for downcasts.

Example:

```cpp
class BaseClass { /* ... */ };
class DerivedClass : public BaseClass { /* ... */ };

BaseClass* basePtr = new DerivedClass;
DerivedClass* derivedPtr = dynamic_cast<DerivedClass*>(basePtr); // Dynamic cast from BaseClass to DerivedClass
```

In Unreal Engine, `dynamic_cast` is rarely needed because the engine's reflection system (`Cast<U>()`) handles type checking more safely.

#### Reinterpret Casting

Reinterprets the raw bits of one type as another. Dangerous — no type checking, no conversion. Use only when you absolutely need to treat memory as a different type.

Example:

```cpp
result_type = reinterpret_cast<result_type>(expression);
```

### 🛼 Inlining

Inlining replaces a function call with the function's body — eliminates call overhead (stack setup/cleanup). The compiler decides whether to actually inline; `inline` is just a hint.

In C++, you can use the inline keyword to suggest to the compiler that a function should be inlined. For example:

```cpp
inline int Add(int a, int b) { return a + b; }
```

`inline` is a hint — the compiler may ignore it for large/complex functions. `__forceinline` forces it (but can bloat code size).

Here's an example of how `__forceinline` can be used:

```cpp
__forceinline int Multiply(int a, int b) { return a * b; }
```

In Unreal Engine, the engine uses `FORCEINLINE` (which maps to `__forceinline` on MSVC) for performance-critical functions like vector math operations. Inlining small, frequently-called functions eliminates function call overhead — this is why your game runs at 60fps instead of 30fps.

Prefer `inline` functions over macros — type-safe, debuggable, no surprise substitutions. The compiler still decides whether to actually inline.

### 📇 Namespace

A namespace groups related code (variables, functions, classes) under a name to avoid collisions. `std::vector` lives in the `std` namespace.

In C++, you can use namespaces to group related code together and avoid naming conflicts. Here's how you can define and use a namespace in C++:

```cpp
// Defining a namespace
namespace MyNamespace
{
    int add(int a, int b) { return a + b; }
}

int result = MyNamespace::add(3, 5);
```

Namespaces prevent naming collisions between libraries or modules. Two libraries can both define `Vector` as `Library1::Vector` and `Library2::Vector` without conflicts.

```cpp
#include <Library1/Vector.h>
#include <Library2/Vector.h>

Library1::Vector vec1;
Library2::Vector vec2;
// Use vec1 and vec2 without conflicts
```

> [!WARNING]
> UHT[^2] doesn't support namespaces. Meaning, you can't expose to Blueprint.

### 🌐 Static members

Static members belong to the class, not to individual objects. All instances share the same static variable. Static functions can't access non-static members.

In C++, you can use the static keyword to define static members in a class. Here's how you can use static members in C++ code:

```cpp
class MyClass
{
public:
    static int staticVariable; // Declaration of a static variable
    static void staticFunction(); // Declaration of a static function
};

// Definition of the static variable
int MyClass::staticVariable = 0;

// Definition of the static function
void MyClass::staticFunction()
{
    // Function implementation
}
```

Access static members with `ClassName::MemberName` — no object needed. They're shared across all instances, so there's only one copy in memory.

Unreal example: `GEngine` is a global pointer (similar concept), and `UWorld::GetWorld()` is a static function that returns the current world instance.

Here's how you can use static members in your code:

```cpp
MyClass::staticVariable = 10; // Accessing static variable
MyClass::staticFunction(); // Calling static function
```

Static members are commonly used for class-level data and utility functions that do not rely on object-specific state. They are particularly useful when you want to maintain a single instance of a variable shared among all objects of the class, or when you need a common function that does not depend on the specific object's data.

### `auto` keyword

`auto` tells the compiler: "figure out the type for me." It was introduced in C++11 and works like `var` in C#[^12].

```cpp
auto variable = 42; // Compiler deduces int
auto name = "John"; // Compiler deduces const char*
auto pi = 3.14; // Compiler deduces double
```

Use `auto` for long, cumbersome types (like iterators or template expressions). Avoid it when the type isn't obvious from the right side — `Player* player = GetPlayer();` is clearer than `auto player = GetPlayer();`.

```cpp
auto player = GetPlayer(); // Bad

Player* player = GetPlayer(); // Good
```

| Pros of Using 'auto' for Return Values         | Cons of Using 'auto' for Return Values                                              |
|-----------------------------------------------|-----------------------------------------------------------------------------------|
| Concise code with reduced type annotations    | Lack of clarity: Return type might not be immediately apparent from the code     |
| Easier to write and understand simple cases   | Debugging and error handling might be more challenging                            |
| Can simplify code in certain situations       | Reduced code readability in complex scenarios                                    |
| Reduces the need to explicitly specify types  | Potential impact on code maintainability as the codebase grows larger and complex |
| Improves code readability in some cases       | Team coding standards and practices may not always favor using 'auto'             |

### 🌱 Polymorphism (In Depth)

Polymorphism lets you use a base class pointer or reference to work with any derived class. At runtime, the correct overridden method is called based on the actual object type.

This means you can write code that works with any derived type without knowing the specifics — just program to the interface.

##### Operator Overloading

Operator overloading lets you redefine what operators like `+`, `-`, `==`, and `>=` do when used with your own classes. Without it, you'd need to write `vector1.Add(vector2)` instead of `vector1 + vector2`.

Here's an example of overloading the greater-than-or-equal-to `>=` operator in C++:

```cpp
class MyClass
{
public:
    int value;

    MyClass(int val) : value(val) {}

    bool operator>=(const MyClass& other) const
    {
        return value >= other.value;
    }
};
```

You can overload arithmetic operators (`+`, `-`, `*`, `/`), comparison operators (`==`, `<`, `>=`), assignment (`=`), and more. In Unreal Engine, this is used everywhere: `FVector + FVector`, `FColor * 0.5f`, `AActor == nullptr` — all operator overloading.

##### Function Overloading

Function overloading lets you define multiple functions with the same name but different parameters. The compiler picks the right one based on what you pass in.

```cpp
void TakeDamage(int DamageAmount)
{
    // Logic...
}

void TakeDamage(float DamageAmount)
{
    // Logic...
}

void TakeDamage(double DamageAmount)
{
    // Logic...
}
```

```cpp
TakeDamage(10); // Calls the int version
TakeDamage(11.1f); // Calls the float version
TakeDamage(12.25052651); // Calls the double version
```

Benefits:
* Reuse a familiar function name (`TakeDamage`) instead of inventing three different names
* The compiler picks the right version at compile-time — no performance cost
* Cleaner, more intuitive API

> [!WARNING]
> UHT[^2] doesn't support function overloading. Meaning, you can't expose to Blueprint.

##### Virtual functions

A virtual function is a function in a base class that can be overridden by derived classes. Without `virtual`, calling the function through a base class pointer always runs the base class version — even if the object is actually a derived type. With `virtual`, the derived class's version runs instead. This is how Blueprint functions override their C++ equivalents in Unreal.

Here's an example:

```cpp
class Shape
{
public:
    virtual void Draw()
    {
        // Common implementation for all shapes
    }
};

class Circle : public Shape
{
public:
    void Draw() override
    {
        // Override implementation
    }
};

class Rectangle : public Shape
{
public:
    void Draw() override
    {
        // Override implementation
    }
};
```

When you call `Draw()` through a `Shape*` pointer, the correct version runs based on what the object actually is. This is called **dynamic dispatch** (or late binding).

In Unreal Engine, virtual functions power the Blueprint system: when you override `BeginPlay()` or `Tick()` in a Blueprint, you're overriding a virtual C++ function.

| Keyword used | Matching virtual function in base class | Result                   |
|--------------|-----------------------------------------|--------------------------|
| Neither      | No                                      | New non-virtual function |
| Neither      | Yes                                     | Override                 |
| `virtual`      | No                                      | New virtual function     |
| `virtual`      | Yes                                     | Override                 |
| `override`     | No                                      | Compile error            |
| `override`     | Yes                                     | Override                 |
| Both         | No                                      | Compile error            |
| Both         | Yes                                     | Override                 |

### 🧙‍♂️ Generic Programming

Generic programming lets you write code that works with any type — no need to rewrite the same logic for `int`, `float`, `FVector`, etc. In C++, this is done with **templates**.

Think of a template like a cookie cutter: the cutter (template) defines the shape, but you can use it to make cookies from any dough (type). The compiler generates a version of your function or class for each type you use it with.

In C++, the `template` keyword[^1] implements this. Templates let you define functions or classes that work with any type — the compiler fills in the details when you use them.

Here is a video about [templates in C++ by Cazz](https://www.youtube.com/watch?v=p3OQDb4nWfg)

Here is an example:

```cpp
template <typename T>
T add(T a, T b)
{
    return a + b;
}

int result1 = add(5, 10);        // Instantiated as add<int>(5, 10)
double result2 = add(3.5, 2.7);  // Instantiated as add<double>(3.5, 2.7)
```

### 😵 Recursion

Recursion is a programming technique where a function calls itself to solve a problem. In simpler terms, it's a process of solving a larger problem by breaking it down into smaller, more manageable subproblems.

Here's an example:

```cpp
int factorial(int n)
{
    if (n == 0 || n == 1)
        return 1;
    else
        return n * factorial(n - 1); // Calling the function again (recursion)
}
```

<table><tr><td>

Benefits of Recursion

* **Simplicity**: Some problems (tree traversal, factorial, Fibonacci) are naturally recursive and cleaner to write recursively
* **Divide and Conquer**: Algorithms like merge sort and quicksort break problems into smaller pieces elegantly
* **No manual stack needed**: The call stack handles the bookkeeping for you

</td></tr></table>

> [!WARNING]
> Recursion is powerful but uses more memory than iteration. Watch out for stack overflows on deep recursion.

### ⚙️ Linker

The [linker](https://en.wikipedia.org/wiki/Linker_(computing)) combines all your compiled `.cpp` files (and any external libraries) into one executable or library. Think of it like a puzzle assembler: each `.cpp` file is a completed section of the puzzle, and the linker snaps them together.

The linker's main job is to resolve "undefined symbols" — when one file calls a function defined in another file, the linker connects them. If it can't find a function or variable, you get a linker error (usually "unresolved external symbol").

You can also flag the linker to export some extra debugging files or so called [.pdb](https://devblogs.microsoft.com/cppblog/whats-inside-a-pdb-file/) (Program Debug Database) file. These files can be helpful for other programmers, as they contain extra information (such as comments and other debugging information).

The linker can be configured to accept either static library or dynamic library when creating your project.

#### Static Library

<table><tr><td>

File extensions

* `.lib` = Windows
* `.a` = Linux
* `.a` = macOS

<br>

</td></tr></table>

When you compile, the source code becomes a [.lib](https://en.wikipedia.org/wiki/Static_library) file that gets baked directly into your `.exe`. The linker copies all the library code into your executable at build time.

> [!NOTE]
> Because the static library is merged into the `.exe`, it increases the final file size.

Use static libraries when you want everything bundled together — no dependency management needed, and compile-time errors catch issues early.

#### Dynamic Library

<table><tr><td>

File extensions

* `.dll` = Windows
* `.so` = Linux
* `.dynlib` = macOS

<br>

</td></tr></table>

[![Watch the video by James McNellis from CppCon 2017](https://img.youtube.com/vi/JPQWQfDhICA/maxresdefault.jpg)](https://youtu.be/JPQWQfDhICA)

When you compile, the source code becomes a [.dll](https://en.wikipedia.org/wiki/Dynamic-link_library) file that loads at runtime. Your `.exe` doesn't include the DLL code — it just knows where to find it when needed.

This creates management headaches: you need to make sure the right DLL version is present, in the right location, and compatible with your executable. This problem is so common it has a name: [DLL Hell](https://en.wikipedia.org/wiki/DLL_Hell).

<table><tr><td>

Benefits

* Can reduce disk and memory space usages
* Improved serviceability (bug fixes, security patching, etc.)
* Improved maintainability

---

Drawbacks

* Increased potential for incompatibles versions. Also, known as [DLL Hell](https://en.wikipedia.org/wiki/DLL_Hell).
* Every call across a DLL boundary is necessarily an indirect call.

</td></tr></table>

To access contents of .dll file, you have to use either `__declspec(dllimport)` or `__declspec(dllexport)`.

* Use `dllimport` for importing functions and variables.
* Use `dllexport` for exporting functions and variables.

> [!IMPORTANT]
> __declspec(dllimport) is required for data imports (such as member variables).

```cpp
// Example of the dllimport and dllexport class attributes
__declspec( dllimport ) int i;
__declspec( dllexport ) void func();
```

```cpp
// To make the code more readable, use macro definitions!
#define DllImport   __declspec( dllimport )
#define DllExport   __declspec( dllexport )

DllExport void func();
DllExport int i = 10;
DllImport int j;
DllExport int n;
```

You can read more about it from [Microsoft Learn](https://learn.microsoft.com/en-us/cpp/cpp/dllexport-dllimport?view=msvc-170).

> [!NOTE]
> Because the dynamic library is loaded at runtime, it's then loaded into RAM memory, instead of being statically compiled into the .exe file. This can take up more memory space. However, if the code use repeatably, throughout other programs, then memory space is greatly improved.

> [!WARNING]
> Using .dll also means that the library stores compiled code directly into the file. It also may contain small extra metadata about the code (debugging symbols, comments and etc). This means, the code is unsecure and more accessible for a reverse engineer to use it and modify it. C# require storing debug symbol information (for the reflection system), hence why it is easier to reverse engineer than C++ code. While you have the options to enable debug symbol information in C++. But is not automatically turn on by default.

> [!IMPORTANT]
> There is no way to guarantee to stop a reverse engineer to look at the compiled code or modify the game unless you run a program, which check the game's content as a hash data and compare to cloud stored version (this would take long time, but would be a safe approach).
>
> When calling a function, you can trace the code execution in .dll file (with the [assembly language](https://en.wikipedia.org/wiki/Assembly_language) viewer), thus understanding the function intention and then either replicated the function or modify it.
>
> Most devs are most likely to focusing on the multiplayer aspect. Such as client/server prediction and assumptions. My suggestion, is to never store any password, API keys or any important information inside the game's source code.
>
> If you need to store important information, use [strip functionality](https://en.wikipedia.org/wiki/Dead-code_elimination). To make sure the final product of your game, doesn't contain any secret information. Also, hash your password and keys ([MD5](https://www.cryptopp.com/wiki/MD5) and [SHA2](https://www.cryptopp.com/wiki/SHA2) methods).

**Use dynamic library if you want to access content at runtime and share the code between different programs.**

### 🫀 Lambda

A lambda is an anonymous (nameless) function you write inline where you use it — no need to define a separate function first. Think of it like writing a quick note instead of drafting a full letter.

Common in Unreal Engine for delegate bindings, array algorithms, and event handlers:

Here is a video by [The Cherno about Lambdas in C++](https://www.youtube.com/watch?v=mWgmBBz0y8c).

The basic syntax of a lambda expression in C++ is as follows:

```cpp
[capture_list](parameters) -> return_type
{
    // Function body
    // Statements
    // Return statement
};
```

Here's how a lambda expression works:

* 1\. Capture List: The capture list, denoted by [ ], specifies variables from the enclosing scope that the lambda function can access. It can capture variables by value ([=]) or by reference ([&]). You can also specify individual variables to capture explicitly.

* 2\. Parameters: The parameters represent the input arguments to the lambda function, similar to regular function parameters.

* 3\. Return Type: The return type, denoted by ->, specifies the type of the value returned by the lambda function. If the return type is omitted, it is deduced by the compiler.

* 4\. Function Body: The function body contains the statements and logic of the lambda function. It can include any valid C++ code, such as variable declarations, control flow statements, and computations.

Here's an example of how to use lambda in action:

```cpp
// Lambda function that takes two integers as parameters and returns their sum.
auto sum = [](int a, int b) { return a + b; };

int num1 = 5;
int num2 = 10;

// Using the lambda to calculate the sum of num1 and num2.
int result = sum(num1, num2);
```

### 🦾 Binary code

Binary is how computers store everything — numbers, text, images, game states. It uses only two symbols: `0` and `1`. Each digit is a **bit** (binary digit), and 8 bits make a **byte**.

You'll encounter binary when working with bitwise operators (see below) or debugging memory issues in Unreal Engine.

#### Logic gates

Logic gates are the building blocks of digital circuits. They take binary inputs and produce a binary output based on a simple rule. You'll use these concepts when working with bitwise operators in C++.

| Gate | Rule | Real-world analogy |
|------|------|-------------------|
| **AND** | Output is 1 only if both inputs are 1 | Both switches must be ON for the light to turn on |
| **OR** | Output is 1 if at least one input is 1 | Either switch can turn the light on |
| **NOT** | Flips the input (1→0, 0→1) | A toggle that reverses the state |
| **NAND** | AND followed by NOT | Opposite of AND |
| **NOR** | OR followed by NOT | Opposite of OR |
| **XOR** | Output is 1 if inputs are different | Two switches that turn light on only when one is ON and the other is OFF |
| **XNOR** | Output is 1 if inputs are the same | Opposite of XOR |

#### Hexadecimal

Hexadecimal (hex) is a base-16 numbering system — it uses digits 0-9 and letters A-F (representing 10-15). It's a compact way to write binary data that humans can read. One hex digit = 4 bits, so two hex digits = one byte.

In Unreal Engine, you'll see hex everywhere: memory addresses (`0x00A3F2C1`), color values (`0xFF884422` for ARGB), and GUIDs.

Here is a comparison of decimal and hexadecimal representations:

| Decimal | Hexadecimal |
|---------|-------------|
| 0       | 0           |
| 1       | 1           |
| 2       | 2           |
| 3       | 3           |
| 4       | 4           |
| 5       | 5           |
| 6       | 6           |
| 7       | 7           |
| 8       | 8           |
| 9       | 9           |
| 10      | A           |
| 11      | B           |
| 12      | C           |
| 13      | D           |
| 14      | E           |
| 15      | F           |

As an example, `255` in hexadecimal would be `FF`.

#### Bitwise Operators

Bitwise operators manipulate individual bits of data. They're fast because they work directly on the CPU's binary representation — no loops, no function calls.

You'll use them in Unreal Engine for: flag-based settings (like `EFastArraySerializerItem::bHasChanged`), color channel manipulation, and performance-critical code.

[![Watch the video by Alex Hyett](https://img.youtube.com/vi/igIjGxF2J-w/maxresdefault.jpg)](https://youtu.be/igIjGxF2J-w)

[![Watch the video by Alex Hyett](https://img.youtube.com/vi/g8ACeN9QMdY/maxresdefault.jpg)](https://youtu.be/g8ACeN9QMdY)

Here's a table listing all the bitwise operators in C++ and their functionality:

| Operator  | Description                                                                                     | Example                   |
|-----------|-------------------------------------------------------------------------------------------------|---------------------------|
| &         | Bitwise AND: Sets each bit to 1 if both corresponding bits are 1.                             | `int result = a & b;`     |
| \|        | Bitwise OR: Sets each bit to 1 if either of the corresponding bits is 1.                       | `int result = a \| b;`    |
| ^         | Bitwise XOR (Exclusive OR): Sets each bit to 1 if only one of the corresponding bits is 1.     | `int result = a ^ b;`     |
| ~         | Bitwise NOT (Complement): Inverts all the bits, changing 0 to 1 and 1 to 0.                     | `int result = ~a;`        |
| <<        | Left Shift: Shifts the bits to the left by the specified number of positions.                  | `int result = a << 3;`    |
| >>        | Right Shift: Shifts the bits to the right by the specified number of positions.                | `int result = a >> 2;`    |

Here's an example:

```cpp
int a = 5;    // Binary representation: 0000 0101
int b = 3;    // Binary representation: 0000 0011

int bitwiseAnd = a & b;     // Binary representation: 0000 0001 (1 in decimal)
int bitwiseOr = a | b;      // Binary representation: 0000 0111 (7 in decimal)
int bitwiseXor = a ^ b;     // Binary representation: 0000 0110 (6 in decimal)
int bitwiseNotA = ~a;       // Binary representation: 1111 1010 (-6 in decimal)
int leftShift = a << 2;     // Binary representation: 0001 0100 (20 in decimal)
int rightShift = a >> 1;    // Binary representation: 0000 0010 (2 in decimal)
```

### 💥 Stack vs Heap

The **stack** stores local variables and function call frames — fast allocation/deallocation, limited size. The **heap** is for dynamic memory (`new`/`delete`) — slower but much larger.

[![Watch the video by Alex Hyett](https://img.youtube.com/vi/5OJRqkYbK-4/maxresdefault.jpg)](https://youtu.be/5OJRqkYbK-4)

Choose stack for local variables and function calls (automatic, fast). Choose heap for dynamic data that needs to outlive its scope (`new`/`delete`).

C++ provides `new` and `delete` operators for explicit heap allocation. Manage it carefully — leaks and dangling pointers are the main risks.

#### Stack Memory Allocation

Stack memory is automatic — the compiler handles it. When a function is called, its local variables go on the stack. When the function returns, they're gone. It's fast because the CPU just moves a pointer up and down.

* Used for: local variables, function parameters, return addresses
* Lifetime: tied to the scope (function, block) where it's declared
* Size: limited (usually 1-8 MB per thread)
* Unreal example: `int Health = 100;` inside a function lives on the stack

#### Heap Memory Allocation

Heap memory is manual — you request it with `new` and return it with `delete`. It lives in a large pool of available RAM and outlives the function that created it.

* Used for: data that needs to outlive a function, large arrays, dynamically sized collections
* Lifetime: until you explicitly free it (or the program exits)
* Size: limited only by available RAM
* Unreal example: `new TArray<FVector>()` allocates on the heap

---

> [!WARNING]
> Don't use `new` and `delete` operators on `UObject` classes, as this would interfere with Unreal's garbage collection system.

| Aspect           | Stack                                    | Heap                                        |
|------------------|------------------------------------------|---------------------------------------------|
| Memory Location  | Contiguous block in RAM                  | Scattered "free store" region               |
| Memory Management| Automatic (LIFO, compiler-managed)       | Manual (`new`/`delete`)                     |
| Memory Size      | Fixed, limited by stack size             | Dynamic, limited by available RAM           |
| Allocation Speed | Fast (just adjust the stack pointer)     | Slow (searches for free blocks)             |
| Deallocation     | Automatic on scope exit                  | Must be explicit, or risk leaks             |
| Use Cases        | Local variables, function call frames    | Data structures needing dynamic sizing or longer lifetime |
| Risk of Overflow | Stack overflow if too deep/nested        | Out-of-memory if not freed properly         |

### Design Patterns And Principles

Design patterns are proven solutions to recurring problems. They provide templates for structuring code — not copy-paste code, but blueprints for good design.

[![Watch the video by Fireship](https://img.youtube.com/vi/tv-_1er1mWI/maxresdefault.jpg)](https://youtu.be/tv-_1er1mWI)

#### SOLID Principle

Five principles that make code more flexible and maintainable:
- **S**ingle Responsibility — one reason to change
- **O**pen/Closed — open for extension, closed for modification
- **L**iskov Substitution — subclasses must not break base class contracts
- **I**nterface Segregation — many small interfaces > one fat one
- **D**ependency Inversion — depend on abstractions, not concretions

[![Watch the video by Alex Hyett](https://img.youtube.com/vi/kF7rQmSRlq0/maxresdefault.jpg)](https://youtu.be/kF7rQmSRlq0)

#### KISS (Keep It Simple, Stupid)

Keep it simple. Avoid unnecessary complexity — the simplest solution that works is usually the best.

[![Watch the video by Smok Code](https://img.youtube.com/vi/bEG94zyZlX0/maxresdefault.jpg)](https://youtu.be/bEG94zyZlX0)

#### Singleton

Guarantees exactly one instance of a class, with global access. Useful for shared resources (e.g., game state managers). In Unreal, prefer `UWorld::GetGameInstance()` or subsystems over manual singletons.

[![Watch the video by Web Dev Simplified](https://img.youtube.com/vi/sJ-c3BA-Ypo/maxresdefault.jpg)](https://youtu.be/sJ-c3BA-Ypo)

#### Observer

One-to-many dependency: when the subject changes, all observers are notified. Unreal's delegates and `UObject` property change notifications are built on this idea.

[![Watch the video by Derek Banas](https://img.youtube.com/vi/wiQdrH2YpT4/maxresdefault.jpg)](https://youtu.be/wiQdrH2YpT4)

#### Factory

Creates objects without exposing the construction logic. Use `UFactory` subclasses in Unreal for editor-level object creation, or simple static factory methods for C++ classes.

[![Watch the video by CppNuts](https://img.youtube.com/vi/XyNWEWUSa5E/maxresdefault.jpg)](https://youtu.be/XyNWEWUSa5E)

#### Strategy

Swappable algorithms behind a common interface. Pick the right behavior at runtime instead of nested `if/else` or `switch` statements.

[![Watch the video by Derek Banas](https://img.youtube.com/vi/-NCgRD9-C6o/maxresdefault.jpg)](https://youtu.be/-NCgRD9-C6o)

#### MVC (Model-View-Controller)

Separates data (Model), UI (View), and input handling (Controller). Less relevant in Unreal — UMG handles views directly, and game logic lives in Actors/Controllers rather than a strict MVC split.

[![Watch the video by Web Dev Simplified](https://img.youtube.com/vi/DUg2SWWK18I/maxresdefault.jpg)](https://youtu.be/DUg2SWWK18I)

---

| Pattern/Principle | Description                                                                           | Use Case                                                 |
|-------------------|---------------------------------------------------------------------------------------|----------------------------------------------------------|
| SOLID Principles  | Five principles for clean, maintainable design                                        | Any codebase that needs to scale                        |
| KISS Principle    | Simplicity over cleverness                                                            | Everyday coding                                         |
| Singleton Pattern | One instance, global access                                                           | Game state, config managers                             |
| Observer Pattern  | Notify listeners when state changes                                                   | Events, delegates, property notifications               |
| Factory Pattern   | Create objects without exposing construction logic                                    | Polymorphic object creation                             |
| Strategy Pattern  | Swappable algorithms behind a common interface                                        | AI behaviors, movement types, combat styles             |
| MVC Pattern       | Separates data, UI, and input handling                                              | Web/UI apps (less relevant in Unreal)                     |

### 💯 Structures

[![Watch the video by Alex Hyett](https://img.youtube.com/vi/SCkbQSPH--A/maxresdefault.jpg)](https://youtu.be/SCkbQSPH--A)

#### Array

A fixed-size collection stored in contiguous memory. Fast random access by index, but can't resize after creation.

Here's an example:

```cpp
#include <array>

// Defining an array
std::array<int, 5> myArray = {1, 2, 3, 4, 5};
```

#### List

Doubly-linked list — fast insert/delete anywhere, but no random access (O(n) traversal). Rarely used in Unreal code; prefer `TArray` or `TList`.

Here's an example:

```cpp
#include <list>

// Defining an list
std::list<int> myList = {1, 2, 3, 4, 5};

myList.push_back(6);
myList.push_front(0);
```

#### Queue

FIFO collection — add at the back, remove from the front. Useful for task queues, event processing. Unreal has `TQueue` for thread-safe variants.

Here's an example:

```cpp
#include <queue>

// Defining an list
std::queue<int> myQueue;

myQueue.push(1);
myQueue.push(2);
myQueue.push(3);
```

#### Hash Set (Lookup table)

Unique elements with O(1) average lookup/insert/delete via hashing. Unreal's `TSet` is the equivalent.

Here's an example:

```cpp
#include <unordered_set>

// Defining an list
std::unordered_set<int> myHashSet = {1, 2, 3, 4, 5};

myHashSet.insert(6);
```

#### Dictionary (Map)

Key-value pairs with unique keys. O(1) average lookup. Unreal's `TMap` is the equivalent; use `TSet` for keys-only.

Here's an example:

```cpp
#include <map>

// Defining an list
std::map<std::string, int> myDictionary;

myDictionary["apple"] = 5;
myDictionary["banana"] = 3;
myDictionary["orange"] = 8;
```

#### Linked List

Nodes linked by pointers — O(1) insert/delete if you have the node, but no random access. More memory per element (stored pointers). Unreal has `TList` for this.

> [!NOTE]
> Linked list structure doesn't exist in C++ standard library.

Here's an example:

```cpp
struct Node
{
    int data;
    Node* next;
};

int main()
{
    Node* head = nullptr;
    Node* second = nullptr;
    Node* third = nullptr;

    head = new Node();
    second = new Node();
    third = new Node();

    head->data = 1;
    head->next = second;

    second->data = 2;
    second->next = third;

    third->data = 3;
    third->next = nullptr;

    Node* current = head;

    while (current != nullptr)
    {
        std::cout << current->data << " ";
        current = current->next;
    }

    std::cout << std::endl;

    delete head;
    delete second;
    delete third;

    return 0;
}
```

---

| Data Structure   | Description                                                                                              | Use Case                                                             |
|------------------|----------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| Array            | Fixed-size, contiguous memory                                                                            | Known size, fast random access                                      |
| List             | Doubly-linked, O(1) insert/delete anywhere                                                                | Frequent insertions/deletions                                       |
| Hash Set         | Unique elements, O(1) lookup via hash                                                                    | Membership checks, deduplication                                    |
| Dictionary       | Key-value pairs, O(1) lookup                                                                              | Fast key-based access                                               |
| Linked List      | Nodes with pointers, no random access                                                                     | Frequent insertions/deletions (when you already have the node)      |

### ⏰ Time Complexity

Time complexity measures how runtime grows with input size. It tells you how an algorithm scales — not exact execution time, but growth rate (Big-O notation).

[![Watch the video by Alex Hyett](https://img.youtube.com/vi/aIG48ldbpRI/maxresdefault.jpg)](https://youtu.be/aIG48ldbpRI)

Here is a graph of Time Complexity:

![Big O Cheat Sheet – Time Complexity Chart](https://miro.medium.com/v2/resize:fit:1400/1*5ZLci3SuR0zM_QlZOADv8Q.jpeg)

#### Constant

<table><tr><td>
Time complexity: `O(1)`
</td></tr></table>

Runtime is independent of input size — always the same number of operations, whether you pass 1 element or 1 million.

Here's an example:

```cpp
#include <iostream>

void constantTimeExample(int num)
{
    std::cout << "This is a constant time example: " << num << std::endl;
}

int main()
{
    int num = 42;

    constantTimeExample(num);

    return 0;
}
```

#### Logarithmic

<table><tr><td>
Time complexity: `O(log n)`
</td></tr></table>

Runtime grows as log(n) — each step cuts the problem in half. Binary search is the classic example: halves the search space every iteration.

Here's an example:

```cpp
#include <iostream>

int binarySearch(int arr[], int size, int target)
{
    int left = 0;
    int right = size - 1;

    while (left <= right)
    {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return -1;
}

int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int target = 7;
    int size = sizeof(arr) / sizeof(arr[0]);

    int result = binarySearch(arr, size, target);
    std::cout << "Element found at index: " << result << std::endl;

    return 0;
}
```

#### Linear

<table><tr><td>
Time complexity: `O(n)`
</td></tr></table>

Runtime scales directly with input size — double the input, double the time. One pass through the data.

Here's an example:

```cpp
#include <iostream>

void linearTimeExample(int arr[], int size)
{
    for (int i = 0; i < size; i++)
    {
        std::cout << arr[i] << " ";
    }

    std::cout << std::endl;
}

int main()
{
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    linearTimeExample(arr, size);

    return 0;
}
```

#### Quadratic

<table><tr><td>
Time complexity: `O(n^2)`
</td></tr></table>

Runtime scales as n² — usually nested loops. Doubling input quadruples runtime. Avoid for large datasets.

Here's an example:

```cpp
#include <iostream>

void quadraticTimeExample(int arr[], int size)
{
    for (int i = 0; i < size; i++)
    {
        for (int j = 0; j < size; j++)
        {
            std::cout << arr[i] * arr[j] << " ";
        }
    }

    std::cout << std::endl;
}

int main()
{
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    quadraticTimeExample(arr, size);

    return 0;
}
```

#### Exponential

<table><tr><td>
Time complexity: `O(2^n)`
</td></tr></table>

Runtime doubles with each additional input element. Extremely slow — avoid for anything beyond tiny inputs (e.g., naive Fibonacci recursion).

Here's an example:

```cpp
#include <iostream>

int fibonacci(int n)
{
    if (n <= 1)
        return n;

    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main()
{
    int n = 5;

    std::cout << "Fibonacci of " << n << " is: " << fibonacci(n) << std::endl;

    return 0;
}

```

#### Factorial

<table><tr><td>
Time complexity: `O(n!)`
</td></tr></table>

Runtime grows as n! — even worse than exponential. Only feasible for tiny inputs (n < 15). Generating all permutations is a common example.

Here's an example:

```cpp
#include <iostream>

int factorial(int n)
{
    if (n == 0)
        return 1;

    return n * factorial(n - 1);
}

int main()
{
    int n = 5;

    std::cout << "Factorial of " << n << " is: " << factorial(n) << std::endl;

    return 0;
}

```

---

| Time Complexity  | Description                                                       | Example                 | Characteristics                                           |
|------------------|-------------------------------------------------------------------|-------------------------|----------------------------------------------------------|
| Constant (O(1)) | Independent of input size                                         | Array index access        | Always the same speed                                     |
| Logarithmic (O(log n)) | Cuts problem in half each step                             | Binary search             | Very fast for large data                                  |
| Linear (O(n))   | One pass through the data                                         | Linear search             | Scales directly with input                                |
| Quadratic (O(n²)) | Nested loops over the data                                      | Bubble sort               | Slow for large inputs                                     |
| Exponential (O(2ⁿ)) | Doubles with each input element                            | Naive Fibonacci           | Only works for tiny inputs                                |
| Factorial (O(n!)) | n × (n-1) × ... × 1                                            | Generating permutations   | Impractical beyond n≈15                                   |

<!-- prettier-ignore-end -->

## 📍 Footnotes

[^1]: Keyword, also known as a [Reserved word](https://en.wikipedia.org/wiki/Reserved_word).
[^2]: The [Unreal Header Tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-header-tool-for-unreal-engine/) (UHT) is a powerful tool for managing dependencies between C++ files in an Unreal Engine project. The header tool is designed to work with the [Unreal Build Tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-build-tool-in-unreal-engine/) (UBT), which is responsible for compiling the engine and all its modules.
[^3]: `ASCII` or American Standard Code for Information Interchange. A character encoding standard for representing English (Latin) characters and symbols.
[^4]: Macros in C++ are preprocessor directives that enable the definition of reusable code snippets through text replacement before compilation. Here is a [video about it](https://www.youtube.com/watch?v=j3mYki1SrKE).
[^5]: GitHub is a web-based platform and version control repository that allows individuals and teams to collaborate on software development projects by providing a centralized location for code storage, version tracking, issue tracking, and collaboration features such as pull requests and code reviews. [Link to there site](https://github.com/).
[^10]: [C](https://en.wikipedia.org/wiki/C_(programming_language)) is a procedural programming language known for its efficiency and portability, commonly used for system-level programming and embedded systems development.
[^11]: [Python](https://en.wikipedia.org/wiki/Python_(programming_language)) is a user-friendly, high-level language often used for scripting, data analysis, web development, and artificial intelligence applications.
[^12]: [C#](https://en.wikipedia.org/wiki/C_Sharp_(programming_language)) is a high-level, object-oriented programming language developed by Microsoft, widely used for building Windows applications and games using the .NET framework.
[^13]: [Java](https://en.wikipedia.org/wiki/Java_(programming_language)) is a versatile, platform-independent language known for its "write once, run anywhere" capability, commonly used in web development and enterprise applications.
[^14]: [JavaScript](https://en.wikipedia.org/wiki/JavaScript) is a versatile, dynamic scripting language commonly used for web development to add interactivity and functionality to websites.
