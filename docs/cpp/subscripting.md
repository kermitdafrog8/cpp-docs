---
description: "Learn more about: Subscripting"
title: "Subscripting"
ms.date: "11/04/2016"
helpviewer_keywords: ["subscript operator [C++], overloaded", "arrays [C++], subscripting", "subscripting [C++]", "operators [C++], overloading", "operator overloading [C++], examples", "subscript operator"]
ms.assetid: eb151281-6733-401d-9787-39ab6754c62c
---
# Subscripting

The built-in subscript operator (**[ ]**) is a binary operator. Before C++23, an overloaded subscript operator (`operator[]`) had to be a nonstatic member function. In C++23 and later, it can also be a static member function. For more information, see [Static subscript operator](static-subscript-operator.md).

The built-in subscript operator (**[ ]**) is a binary operator. Before C++23, subscript operator (`operator[]`) overloads had to be nonstatic member functions. In C++23 and later, you can also overload using a static member function. For more information, see [Static subscript operator](static-subscript-operator.md).

The argument can be any type and designates the desired array subscript.

## Example

The following example demonstrates how to create a vector of type **`int`** that implements bounds checking:

```cpp
// subscripting.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
class IntVector {
public:
   IntVector( int cElements );
   ~IntVector() { delete [] _iElements; }
   int& operator[](int nSubscript);
private:
   int *_iElements;
   int _iUpperBound;
};

// Construct an IntVector.
IntVector::IntVector( int cElements ) {
   _iElements = new int[cElements];
   _iUpperBound = cElements;
}

// Subscript operator for IntVector.
int& IntVector::operator[](int nSubscript) {
   static int iErr = -1;

   if( nSubscript >= 0 && nSubscript < _iUpperBound )
      return _iElements[nSubscript];
   else {
      clog << "Array bounds violation." << endl;
      return iErr;
   }
}

// Test the IntVector class.
int main() {
   IntVector v( 10 );
   int i;

   for( i = 0; i <= 10; ++i )
      v[i] = i;

   v[3] = v[9];

   for ( i = 0; i <= 10; ++i )
      cout << "Element: [" << i << "] = " << v[i] << endl;
}
```

```Output
Array bounds violation.
Element: [0] = 0
Element: [1] = 1
Element: [2] = 2
Element: [3] = 9
Element: [4] = 4
Element: [5] = 5
Element: [6] = 6
Element: [7] = 7
Element: [8] = 8
Element: [9] = 9
Array bounds violation.
Element: [10] = 10
```

## Comments

When `i` reaches 10 in the preceding program, **operator[]** detects that an out-of-bounds subscript is being used and issues an error message.

Note that the function **operator[]** returns a reference type. This causes it to be an l-value, allowing you to use subscripted expressions on either side of assignment operators.

## See also

[Static subscript operator](static-subscript-operator.md)\
[Operator Overloading](../cpp/operator-overloading.md)
