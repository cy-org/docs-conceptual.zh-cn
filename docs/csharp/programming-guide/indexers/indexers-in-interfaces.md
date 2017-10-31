---
title: "接口中的索引器（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- indexers [C#], in interfaces
- accessors [C#], indexers
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
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
ms.openlocfilehash: 2715602dadea40324f613bb07b5dd332ed18c25c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="indexers-in-interfaces-c-programming-guide"></a>接口中的索引器（C# 编程指南）
可以在[接口](../../../csharp/language-reference/keywords/interface.md)上声明索引器。 接口索引器的访问器与[类](../../../csharp/language-reference/keywords/class.md)索引器的访问器有所不同，差异如下：  
  
-   接口访问器不使用修饰符。  
  
-   接口访问器没有正文。  
  
 因此，访问器的用途是指示索引器为读写、只读还是只写。  
  
 下面是接口索引器访问器的示例：  
  
 [!code-cs[csProgGuideIndexers#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/indexers-in-interfaces_1.cs)]  
  
 索引器的签名必须不同于同一接口中声明的所有其他索引器的签名。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现接口索引器。  
  
 [!code-cs[csProgGuideIndexers#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/indexers-in-interfaces_2.cs)]  
  
 在前面的示例中，可通过使用接口成员的完全限定名来使用显示接口成员实现。 例如：  
  
```  
public string ISomeInterface.this   
{   
}   
```  
  
 但仅当类采用相同的索引签名实现多个接口时，才需用到完全限定名称以避免歧义。 例如，如果 `Employee` 类正在实现接口 `ICitizen` 和接口 `IEmployee`，而这两个接口具有相同的索引签名，则需要用到显式接口成员实现。 即是说以下索引器声明：  
  
```  
public string IEmployee.this   
{   
}   
```  
  
 在 `IEmployee` 接口中实现索引器，而以下声明：  
  
```  
public string ICitizen.this   
{   
}   
```  
  
 在 `ICitizen` 接口中实现索引器。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [接口](../../../csharp/programming-guide/interfaces/index.md)

