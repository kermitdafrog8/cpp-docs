---
description: "Learn more about: <experimental/filesystem> filesystem_error Class"
title: "<experimental/filesystem> filesystem_error Class"
ms.date: 08/27/2026
f1_keywords: ["filesystem/std::experimental::filesystem::filesystem_error"]
---
# `<experimental/filesystem>` filesystem_error Class

> [!IMPORTANT]
> This article describes the prestandard `<experimental/filesystem>` implementation of `filesystem_error`. It documents the historical File System Technical Specification ([ISO/IEC JTC 1/SC 22/WG 21 N4100](https://wg21.link/n4100)), not the C++17 `std::filesystem::filesystem_error` class. The experimental implementation was removed starting with MSVC version 14.51. For current code, use the standard [filesystem_error Class](../standard-library/filesystem-error-class.md).

A base class for all exceptions that are thrown to report a low-level system error.

## Syntax

```cpp
class filesystem_error : public system_error;
```

## Remarks

The class serves as the base class for all exceptions thrown to report an error in \<experimental/filesystem> functions. It stores an object of type `string`, called `mymesg` here for the purposes of exposition. It also stores two objects of type `path`, called `mypval1` and `mypval2`.

## Members

### Constructors

|Name|Description|
|-|-|
|[filesystem_error](#filesystem_error)|Constructs a `filesystem_error` message.|

### Functions

|Name|Description|
|-|-|
|[path1](#path1)|Returns `mypval1`|
|[path2](#path2)|Returns `mypval2`|
|[what](#what)|Returns a pointer to an `NTBS`.|

## Requirements

**Header:** \<experimental/filesystem>

**Namespace:** std::experimental::filesystem

## <a name="filesystem_error"></a> filesystem_error

The first constructor constructs its message from *what_arg* and *ec*. The second constructor also constructs its message from *pval1*, which it stores in `mypval1`. The third constructor also constructs its message from *pval1*, which it stores in `mypval1`, and from *pval2*, which it stores in `mypval2`.

```cpp
filesystem_error(const string& what_arg,
    error_code ec);

filesystem_error(const string& what_arg,
    const path& pval1,
    error_code ec);

filesystem_error(const string& what_arg,
    const path& pval1,
    const path& pval2,
    error_code ec);
```

### Parameters

*what_arg*\
Specified message.

*ec*\
Specified error code.

*mypval1*\
Further specified message parameter.

*mypval2*\
Further specified message parameter.

## <a name="path1"></a> path1

The member function returns `mypval1`

```cpp
const path& path1() const noexcept;
```

## <a name="path2"></a> path2

The member function returns `mypval2`

```cpp
const path& path2() const noexcept;
```

## <a name="what"></a> what

The member function returns a pointer to an `NTBS`, preferably composed from `runtime_error::what()`, `system_error::what()`, `mymesg`, `mypval1.native_string()`, and `mypval2.native_string()`.

```cpp
const char *what() const noexcept;
```

## See also

[`<experimental/filesystem>`](../standard-library/experimental-filesystem.md)\
[`path` class](../standard-library/experimental-filesystem-path-class.md)
