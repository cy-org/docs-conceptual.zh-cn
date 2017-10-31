---
title: "new 运算符（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
caps.latest.revision: 22
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
ms.openlocfilehash: 59e1cc2006548df9a7a10283a34044040e5c2fef
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="new-operator-c-reference"></a>new 运算符（C# 参考）
用于创建对象和调用构造函数。 例如：  
  
```  
Class1 obj  = new Class1();  
```  
  
 它还用于创建匿名类型的实例：  
  
```  
var query = from cust in customers  
            select new {Name = cust.Name, Address = cust.PrimaryAddress};  
```  
  
 `new` 运算符还用于调用值类型的默认构造函数。 例如：  
  
```  
int i = new int();  
```  
  
 在前面的语句中，`i` 的初始值为 `0`，这是类型 `int` 的默认值。 此语句与下面的语句的效果相同：  
  
```  
int i = 0;  
```  
  
 有关默认值的完整列表，请参阅[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  
  
 请记住，为 [struct](../../../csharp/language-reference/keywords/struct.md) 声明默认构造函数是错误的，因为每个值类型均隐式含有公共默认构造函数。 可以对结构类型声明参数化构造函数，以设置其初始值，但仅在需要除默认值以外的值时才需要这样做。  
  
 值类型对象（例如结构）是在堆栈上创建的，而引用类型对象（例如类）是在堆上创建的。 这两种类型的对象均被自动销毁，但基于值类型的对象是在它们超出范围时被销毁，而基于引用类型的对象是在删除对它们的最后一个引用后在非指定时间被销毁。 对于占用固定资源（如大量内存、文件句柄或网络连接）的引用类型，有时需要应用确定性终结，以确保尽快销毁对象。 有关详细信息，请参阅 [Using 语句](../../../csharp/language-reference/keywords/using-statement.md)。  
  
 不能重载 `new` 运算符。  
  
 如果 `new` 运算符无法分配内存，则引发异常 <xref:System.OutOfMemoryException>。  
  
## <a name="example"></a>示例  
 在下面的示例中，使用 `new` 运算符创建并初始化 `struct` 对象和类对象，并向它们分配值。 显示默认值和分配的值。  
  
 [!code-cs[csrefKeywordsOperator#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-operator_1.cs)]  
  
 请注意，本示例中字符串的默认值为 `null`。 因此，未显示此字符串。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)

