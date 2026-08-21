---
description: "Learn how to declare and use the static subscript operator in C++."
title: "Static subscript operator (C++)"
ms.date: 08/19/2026
ai-usage: ai-assisted
helpviewer_keywords: ["static subscript operator [C++]", "static operator[] [C++]", "operator overloading [C++]"]
---

# Static subscript operator (C++)

In C++23, you can declare the subscript operator (`operator[]`) as a static member function. A static subscript operator doesn't have an implicit object parameter. Use it when a subscript operation doesn't need to access instance data.

Support for this feature was introduced in Visual Studio 2022 version 17.14 (MSVC 14.44). Use the `/std:c++latest` compiler option.

## Syntax

```cpp
static return-type operator[](parameter-list);
```

## Remarks

A static subscript operator doesn't have a `this` pointer. It can't be `virtual` or have a cv-qualifier (`const` or `volatile`) or ref-qualifier (`&`, `&&`).

You can call a static subscript operator by using an object of its class, which allows the object to use subscript syntax. You can also call it by using its qualified name. Taking its address produces a regular function pointer instead of a pointer-to-member function.

The feature-test macro `__cpp_static_call_operator` is defined when the static subscript operator is available.

## Example

The following example defines a stateless type that calculates powers of two and calls its static subscript operator in three ways:

```cpp
// Compile with: /std:c++latest

#include <iostream>

struct PowersOfTwo
{
    static constexpr unsigned int operator[](unsigned int exponent) noexcept
    {
        return 1U << exponent;
    }
};

int main()
{
    PowersOfTwo powers_of_two;

    std::cout << "powers_of_two[6] = " << powers_of_two[6] << std::endl;
    std::cout << "PowersOfTwo::operator[](4) = "
              << PowersOfTwo::operator[](4) << std::endl;

    auto power_function = &PowersOfTwo::operator[];
    std::cout << "power_function(5) = " << power_function(5) << std::endl;
}
```

```output
powers_of_two[6] = 64
PowersOfTwo::operator[](4) = 16
power_function(5) = 32
```

## See also

[Subscripting](subscripting.md)\
[Operator overloading](operator-overloading.md)\
[`static` members](static-members-cpp.md)\
[Proposal P2589R1: static `operator[]`](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2022/p2589r1.pdf)