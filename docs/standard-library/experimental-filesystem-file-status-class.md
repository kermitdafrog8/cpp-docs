---
title: "<experimental/filesystem> file_status Class"
description: "Learn more about: <experimental/filesystem> file_status Class"
ms.date: 08/27/2026
f1_keywords: ["filesystem/std::experimental::filesystem::file_status", "filesystem/std::experimental::filesystem::file_status::operator=", "filesystem/std::experimental::filesystem::file_status::type", "filesystem/std::experimental::filesystem::file_status::permissions"]
helpviewer_keywords: ["std::experimental::filesystem::file_status", "std::experimental::filesystem::file_status::operator=", "std::experimental::filesystem::file_status::type", "std::experimental::filesystem::file_status::permissions"]
---
# `<experimental/filesystem>` file_status class

> [!IMPORTANT]
> This article describes the prestandard `<experimental/filesystem>` implementation of `file_status`. It documents the historical File System Technical Specification ([ISO/IEC JTC 1/SC 22/WG 21 N4100](https://wg21.link/n4100)), not the C++17 `std::filesystem::file_status` class. The experimental implementation was removed starting with MSVC version 14.51. For current code, use the standard [file_status Class](../standard-library/file-status-class.md).

Wraps a [`file_type`](../standard-library/experimental-filesystem-enumerations.md#file_type) and file [`perms`](../standard-library/experimental-filesystem-enumerations.md#perms).

## Syntax

```cpp
class file_status;
```

### Constructors

|Constructor|Description|
|-|-|
|[file_status](#file_status)|Constructs a wrapper for [`file_type`](../standard-library/experimental-filesystem-enumerations.md#file_type) and file [`perms`](../standard-library/experimental-filesystem-enumerations.md#perms).|

### Member functions

|Member function|Description|
|-|-|
|[type](#type)|Gets or sets the `file_type`.|
|[permissions](#permissions)|Gets or sets the file permissions.|

### Operators

|Operator|Description|
|-|-|
|[operator=](#op_as)|The defaulted member assignment operators behave as expected.|

## Requirements

**Header:** \<experimental/filesystem>

**Namespace:** std::experimental::filesystem

## <a name="file_status"></a> file_status::file_status

Constructs a wrapper for [`file_type`](../standard-library/experimental-filesystem-enumerations.md#file_type) and file [`perms`](../standard-library/experimental-filesystem-enumerations.md#perms).

```cpp
explicit file_status(
   file_type ftype = file_type::none,
   perms mask = perms::unknown) noexcept;

file_status(const file_status&) noexcept = default;

file_status(file_status&&) noexcept = default;

~file_status() noexcept = default;
```

### Parameters

*ftype*\
Specified `file_type`, defaults to `file_type::none`.

*mask*\
Specified file `perms`, defaults to `perms::unknown`.

*file_status*\
The stored object.

## <a name="op_as"></a> file_status::operator=

The defaulted member assignment operators behave as expected.

```cpp
file_status& operator=(const file_status&) noexcept = default;
file_status& operator=(file_status&&) noexcept = default;
```

### Parameters

*file_status*\
The [file_status](../standard-library/experimental-filesystem-file-status-class.md) being copied into the `file_status`.

## <a name="type"></a> type

Gets or sets the `file_type`.

```cpp
file_type type() const noexcept;
void type(file_type ftype) noexcept;
```

### Parameters

*ftype*\
Specified `file_type`.

## <a name="permissions"></a> permissions

Gets or sets the file permissions.

Use the setter to make a file `readonly` or remove the `readonly` attribute.

```cpp
perms permissions() const noexcept;
void permissions(perms mask) noexcept;
```

### Parameters

*mask*\
Specified `perms`.

## See also

[`<experimental/filesystem>`](../standard-library/experimental-filesystem.md)\
[`path` class](../standard-library/experimental-filesystem-path-class.md)
