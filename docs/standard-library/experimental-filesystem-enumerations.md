---
description: "Learn more about: <experimental/filesystem> enumerations"
title: "<experimental/filesystem> enumerations"
ms.date: 08/27/2026
f1_keywords: ["filesystem/std::experimental::filesystem::copy_options", "filesystem/std::experimental::filesystem::directory_options", "filesystem/std::experimental::filesystem::file_type", "filesystem/std::experimental::filesystem::perms"]
helpviewer_keywords: ["std::experimental::filesystem::copy_options", "std::experimental::filesystem::directory_options", "std::experimental::filesystem::file_type", "std::experimental::filesystem::perms"]
---
# `<experimental/filesystem>` enumerations

> [!IMPORTANT]
> The `<experimental/filesystem>` header and the `std::experimental::filesystem` namespace provided a prestandard implementation of the File System Technical Specification (TS). This documentation is retained for code written against MSVC's original filesystem implementation, which was removed starting in MSVC version 14.51. For new code, use the C++17 [`<filesystem>`](../standard-library/filesystem.md) header and the `std::filesystem` namespace instead. For the standard equivalents of these enumerations, see [`<filesystem>` enumerations](../standard-library/filesystem-enumerations.md).

This article documents the enumerations in the historical prestandard `std::experimental::filesystem` implementation.

## Requirements

**Header:** `<experimental/filesystem>`

**Namespace:** `std::experimental::filesystem`

## <a name="copy_options"></a> copy_options

An enumeration of bitmask values that is used with [copy](experimental-filesystem-functions.md#copy) and [copy_file](experimental-filesystem-functions.md#copy_file) functions to specify behavior.

### Syntax

```cpp
enum class copy_options {
   none = 0,
   skip_existing = 1,
   overwrite_existing = 2,
   update_existing = 4,
   recursive = 8,
   copy_symlinks = 16,
   skip_symlinks = 32,
   directories_only = 64,
   create_symlinks = 128,
   create_hard_links = 256
};
```

### Values

| Name | Description |
|------------|-----------------|
|`none`|Perform the default behavior for the operation.|
|`skip_existing`|Do not copy if the file already exists, do not report an error.|
|`overwrite_existing`|Overwrite the file if it already exists.|
|`update_existing`|Overwrite the file if it already exists and is older than the replacement.|
|`recursive`|Recursively copy subdirectories and their contents.|
|`copy_symlinks`|Copy symbolic links as symbolic links, instead of copying the files they point to.|
|`skip_symlinks`|Ignore symbolic links.|
|`directories_only`|Only iterate over directories, ignore files.|
|`create_symlinks`|Make symbolic links instead of copying files. An absolute path must be used as the source path unless the destination is the current directory.|
|`create_hard_links`|Make hard links instead of copying files.|

## <a name="directory_options"></a> directory_options

A bitmask enumeration that controls how directory iteration handles symbolic links to directories.

### Syntax

```cpp
enum class directory_options {
   none = 0,
   follow_directory_symlink = 1
};
```

### Values

|Name|Description|
|----------|-----------------|
|`none`|Default behavior: don't follow symbolic links to directories.|
|`follow_directory_symlink`|Follow symbolic links to directories rather than skipping them.|

## <a name="file_type"></a> file_type

An enumeration for file types.

### Syntax

```cpp
enum class file_type {
   not_found = -1,
   none = 0,
    regular,
    directory,
    symlink,
    block,
    character,
    fifo,
    socket,
    unknown
};
```

The underlying integer values of these enumerators aren't fixed, so don't depend on specific numeric values.

### Values

|Name|Description|
|----------|-----------------|
|`none`|The file type hasn't been evaluated yet, or an error occurred when evaluating it.|
|`not_found`|The file wasn't found.|
|`regular`|A regular file.|
|`directory`|A directory.|
|`symlink`|A symbolic link.|
|`block`|A block-special file. (Not used on Windows.)|
|`character`|A character-special file. (Not used on Windows.)|
|`fifo`|A FIFO or pipe file. (Not used on Windows.)|
|`socket`|A socket. (Not used on Windows.)|
|`unknown`|The file exists but its type can't be determined.|

## <a name="perms"></a> perms

A bitmask enumeration of file permission bits together with the control flags that the [`permissions`](experimental-filesystem-functions.md#permissions) function uses to decide how to apply those bits. On Windows, the supported permission values are essentially "read-only" and `all`. For a read-only file, none of the `*_write` bits are set. Otherwise, the `all` bit (0777) is set.

### Syntax

```cpp
enum class perms {// names for permissions
   none = 0,
   owner_read = 0400,  // S_IRUSR
   owner_write = 0200, // S_IWUSR
   owner_exec = 0100,  // S_IXUSR
   owner_all = 0700,   // S_IRWXU
   group_read = 040,   // S_IRGRP
   group_write = 020,  // S_IWGRP
   group_exec = 010,   // S_IXGRP
   group_all = 070,    // S_IRWXG
   others_read = 04,   // S_IROTH
   others_write = 02,  // S_IWOTH
   others_exec = 01,   // S_IXOTH
   others_all = 07,    // S_IRWXO
   all = 0777,
   set_uid = 04000,    // S_ISUID
   set_gid = 02000,    // S_ISGID
   sticky_bit = 01000, // S_ISVTX
   mask = 07777,
   unknown = 0xFFFF,
   add_perms = 0x10000,       // control flag
   remove_perms = 0x20000,    // control flag
   resolve_symlinks = 0x40000 // control flag
};
```

### Control flags

Unlike the C++17 `std::filesystem` implementation, which controls the `permissions` function with a separate `perm_options` enumeration, the prestandard TS implementation carries the control flags in `perms` itself.

|Name|Description|
|----------|-----------------|
|`add_perms`|Add the specified permission bits to the file's current permissions instead of replacing them.|
|`remove_perms`|Remove the specified permission bits from the file's current permissions.|
|`resolve_symlinks`|Resolve symbolic links so the permission change applies to the target file rather than the link.|

## See also

[`<experimental/filesystem>`](../standard-library/experimental-filesystem.md)\
[`<experimental/filesystem>` functions](../standard-library/experimental-filesystem-functions.md)\
[`<experimental/filesystem>` operators](../standard-library/experimental-filesystem-operators.md)
