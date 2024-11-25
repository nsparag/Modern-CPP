# C++11

C++11 is an ISO/IEC 14882:2011 standard published in the year 2011. 

To compile a code written in C++11, one need to use `-std=c++11` flag to the command line compilation string. If we want to compile a file `mainFile.cpp` then the command line string to compile this file will be 
````C++
g++ -std=c++11 mainFile.cpp
````
* Core Language Enhancements
  * Runtime performance enhancement
    * Move semantics
    * Rvalue reference
    * constexpr
  * Build-time performance enhancement
    * Extern template
  * Usability enhancement
    * Initializer lists
    * brace-or-equal initializers
    * nullptr
    * Range-Based Loops
    * Lambda Expressions
    * Automatic Type Deduction
    * Trailing Return Types
    * `final` specifier
    * `Override` specifier
    * Scoped enum
    * Type Aliases
    * `noexcept` Specifier and `noexcept` Operator
  * Functionality Improvement
    * Variadic templates
    * long long
    * char16_t and char32_t
    * literal types
    * User-Defined Literals
    * static_assert
    * `alignof` and `alignas`
    * Attributes
    * `default` function
    * `delete` function
* Standard Library Features
  * Thread library
  * Tuple
  * Hash Tables
  * `std::array`
  * `std::forward_list`
  * Regular expressions
  * Smart Pointers
  * Chrono Library
  * to_string
  * Type traits
  * `std::tie`
----------------------------------------------------------------------------------------------
## Move semantics

It allows objects to be transferred from one location to another, without copying the object. It means transfer ownership of some resource it manages to another object.

It works based on following points:
* **Rvalue References**: Rvalue references are a type of reference that can bind to an rvalue (an expression that can appear on the right-hand side of an assignment). They are used to implement move semantics.
* **Move Constructors**: Move constructors are special constructors that are used to transfer the contents of an object when it is moved. They take an rvalue reference to the object being moved as an argument.
* **Move Assignment Operators**: Move assignment operators are special assignment operators that are used to transfer the contents of an object when it is moved. They take an rvalue reference to the object being moved as an argument.
* **std::move**: The `std::move` function is used to convert an lvalue into an rvalue, allowing it to be moved.

Benefits of Move Semantics:
* Improved Performance: Move semantics can improve performance by reducing the number of copies made when objects are transferred.
* Reduced Memory Allocation: Move semantics can reduce memory allocation by allowing objects to be transferred without creating a new copy.
* Simplified Code: Move semantics can simplify code by reducing the need for copy constructors and copy assignment operators.

## Rvalue Reference

Rvalue references are a type of reference that allows us to bind to an rvalue. 
An rvalue is an expression that can appear on the right-hand side of an assignment. An expression is _rvalue_ if it it results in a temporary object.
Examples of rvalue
````C++
int var = 2;    // 2 is rvalue & var is lvalue
int variable = foo(); // function call is rvalue and & variable is lvalue
````       
An rvalue reference is a type of reference that can bind to an rvalue. It is declared using the `&&` syntax. When an rvalue reference is created, it binds to the rvalue and prevents it from being destroyed until the reference goes out of scope.

Example: 
````C++
int main() {
    int&& r = 5; // r binds to the rvalue 5; Rvalue reference (a reference to a temporary value)
    std::cout << r << std::endl; // prints 5
    return 0;
}
````
Rvalue Reference is useful when the function needs to implement move semantics or transfer ownership of an object.

## Move Constructor
A move constructor is a special type of constructor in C++ that is used to transfer the ownership of an object from one instance to another.
When an object is created, it typically acquires resources such as memory, file handles, or network connections. However, when an object is copied, the copied object also acquires the same resources, which can lead to problems such as:
* Resource leaks: When the copied object is destroyed, it does not release the resources, causing a resource leak.
* Data corruption: When multiple objects access the same resource, it can lead to data corruption.

**Syntax**
````C++
class MyClass {
public:
    MyClass(MyClass&& other) noexcept {
        // Transfer ownership of resources from other to this object
    }
};
````
When a move constructor is called, it transfers the ownership of the resources from the source object to the target object. The source object is left in a valid but unspecified state, which means that it can be safely destroyed or reassigned.

