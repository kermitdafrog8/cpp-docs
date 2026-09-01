---
description: "Learn more about: <experimental/filesystem> recursive_directory_iterator class"
title: "<experimental/filesystem> recursive_directory_iterator class"
ms.date: 08/27/2026
f1_keywords: ["filesystem/std::experimental::filesystem::recursive_directory_iterator"]
helpviewer_keywords: ["std::experimental::filesystem::recursive_directory_iterator"]
---

# `<experimental/filesystem>` `recursive_directory_iterator` class

> [!IMPORTANT]
> This article describes the `recursive_directory_iterator` class from the prestandard `<experimental/filesystem>` implementation of the ISO C++ Filesystem Technical Specification (N4100). This API isn't the same as the C++17 [`recursive_directory_iterator`](recursive-directory-iterator-class.md) class in `<filesystem>`. It uses different signatures, including a `noexcept` `increment` and a single-form `pop` with no `error_code` overload. The experimental implementation was removed starting with the Microsoft Visual C++ (MSVC) 14.51 toolset. New code should use the C++17 [`recursive_directory_iterator`](recursive-directory-iterator-class.md) class instead.

Describes an input iterator that sequences through the filenames in a directory, possibly descending into subdirectories recursively. For an iterator `X`, the expression `*X` returns an object of class `directory_entry` that wraps the filename and anything known about its status.

## Syntax

```cpp
class recursive_directory_iterator;
```

## Remarks

The class stores:

1. an object of type `stack<pair<directory_iterator, path>>`, called `mystack` here for the purposes of exposition, which represents the nest of directories to sequence

1. an object of type `directory_entry` called `myentry` here, which represents the current filename in the directory sequence

1. an object of type **`bool`**, called `no_push` here, which records whether recursive descent into subdirectories is disabled

1. an object of type `directory_options`, called `myoptions` here, which records the options established at construction

A default-constructed object of type `recursive_directory_iterator` has an end-of-sequence iterator at `mystack.top().first` and represents the end-of-sequence iterator. For example, given the directory `abc` with entries `def` (a directory), `def/ghi`, and `jkl`, the code:

```cpp
for (recursive_directory_iterator next(path("abc")), end; next != end; ++next)
    visit(next->path());
```

calls `visit` with the arguments `path("abc/def/ghi")` and `path("abc/jkl")`. You can qualify sequencing through a directory subtree in two ways:

1. A directory symlink is scanned only if you construct a `recursive_directory_iterator` with a `directory_options` argument whose value is `directory_options::follow_directory_symlink`.

1. If you call `disable_recursion_pending`, a subsequent directory encountered during an increment isn't recursively scanned.

### Constructors

