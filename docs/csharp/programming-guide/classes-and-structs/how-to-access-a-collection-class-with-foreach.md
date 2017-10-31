---
title: "如何：使用 foreach 访问集合类（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- collection classes [C#], foreach statement
ms.assetid: a6b9cf5c-6c8d-4223-b12c-288949434493
caps.latest.revision: 21
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
ms.openlocfilehash: 2ad81ab699b079f4aabb04a886211e94a937335d
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-access-a-collection-class-with-foreach-c-programming-guide"></a>如何：使用 foreach 访问集合类（C# 编程指南）
下面的代码示例演示如何编写可与 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 结合使用的非泛型集合类。 该示例定义了字符串 tokenizer 类。  
  
> [!NOTE]
>  此示例介绍的是只在无法使用泛型集合类时才采用的推荐做法。 有关如何实现支持 <xref:System.Collections.Generic.IEnumerable%601> 的类型安全的泛型集合类，请参阅[迭代器](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7)。  
  
 在该示例中，下面的代码段使用 `Tokens` 类， 通过“ ”和“-”分隔符将句子“This is a sample sentence.”分成若干标记。 然后，该代码使用 `foreach` 语句显示这些标记。  
  
 [!code-cs[csProgGuideCollections#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-access-a-collection-class-with-foreach_1.cs)]  
  
## <a name="example"></a>示例  
 在内部，`Tokens` 类使用数组存储这些标记。 数组实现 <xref:System.Collections.IEnumerator> 和 <xref:System.Collections.IEnumerable>，因此，此代码示例本可以使用数组的枚举方法（<xref:System.Collections.IEnumerable.GetEnumerator%2A>、<xref:System.Collections.IEnumerator.MoveNext%2A>、<xref:System.Collections.IEnumerator.Reset%2A> 和 <xref:System.Collections.IEnumerator.Current%2A>），而不是在 `Tokens` 类中对其进行定义。 方法定义包括在该示例中，用于明确如何定义它们以及每个定义的内容。  
  
 [!code-cs[csProgGuideCollections#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-access-a-collection-class-with-foreach_2.cs)]  
  
 在 C# 中，为兼容 <xref:System.Collections.IEnumerable>，集合类并非一定要实现 <xref:System.Collections.IEnumerator> 和 `foreach`。 如果类具有所需的 <xref:System.Collections.IEnumerable.GetEnumerator%2A>、<xref:System.Collections.IEnumerator.MoveNext%2A><xref:System.Collections.IEnumerator.Reset%2A> 和 <xref:System.Collections.IEnumerator.Current%2A> 成员，则它将适用于 `foreach`。 省略接口有一个好处：可以比 <xref:System.Object> 更为具体地定义 `Current` 的返回类型。 这提供类型安全性。  
  
 例如，可更改上述示例中的以下行。  
  
```csharp  
// Change the Tokens class so that it no longer implements IEnumerable.  
public class Tokens  
{  
    // . . .  
  
    // Change the return type for the GetEnumerator method.  
    public TokenEnumerator GetEnumerator()  
    {   }  
  
    // Change TokenEnumerator so that it no longer implements IEnumerator.  
    public class TokenEnumerator  
    {  
        // . . .  
  
        // Change the return type of method Current to string.  
        public string Current  
        {   }  
    }  
 }  
```  
  
 由于 `Current` 返回字符串，因此编译器可检测何时在 `foreach` 语句中使用了不兼容的类型，如以下代码所示。  
  
```csharp  
// Error: Cannot convert type string to int.  
foreach (int item in f)    
```  
  
 省略 <xref:System.Collections.IEnumerable> 和 <xref:System.Collections.IEnumerator> 的缺点是：集合类不再可与其他公共语言运行时语言的 `foreach` 语句或等效语句互操作。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Generic>   
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [数组](../../../csharp/programming-guide/arrays/index.md)   
 [集合](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b)

