---
description: "Learn more about: directory_entry Class"
title: "directory_entry Class"
ms.date: 08/28/2026
f1_keywords: ["filesystem/std::filesystem::directory_entry", "filesystem/std::filesystem::directory_entry::directory_entry", "filesystem/std::filesystem::directory_entry::operator=", "filesystem/std::filesystem::directory_entry::assign", "filesystem/std::filesystem::directory_entry::replace_filename", "filesystem/std::filesystem::directory_entry::refresh", "filesystem/std::filesystem::directory_entry::path", "filesystem/std::filesystem::directory_entry::operator const std::filesystem::path &", "filesystem/std::filesystem::directory_entry::exists", "filesystem/std::filesystem::directory_entry::is_block_file", "filesystem/std::filesystem::directory_entry::is_character_file", "filesystem/std::filesystem::directory_entry::is_directory", "filesystem/std::filesystem::directory_entry::is_fifo", "filesystem/std::filesystem::directory_entry::is_other", "filesystem/std::filesystem::directory_entry::is_regular_file", "filesystem/std::filesystem::directory_entry::is_socket", "filesystem/std::filesystem::directory_entry::is_symlink", "filesystem/std::filesystem::directory_entry::file_size", "filesystem/std::filesystem::directory_entry::hard_link_count", "filesystem/std::filesystem::directory_entry::last_write_time", "filesystem/std::filesystem::directory_entry::status", "filesystem/std::filesystem::directory_entry::symlink_status", "filesystem/std::filesystem::directory_entry::operator==", "filesystem/std::filesystem::directory_entry::operator<=>"]
helpviewer_keywords: ["std::filesystem::directory_entry", "std::filesystem::directory_entry::directory_entry", "std::filesystem::directory_entry::operator=", "std::filesystem::directory_entry::assign", "std::filesystem::directory_entry::replace_filename", "std::filesystem::directory_entry::refresh", "std::filesystem::directory_entry::path", "std::filesystem::directory_entry::operator const std::filesystem::path &", "std::filesystem::directory_entry::exists", "std::filesystem::directory_entry::is_block_file", "std::filesystem::directory_entry::is_character_file", "std::filesystem::directory_entry::is_directory", "std::filesystem::directory_entry::is_fifo", "std::filesystem::directory_entry::is_other", "std::filesystem::directory_entry::is_regular_file", "std::filesystem::directory_entry::is_socket", "std::filesystem::directory_entry::is_symlink", "std::filesystem::directory_entry::file_size", "std::filesystem::directory_entry::hard_link_count", "std::filesystem::directory_entry::last_write_time", "std::filesystem::directory_entry::status", "std::filesystem::directory_entry::symlink_status", "std::filesystem::directory_entry::operator==", "std::filesystem::directory_entry::operator<=>"]
ms.custom: devdivchpfy22
---

# `directory_entry` class

Describes an object that's returned by dereferencing a [`directory_iterator`](../standard-library/directory-iterator-class.md) or a [`recursive_directory_iterator`](../standard-library/recursive-directory-iterator-class.md). A `directory_entry` wraps a [`path`](../standard-library/path-class.md) and, as an optimization, can cache file attributes that are obtained while iterating a directory.

## Syntax

```cpp
class directory_entry;
```

## Remarks

