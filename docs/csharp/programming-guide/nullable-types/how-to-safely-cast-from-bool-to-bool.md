---
title: "如何：安全地将 bool? 强制转换为 bool（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- casting [C#], nullable types
- nullable types [C#], casting bool? to bool
ms.assetid: e06e4274-a443-422d-8ef1-9dbf9df55237
caps.latest.revision: 9
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
ms.openlocfilehash: c8a3dc3280b7dca802b327d9454c7f0ba9ed44be
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-safely-cast-from-bool-to-bool-c-programming-guide"></a>如何：安全地将 bool? 强制转换为 bool（C# 编程指南）
可以为 null 的类型 `bool?` 可包含三个不同的值：`true`、`false` 和 `null`。 因此，`bool?` 类型不能用于条件语句，例如与 `if`、`for` 或 `while` 等一起使用。 例如，下面的代码会导致编译器错误。  
  
```  
bool? b = null;  
if (b) // Error CS0266.  
{  
}  
```  
  
 这是不允许的，因为在条件语句上下文中，`null` 表示的含义不清楚。 若要在条件语句中使用 `bool?`，首先请检查其 <xref:System.Nullable%601.HasValue%2A> 属性，确保该属性的值不是 `null`，然后将其转换为 `bool`。 有关详细信息，请参阅 [bool](../../../csharp/language-reference/keywords/bool.md)。 如果对值为 `null` 的 `bool?` 执行转换，则会在条件测试中引发 <xref:System.InvalidOperationException>。 以下示例演示了一种将 `bool?` 安全转换为 `bool` 的方式：  
  
## <a name="example"></a>示例  
  
```csharp  
bool? test = null;  
// Other code that may or may not  
// give a value to test.  
if(!test.HasValue) //check for a value  
{  
    // Assume that IsInitialized  
    // returns either true or false.  
    test = IsInitialized();  
}  
if((bool)test) //now this cast is safe  
{  
   // Do something.  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [文字关键字](../../../csharp/language-reference/keywords/literal-keywords.md)   
 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)   
 [??运算符](../../../csharp/language-reference/operators/null-conditional-operator.md)

