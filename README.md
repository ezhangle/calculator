calculator
==========
[![Build Status](https://travis-ci.org/kimwalisch/calculator.svg)](https://travis-ci.org/kimwalisch/calculator)

calculator is a simple C++ operator-precedence parser with
infix notation for integer arithmetic expressions. ```calculator.hpp```
is a header-only library that compiles with any C++ compiler. I
wrote it because I needed a portable and GPL compatible calculator
for 64-bit integers and could not find one elsewhere.

### Supported operators
calculator.hpp uses the same operator precedence and associativity as
the C++ programming language and also supports the power operator.

<table>
  <tr align="center">
    <td><b>Operator</b></td>
    <td><b>Description</b></td>
  </tr>
  <tr align="left">
    <td>|</td>
    <td>Bitwise Inclusive OR</td>
  </tr>
  <tr align="left">
    <td>^</td>
    <td>Bitwise Exclusive OR</td>
  </tr>
  <tr align="left">
    <td>&</td>
    <td>Bitwise AND</td>
  </tr>
  <tr align="left">
    <td>~</td>
    <td>Unary Complement </td>
  </tr>
  <tr align="left">
    <td>&lt;&lt;</td>
    <td>Shift Left</td>
  </tr>
  <tr align="left">
    <td>&gt;&gt;</td>
    <td>Shift Right</td>
  </tr>
  <tr align="left">
    <td>+</td>
    <td>Addition</td>
  </tr>
  <tr align="left">
    <td>-</td>
    <td>Subtraction</td>
  </tr>
  <tr align="left">
    <td>*</td>
    <td>Multiplication</td>
  </tr>
  <tr align="left">
    <td>/</td>
    <td>Division</td>
  </tr>
  <tr align="left">
    <td>%</td>
    <td>Modulo</td>
  </tr>
  <tr align="left">
    <td>**</td>
    <td>Raise to power</td>
  </tr>
</table>

### C++ API
```C++
int calculator::eval(const std::string& expression);
int calculator::eval(char c);

template <typename T> T calculator::eval<T>(const std::string& expression);
template <typename T> T calculator::eval<T>(char c);

// calculator throws a calculator::error
// exception if an error occurs
class calculator::error;
```

### How to use it
The following C++ code snippet shows how to use calculator.hpp, if the
expression string is not a valid integer arithmetic expression a
```calculator::error``` exception is thrown.

```C++
#include "calculator.hpp"
#include <iostream>

int main()
{
  try
  {
    int result = calculator::eval("(0 + ~(0xFF & 1000)*3) / -2");
    std::cout << result << std::endl;

    // 64-bit arithmetic
    long long r64 = calculator::eval<long long>("2**60");
    std::cout << r64 << std::endl;
  }
  catch (calculator::error& e)
  {
    std::cerr << e.what() << std::endl;
  }
  return 0;
}
```
