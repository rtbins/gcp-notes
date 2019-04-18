# C++

## Introduction

C++ is a general purpose language with a bias towards systems programming that

- is a better C
- supports data abstraction
- supports object oriented programming
- supports generic programming

### Sample

```cpp
1. #include <iostream>
2.
3. int main()
4. {
5.   std::cout << "Hello World!";
6.   return 0;
7. }
```

- Line 1
  - is a pre-processor directive
  - instructs the compiler to locate the file that contains code for a library known as iostream
- Line 3
  - every C++ program must have a method known as main()
  - is the entry point for the application when the execution of program starts
  - int portion is the return type of the method
  - empty parenthesis indicates no arguments are for this function
- Line 5
  - std:: prefix to this command is a way of indicating that cout is `part of a namespace` known as std
  - `::` is is used to indicate that cout is part of the std namespace.
- Line 6
  - return statement is used to end a function when a value is expected to be sent back to a caller
  - the caller is the operating system and the value returned is an integer value of 0
  - If the program reaches this statement, returning a value of 0 is an indication to the operating system that the code executed successfully
- Line 7
  - closes out the body of the function main()
  - also used for other purposes like variable scope and visibility.