|Constructor|Description|
|-|-|
|[recursive_directory_iterator](#recursive_directory_iterator)|Constructs a `recursive_directory_iterator`.|

### Member functions

|Member function|Description|
|-|-|
|[depth](#depth)|Returns `mystack.size() - 1`, so `pval` is at depth zero.|
|[disable_recursion_pending](#disable_recursion_pending)|Stores **`true`** in `no_push`.|
|[increment](#increment)|Advances to the next filename in sequence.|
|[options](#options)|Returns `myoptions`.|
|[pop](#pop)|Moves the iterator to the next entry at the next lower depth.|
|[recursion_pending](#recursion_pending)|Returns `!no_push`.|

### Operators

|Operator|Description|
|-|-|
|[operator!=](#op_neq)|Returns `!(*this == right)`.|
|[operator=](#op_as)|The defaulted member assignment operators behave as expected.|
|[operator==](#op_eq)|Returns **`true`** only if both **`*this`** and *right* are end-of-sequence iterators or both aren't end-of-sequence-iterators.|
|[operator*](#op_multiply)|Returns `myentry`.|
|[operator->](#op_cast)|Returns `&**this`.|
|[operator++](#op_increment)|Increments the `recursive_directory_iterator`.|

## Requirements

**Header:** `<experimental/filesystem>`

**Namespace:** `std::experimental::filesystem`

## <a name="depth"></a> recursive_directory_iterator::depth

Returns `mystack.size() - 1`, so `pval` is at depth zero.

```cpp
int depth() const;
```

## <a name="disable_recursion_pending"></a> recursive_directory_iterator::disable_recursion_pending

Stores **`true`** in `no_push`.

```cpp
void disable_recursion_pending();
```

## <a name="increment"></a> recursive_directory_iterator::increment

Advances to the next filename in sequence.

```cpp
recursive_directory_iterator& increment(error_code& ec) noexcept;
```

### Parameters

`ec`\
Specified error code.

### Remarks

The function attempts to advance to the next filename in the nested sequence. If successful, it stores that filename in `myentry`; otherwise it produces an end-of-sequence iterator.

## <a name="op_neq"></a> recursive_directory_iterator::operator!=

Returns `!(*this == right)`.

```cpp
bool operator!=(const recursive_directory_iterator& right) const;
```

### Parameters

*right*\
The `recursive_directory_iterator` for comparison.

## <a name="op_as"></a> recursive_directory_iterator::operator=

The defaulted member assignment operators behave as expected.

```cpp
recursive_directory_iterator& operator=(const recursive_directory_iterator&) = default;
recursive_directory_iterator& operator=(recursive_directory_iterator&&) = default;
```

### Parameters

*recursive_directory_iterator*\
The `recursive_directory_iterator` being copied into the `recursive_directory_iterator`.

## <a name="op_eq"></a> recursive_directory_iterator::operator==

Returns **`true`** only if both **`*this`** and *right* are end-of-sequence iterators or both aren't end-of-sequence iterators.

```cpp
bool operator==(const recursive_directory_iterator& right) const;
```

### Parameters

*right*\
The `recursive_directory_iterator` for comparison.

## <a name="op_multiply"></a> recursive_directory_iterator::operator*

Returns `myentry`.

```cpp
const directory_entry& operator*() const;
```

## <a name="op_cast"></a> recursive_directory_iterator::operator->

Returns `&**this`.

```cpp
const directory_entry * operator->() const;
```

## <a name="op_increment"></a> recursive_directory_iterator::operator++

Increments the `recursive_directory_iterator`.

```cpp
recursive_directory_iterator& operator++();

recursive_directory_iterator operator++(int);
```

### Parameters

*int*\
Dummy argument. It's a C++ convention used only to distinguish the postfix increment operator from the prefix increment operator. The C++ standard requires the postfix form to take a dummy int parameter.

### Remarks

The first member function calls `increment()`, then returns **`*this`**. The second member function makes a copy of the object, calls `increment()`, then returns the copy.

## <a name="options"></a> recursive_directory_iterator::options

Returns `myoptions`.

```cpp
directory_options options() const;
```

## <a name="pop"></a> recursive_directory_iterator::pop

Moves the iterator to the next entry at the next lower depth.

```cpp
void pop();
```

### Remarks

If `depth() == 0`, the object becomes an end-of-sequence iterator. Otherwise, the member function terminates scanning of the current (deepest) directory and resumes at the next lower depth.

## <a name="recursion_pending"></a> recursive_directory_iterator::recursion_pending

Returns `!no_push`.

```cpp
bool recursion_pending() const;
```

## <a name="recursive_directory_iterator"></a> recursive_directory_iterator::recursive_directory_iterator

Constructs a `recursive_directory_iterator`.

```cpp
recursive_directory_iterator() noexcept;
explicit recursive_directory_iterator(const path& pval,
    directory_options opts = directory_options::none);

recursive_directory_iterator(const path& pval,
    directory_options opts,
    error_code& ec) noexcept;
recursive_directory_iterator(const path& pval,
    error_code& ec) noexcept;
recursive_directory_iterator(const recursive_directory_iterator&) = default;
recursive_directory_iterator(recursive_directory_iterator&&) = default;
```

### Parameters

`pval`\
The specified path.

*error_code*\
The specified error code.

*opts*\
The specified directory options.

*recursive_directory_iterator*\
The `recursive_directory_iterator` of which the constructed `recursive_directory_iterator` is to be a copy.

### Remarks

The first constructor creates an end-of-sequence iterator. The second constructor stores **`false`** in `no_push` and *opts* in `myoptions`, then tries to open and read *pval* as a directory. If it succeeds, it initializes `mystack` and `myentry` to point to the first non-directory filename in the nested sequence. If it fails, it creates an end-of-sequence iterator.

The third and fourth constructors behave the same as the second, except that they report errors in *ec* instead of throwing an exception. The fourth constructor stores `directory_options::none` in `myoptions`. The default constructor behaves as expected.

## See also

[`<experimental/filesystem>`](../standard-library/experimental-filesystem.md)\
[`directory_entry` class](../standard-library/experimental-filesystem-directory-entry-class.md)