**Example**:
````c++
#include <iostream>

class MyClass {
public:
    MyClass() {
        std::cout << "Default constructor" << std::endl;
    }

    MyClass(MyClass&& other) noexcept {
        std::cout << "Move constructor" << std::endl;
    }

    ~MyClass() {
        std::cout << "Destructor" << std::endl;
    }
};

int main() {
    MyClass obj1;
    MyClass obj2 = std::move(obj1);

    return 0;
}
````
This shows that the move constructor is used to transfer ownership from obj1 to obj2, and then both objects are destroyed.

## `constexpr` 
It allows to evaluate function or expressions at compile-time.

**Example**: constexpr Variable
````c++
constexpr const double PI = 3.14159; // a compile-time constant
constexpr int variable = 10; // a compile-time constant
double radius = 2; //
constexpr double circlePerimeter = 2*PI*radius;    // compile-time error as value of radius is not known at compile time
````
**Example**: constexpr Function
````c++
constexpr int square(int x) {
return x * x;
}
````
**Benefits**:
* Improved Performance: constexpr functions can improve performance by reducing the overhead of runtime evaluation.
* Increased Efficiency: constexpr can reduce the number of runtime computations, which can improve the efficiency of your code.
* Better Code Optimization: constexpr allows the compiler to perform better optimizations, which can result in smaller and faster code.
* Better Error Messages: constexpr functions provide better error messages than runtime errors, which can make it easier to diagnose and fix issues.


## `extern template`
It is a feature in C++11 that allows you to specify that a template instantiation should be defined in a separate translation unit, rather than in the current translation unit. It is analogous to extern data declarations.

**Example**:
````c++
extern template class MyClass<int>;
````
## Initializer Lists
An initializer list is a list of values enclosed in curly braces `{}`. It allows to initialize objects in a uniform way.

**Syntax**:
````c++
Type variable_name = {value1, value2, ..., valueN};
````

**Example 1**:
````C++
int var1{24}; // initialize var1 with value 24 - Direct initialization
int var1 = {24}; // initialize var1 with value 24 - Copy initialization
char var2{'p'}; // initialize var2 with value 'p'- Direct initialization
char var2 = {'p'}; // initialize var2 with value 'p' - Copy initialization
std::vector<int> v{ 1, 2, 3, 4, 5 }; // initialize vector v with values 1, 2, 3, 4, 5 - Direct initialization
std::vector<int> v = { 1, 2, 3, 4, 5 }; // initialize vector v with values 1, 2, 3, 4, 5 - Copy initialization
````

**Example 2**:
````C++
struct Person {
    int age;
    std::string name;
};
Person person = {30, "John"}; // Aggregate initialization
````

## brace-or-equal initializers
Brace-or-equal initializers are a feature in C++ that allows for initializing objects with either the `=` operator or with curly brackets `{}`.

**Syntax**:
````c++
Type variable_name = value; // Equal initializer
Type variable_name{value}; // Brace initializer
````
**Difference**:

| Characteristic    |    Equal Initializer | Brace Initializer |
|:----------|:----------:|:----------:|
| Initialization Method | Uses the = operator	| Uses curly brackets {}| 
| Syntax	| Type variable_name = value;| 	Type variable_name{value};| 
| Implicit Conversions	| Allows implicit conversions| 	Prevents implicit conversions| 
| Narrowing Conversions	| Allows narrowing conversions	| Prevents narrowing conversions| 
| Type Deduction	| Supports type deduction	| Does not support type deduction| 
| Example| 	int x = 3.14;| 	int x{3.14};| 

## `nullptr`
`nullptr` is a keyword in C++ that was introduced in C++11 as a replacement for the older `NULL` macro. 
`nullptr` itself is of type `std::nullptr_t` and can be implicitly converted into pointer types, and unlike `NULL`, not convertible to integral types except bool.

**Example**:
````c++
int* ptr = nullptr;
````

## Range-Based Loops

A Range-Based Loop is a type of loop that allows you to iterate over a range of values, such as the elements of a container or an array, without having to manually manage the loop counter or index.
Syntax:

