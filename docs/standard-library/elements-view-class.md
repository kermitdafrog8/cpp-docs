---
title: elements_view class (C++ Standard Library)
description: "API reference for the Standard Template Library (STL) <ranges> elements_view class, which provides a view over the selected index into each tuple-like value in a range."
ms.date: 09/27/2022
f1_keywords: ["ranges/std::elements_view", "ranges/std::elements_view::base", "ranges/std::elements_view::begin", "ranges/std::elements_view::empty", "ranges/std::elements_view::end", "ranges/std::elements_view::size", "ranges/std::elements_view::operator bool", "ranges/std::elements_view::back", "ranges/std::elements_view::front", "ranges/std::elements_view::operator[]"]
helpviewer_keywords: ["std::ranges::elements_view [C++]", "std::ranges::elements_view::base [C++]", "std::ranges::elements_view::begin [C++]", "std::ranges::elements_view::empty [C++]", "std::ranges::elements_view::end [C++]", "std::ranges::elements_view::size [C++]", "std::ranges::elements_view::back [C++]", "std::ranges::elements_view::front [C++]", "std::ranges::elements_view::operator[] [C++]", "std::ranges::elements_view::operator bool [C++]"]
dev_langs: ["C++"]
---
# `elements_view` class (C++ Standard Library)

A view over the elements at a selected index in each tuple-like value in a range. For example, given a range of `std::tuple<string, int>`, create a view consisting of the `string` elements from each tuple.

## Syntax

```cpp
template<input_range V, size_t N>
class elements_view : public view_interface<elements_view<V, N>>;
```

### Template parameters

*`N`*\
The index of the element to select for the view.

*`V`*\
 The type of the underlying range. This type must satisfy `ranges::input_range`.

## View characteristics