A `directory_entry` object stores a [`path`](../standard-library/path-class.md). As an optimization, it can also cache the attributes and status of the file that the path refers to. The cached data is populated when the entry is created by a directory iterator, or when you call [`refresh`](#refresh). Observers such as [`file_size`](#file_size), [`last_write_time`](#last_write_time), [`status`](#status), and the various `is_*` predicates return the cached data when it's available; otherwise, they query the file system.

For more information and code examples, see [File System Navigation (C++)](../standard-library/file-system-navigation.md).

### Constructors

| Constructor | Description |
|-|-|
| [`directory_entry`](#directory_entry) | Constructs a `directory_entry`. |

### Member functions

| Member function | Description |
|-|-|
| [`assign`](#assign) | Replaces the stored path and refreshes the cached attributes. |
| [`exists`](#exists) | Checks whether the entry refers to an existing file. |
| [`file_size`](#file_size) | Gets the size, in bytes, of the referenced file. |
| [`hard_link_count`](#hard_link_count) | Gets the number of hard links to the referenced file. |
| [`is_block_file`](#is_block_file) | Checks whether the referenced file is a block special file. |
| [`is_character_file`](#is_character_file) | Checks whether the referenced file is a character special file. |
| [`is_directory`](#is_directory) | Checks whether the referenced file is a directory. |
| [`is_fifo`](#is_fifo) | Checks whether the referenced file is a named pipe (FIFO). |
| [`is_other`](#is_other) | Checks whether the referenced file is an other file. |
| [`is_regular_file`](#is_regular_file) | Checks whether the referenced file is a regular file. |
| [`is_socket`](#is_socket) | Checks whether the referenced file is a socket. |
| [`is_symlink`](#is_symlink) | Checks whether the referenced file is a symbolic link. |
| [`last_write_time`](#last_write_time) | Gets the time of the last data modification of the referenced file. |
| [`path`](#path) | Returns the stored path. |
| [`refresh`](#refresh) | Refreshes the cached file attributes. |
| [`replace_filename`](#replace_filename) | Replaces the filename of the stored path and refreshes the cached attributes. |
| [`status`](#status) | Gets the status of the referenced file, following symbolic links. |
| [`symlink_status`](#symlink_status) | Gets the status of the referenced file, without following symbolic links. |

### Operators

| Operator | Description |
|-|-|
| [`operator=`](#op_as) | Assigns to the `directory_entry`. |
| [`operator const path&`](#path_type) | Returns the stored path. |
| [`operator==`](#op_eq) | Checks whether two `directory_entry` objects are equal. |
| [`operator<=>`](#op_spaceship) | Performs a three-way comparison of two `directory_entry` objects. (C++20) |
| [`operator!=`](#op_neq) | Checks whether two `directory_entry` objects are unequal. An explicit member in C++17; supported through rewritten comparisons in C++20 and later. |
| [`operator<`](#op_lt) | Checks whether the `directory_entry` sorts before another `directory_entry`. An explicit member in C++17; supported through rewritten comparisons in C++20 and later. |
| [`operator<=`](#op_lteq) | Checks whether the `directory_entry` sorts before or equal to another `directory_entry`. An explicit member in C++17; supported through rewritten comparisons in C++20 and later. |
| [`operator>`](#op_gt) | Checks whether the `directory_entry` sorts after another `directory_entry`. An explicit member in C++17; supported through rewritten comparisons in C++20 and later. |
| [`operator>=`](#op_gteq) | Checks whether the `directory_entry` sorts after or equal to another `directory_entry`. An explicit member in C++17; supported through rewritten comparisons in C++20 and later. |

## Requirements

**Header:** `<filesystem>`

**Namespace:** `std::filesystem`

## <a name="directory_entry"></a> directory_entry

Constructs a `directory_entry`.

```cpp
directory_entry() noexcept = default;
directory_entry(const directory_entry&) = default;
directory_entry(directory_entry&&) noexcept = default;

explicit directory_entry(const std::filesystem::path& p);
directory_entry(const std::filesystem::path& p, std::error_code& ec);

~directory_entry();
```

### Parameters

*p*\
The path to the file that the entry refers to.

*ec*\
The output error code for the operation.

### Remarks

The default, copy, and move constructors behave as expected. The constructors that take a `path` store *p* and then call [`refresh`](#refresh) to populate the cached attributes. The overload that takes an `error_code` reports errors in *ec* instead of throwing, and clears the stored path if the refresh fails.

## <a name="op_as"></a> operator=

Assigns to the `directory_entry`.

```cpp
directory_entry& operator=(const directory_entry&) = default;
directory_entry& operator=(directory_entry&&) noexcept = default;
```

### Parameters

*right*\
The `directory_entry` to copy or move into this `directory_entry`.

### Remarks

The defaulted assignment operators behave as expected.

## <a name="assign"></a> assign

Replaces the stored path and refreshes the cached attributes.

```cpp
void assign(const std::filesystem::path& p);
void assign(const std::filesystem::path& p, std::error_code& ec);
```

### Parameters

*p*\
The new path to store.

*ec*\
The output error code for the operation.

### Remarks

Replaces the stored path with *p*, then calls [`refresh`](#refresh) to update the cached attributes. The overload that takes an `error_code` reports errors in *ec* instead of throwing.

## <a name="replace_filename"></a> replace_filename

Replaces the filename of the stored path and refreshes the cached attributes.

```cpp
void replace_filename(const std::filesystem::path& p);
void replace_filename(const std::filesystem::path& p, std::error_code& ec);
```

### Parameters

*p*\
The replacement filename.

*ec*\
The output error code for the operation.

### Remarks

Replaces the filename component of the stored path with *p*, as if by `path().replace_filename(p)`, then calls [`refresh`](#refresh). The overload that takes an `error_code` reports errors in *ec* instead of throwing.

## <a name="refresh"></a> refresh

Refreshes the cached file attributes.

```cpp
void refresh();
void refresh(std::error_code& ec) noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Remarks

Reads the attributes of the file that the stored path refers to and caches them in the `directory_entry`. Call `refresh` to update the cached data after the referenced file changes. The overload that takes an `error_code` reports errors in *ec* instead of throwing.

## <a name="path"></a> path

Returns the stored path.

```cpp
const std::filesystem::path& path() const noexcept;
```

## <a name="path_type"></a> operator const path&

Returns the stored path.

```cpp
operator const std::filesystem::path&() const noexcept;
```

## <a name="exists"></a> exists

Checks whether the entry refers to an existing file.

```cpp
bool exists() const;
bool exists(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the stored path refers to an existing file; otherwise, `false`. Equivalent to calling `filesystem::exists(status())`.

## <a name="is_block_file"></a> is_block_file

Checks whether the referenced file is a block special file.

```cpp
bool is_block_file() const;
bool is_block_file(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the referenced file is a block special file; otherwise, `false`. This function always returns `false` on Windows.

## <a name="is_character_file"></a> is_character_file

Checks whether the referenced file is a character special file.

```cpp
bool is_character_file() const;
bool is_character_file(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the referenced file is a character special file; otherwise, `false`. This function always returns `false` on Windows.

## <a name="is_directory"></a> is_directory

Checks whether the referenced file is a directory.

```cpp
bool is_directory() const;
bool is_directory(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the referenced file is a directory; otherwise, `false`. Equivalent to calling `filesystem::is_directory(status())`.

## <a name="is_fifo"></a> is_fifo

Checks whether the referenced file is a named pipe (FIFO).

```cpp
bool is_fifo() const;
bool is_fifo(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the referenced file is a FIFO; otherwise, `false`. This function always returns `false` on Windows.

## <a name="is_other"></a> is_other

Checks whether the referenced file is an other file.

```cpp
bool is_other() const;
bool is_other(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the referenced file exists but isn't a regular file, directory, or symbolic link; otherwise, `false`. Equivalent to calling `filesystem::is_other(status())`.

## <a name="is_regular_file"></a> is_regular_file

Checks whether the referenced file is a regular file.

```cpp
bool is_regular_file() const;
bool is_regular_file(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the referenced file is a regular file; otherwise, `false`. Equivalent to calling `filesystem::is_regular_file(status())`.

## <a name="is_socket"></a> is_socket

Checks whether the referenced file is a socket.

```cpp
bool is_socket() const;
bool is_socket(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the referenced file is a socket; otherwise, `false`. This function always returns `false` on Windows.

## <a name="is_symlink"></a> is_symlink

Checks whether the referenced file is a symbolic link.

```cpp
bool is_symlink() const;
bool is_symlink(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

`true` if the referenced file is a symbolic link; otherwise, `false`. Equivalent to calling `filesystem::is_symlink(symlink_status())`.

## <a name="file_size"></a> file_size

Gets the size, in bytes, of the referenced file.

```cpp
uintmax_t file_size() const;
uintmax_t file_size(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

The size, in bytes, of the referenced file, as if by `filesystem::file_size(path())`. Uses cached data when it's available.

## <a name="hard_link_count"></a> hard_link_count

Gets the number of hard links to the referenced file.

```cpp
uintmax_t hard_link_count() const;
uintmax_t hard_link_count(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

The number of hard links to the referenced file, as if by `filesystem::hard_link_count(path())`. Uses cached data when it's available.

## <a name="last_write_time"></a> last_write_time

Gets the time of the last data modification of the referenced file.

```cpp
file_time_type last_write_time() const;
file_time_type last_write_time(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

The time of the last data modification of the referenced file, as if by `filesystem::last_write_time(path())`. Uses cached data when it's available.

## <a name="status"></a> status

Gets the status of the referenced file, following symbolic links.

```cpp
file_status status() const;
file_status status(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

The status of the referenced file, as if by `filesystem::status(path())`. Uses cached data when it's available.

## <a name="symlink_status"></a> symlink_status

Gets the status of the referenced file, without following symbolic links.

```cpp
file_status symlink_status() const;
file_status symlink_status(std::error_code& ec) const noexcept;
```

### Parameters

*ec*\
The output error code for the operation.

### Return value

The symlink status of the referenced file, as if by `filesystem::symlink_status(path())`. Uses cached data when it's available.

## <a name="op_eq"></a> operator==

Checks whether two `directory_entry` objects are equal.

```cpp
bool operator==(const directory_entry& right) const noexcept;
```

### Parameters

*right*\
The `directory_entry` to compare against.

### Return value

Returns `path() == right.path()`.

## <a name="op_spaceship"></a> `operator<=>`

Performs a three-way comparison of two `directory_entry` objects.

```cpp
std::strong_ordering operator<=>(const directory_entry& right) const noexcept; // C++20
```

### Parameters

*right*\
The `directory_entry` to compare against.

### Return value

Returns `path() <=> right.path()`.

### Remarks

Available in C++20 and later. The compiler rewrites comparisons that use `operator<`, `operator<=`, `operator>`, or `operator>=` to use this operator. It rewrites comparisons that use `operator!=` to use [`operator==`](#op_eq).

## <a name="op_neq"></a> operator!=

Checks whether two `directory_entry` objects are unequal.

```cpp
bool operator!=(const directory_entry& right) const noexcept; // C++17
```

### Parameters

*right*\
The `directory_entry` to compare against.

### Return value

Returns `!(*this == right)`.

### Remarks

In C++17, this operator is an explicitly declared member function. In C++20 and later, an expression that uses `operator!=` is rewritten to use [`operator==`](#op_eq).

## <a name="op_lt"></a> `operator<`

Checks whether the `directory_entry` sorts before another `directory_entry`.

```cpp
bool operator<(const directory_entry& right) const noexcept; // C++17
```

### Parameters

*right*\
The `directory_entry` to compare against.

### Return value

Returns `path() < right.path()`.

### Remarks

In C++17, this operator is an explicitly declared member function. In C++20 and later, an expression that uses `operator<` is rewritten to use [`operator<=>`](#op_spaceship).

## <a name="op_lteq"></a> `operator<=`

Checks whether the `directory_entry` sorts before or equal to another `directory_entry`.

```cpp
bool operator<=(const directory_entry& right) const noexcept; // C++17
```

### Parameters

*right*\
The `directory_entry` to compare against.

### Return value

Returns `!(right < *this)`.

### Remarks

In C++17, this operator is an explicitly declared member function. In C++20 and later, an expression that uses `operator<=` is rewritten to use [`operator<=>`](#op_spaceship).

## <a name="op_gt"></a> `operator>`

Checks whether the `directory_entry` sorts after another `directory_entry`.

```cpp
bool operator>(const directory_entry& right) const noexcept; // C++17
```

### Parameters

*right*\
The `directory_entry` to compare against.

### Return value

Returns `right < *this`.

### Remarks

In C++17, this operator is an explicitly declared member function. In C++20 and later, an expression that uses `operator>` is rewritten to use [`operator<=>`](#op_spaceship).

## <a name="op_gteq"></a> `operator>=`

Checks whether the `directory_entry` sorts after or equal to another `directory_entry`.

```cpp
bool operator>=(const directory_entry& right) const noexcept; // C++17
```

### Parameters

*right*\
The `directory_entry` to compare against.

### Return value

Returns `!(*this < right)`.

### Remarks

In C++17, this operator is an explicitly declared member function. In C++20 and later, an expression that uses `operator>=` is rewritten to use [`operator<=>`](#op_spaceship).

## See also

[Header Files Reference](../standard-library/cpp-standard-library-header-files.md)\
[`<filesystem>`](../standard-library/filesystem.md)\
[File System Navigation (C++)](../standard-library/file-system-navigation.md)