````C++
for (range_declaration : range_expression) {
    // statement(s)
}
````
Example:
````C++
// Print the values in `numbers` vector
std::vector<int> numbers = {1, 2, 3, 4, 5};
for (auto& num : numbers) {
    std::cout << num << " ";
}
````
It is same as traditional for loop as implemented below.
````C++
std::vector<int> numbers = {1, 2, 3, 4, 5};
for(int i=0; i<=4; i++){
    std::cout << numbers[i] << " ";
}
````

Advantages:
* Concise code: Range-Based Loops make your code more concise and easier to read.
* Less error-prone: You don't have to manually manage the loop counter or index, which reduces the risk of off-by-one errors or other mistakes.
* Type-safe: The type of the loop variable is automatically deduced by the compiler, which ensures type safety.

## Lambda Expressions
It allows to define anonymous functions. They allow us to write a short code snippet to be used as a standard library function predicate.

**Syntax**:
````c++
[capture](parameters) -> return-type {
    function-body
}
````

Lambdas have a capture list marked by `[ ]` where we can capture local variables by reference or copy, a parameter list with optional parameters marked with `( )`, and a lambda body marked
with `{ }`.

**Capture**
The capture clause is used to specify the variables that are captured by the lambda expression.

* **Empty capture**: `[]` does not capture any variables
* **Value capture**: `[x]` captures x by value.
* **Reference capture**: `[&x]` captures x by reference.
* **Default capture**: `[=]` captures all variables in scope by value.
* **Default reference capture**: `[&]` captures all variables in scope by reference.

**Example**: **Empty capture**
````c++
auto add = [](int x, int y) -> int {
    return x + y;
};

std::cout << add(2, 3) << std::endl; // Output: 5
````
The lambda expression has an empty capture clause, which means it does not capture any variables from the surrounding scope.

**Example**: **Value capture**
````c++
int x = 5;
auto add = [x](int y) -> int {
    return x + y;
};

std::cout << add(3) << std::endl; // Output: 8
````
The lambda expression captures the variable x from the surrounding scope by value, which means that the lambda expression creates a copy of x that is used within the lambda expression.

**Behavior**
When a variable is captured by value in a lambda expression, the following behavior occurs:
* Initialization: The captured variable is initialized with the value of the variable in the surrounding scope at the time the lambda expression is created.
* Scope: The captured variable is in scope within the lambda expression, and its value can be accessed and modified within the lambda expression.
* Lifetime: The captured variable remains in scope for the lifetime of the lambda expression, and its value is destroyed when the lambda expression goes out of scope.

**Example**: **Reference capture**
````c++
int x = 5;
auto add = [&x](int y) -> int {
    return x + y;
};

x = 10;
std::cout << add(3) << std::endl; // Output: 13
````
The lambda expression captures the variable x from the surrounding scope by reference, which means that the lambda expression has access to the original variable x and can modify it.

**Behavior**
When a variable is captured by reference in a lambda expression, the following behavior occurs:
* Initialization: The captured variable is initialized with a reference to the variable in the surrounding scope at the time the lambda expression is created.
* Scope: The captured variable is in scope within the lambda expression, and its value can be accessed and modified within the lambda expression.
* Lifetime: The captured variable remains in scope for the lifetime of the lambda expression, and its value is not destroyed when the lambda expression goes out of scope.

**Example**: **Default capture**
````c++
int x = 5;
int y = 10;
auto add = [=](int z) -> int {
    return x + y + z;
};

x = 20;
y = 30;

std::cout << add(3) << std::endl; // Output: 18
````
The lambda expression captures all variables x and y in the surrounding scope by value using the value default capture [=]. When the values of x and y are modified, the lambda expression still uses their original values.

**Example**: **Reference Default Capture**
````c++
int x = 5;
int y = 10;
auto add = [&](int z) -> int {
    return x + y + z;
};

x = 20;
y = 30;

std::cout << add(3) << std::endl; // Output: 53
````

**Example**:

````c++
#include <iostream>

