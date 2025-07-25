---
title: "vprintf_s, _vprintf_s_l, vwprintf_s, _vwprintf_s_l"
description: "Learn more about: vprintf_s, _vprintf_s_l, vwprintf_s, _vwprintf_s_l"
ms.date: 3/9/2021
api_name: ["_vwprintf_s_l", "vwprintf_s", "_vprintf_s_l", "vprintf_s"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["STDIO/vprintf_s", "STDIO/_vprintf_s_l", "CORECRT_WSTDIO/vwprintf_s", "CORECRT_WSTDIO/_vwprintf_s_l", "TCHAR/_vtprintf_s", "TCHAR/_vtprintf_s_l", "vprintf_s", "_vprintf_s_l", "vwprintf_s", "_vwprintf_s_l", "_vtprintf_s", "_vtprintf_s_l"]
helpviewer_keywords: ["vwprintf_s_l function", "_vwprintf_s_l function", "vwprintf_s function", "_vtprintf_s_l function", "vprintf_s_l function", "vtprintf_s_l function", "_vtprintf_s function", "vtprintf_s function", "_vprintf_s_l function", "formatted text [C++]", "vprintf_s function"]
---
# `vprintf_s`, `_vprintf_s_l`, `vwprintf_s`, `_vwprintf_s_l`

Writes formatted output by using a pointer to a list of arguments. These versions of [`vprintf`, `_vprintf_l`, `vwprintf`, `_vwprintf_l`](vprintf-vprintf-l-vwprintf-vwprintf-l.md) have security enhancements, as described in [Security features in the CRT](../security-features-in-the-crt.md).

## Syntax

```C
int vprintf_s(
   const char *format,
   va_list argptr
);
int _vprintf_s_l(
   const char *format,
   _locale_t locale,
   va_list argptr
);
int vwprintf_s(
   const wchar_t *format,
   va_list argptr
);
int _vwprintf_s_l(
   const wchar_t *format,
   _locale_t locale,
   va_list argptr
);
```

### Parameters

*`format`*\
Format specification.

*`argptr`*\
Pointer to list of arguments.

*`locale`*\
The locale to use.

For more information, see [Format specification syntax](../format-specification-syntax-printf-and-wprintf-functions.md).

## Return value

**`vprintf_s`** and **`vwprintf_s`** return the number of characters written, not including the terminating null character, or a negative value if an output error occurs. If *`format`* is a null pointer, or if the format string contains invalid formatting characters, the invalid parameter handler is invoked, as described in [Parameter validation](../parameter-validation.md). If execution is allowed to continue, the functions return -1 and set `errno` to `EINVAL`.

For information on these and other error codes, see [`errno`, `_doserrno`, `_sys_errlist`, and `_sys_nerr`](../errno-doserrno-sys-errlist-and-sys-nerr.md).

## Remarks

Each of these functions takes a pointer to an argument list, then formats and writes the given data to `stdout`.

The secure versions of these functions differ from `vprintf` and `vwprintf` only in that the secure versions check that the format string contains valid formatting characters.

**`vwprintf_s`** is the wide-character version of **`vprintf_s`**; the two functions behave identically if the stream is opened in ANSI mode. **`vprintf_s`** doesn't currently support output into a UNICODE stream.

The versions of these functions with the `_l` suffix are identical except that they use the locale parameter passed in instead of the current thread locale.

> [!IMPORTANT]
> Ensure that *`format`* is not a user-defined string. For more information, see [Avoiding buffer overruns](/windows/win32/SecBP/avoiding-buffer-overruns).
> Starting in Windows 10 version 2004 (build 19041), the `printf` family of functions prints exactly representable floating point numbers according to the IEEE 754 rules for rounding. In previous versions of Windows, exactly representable floating point numbers ending in '5' would always round up. IEEE 754 states that they must round to the closest even digit (also known as "Banker's Rounding"). For example, both `printf("%1.0f", 1.5)` and `printf("%1.0f", 2.5)` should round to 2. Previously, 1.5 would round to 2 and 2.5 would round to 3. This change only affects exactly representable numbers. For example, 2.35 (which, when represented in memory, is closer to 2.35000000000000008) continues to round up to 2.4. Rounding done by these functions now also respects the floating point rounding mode set by [`fesetround`](fegetround-fesetround2.md). Previously, rounding always chose `FE_TONEAREST` behavior. This change only affects programs built using Visual Studio 2019 version 16.2 and later. To use the legacy floating point rounding behavior, link with [`legacy_stdio_float_rounding.obj`](../link-options.md).

### Generic-text routine mappings

| TCHAR.H routine | `_UNICODE` and `_MBCS` not defined | `_MBCS` defined | `_UNICODE` defined |
|---|---|---|---|
| `_vtprintf_s` | **`vprintf_s`** | **`vprintf_s`** | **`vwprintf_s`** |
| `_vtprintf_s_l` | **`_vprintf_s_l`** | **`_vprintf_s_l`** | **`_vwprintf_s_l`** |

## Requirements

| Routine | Required header | Optional headers |
|---|---|---|
| **`vprintf_s`**, **`_vprintf_s_l`** | \<stdio.h> and \<stdarg.h> | \<varargs.h>* |
| **`vwprintf_s`**, **`_vwprintf_s_l`** | \<stdio.h> or \<wchar.h>, and \<stdarg.h> | \<varargs.h>* |

\* Required for UNIX V compatibility.

The console isn't supported in Universal Windows Platform (UWP) apps. The standard stream handles that are associated with the console, `stdin`, `stdout`, and `stderr`, must be redirected before C run-time functions can use them in UWP apps. For more compatibility information, see [Compatibility](../compatibility.md).

## See also

[Stream I/O](../stream-i-o.md)\
[`vprintf` functions](../vprintf-functions.md)\
[`fprintf`, `_fprintf_l`, `fwprintf`, `_fwprintf_l`](fprintf-fprintf-l-fwprintf-fwprintf-l.md)\
[`printf`, `_printf_l`, `wprintf`, `_wprintf_l`](printf-printf-l-wprintf-wprintf-l.md)\
[`sprintf`, `_sprintf_l`, `swprintf`, `_swprintf_l`, `__swprintf_l`](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)\
[`va_arg`, `va_copy`, `va_end`, `va_start`](va-arg-va-copy-va-end-va-start.md)
