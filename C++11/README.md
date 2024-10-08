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