int main() {
    int x = 5;
    int y = 20;
    auto addValueCapture = [x](int y) -> int { 
        return x + y;
    };
    std::cout << addValueCapture(2) << std::endl; // Output: 5+2=7

    auto addReferenceCapture = [&x](int y) -> int {
        return x + y;
    };
    x = 10;
    std::cout << addReferenceCapture(2) << std::endl; // Output: 10+2=12

    auto addDefaultCapture = [=](int z) -> int {
        return x + y + z;
    };
    y = 10;
    std::cout << addDefaultCapture(2) << std::endl; // Output: 10+20+2=32

    auto addReferenceDefaultCapture = [&](int z) -> int {
        return x + y + z;
    };
    std::cout << addReferenceDefaultCapture(2) << std::endl; // Output: 10+10+2=32

    auto add = [x,&y](int a, int b) -> int {
        return a+b+x+y;
    };
    x = 5;
    y = 5;
    std::cout << add(2,3) << std::endl; // Output: 10+5+2+3=32
}
````

Lambda functions in C++ can be defined in various places, including:
* **Inside a function body**: Lambda functions can be defined inside the body of another function. They are known as local lambda functions.
* **As a class member**: Lambda functions can be defined as a member of a class. They are known as member lambda functions.
* **As a namespace variable**: Lambda functions can be defined in a namespace, either in a header file or a source file.
* **As a global variable**: Lambda functions can be defined at the global scope, outside of any function or class.

**Benefits**:
* Conciseness: Lambda functions are concise and can be defined inline within a larger expression. This makes them ideal for small, one-time use functions.
* Readability: Lambda functions can improve code readability by encapsulating complex logic within a single expression.
* Flexibility: Lambda functions can capture variables from the surrounding scope, making them flexible and reusable.
* Anonymous: Lambda functions do not require a declared name, making them useful when you need a small, one-time use function.
* Type Inference: Many programming languages can infer the type of a lambda function, making it easier to write and maintain code.
* Closures: Lambda functions can be used to create closures, which are functions that have access to their own scope and can capture variables from that scope.
* Higher-Order Functions: Lambda functions can be used as higher-order functions, which are functions that take other functions as arguments or return functions as output.
* Event Handling: Lambda functions are often used in event handling, such as handling button clicks or network requests.
* Data Processing: Lambda functions are useful in data processing, such as data transformation, filtering, or mapping.
* Concurrency: Lambda functions can be used in concurrent programming, such as parallel processing or asynchronous programming.

## Automatic Type Deduction

With auto, you can let the compiler figure out the type of the variable, making your code more concise and easier to read.

**Example**:

````C++
auto intVariable = 34;	// integer
auto charVariable = 'k'; // character
auto doubleVariable = 34.566; // double
auto constCharVariable = "Hello"; // const char*
````

**Advantages**:
* Conciseness: With auto, you can skip explicit type declarations, making your code more concise.
* Readability: Your code becomes more readable, as the focus is on the variable's name and its purpose, rather than its type.
* Reduced typing errors: The compiler will detect type errors at compile-time, reducing the likelihood of runtime errors.

## `decltype`
`decltype` is a keyword that allows to deduce the type of an expression.

**Example**:
````C++
int var1 = 5;
decltype(var1) var2; // var2 is of type int
decltype(var1+5) var2; // var2 is of type int
````
**Use Cases**
* Template Metaprogramming: decltype is commonly used in template metaprogramming to deduce the type of expressions.
* SFINAE: decltype can be used with SFINAE to enable or disable function templates based on the type of expressions.
* Variable Declaration: decltype can be used to deduce the type of variables, making the code more concise and easier to maintain.

## Trailing Return Types
It deals about specifying the return type of a function after the function name. his syntax is especially useful when the return type depends on the template parameters of the function.

**Example 1:**: the function will return int type value
````C++
auto calculateArea(int length, int width) -> int {
    return length * width;
}
````
**Example 2:** the function will return value of type (x+y)
````C++
template <typename T, typename U>
auto add(T x, U y) -> decltype(x + y) {
    return x + y;
}
````
By using trailing return types, you can write more expressive and maintainable code in C++.

## `final` specifier
The final keyword is used to specify that a virtual function cannot be overridden in a derived class. 
It is typically used to prevent unwanted overrides and ensure that a function behaves consistently across all derived classes.

**Example:**
````C++
class Base {
public:
    virtual void foo() final {
        // Implementation
    }
};

