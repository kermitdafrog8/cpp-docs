---
title: "Walkthrough: Create and use a static library (C++)"
description: Learn to create and use a static library in C++ using Visual Studio. This walkthrough covers building a .lib file, adding a class, and referencing it in an app.
ms.custom: "get-started-article"
ms.date: 07/14/2026
helpviewer_keywords: ["libraries [C++], static", "static libraries [C++]"]
ms.assetid: 3cc36411-7d66-4240-851e-dacb9a8fd6ac
#customer intent: As a C++ developer, I want to create a static library in Visual Studio, so that I can reuse common code across multiple apps.
---
# Walkthrough: Create and use a static library

This step-by-step walkthrough shows how to create a static library (.lib file) for use with C++ apps. Using a static library is a great way to reuse code. Rather than reimplementing the same routines in every app that requires the functionality, write them one time in a static library and then reference it from the apps. Code linked from a static library becomes part of your app. You don't have to install another file to use the code.

This walkthrough covers these tasks:

- [Create a static library project](#CreateLibProject)

- [Add a class to the static library](#AddClassToLib)

- [Create a C++ console app that references the static library](#CreateAppToRefTheLib)

- [Use the functionality from the static library in the app](#UseLibInApp)

- [Run the app](#RunApp)

## Prerequisites

An understanding of the fundamentals of the C++ language.

## <a name="CreateLibProject"></a> Create a static library project

The instructions for how to create the project vary depending on your version of Visual Studio. To see the documentation for your preferred version of Visual Studio, use the **Version** selector control. It's found at the top of the table of contents on this page.

::: moniker range=">=msvc-160"

To create a static library project in Visual Studio:

1. On the menu bar, choose **File** > **New** > **Project** to open the **Create a new project** dialog.

1. At the top of the dialog, set  **Language** to **C++**, set **Platform** to **Windows**, and set **Project type** to **Library**.

1. From the filtered list of project types, select **Windows Desktop Wizard**, and then choose **Next**.

1. In the **Configure your new project** page, enter *MathLibrary* in the **Project name** box to specify a name for the project. Enter *StaticMath* in the **Solution name** box. Choose the **Create** button to open the **Windows Desktop Project** dialog.

1. In the **Windows Desktop Project** dialog, under **Application type**, select **Static Library (.lib)**.

1. Under **Additional options**, clear the **Precompiled header** check box if it's selected. Select **Empty project**.

1. Choose **OK** to create the project.

::: moniker-end

::: moniker range="msvc-150"

To create a static library project in Visual Studio 2017:

1. On the menu bar, choose **File** > **New** > **Project**.

1. In the **New Project** dialog, select **Installed** > **Visual C++** > **Windows Desktop**. In the center pane, select **Windows Desktop Wizard**.

1. Specify a name for the project, such as *MathLibrary*, in the **Name** box. Specify a name for the solution, such as *StaticMath*, in the **Solution Name** box. Choose **OK**.

1. In the **Windows Desktop Project** dialog, under **Application type**, select **Static Library (.lib)**.

1. Under **Additional Options**, clear the **Precompiled header** check box if it's selected. Select **Empty project**.

1. Choose **OK** to create the project.

::: moniker-end

::: moniker range="msvc-140"

To create a static library project in Visual Studio 2015:

1. On the menu bar, choose **File** > **New** > **Project**.

1. In the **New Project** dialog, select **Installed** > **Templates** > **Visual C++** > **Win32**. In the center pane, select **Win32 Console Application**.

1. Specify a name for the project, such as *MathLibrary*, in the **Name** box. Specify a name for the solution, such as *StaticMath*, in the **Solution Name** box. Choose **OK**.

1. In the **Win32 Application Wizard**, choose **Next**.

1. In the **Application Settings** page, under **Application type**, select **Static library**. Under **Additional options**, clear the **Precompiled header** checkbox. Choose **Finish** to create the project.

::: moniker-end

## <a name="AddClassToLib"></a> Add a class to the static library

To add a class to the static library:

1. Create a header file for a new class. In **Solution Explorer**, right-click **MathLibrary** to open the context menu for the project. Select **Add** > **New Item**.

1. In the **Add New Item** dialog, select **Visual C++** > **Code**. In the center pane, select **Header File (.h)**. Specify a name for the header file, such as *MathLibrary.h*, and then select **Add**. A nearly blank header file is displayed.

1. Add a declaration for a class named `Arithmetic` to do common mathematical operations such as addition, subtraction, multiplication, and division. The code should resemble:

    ```cpp
    // MathLibrary.h
    #pragma once

    namespace MathLibrary
    {
        class Arithmetic
        {
        public:
            // Returns a + b
            static double Add(double a, double b);

            // Returns a - b
            static double Subtract(double a, double b);

            // Returns a * b
            static double Multiply(double a, double b);

            // Returns a / b
            static double Divide(double a, double b);
        };
    }
    ```

1. To create a source file for the new class, open the context menu for the **MathLibrary** project in **Solution Explorer**, and then choose **Add** > **New Item**.

1. In the **Add New Item** dialog, in the center pane, select **C++ File (.cpp)**. Specify a name for the source file, such as *MathLibrary.cpp*. Then select **Add**. A blank source file is displayed.

1. Use this source file to implement the functionality for class `Arithmetic`. The code should resemble:

    ```cpp
    // MathLibrary.cpp
    // compile with: cl /c /EHsc MathLibrary.cpp
    // post-build command: lib MathLibrary.obj

    #include "MathLibrary.h"

    namespace MathLibrary
    {
        double Arithmetic::Add(double a, double b)
        {
            return a + b;
        }

        double Arithmetic::Subtract(double a, double b)
        {
            return a - b;
        }

        double Arithmetic::Multiply(double a, double b)
        {
            return a * b;
        }

        double Arithmetic::Divide(double a, double b)
        {
            return a / b;
        }
    }
    ```

1. To build the static library, select **Build** > **Build Solution** on the menu bar. The build creates a static library, *MathLibrary.lib*, that other programs can use.

   > [!NOTE]
   > When you build on the Visual Studio command line, you must build the program in two steps.
   >
   > 1. Run `cl /c /EHsc MathLibrary.cpp` to compile the code and create an object file named *MathLibrary.obj*. The `cl` command invokes the compiler, Cl.exe, and the `/c` option specifies compile without linking. For more information, see [/c (Compile Without Linking)](../build/reference/c-compile-without-linking.md).
   > 1. Run `lib MathLibrary.obj` to link the code and create the static library *MathLibrary.lib*. The `lib` command invokes the Library Manager, Lib.exe. For more information, see [LIB Reference](../build/reference/lib-reference.md).

## <a name="CreateAppToRefTheLib"></a> Create a C++ console app that references the static library

::: moniker range=">=msvc-160"

To create a C++ console app that references the static library in Visual Studio:

1. In **Solution Explorer**, right-click on the top node, **Solution 'StaticMath'**, to open the context menu. Choose **Add** > **New Project** to open the **Add a New Project** dialog.

1. At the top of the dialog, set the **Project type** filter to **Console**.

1. From the filtered list of project types, choose **Console App** then choose **Next**. In the next page, enter *MathClient* as the name for the project.

1. Choose **Create** to create the client project.

   After you create a console app, an empty program is created for you. The name for the source file is the same as the name that you chose earlier. In the example, it's named `MathClient.cpp`.

::: moniker-end

::: moniker range="msvc-150"

To create a C++ console app that references the static library in Visual Studio 2017:

1. In **Solution Explorer**, right-click on the top node, **Solution 'StaticMath'**, to open the context menu. Choose **Add** > **New Project** to open the **Add a New Project** dialog.

1. In the **Add New Project** dialog, select **Installed** > **Visual C++** > **Windows Desktop**. In the center pane, select **Windows Desktop Wizard**.

1. Specify a name for the project—for example, *MathClient*—in the **Name** box. Choose the **OK** button.

1. In the **Windows Desktop Project** dialog, under **Application type**, select **Console Application (.exe)**.

1. Under **Additional Options**, clear the **Precompiled header** check box if it's selected.

1. Choose **OK** to create the project.

1. After you create a console app, an empty program is created for you. The name for the source file is the same as the name that you chose earlier. In the example, it's named `MathClient.cpp`.

::: moniker-end

::: moniker range="msvc-140"

To create a C++ console app that references the static library in Visual Studio 2015:

1. In **Solution Explorer**, right-click on the top node, **Solution 'StaticMath'**, to open the context menu. Choose **Add** > **New Project** to open the **Add a New Project** dialog.

1. In the **Add New Project** dialog, select **Installed** > **Visual C++** > **Win32**. In the center pane, select **Win32 Console Application**.

1. Specify a name for the project—for example, *MathClient*—in the **Name** box. Choose the **OK** button.

1. In the **Win32 Application Wizard** dialog, choose **Next**.

1. On the **Application Settings** page, under **Application type**, make sure **Console application** is selected. Under **Additional options**, clear **Precompiled header**, and then select **Empty Project**. Choose **Finish** to create the project.

1. To add a source file to the empty project, right-click to open the context menu for the **MathClient** project in **Solution Explorer**, and then choose **Add** > **New Item**.

1. In the **Add New Item** dialog, select **Visual C++** > **Code**. In the center pane, select **C++ File (.cpp)**. Specify a name for the source file—for example, *MathClient.cpp*—and then choose the **Add** button. A blank source file is displayed.

::: moniker-end

## <a name="UseLibInApp"></a> Use the functionality from the static library in the app

To use the functionality from the static library in the app:

1. Reference the static library before using the math routines in it. Open the context menu for the **MathClient** project in **Solution Explorer**, and then choose **Add** > **Reference**.

1. The **Add Reference** dialog lists the libraries that you can reference. The **Projects** tab lists the projects in the current solution and any libraries they reference. Open the **Projects** tab, select **MathLibrary**, and then select **OK**.

1. Modify the included directories path to reference the `MathLibrary.h` header file. In **Solution Explorer**, right-click on **MathClient** to open the context menu. Choose **Properties** to open the **MathClient Property Pages** dialog.

1. In the **MathClient Property Pages** dialog, set the **Configuration** value to **All Configurations**. Set **Platform** to **All Platforms**.

1. Select the **Configuration Properties** > **C/C++** > **General** property page. In the **Additional Include Directories** property, specify the path of the **MathLibrary** directory, or browse for it.

   To browse for the directory path:

   1. Open the **Additional Include Directories** property value drop-down list, and then choose **Edit**.

   1. In the **Additional Include Directories** dialog, double-click in the top of the text box. Then choose the ellipsis button (**...**) at the end of the line.

   1. In the **Select Directory** dialog, navigate up a level, and then select the **MathLibrary** directory. Then choose the **Select Folder** button to save your selection.

   1. In the **Additional Include Directories** dialog, choose the **OK** button.

   1. In the **Property Pages** dialog, choose the **OK** button to save your changes to the project.

1. You can now use the `Arithmetic` class in this app by including the `#include "MathLibrary.h"` header in your code. Replace the contents of `MathClient.cpp` with this code:

    ```cpp
    // MathClient.cpp
    // compile with: cl /EHsc MathClient.cpp /link MathLibrary.lib

    #include <iostream>
    #include "MathLibrary.h"

    int main()
    {
        double a = 7.4;
        int b = 99;

        std::cout << "a + b = " <<
            MathLibrary::Arithmetic::Add(a, b) << std::endl;
        std::cout << "a - b = " <<
            MathLibrary::Arithmetic::Subtract(a, b) << std::endl;
        std::cout << "a * b = " <<
            MathLibrary::Arithmetic::Multiply(a, b) << std::endl;
        std::cout << "a / b = " <<
            MathLibrary::Arithmetic::Divide(a, b) << std::endl;

        return 0;
    }
    ```

1. To build the executable, choose **Build** > **Build Solution** on the menu bar.

## <a name="RunApp"></a> Run the app

To run the app:

1. Make sure that **MathClient** is selected as the default project. To select it, right-click **MathClient** in **Solution Explorer** to open the context menu, and then choose **Set as StartUp Project**.

1. On the menu bar, choose **Debug** > **Start Without Debugging** to run the project. The output should resemble:

    ```Output
    a + b = 106.4
    a - b = -91.6
    a * b = 732.6
    a / b = 0.0747475
    ```

## See also

[Walkthrough: Creating and Using a Dynamic Link Library (C++)](../build/walkthrough-creating-and-using-a-dynamic-link-library-cpp.md)
