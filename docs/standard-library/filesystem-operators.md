---
description: "Learn more about: <filesystem> operators"
title: "<filesystem> operators"
ms.date: 08/27/2026
f1_keywords: ["filesystem/std::filesystem::operator==", "filesystem/std::filesystem::operator!=", "filesystem/std::filesystem::operator<", "filesystem/std::filesystem::operator<=", "filesystem/std::filesystem::operator>", "filesystem/std::filesystem::operator>=", "filesystem/std::filesystem::operator/", "filesystem/std::filesystem::operator<<", "filesystem/std::filesystem::operator>>"]
helpviewer_keywords: ["std::filesystem::operator==", "std::filesystem::operator!=", "std::filesystem::operator<", "std::filesystem::operator<=", "std::filesystem::operator>", "std::filesystem::operator>=", "std::filesystem::operator/", "std::filesystem::operator<<", "std::filesystem::operator>>"]
---
# `<filesystem>` operators

These nonmember operators for [`std::filesystem::path`](../standard-library/path-class.md) are declared in the C++17 [`<filesystem>`](../standard-library/filesystem.md) header. The comparison operators compare two paths element by element in generic format by using `path::compare`, not as raw strings. Use the [`equivalent`](../standard-library/filesystem-functions.md#equivalent) function to determine whether two paths (for example, a relative path and an absolute path) refer to the same file or directory on disk.

> [!NOTE]
> This page documents the C++17 `std::filesystem` operators. For the historical prestandard operators that MSVC provided in `<experimental/filesystem>`, see [`<experimental/filesystem>` operators](../standard-library/experimental-filesystem-operators.md).

For more information, see [File System Navigation (C++)](../standard-library/file-system-navigation.md).

## Requirements

**Header:** `<filesystem>`

**Namespace:** `std::filesystem`

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

The function inserts the path into the stream as a quoted string. It returns `os << quoted(pval.string<Elem, Traits>())`.

## operator>>

```cpp
template <class Elem, class Traits>
basic_istream<Elem, Traits>& operator>>(basic_istream<Elem, Traits>& is, path& pval);
```

The function extracts a quoted string from the stream and assigns it to *`pval`*. It executes:

```cpp
basic_string<Elem, Traits> str;
is >> quoted(str);
pval = str;
return is;
```

## See also

[Header Files Reference](../standard-library/cpp-standard-library-header-files.md)\
[`<filesystem>`](../standard-library/filesystem.md)\
[File System Navigation (C++)](../standard-library/file-system-navigation.md)