class Derived : public Base {
public:
    void foo() override { // Error: cannot override final function
    }
};
````
## `Override` specifier
The override keyword is used to specify that a virtual function is intended to override a function in a base class. It is typically used to ensure that a function is correctly overriding a base class function, rather than introducing a new function with the same name.
````C++
class Base {
public:
    virtual void foo() {
        // Implementation
    }
};

class Derived : public Base {
public:
    void foo() override { // Correct override of Base::foo()
        // Implementation
    }
};
````

## Scoped Enums
A type of enumeration that limits the scope of the enumeration values to the enum itself, rather than having them be part of the surrounding scope.

**Example**:
````c++
#include <iostream>
enum class enumColor {
    RED,
    GREEN,
    BLUE
};

enum Color{
    RED,
    GREEN,
    BLUE
};

int main() {
    enumColor color = enumColor::RED;
    std::cout << "color is " << RED << std::endl;
    // You can't use RED directly, you need to use enumColor::RED
    std::cout << "color is " << static_cast<int>(color) << std::endl; // static_cast is used because `<<` operator is not overloaded for scoped enums.
    return 0;
}
````
In this example, enumColor is a scoped enum, and its values (RED, GREEN, BLUE) are only accessible through the enumColor enum itself. This is in contrast to unscoped enums, where the values would be directly accessible in the surrounding scope.

**Benefits**
* Improved Readability: Scoped enums make it clear that a value is part of a specific enumeration, which can improve readability and avoid ambiguity.
* Large Projects: Use scoped enums in large projects to improve readability, avoid ambiguity, and prevent type errors.
* Complex Codebases: Use scoped enums in complex codebases where there are many enumeration values and overlapping scopes.

## Type Aliases
A type alias is a new name given to an existing data type. It is a way to create a shorthand or a more meaningful name for a type.

**Syntax**:
````c++
using new_type_name = existing_type;
````

**Example**:
````c++
using Byte = unsigned char;
````

**Benefits**
* Improved Readability: Type aliases can make code more readable by providing a more meaningful name for a type.
* Reduced Complexity: Type aliases can simplify complex type declarations by breaking them down into smaller, more manageable parts.
* Improved Maintainability: Type aliases can make code easier to maintain by allowing developers to change the underlying type without affecting the rest of the code.
* Common Use Cases

**Use Cases**
* Renaming built-in types: Type aliases can be used to create more meaningful names for built-in types, such as Byte for unsigned char.
* Simplifying complex types: Type aliases can be used to simplify complex type declarations, such as Vector for std::vector<float>.
* Defining domain-specific types: Type aliases can be used to define domain-specific types, such as Point for std::pair<float, float>.

## `noexcept` Specifier and `noexcept` Operator
The noexcept specifier and noexcept operator are used to specify that a function does not throw any exceptions.

**`noexcept` Specifier**

The noexcept specifier is used to declare that a function does not throw any exceptions. 
````c++
void myFunction() noexcept;
````
**`noexcept` Operator**

The noexcept operator is used to check whether a function is declared as noexcept. It returns true if the function is declared as noexcept and false otherwise.
````c++
bool isNoexcept = noexcept(myFunction());
````
**Benefits**
* Improved Performance: Functions declared as noexcept are more efficient because the compiler can optimize them without considering the possibility of exceptions.
* Better Code Quality: The noexcept specifier helps to ensure that functions are written to handle errors correctly and avoids the use of exceptions for flow control.


## Variadic Templates
It allows a function or class to take a variable number of template parameters.

**Synatx**:
````c++
template<typename... Args>
````

**Example**:
````c++
template<typename... Args>
void printArgs(Args... args) {
    ((std::cout << args << " "), ...);
    std::cout << std::endl;
}

int main() {
    printArgs(1, "hello", 3.14);
    printArgs(1, 3.14, "hello");
    return 0;
}
````
Here, printArgs that takes a variable number of arguments using the Args... syntax. We then use the ((std::cout << args << " "), ...) syntax to print each argument, followed by a space.

## long long
A data type that represents a 64-bit integer value.

## char16_t and char32_t
Two new character types that were introduced to support Unicode characters. They represent 16 bit and 32 bit characters values respectively.

