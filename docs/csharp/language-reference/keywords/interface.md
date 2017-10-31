---
title: "接口（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- interface_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- interface keyword [C#]
ms.assetid: 7da38e81-4f99-4bc5-b07d-c986b687eeba
caps.latest.revision: 29
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
ms.openlocfilehash: 126e674a2c56f04f54f35a011c24ebf0f713ee8d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="interface-c-reference"></a>接口（C# 参考）
接口只包含[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)、[属性](../../../csharp/programming-guide/classes-and-structs/properties.md)、[事件](../../../csharp/programming-guide/events/index.md)或[索引器](../../../csharp/programming-guide/indexers/index.md)的签名。 实现接口的类或结构必须实现接口定义中指定的接口成员。 在以下示例中，类 `ImplementationClass` 必须实现一个不含参数但返回 `void` 的名为 `SampleMethod` 的方法。  
  
 有关详细信息和示例，请参阅[接口](../../../csharp/programming-guide/interfaces/index.md)。  
  
## <a name="example"></a>示例  
 [!code-cs[csrefKeywordsTypes#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/interface_1.cs)]  
  
 接口可以是命名空间或类的成员，并且可以包含下列成员的签名：  
  
-   [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [属性](../../../csharp/programming-guide/classes-and-structs/using-properties.md)  
  
-   [索引器](../../../csharp/programming-guide/indexers/using-indexers.md)  
  
-   [事件](../../../csharp/language-reference/keywords/event.md)  
  
 一个接口可从一个或多个基接口继承。  
  
 基类型列表包含基类和接口时，基类必须是列表中的第 1 项。  
  
 实现接口的类可以显式实现该接口的成员。 显式实现的成员不能通过类实例访问，而只能通过接口实例访问。  
  
 有关显式接口实现的更多详细信息和代码示例，请参阅[显式接口实现](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md)。  
  
## <a name="example"></a>示例  
 下例演示了接口实现。 在此示例中，接口包含属性声明，类包含实现。 实现 `IPoint` 的类的任何实例都具有整数属性 `x` 和 `y`。  
  
 [!code-cs[csrefKeywordsTypes#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/interface_2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [引用类型](../../../csharp/language-reference/keywords/reference-types.md)   
 [接口](../../../csharp/programming-guide/interfaces/index.md)   
 [使用属性](../../../csharp/programming-guide/classes-and-structs/using-properties.md)   
 [使用索引器](../../../csharp/programming-guide/indexers/using-indexers.md)   
 [类](../../../csharp/language-reference/keywords/class.md)   
 [结构](../../../csharp/language-reference/keywords/struct.md)   
 [接口](../../../csharp/programming-guide/interfaces/index.md)

