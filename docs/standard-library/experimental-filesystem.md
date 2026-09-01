---
title: "<experimental/filesystem>"
description: "Describes the historical, prestandard MSVC experimental/filesystem header, which was removed starting in MSVC version 14.51."
ms.date: 08/27/2026
f1_keywords: ["<experimental/filesystem>", "filesystem/std::experimental::filesystem", "std::experimental::filesystem"]
no-loc: [experimental, filesystem, char, wchar_t, char16_t, char32_t]
---
# `<experimental/filesystem>`

> [!IMPORTANT]
> This article documents the historical, prestandard MSVC implementation of the File System Technical Specification that was provided in the `<experimental/filesystem>` header. It's **not** the C++17 `std::filesystem` library. This experimental implementation was **removed starting in MSVC version 14.51**. For current file system support, use the C++17 [`<filesystem>`](../standard-library/filesystem.md) header and the `std::filesystem` namespace.

Use this documentation only when maintaining older code that includes `<experimental/filesystem>` or uses the `std::experimental::filesystem` namespace. The reference links on this page stay within that historical API unless they're explicitly labeled as current C++17 documentation.

Before C++17 standardized file system support, MSVC shipped a prestandard implementation of the File System Technical Specification in the `<experimental/filesystem>` header, under the `std::experimental::filesystem` namespace. This article is retained for historical reference. New code should use the C++17 [`<filesystem>`](../standard-library/filesystem.md) header instead.

## Syntax

```cpp
#include <experimental/filesystem> // Removed starting in MSVC version 14.51
using namespace std::experimental::filesystem::v1;
```

## Visual Studio version history

- When Visual Studio 2017 was released, the C++17 `<filesystem>` header wasn't yet standardized. C++ in Visual Studio 2017 implemented the prestandard File System Technical Specification in the `<experimental/filesystem>` header.
- Visual Studio 2017 version 15.7 and later added support for the new C++17 `<filesystem>` standard. This C++17 implementation is a completely new implementation, incompatible with the previous `std::experimental` version.
- In Visual Studio 2019 version 16.3 and later, including `<filesystem>` provides only the new `std::filesystem`, and including `<experimental/filesystem>` provides only the old experimental implementation.
- The experimental implementation was removed starting in MSVC Build Tools version 14.51, which became the default toolset in Visual Studio 2026 version 18.6.

## Classes

|Name|Description|
|-|-|
|[`directory_entry` class](../standard-library/experimental-filesystem-directory-entry-class.md)|Describes an object that is returned by a `directory_iterator` or a `recursive_directory_iterator` and contains a `path`.|
|[`directory_iterator` class](../standard-library/experimental-filesystem-directory-iterator-class.md)|Describes an input iterator that sequences through the file names in a file-system directory.|
|[`filesystem_error` class](../standard-library/experimental-filesystem-error-class.md)|A base class for exceptions that are thrown to report a low-level system error.|
|[`path` class](../standard-library/experimental-filesystem-path-class.md)|Defines a class that stores an object of template type `String` that is suitable for use as a file name.|
|[`recursive_directory_iterator` class](../standard-library/experimental-filesystem-recursive-directory-iterator-class.md)|Describes an input iterator that sequences through the file names in a file-system directory. The iterator can also descend into subdirectories.|
|[`file_status` class](../standard-library/experimental-filesystem-file-status-class.md)|Wraps a `file_type`.|

## Structs

|Name|Description|
|-|-|
|[`space_info` structure](../standard-library/experimental-filesystem-space-info-structure.md)|Holds information about a volume.|

## Functions

[`<experimental/filesystem>` functions](../standard-library/experimental-filesystem-functions.md)

## Operators

[`<experimental/filesystem>` operators](../standard-library/experimental-filesystem-operators.md)

## Enumerations

|Name|Description|
|-|-|
|[`copy_options`](../standard-library/experimental-filesystem-enumerations.md#copy_options)|An enumeration that is used with `copy_file` and determines behavior if a destination file already exists.|
|[`directory_options`](../standard-library/experimental-filesystem-enumerations.md#directory_options)|An enumeration that specifies options for directory iterators.|
|[`file_type`](../standard-library/experimental-filesystem-enumerations.md#file_type)|An enumeration for file types.|
|[`perms`](../standard-library/experimental-filesystem-enumerations.md#perms)|A bitmask type used to convey permissions and options to permissions.|

## See also

[Current `<filesystem>` documentation](../standard-library/filesystem.md)