Example:
````c++
char16_t c1 = u'\u1234'; // char16_t
char32_t c2 = U'\U00012345'; // char32_t
````

## literal types

**Literal types** in C++ are types that can be initialized with a constant expression, such as an integer or floating-point literal. These types are also known as "literal type" or "compile-time constant type".
* Integer literals (e.g., 1, 2, 3)
* Floating-point literals (e.g., 3.14, -0.5)
* Character literals (e.g., 'a', 'B')
* String literals (e.g., "hello", "world")
* Boolean literals (e.g., true, false)
* Null pointer literals (e.g., nullptr)

**Characteristics**:
* They can be initialized with a constant expression.
* They are evaluated at compile-time, which means their values are known at compile-time.
* They are not subject to runtime evaluation or execution.
* They do not have any side effects.

**Benefits**:
* Improved performance: Since literal types are evaluated at compile-time, they do not incur any runtime overhead.
* Better code readability: Using literal types can make your code more readable, as the values are explicitly specified.
* Reduced errors: Since literal types are evaluated at compile-time, errors are detected earlier, reducing the likelihood of runtime errors.


## User-Defined Literals
User-defined literals are a way to define new literal types that can be used in your code. 

**Syntax**:
````c++
long double operator "" ldl(long double);
unsigned long long operator "" ulll(unsigned long long);
long long operator "" lll(long long);
unsigned long operator "" ul(unsigned long);
long operator "" l(long);
unsigned operator "" u(unsigned);
const char* operator "" s(const char*, size_t);
char16_t operator "" su(const char16_t*, size_t);
char32_t operator "" suu(const char32_t*, size_t);
wchar_t operator "" sw(const wchar_t*, size_t);
````

**Example**:
````c++
long long operator "" _sec(long long value) {
    return value * 1000; // convert seconds to milliseconds
}

int main() {
    auto duration = 10_sec; // equivalent to 10000 milliseconds
    // do something with the duration
    return 0;
}
````
A user-defined literal `_sec` that takes a `long long` value and returns the equivalent time duration in milliseconds.

**Benefits**
* Improved readability: User-defined literals can make your code more readable by allowing you to express specific types of data in a more intuitive way.
* Increased expressiveness: User-defined literals can increase the expressiveness of your code by allowing you to define new literal types that are tailored to your specific needs.
* Improved maintainability: User-defined literals can improve the maintainability of your code by making it easier to modify or extend existing code.

## `static_assert`
It is a keyword used to verify that a constant expression is true at compile-time. Here, 'expression' is a constant expression that can be evaluated at compile time, and 'message' is a string literal that is displayed if the assertion fails.

**Syntax**:
````c++
static_assert(expression, message);
````

**Example**:
````c++
static_assert(sizeof(int) == 4, "Incorrect size for int");
````
## `alignof` and `alignas`

`alignof` is an operator that returns the alignment requirement of a type. The alignment requirement is the minimum alignment that must be satisfied for an object of that type to be properly aligned.

`alignas` is a specifier that can be used to specify the alignment requirement for a variable or a type.

**Syntax**
````c++
alignof(type)
alignof(expression)

alignas(type)
alignas(expression)
alignas(alignment value)
````

Here, `type` is the type for which you want to know the alignment requirement, and `expression` is an expression that can be evaluated at compile-time to determine the underlying type. 
Also, `type` is a type that has an alignment requirement that you want to use, `expression` is an expression that can be evaluated at compile-time to determine the underlying type, and `alignment value` is a constant expression that specifies the alignment requirement.

**Example**:
````c++
std::cout << "Alignment of int: " << alignof(int) << std::endl;    // display the alignment required by int
alignas(double) char arr[10];  // Each element of arr will be aligned to double
````
## Attributes
A way to provide additional information about a function, variable, or type. 

**Syntax**:
````c++
[[attribute]] declaration
````

**Example**:
````c++
[[deprecated]] void old_function() {
    // do something
}
````
The `[[deprecated]]` attribute is used to mark the `old_function` function as deprecated.

Some of the Standard attitbutes:
* `[[deprecated]]`: marks a function, variable, or type as deprecated.
* `[[fallthrough]]`: indicates that a fallthrough from a switch statement is intentional.
* `[[maybe_unused]]`: indicates that a variable or function parameter may be unused.
* `[[nodiscard]]`: indicates that the return value of a function should not be ignored.
* `[[noreturn]]`: indicates that a function does not return.

