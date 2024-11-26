# C++14

C++14 is a version of the ISO/IEC 14882 standard for the C++ programming language. It is a small extension over C++11 standards.

* New language features
  * Function return type deduction
  * decltype(auto)
  * Variable templates
  * Generic lambdas
  * Lambda init-capture
  * Binary literals
  * Digit separators
  * Relaxed constexpr restrictions

## :pushpin: Function return type deduction

In order to induce return type deduction, the function must be declared with `auto` as the return type.

**Example**:
````c++
int variable = 1;
auto myFuncrtion(){ return x }; // Return type to be determined. Here, return type is 'int'.
````
* If there are multiple return statements, they must all deduce to the same type.
* If there is no return statement or if the argument of the return statement is a void expression then the deduced return type is void.
* Virtual functions cannot use return type deduction.

## :pushpin: decltype(auto)

It is used to deduce the return type of a function, and it preserves the value category (lvalue or rvalue) of the expression.
When you use decltype(auto) as the return type of a function, the type is deduced as follows:
* If the expression is an lvalue, the deduced type is T&, where T is the type of the expression.
* If the expression is an rvalue, the deduced type is T, where T is the type of the expression.

**Example**:
````c++
const int x = 0;
auto x1 = x; // int
decltype(auto) x2 = x; // const int
int y = 0;
int& y1 = y;
auto y2 = y1; // int
decltype(auto) y3 = y1; // int&
int&& z = 0;
auto z1 = std::move(z); // int
decltype(auto) z2 = std::move(z); // int&&
````

## :pushpin: Variable templates

In prior versions of C++, only functions, classes or type aliases could be templated. C++14 allows the creation of variables that are templated.

## :pushpin: Generic lambdas

In C++11, lambda function parameters need to be declared with concrete types. C++14 relaxes this requirement, allowing lambda function parameters to be declared with the auto type specifier.
**Example**
````c++
auto add = [](auto x, auto y){
    return x + y;
};

std::cout << add(2, 3) << std::endl; // Output: 5
````

[C++11 Lambda Expression](https://github.com/nsparag/Modern-CPP/blob/main/C++11/README.md#pushpin-lambda-expressions)

## :pushpin: Binary literals

It allows you to represent integers using binary notation.
**Example**:
````c++
int x = 0b1010;
````

The literal starts with `0b` to indicate that it's a binary number.

## :pushpin: Digit separators

It allows you to make your code more readable by separating digits in numeric literals.
**Example**:
````c++
int x = 1'234'567;
````
The digit separator can be used with any type of numeric literal, including integers, floating-point numbers, and hexadecimal literals.

## :pushpin: Relaxed constexpr restrictions

C++11 introduced the concept of a constexpr-declared function; a function which could be executed at compile time. Their return values could be consumed by operations that require constant expressions, such as an integer template argument. However, C++11 constexpr functions could only contain a single expression that is returned (as well as static_asserts and a small number of other declarations).

C++14 relaxes these restrictions. Constexpr-declared functions may now contain the following:
* Variable declarations without initializers.
* The conditional branching statements if and switch.
* Any looping statement, including range-based for.

[C++11 constexpr](https://github.com/nsparag/Modern-CPP/blob/main/C++11/README.md#pushpin--constexpr)
