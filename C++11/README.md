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
An rvalue is an expression that can appear on the right-hand side of an assignment. 
Examples of rvalue
````C++
int var = 2;    // 2 is rvalue
int variable = foo(); // function call is rvalue
````       
An rvalue reference is a type of reference that can bind to an rvalue. It is declared using the `&&` syntax. Rvalue references work by allowing us to bind to an rvalue and extend its lifetime. When an rvalue reference is created, it binds to the rvalue and prevents it from being destroyed until the reference goes out of scope.

Example: 
````C++
int main() {
    int&& r = 5; // r binds to the rvalue 5
    std::cout << r << std::endl; // prints 5
    return 0;
}
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

## Initializer Lists
An initializer list is a list of values enclosed in curly braces `{}`. It allows to initialize objects in a uniform way.

Example:
````C++
int var1{24}; // initialize var1 with value 24
int var1 = {24}; // initialize var1 with value 24
char var2{'p'}; // initialize var2 with value 'p'
char var2 = {'p'}; // initialize var2 with value 'p'
std::vector<int> v{ 1, 2, 3, 4, 5 }; // initialize vector v with values 1, 2, 3, 4, 5
std::vector<int> v = { 1, 2, 3, 4, 5 }; // initialize vector v with values 1, 2, 3, 4, 5
````