**User Defined Attributes**:
Example of defining a custom attribute to mark a function as a unit test:
````c++
#define unittest [[attribute(unittest)]]

unittest void test_function() {
    // do something
}
````

## `default` function

Explicitly defaulted functions in C++ are a feature that allows you to explicitly declare a special member function (such as constructors, destructors, assignment operators, etc.) as = default in the class definition. This tells the compiler to generate a default implementation for that function, just like it would if the function wasn't declared at all.
It is achieved by writing `default` in the function declaration.

**Example**:
````c++
class temp
{
    temp() = default; //The default constructor is explicitly stated.
    temp(OtherType value);
};
````

## `delete` function
It allows a function to be explicitly disabled. It is achieved by keyword `delete` in the function declaration.

**Example**:
````c++
void noInt(double i);
void noInt(int) = delete;
````
An attempt to call noInt() with an int parameter will be rejected by the compiler, instead of performing a silent conversion to double. Calling noInt() with a float still works.

----------------------------------------------------------------------------------------------

## Thread library

It provides a high-level abstraction for working with threads, making it easier to write concurrent programs.

Here are some key features of the thread library in C++11:
* `std::thread`: This is the core class of the thread library. It represents a thread of execution and provides methods to start, join, and detach a thread.
* `std::this_thread`: This namespace provides functions that allow threads to manipulate their own state.
* `std::mutex`: This is a mutex (short for mutual exclusion) class that can be used to synchronize access to shared resources.
* `std::lock_guard` and `std::unique_lock`: These classes are RAII (Resource Acquisition Is Initialization) wrappers around mutexes. They provide a way to automatically acquire and release locks when entering or exiting a scope.
* `std::condition_variable`: This class is used to implement condition variables, which allow threads to wait until a certain condition is met before proceeding.

## Tuple

It allows to create objects that hold multiple values of different types.

**Example**:
````c++
// Tuple Declaration
std::tuple<int, double, std::string> myTuple;

// declare and initialize a tuple at the same time
auto myTuple = std::make_tuple(10, 3.14, "Hello");
````

Tuple and Structures - Key differences:
* Naming: In a structure, you can name each member, which makes it easier to access and understand the data. In a tuple, the elements are referenced by their index.
* Readability: Structures are more readable, especially for complex data types, because you can clearly see what each member represents.
* Performance: Tuples are generally faster and more lightweight than structures because they don't require the overhead of member access.
* Flexibility: Tuples are more flexible than structures because you can easily modify the elements or add new ones.

