# C++11

C++11 is an ISO standard published in the year 2011. 

To compile a code written in C++11, one need to use `-std=c++11` flag to the command line compilation string. If we want to compile a file `mainFile.cpp` then the command line string to compile this file will be 
````C++
g++ -std=c++11 mainFile.cpp
````
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

## `default` function

## `delete` function

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
## Override
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
## Move Assignment Operators

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

## `constexpr` and literal types
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

## nullptr
`nullptr` is a keyword in C++ that was introduced in C++11 as a replacement for the older `NULL` macro. 
`nullptr` itself is of type `std::nullptr_t` and can be implicitly converted into pointer types, and unlike `NULL`, not convertible to integral types except bool.

**Example**:
````c++
int* ptr = nullptr;
````
## long long
A data type that represents a 64-bit integer value.

## char16_t and char32_t
Two new character types that were introduced to support Unicode characters. They represent 16 bit and 32 bit characters values respectively.

Example:
````c++
char16_t c1 = u'\u1234'; // char16_t
char32_t c2 = U'\U00012345'; // char32_t
````

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




**Syntax**:
````c++

````

**Example**:
````c++

````
