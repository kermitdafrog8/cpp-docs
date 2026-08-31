---
description: "Learn more about: <experimental/filesystem> space_info Structure"
title: "<experimental/filesystem> space_info Structure"
ms.date: 08/27/2026
f1_keywords: ["filesystem/std::experimental::filesystem::space_info"]
---
# `<experimental/filesystem>` space_info Structure

> [!IMPORTANT]
> This article describes the prestandard `<experimental/filesystem>` implementation of `space_info`. It documents the historical File System Technical Specification ([ISO/IEC JTC 1/SC 22/WG 21 N4100](https://wg21.link/n4100)), not the C++17 `std::filesystem::space_info` structure. The experimental implementation was removed starting with MSVC version 14.51. For current code, use the standard [space_info Structure](../standard-library/space-info-structure.md).

Holds information about a volume.

## Syntax

```cpp
struct space_info
{
    uintmax_t capacity;
    uintmax_t free;
    uintmax_t available;
};
```

## Members

### Public Data Members

|Name|Description|
|----------|-----------------|
|`uintmax_t capacity`|Represents the total number of bytes that the volume can represent.|
|`uintmax_t free`|Represents the number of bytes that are not used to represent data on the volume.|
|`uintmax_t available`|Represents the number of bytes that are available to represent data on the volume.|

## Requirements

**Header:** \<experimental/filesystem>

**Namespace:** std::experimental::filesystem

## See also

[`<experimental/filesystem>`](../standard-library/experimental-filesystem.md)\
[`space`](../standard-library/experimental-filesystem-functions.md#space)