When to use each:
Use a structure when:
* You need to represent complex data types with clear, descriptive names.
* Readability and maintainability are important.
* You need to perform operations on the data that depend on its meaning (e.g., you have a Person structure and you want to calculate the person's age).
Use a tuple when:
* You need to return multiple values from a function.
* You need to represent simple data types.
* Performance is critical, and you can't afford the overhead of a structure.

## Hash Tables

Hash table is a fundamental data structure that provide an efficient way to store and retrieve data.

The hash table containers supported are:
* `std::unordered_map`: a hash table that stores key-value pairs in an unordered manner.
* `std::unordered_multimap`: a hash table that stores key-value pairs, allowing multiple values for each key.
* `std::unordered_set`: a hash table that stores unique keys without associated values.
* `std::unordered_multiset`: a hash table that stores unique keys, allowing multiple instances of each key.

## `std::array`

`std::array` is a fixed-size container that stores a collection of elements of the same type in contiguous memory locations. It is similar to a C-style array, but with additional features and safeguards.
It is more efficient than std::vector but safer and easier to use than a c-style array.

## `std::forward_list`
It is a singly-linked list that provides efficient insertion and deletion of elements. It is similar to `std::list`, but with a few key differences.
* efficient insertion and deletion of elements at the beginning and end of the list.
* can not access elements by index
* provides `insert_after()` and `erase_after` for inserting and deleting elements after a specified iterator.

## Regular expressions

`std::regex` represents a regular expression
`std::match_results` represents the results of a match.

The <regex> library provides several match algorithms:
* `std::regex_search`: Searches for a match anywhere in the string.
* `std::regex_match`: Matches the entire string against the pattern.
* `std::regex_replace`: Replaces matches with a replacement string.

## Smart Pointers

Smart pointers are a type of container that provide automatic memory management for dynamically allocated objects. They are designed to replace raw pointers and automatically handle the deallocation of memory when the object is no longer needed.

* `std::unique_ptr`: A unique pointer is a smart pointer that owns and manages another object through a pointer.
* `std::shared_ptr`: A shared pointer is a smart pointer that retains shared ownership of an object through a pointer. Several shared_ptr objects may own the same object.
* `std::weak_ptr`: A weak pointer is a smart pointer that observes an object owned by a shared_ptr without participating in the ownership. It is used to prevent circular references.

All three smart pointers provide automatic memory management, eliminating the need for manual memory management using `new` and `delete`.
All three smart pointers support exception safety, ensuring that memory is properly released even when exceptions occur.
All three smart pointers are designed to prevent memory leaks and dangling pointers.


|	std::unique_ptr	| std::shared_ptr	| std::weak_ptr |
|:----------|:----------:|:----------: |
| Ownership	| Exclusive	| Shared	Observing
| Deletion		| Automatically deletes the object when it goes out of scope		| Automatically deletes the object when the last shared_ptr to it goes out of scope		| Does not delete the object	| 
| Copy Semantics	| 	No copy semantics	| 	Can be copied		| No copy semantics	| 
| Move Semantics		| Supports move semantics	| 	Supports move semantics		| No move semantics	| 
| Example Use Case		| Exclusive ownership of an object	| 	Shared ownership of an object	| 	Observing an object without taking ownership	| 

## Chrono Library

`std::chrono` provides a flexible and efficient way to work with time and durations. It introduces several key components:

* `std::chrono::duration` class template, durations define a length of time, such as seconds, milliseconds, or microseconds.
* `std::chrono::time_point` class template, time points represent a specific moment in time.
* `std::chrono::system_clock`, `std::chrono::steady_clock`, and `std::chrono::high_resolution_clock` classes, clocks provide a way to obtain time points.

**Example**:
````c++
#include <iostream>
#include <chrono>

void myFunction() {
    // Simulate some work
    for (int i = 0; i < 100000000; ++i);
}

int main() {
    auto start = std::chrono::high_resolution_clock::now();
    myFunction();
    auto end = std::chrono::high_resolution_clock::now();

    auto duration = std::chrono::duration_cast<std::chrono::milliseconds>(end - start);
    std::cout << "Time taken: " << duration.count() << " milliseconds" << std::endl;

    return 0;
}
````

## `to_string`

`std::to_string` Converts a numeric argument to a `std::string`

Example:
````c++
std::to_string(1.2); // == "1.2"
std::to_string(12); // == "12"
````

## Type traits

Type traits are the features that allow to query and manipulate the properties of types at compile-time. 

* `std::is_same`: Checks if two types are the same.
* `std::is_base_of`: Checks if a type is a base class of another type.
* `std::is_class`: Checks if a type is a class.
* `std::is_enum`: Checks if a type is an enumeration.
* `std::is_function`: Checks if a type is a function.
* `std::is_arithmetic`: Checks if a type is an arithmetic type (e.g., int, float).
* `std::is_pointer`: Checks if a type is a pointer.
* `std::is_reference`: Checks if a type is a reference.
* `std::is_const`: Checks if a type is const.
* `std::is_volatile`: Checks if a type is volatile.

Use of type traits to modify types, such as

* `std::remove_const`: Removes const from a type.
* `std::remove_volatile`: Removes volatile from a type.
* `std::add_const`: Adds const to a type.
* `std::add_volatile`: Adds volatile to a type.


## `std::tie`
It is a function in that allows you to unpack a tuple (or a pair) and assign its elements to multiple variables. It is commonly used when working with functions that return multiple values, or when working with tuples that need to be decomposed into individual variables.

**Example**:
````c++
std::tie(var1, var2, ..., varN) = tuple;
````
Where var1, var2, ..., varN are the variables to be assigned, and tuple is the tuple that contains the values to be unpacked.
