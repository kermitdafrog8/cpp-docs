---
description: "Learn how to declare and use the static function call operator in C++."
title: "Static function call operator (C++23)"
ms.date: 08/26/2026
ai-usage: ai-assisted
helpviewer_keywords: ["static function call operator [C++]", "static operator() [C++]", "operator overloading [C++]"]
---

# Static function call operator (C++)

In C++23, you can declare the function call operator (`operator()`) as a static member function. A static function call operator doesn't have an implicit object parameter. Use it when a callable type doesn't need to access instance data.

Support for this feature was introduced in Visual Studio 2022 version 17.14 (MSVC 14.44). Use the `/std:c++latest` or `/std:c++23preview` compiler option.

## Syntax

```cpp
static return-type operator()(parameter-list);
```

You can also declare the function call operator generated for a lambda expression as static:

```cpp
[](parameter-list) static { function-body }
[] static { function-body }
```

## Remarks

A static function call operator doesn't have a `this` pointer. It can't be `virtual` or have a cv-qualifier (`const` or `volatile`) or ref-qualifier (`&`, `&&`).

You can call a static function call operator by using an object of its class, which allows the object to work as a function object. You can also call it by using its qualified name. Taking its address produces a regular function pointer instead of a pointer-to-member function.

A lambda expression can specify `static` after its parameter list. When the lambda has no parameters, you can omit the empty parameter list and specify `static` after the lambda introducer (`[]`). A static lambda can't have captures or be declared `mutable`. Declaring a captureless lambda doesn't make it static automatically; you must specify `static` to opt in to this behavior.

The feature-test macro `__cpp_static_call_operator` is defined when the static function call operator is available.

## Example

The following example defines a stateless function object and calls its static function call operator in three ways. It also defines a static lambda expression and calls it:

```cpp
// Compile with: /std:c++latest

#include <iostream>

struct Multiply
{
    static constexpr int operator()(int left, int right) noexcept
    {
        return left * right;
    }
};

int main()
{
    Multiply multiply;

    std::cout << "multiply(6, 7) = " << multiply(6, 7) << std::endl;
    std::cout << "Multiply::operator()(3, 4) = "
              << Multiply::operator()(3, 4) << std::endl;

    auto multiply_function = &Multiply::operator();
    std::cout << "multiply_function(5, 5) = "
              << multiply_function(5, 5) << std::endl;

    // A static lambda expression that doubles its argument
    auto twice = [](int value) static noexcept
    {
        return value * 2;
    };

    std::cout << "twice(21) = " << twice(21) << std::endl;
}
```

```output
multiply(6, 7) = 42
Multiply::operator()(3, 4) = 12
multiply_function(5, 5) = 25
twice(21) = 42
```

## See also

[Function call](function-call-cpp.md)\
[Function-call operator](function-call-operator-parens.md)\
[Operator overloading](operator-overloading.md)\
[`static` members](static-members-cpp.md)\
[Proposal P1169R4: static `operator()`](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2022/p1169r4.html)