For a description of the following entries, see [View class characteristics](view-classes.md#view-classes-characteristics)

| Characteristic | Description |
|--|--|
| **Range adaptor** | [`views::elements`](range-adaptors.md#elements) |
| **Underlying range** | Must satisfy [`input_range`](range-concepts.md#input_range) or higher |
| **Element type** | Same as the type of the indexed tuple element |
| **View iterator category** | [`forward_range`](range-concepts.md#forward_range), [`bidirectional_range`](range-concepts.md#bidirectional_range), or [`random_access_range`](range-concepts.md#random_access_range) |
| **Sized** | Only if the underlying range satisfies [`sized_range`](range-concepts.md#sized_range) |
| **Is `const`-iterable** | Only if the underlying range satisfies `const-iterable` |
| **Common range** | Only if the underlying range satisfies [`common_range`](range-concepts.md#common_range) |
| **Borrowed range** | Only if the underlying range satisfies [`borrowed_range`](range-concepts.md#borrowed_range) |

## Members

| **Member functions** | **Description** |
|--|--|
| [Constructors](#constructors)<sup>C++20</sup> | Construct a `elements_view`. |
| [`base`](#base)<sup>C++20</sup> | Get the underlying range. |
| [`begin`](#begin)<sup>C++20</sup> | Get an iterator to the first element. |
| [`end`](#end)<sup>C++20</sup> | Get the sentinel at the end of the view. |
| [`size`](#size)<sup>C++20</sup> | Get the number of elements in this view. The underlying range must satisfy [`sized_range`](range-concepts.md#sized_range). |
| **Inherited from [`view_interface`](view-interface.md)** | **Description** |
| [`back`](view-interface.md#back)<sup>C++20</sup> | Get the last element. |
| [`empty`](view-interface.md#empty)<sup>C++20</sup> | Test whether the `elements_view` is empty. |
| [`front`](view-interface.md#front)<sup>C++20</sup> | Get the first element. |
| [`operator[]`](view-interface.md#op_at)<sup>C++20</sup> | Get the element at the specified position. |
| [`operator bool`](view-interface.md#op_bool)<sup>C++20</sup> | Test whether the `elements_view` isn't empty. |

## Requirements

**Header:** `<ranges>` (since C++20)

**Namespace:** `std::ranges`

**Compiler Option:** [`/std:c++20`](../build/reference/std-specify-language-standard-version.md) or later is required.

## Remarks

The tuple-like types that you can use with `elements_view` are [`std::tuple`](tuple.md), [`std::pair`](pair-structure.md), and [`std::array`](array.md).

## Constructors

Construct an instance of a `elements_view`.

```cpp
1) constexpr elements_view(V base);
2) elements_view() requires std::default_initializable<V> = default;
```

### Parameters

*`base`*\
The underlying range.

For information about the template parameter type, see [Template parameters](#template-parameters).

### Return value

An `elements_view` instance.

### Remarks

The best way to create an `elements_view` is by using the [`elements`](range-adaptors.md#elements) range adaptor. Range adaptors are the intended way to create view classes. The view types are exposed in case you want to create your own custom view type.

1\) Create an `elements_view` from the specified view.\
2\) Default construct an `elements_view`.

### Example: `elements_view`

```cpp
// requires /std:c++20 or later
#include <array>
#include <iostream>
#include <map>
#include <ranges>
#include <vector>
#include <string>
#include <utility>

int main()
{
    // ========== work with a std::map

    std::map<std::string, int> cpp_standards
    {
        {"C++98", 1988},
        {"C++03", 2003},
        {"C++11", 2011},
        {"C++14", 2014},
        {"C++17", 2017},
        {"C++20", 2020}
    };

    // create an elements_view of all the string elements (<1>) from each tuple
    for (int const year : std::views::elements<1>(cpp_standards))
    {
        std::cout << year << ' '; // 2003 2011 2014 2017 1988 2020
    }

    std::cout << '\n';

    // Another way to call the range adaptor using pipe (|) syntax
    for (auto&& name : cpp_standards | std::views::elements<0>)
    {
        std::cout << name << ' '; // C++03 C++11 C++14 C++17 C++98 C++20
    }
    std::cout << '\n';

    // ========== working with arrays

    std::array<std::array<int, 4>, 3> arr = { {{0,1,2,3}, {4,5,6,7}, {8,9,10,11}} };
    for (int& fourth : arr | std::views::elements<3>)
    {
        std::cout << fourth << ' '; // 3 7 11
    }
    std::cout << '\n';

    // ========== work with a std::pair

    std::vector<std::pair<std::string, int>> windows
    {
        {"Windows 1.0", 1985},
        {"Windows 2.0", 1987},
        {"Windows 3.0", 1990},
        {"Windows 3.1", 1992},
        {"Windows NT 3.1", 1993},
        {"Windows 95", 1995},
        {"Windows NT 4.0", 1996},
        {"Windows 98", 1998},
        {"Windows 2000", 2000}
    };

    for (int year : std::views::elements<1>(windows))
    {
        std::cout << year << ' '; // 1985 1987 1990 1992 1993 1995 1996 1998 2000
    }
}
```

```output
2003 2011 2014 2017 1988 2020
C++03 C++11 C++14 C++17 C++98 c++20
3 7 11
1985 1987 1990 1992 1993 1995 1996 1998 2000
```

## `base`

Gets a copy of the underlying range.

```cpp
// Uses a copy constructor to return the underlying range
constexpr V base() const& requires std::copy_constructible<V>;

// Uses a move constructor to return the underlying range
constexpr V base() &&;
```

### Parameters

None.

### Return value

The underlying range.

## `begin`

Get an iterator to the first element in the `elements_view`.

```cpp
1) constexpr auto begin() requires (!Simple_view<V>);
2) constexpr auto begin() const requires range<const V>;
```

### Parameters

None.

### Return value

An iterator pointing at the first element in the `elements_view`.

:::image type="content" source="media/begin-end-sentinel.png" alt-text="Picture of a vector with the elements 10, 20, and 30. The first element contains 10 and is labeled begin(). The last element contains 30 and is labeled 'last element'. An imaginary box after the last element indicates the sentinel and is labeled end().":::

## `end`

Get the sentinel at the end of the `elements_view`

```cpp
1) constexpr auto end() requires (!Simple_view<V> && !ranges::common_range<V>);
2) constexpr auto end() requires (!Simple_view<V> && ranges::common_range<V>);
3) constexpr auto end() const requires ranges::range<const V>;
4) constexpr auto end() const requires ranges::common_range<const V>;
```

### Parameters

None.

### Return value

The sentinel that follows the last element in the `elements_view`:

:::image type="content" source="media/begin-end-sentinel.png" alt-text="Picture of a vector with the elements 10, 20, and 30. The first element contains 10 and is labeled begin(). The last element contains 30 and is labeled 'last element'. An imaginary box after the last element indicates the sentinel and is labeled end().":::

## `size`

Get the number of elements in the view.

```cpp
constexpr auto size() requires sized_range<V>;
constexpr auto size() const requires sized_range<const V>;
```

### Parameters

None.

### Return value

The number of elements in the `elements_view`.

### Remarks

The size of the view is only available if the underlying range is a [`sized_range`](range-concepts.md#sized_range), or in other words, bounded.

## See also

[`keys_view`](keys-view-class.md)\
[`values_view`](values-view-class.md)\
[View classes](view-classes.md)\
[`<ranges>`](ranges.md)
