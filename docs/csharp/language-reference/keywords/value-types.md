---
title: "值类型（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.valuetypes
dev_langs:
- CSharp
helpviewer_keywords:
- value types [C#]
- types [C#], value types
- C# language, value types
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
caps.latest.revision: 18
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7500426846562dd7f3bbb8ea99f300a3e8a26546
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="value-types-c-reference"></a>值类型（C# 参考）
值类型包含两个主要类别：  
  
-   [结构](../../../csharp/language-reference/keywords/struct.md)  
  
-   [枚举](../../../csharp/language-reference/keywords/enum.md)  
  
 结构分为以下类别：  
  
-   数值类型  
  
    -   [整型类型](../../../csharp/language-reference/keywords/integral-types-table.md)  
  
    -   [浮点类型](../../../csharp/language-reference/keywords/floating-point-types-table.md)  
  
    -   [小数](../../../csharp/language-reference/keywords/decimal.md)  
  
-   [bool](../../../csharp/language-reference/keywords/bool.md)  
  
-   用户定义的结构。  
  
## <a name="main-features-of-value-types"></a>值类型的主要功能  
 直接基于值类型的变量包含值。 将一个值类型变量分配给另一个值类型变量将复制包含的值。 这不同于分配引用类型变量，后者复制对对象的引用，但不复制对象本身。  
  
 所有值类型都隐式派生自 <xref:System.ValueType?displayProperty=fullName>。  
  
 与引用类型不同，不能从值类型派生新类型。 但是，与引用类型一样，结构可以实现接口。  
  
 与引用类型不同，值类型不能包含 `null` 值。 但是，[可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)功能允许将值类型分配给 `null`。  
  
 每个值类型都具有一个初始化该类型的默认值的隐式默认构造函数。 有关值类型的默认值的信息，请参阅[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  
  
## <a name="main-features-of-simple-types"></a>简单类型的主要功能  
 所有简单类型（在 C# 语言中必不可少）都是 .NET Framework 系统类型的别名。 例如， [int](../../../csharp/language-reference/keywords/int.md) 是 <xref:System.Int32?displayProperty=fullName> 的别名。 有关别名的完整列表，请参阅[内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)。  
  
 其操作数都是简单类型常数的常量表达式在编译时进行评估。  
  
 可以使用文本初始化简单类型。 例如，“A”是类型 `char` 的文本，2001 是类型 `int` 的文本。  
  
## <a name="initializing-value-types"></a>初始化值类型  
 在使用 C# 中的本地变量之前，必须对其进行初始化。 例如，可以声明未初始化的本地变量，如以下示例所示：  
  
```  
int myInt;  
```  
  
 在未初始化之前，无法使用。 可以使用以下语句将其初始化：  
  
```  
myInt = new int();  // Invoke default constructor for int type.  
```  
  
 此语句等效于以下语句：  
  
```  
myInt = 0;         // Assign an initial value, 0 in this example.  
```  
  
 当然，可以在同一语句中进行声明和初始化，如以下示例所示：  
  
```  
int myInt = new int();  
```  
  
 - 或 -  
  
```  
int myInt = 0;  
```  
  
 使用 [new](../../../csharp/language-reference/keywords/new.md) 运算符将调用特定类型的默认构造函数，并向变量赋予默认值。 在前面的示例中，默认构造函数将值 `0` 赋予了 `myInt`。 有关通过调用默认构造函数所赋予的值的详细信息，请参阅[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  
  
 对于用户定义类型，请使用 [new](../../../csharp/language-reference/keywords/new.md) 调用默认构造函数。 例如，以下语句调用 `Point` 结构的默认构造函数：  
  
```  
Point p = new Point(); // Invoke default constructor for the struct.  
```  
  
 进行此调用后，该结构被视为已明确赋值；即，它的所有成员都被初始化为其默认值。  
  
 有关 new 运算符的详细信息，请参阅 [new](../../../csharp/language-reference/keywords/new.md)。  
  
 有关设置数值类型的输出格式的信息，请参阅[设置数值结果表的格式](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)

