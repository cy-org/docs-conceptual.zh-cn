---
title: "结构（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, structs
- structs [C#]
ms.assetid: b7cf4ff2-0eb7-4e5c-93d5-b2196b4f5d89
caps.latest.revision: 31
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
ms.openlocfilehash: ce12f402c0748ea6729c82e3f188c0a58f63d628
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="structs-c-programming-guide"></a>结构（C# 编程指南）
通过使用[结构](../../../csharp/language-reference/keywords/struct.md)关键字来定义结构，例如：  
  
 [!code-cs[csProgGuideObjects#39](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/structs_1.cs)]  
  
 结构与类具有许多相同的语法，但结构比类受到的限制更多：  
  
-   在结构声明中，除非将字段声明为 const 或 static，否则无法初始化。  
  
-   结构不能声明默认构造函数（没有参数的构造函数）或终结器。  
  
-   结构在分配时进行复制。 将结构分配给新变量时，将复制所有数据，并且对新副本所做的任何修改不会更改原始副本的数据。 使用值类型的集合（如 Dictionary\<string, myStruct>）时，请务必记住这一点。  
  
-   结构是值类型，而类是引用类型。  
  
-   与类不同，无需使用 `new` 运算符即可对结构进行实例化。  
  
-   结构可以声明具有参数的构造函数。  
  
-   一个结构无法继承自另一个结构或类，并且它不能为类的基类。 所有结构都直接继承自 `System.ValueType`，后者继承自 `System.Object`。  
  
-   结构可以实现接口。  
  
-   结构可用作可以为 null 的类型，并且可以向其分配一个 null 值。  
  
## <a name="related-sections"></a>相关章节  
 更多相关信息：  
  
-   [使用结构](../../../csharp/programming-guide/classes-and-structs/using-structs.md)  
  
-   [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)  
  
-   [如何：了解向方法传递结构和向方法传递类引用之间的区别](../../../csharp/programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md)  
  
-   [如何：在结构之间实现用户定义的转换](../../../csharp/programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [类](../../../csharp/programming-guide/classes-and-structs/classes.md)

