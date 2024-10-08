# C++11

C++11 is an ISO standard published in the year 2011. 

To compile a code written in C++11, one need to use `-std=c++11` flag to the command line compilation string. If we want to compile a file `mainFile.cpp` then the command line string to compile this file will be 

    g++ -std=c++11 mainFile.cpp

## Automatic Type Deduction

With auto, you can let the compiler figure out the type of the variable, making your code more concise and easier to read.

Example:

    auto intVariable = 34;	// integer
    auto charVariable = 'k'; // character
    auto doubleVariable = 34.566; // double
    auto constCharVariable = "Hello"; // const char*

Advantages:
* Conciseness: With auto, you can skip explicit type declarations, making your code more concise.
* Readability: Your code becomes more readable, as the focus is on the variable's name and its purpose, rather than its type.
* Reduced typing errors: The compiler will detect type errors at compile-time, reducing the likelihood of runtime errors.

## Range-Based Loops

A Range-Based Loop is a type of loop that allows you to iterate over a range of values, such as the elements of a container or an array, without having to manually manage the loop counter or index.
Syntax:

        for (range_declaration : range_expression) {
            // statement(s)
        }

Example:

        // Print the values in `numbers` vector
        std::vector<int> numbers = {1, 2, 3, 4, 5};
        for (auto& num : numbers) {
            std::cout << num << " ";
        }

It is same as traditional for loop as implemented below.

        std::vector<int> numbers = {1, 2, 3, 4, 5};
        for(int i=0; i<=4; i++){
            std::cout << numbers[i] << " ";
        }

Advantages:
* Concise code: Range-Based Loops make your code more concise and easier to read.
* Less error-prone: You don't have to manually manage the loop counter or index, which reduces the risk of off-by-one errors or other mistakes.
* Type-safe: The type of the loop variable is automatically deduced by the compiler, which ensures type safety.

## Initializer Lists
An initializer list is a list of values enclosed in curly braces `{}`. It allows to initialize objects in a uniform way.

Example:

    int var1{24}; // initialize var1 with value 24
    int var1 = {24}; // initialize var1 with value 24
    char var2{'p'}; // initialize var2 with value 'p'
    char var2 = {'p'}; // initialize var2 with value 'p'
    std::vector<int> v{ 1, 2, 3, 4, 5 }; // initialize vector v with values 1, 2, 3, 4, 5
    std::vector<int> v = { 1, 2, 3, 4, 5 }; // initialize vector v with values 1, 2, 3, 4, 5
