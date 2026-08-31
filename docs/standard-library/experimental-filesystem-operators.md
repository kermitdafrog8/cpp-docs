---
description: "Learn more about: <experimental/filesystem> operators"
title: "<experimental/filesystem> operators"
ms.date: 08/27/2026
f1_keywords: ["filesystem/std::experimental::filesystem::operator==", "filesystem/std::experimental::filesystem::operator!=", "filesystem/std::experimental::filesystem::operator<", "filesystem/std::experimental::filesystem::operator<=", "filesystem/std::experimental::filesystem::operator>", "filesystem/std::experimental::filesystem::operator>=", "filesystem/std::experimental::filesystem::operator/", "filesystem/std::experimental::filesystem::operator<<", "filesystem/std::experimental::filesystem::operator>>"]
helpviewer_keywords: ["std::experimental::filesystem::operator==", "std::experimental::filesystem::operator!=", "std::experimental::filesystem::operator<", "std::experimental::filesystem::operator<=", "std::experimental::filesystem::operator>", "std::experimental::filesystem::operator>=", "std::experimental::filesystem::operator/", "std::experimental::filesystem::operator<<", "std::experimental::filesystem::operator>>"]
---
# `<experimental/filesystem>` operators

> [!IMPORTANT]
> The `<experimental/filesystem>` header and the `std::experimental::filesystem` namespace provided a prestandard implementation of the File System Technical Specification (TS). This documentation is retained for code written against MSVC's original filesystem implementation, which was removed starting in MSVC version 14.51. For new code, use the C++17 [`<filesystem>`](../standard-library/filesystem.md) header and the `std::filesystem` namespace instead. For the standard equivalents of these operators, see [`<filesystem>` operators](../standard-library/filesystem-operators.md).

These nonmember operators for `std::experimental::filesystem::path` are declared in the historical `<experimental/filesystem>` header. The comparison operators compare two paths element by element in generic format by using `path::compare`, not as raw strings. Use the [`equivalent`](../standard-library/experimental-filesystem-functions.md#equivalent) function to determine whether two paths (for example, a relative path and an absolute path) refer to the same file or directory on disk.

For more information, see [File System Navigation (C++)](../standard-library/file-system-navigation.md).

## Requirements

**Header:** `<experimental/filesystem>`

**Namespace:** `std::experimental::filesystem`

## operator==

```cpp
bool operator==(const path& left, const path& right) noexcept;
```

The function returns `left.compare(right) == 0`.

## operator!=

```cpp
bool operator!=(const path& left, const path& right) noexcept;
```

The function returns `!(left == right)`.

## operator<

```cpp
bool operator<(const path& left, const path& right) noexcept;
```

The function returns `left.compare(right) < 0`.

## operator<=

```cpp
bool operator<=(const path& left, const path& right) noexcept;
```

The function returns `!(right < left)`.

## operator>

```cpp
bool operator>(const path& left, const path& right) noexcept;
```

The function returns `right < left`.

## operator>=

```cpp
bool operator>=(const path& left, const path& right) noexcept;
```

The function returns `!(left < right)`.

## operator/

```cpp
path operator/(const path& left, const path& right);
```

The function returns `path(left) /= right`.

## operator<<

```cpp
template <class Elem, class Traits>
basic_ostream<Elem, Traits>& operator<<(basic_ostream<Elem, Traits>& os, const path& pval);
```

The function inserts the path's string representation into the stream. It returns `os << pval.string<Elem, Traits>()`.

## operator>>

```cpp
template <class Elem, class Traits>
basic_istream<Elem, Traits>& operator>>(basic_istream<Elem, Traits>& is, path& pval);
```

The function extracts a string from the stream and assigns it to *`pval`*. It executes:

```cpp
basic_string<Elem, Traits> str;
is >> str;
pval = str;
return is;
```

## See also

[`<experimental/filesystem>`](../standard-library/experimental-filesystem.md)\
[`<experimental/filesystem>` functions](../standard-library/experimental-filesystem-functions.md)\
[`<experimental/filesystem>` enumerations](../standard-library/experimental-filesystem-enumerations.md)
