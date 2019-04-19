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

### Portability, Compiling and linking

- A portable application can be compiled across platforms(OS, CPU architecture etc) and compilers without major changes
- Compilers converts the code into an machine executable form
- After compilers linkers are invoked
- linkers takes object files, which are part of app's executable code, and link them together in application .exe file
- linkers ensures all promises of the compiler are kept during linking proces (e.g. it needs to include iostream library as a part of .exe)

### Code formatting

- it's a case sensitive language
- `preprocessor directives` instructs the compiler to execute task prior to compiling source code
- `using` to indicate which namespace to use in the fiel
- c++ compiler ignores whitespaces, with a small exception concerning if statements

C++ statements

- declaration: variables and constants
- assignments
- preprocessor directives
- comments
- function declaration
- executable statements (`cout<<"hello world";`)

## Data Types

### Numeric Data

- Numeric data types are binary based and are not flexible as their base 10 counterparts (wrt domain `(-inf, inf)`)
- type name starting with `__` character are considered as non-standard types

| Type Name          | Bytes | Alias                              | Range                                                   |
|--------------------|-------|------------------------------------|---------------------------------------------------------|
| int                | 4     | signed                             | –2,147,483,648 to 2,147,483,647                         |
| unsigned int       | 4     | unsigned                           | 0 to 4,294,967,295                                      |
| __int8             | 1     | char                               | -128 to 127                                             |
| unsigned __int8    | 1     | unsigned char                      | 0 to 255                                                |
| __int16            | 2     | short, short int, signed short int | –32,768 to 32,767                                       |
| unsigned __int16   | 2     | unsigned short, unsigned short int | 0 to 65,535                                             |
| __int32            | 4     | signed, signed int, int            | –2,147,483,648 to 2,147,483,647                         |
| unsigned __int32   | 4     | unsigned, unsigned int             | 0 to 4,294,967,295                                      |
| __int64            | 8     | long long, signed long long        | –9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| unsigned __int64   | 8     | unsigned long long                 | 0 to 18,446,744,073,709,551,615                         |
| short              | 2     | short int, signed short int        | -32,768 to 32,767                                       |
| unsigned short     | 2     | unsigned short int                 | 0 to 65,535                                             |
| long               | 4     | long int, signed long int          | –2,147,483,648 to 2,147,483,647                         |
| unsigned long      | 4     | unsigned long int                  | 0 to 4,294,967,295                                      |
| long long          | 8     | none                               | –9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| unsigned long long | 8     | none                               | 0 to 18,446,744,073,709,551,615                         |
| float              | 4     | none                               | 3.4E +/- 38 (7 digits)                                  |
| double             | 8     | none                               | 1.7E +/- 308 (15 digits)                                |
| long double        | 8     | none                               | 1.7E +/- 308 (15 digits)                                |

### Character Data

- charater data is usually represented as numeric data
- this representation depends on a pirticular computer and determined by the locale settings
- `wchar_t` expands the available characters across different language

| Type Name                       | Bytes  | Alias     | Range                                                           |
|---------------------------------|--------|-----------|-----------------------------------------------------------------|
| char                            | 1      | none      | –128 to 127 by default 0 to 255 when compiled by using /J       |
| signed char                     | 1      | none      | -128 to 127                                                     |
| unsigned char                   | 1      | none      | 0 to 255                                                        |
| wchar_t, char16_t, and char32_t | 2 or 4 | __wchar_t | 0 to 65,535 (wchar_t & char16_t), 0 to 4,294,967,295 (char32_t) |

### Other Types

- bool {true, false}
- enumeration, limits the domain of available values, e.g. days of week

### Choosing Data Types

- choosing correct data type makes data representation correct and efficient
- use double rather than float to get better accuracy for money values
- use `wchar_t` to represent characters beyond `ASCII`, e.g. Japanese kanji

## Variables and Constants

- are case-sensitive
- un-initialized variables can't be used
- can't start the identifier with a digit or special character (except `_`)
- reserved keywords can't be used
- const enforces compiler t=from mutating a variable
- const variable must be assigned at the time of declaration

## Type Conversion

- casting refers to converting one datatype to other
- some casting are not possible
- some are possible and may result in data loss
- `implicit casting` in cpp (int data to long, `widening /expanding conversion`)
- implicit casting can cause loss of precision, fractional part
