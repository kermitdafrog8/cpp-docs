---
description: "Learn more about: Formatting the output of a custom build step or build event"
title: "Formatting the output of a custom build step or build event"
ms.date: 09/03/2026
helpviewer_keywords: ["builds [C++], build events", "custom build steps [C++], output format", "events [C++], build", "build events [C++], output format", "build steps [C++], output format", "builds [C++], custom build steps"]
ms.topic: concept-article
---
# Formatting the output of a custom build step or build event

If the output of a custom build step or build event is formatted correctly, users get the following benefits:

- Warnings and errors appear in the **Output** window.
- Warnings and errors appear in the **Error List** window.
- Clicking on the output in the **Output** or **Error List** windows displays the appropriate location.
- **F1** help is enabled in the **Error List** and **Output** windows.

## Output format

The format of the output should be:

> { *filename*`(`*line-number*\[`,`*column-number*]`)` \| *tool-name* } `:` \[ *any-text* ] {`error` \| `warning`} *code-type-and-number* `:` *localizable-string* \[ *any-text* ]

Don't include a space between the comma and the column number. Use `filename(1,2)` instead of `filename(1, 2)` to ensure that selecting the output navigates to the correct location from both the **Error List** and **Output** windows.

Where:

- { *a* \| *b* } is a choice of either *a* or *b*,
- \[ *item* ] is an optional string or parameter,
- `text` represents a literal.

For example:

> C:\\sourcefile.cpp(134) : error C2143: syntax error : missing ';' before '}'
>
> LINK : fatal error LNK1104: cannot open file 'some-library.lib'

## See also

[Understanding custom build steps and build events](understanding-custom-build-steps-and-build-events.md)
