---
title: "泛型的优点（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- generics [C#], benefits
ms.assetid: 80f037cd-9ea7-48be-bfc1-219bfb2d4277
caps.latest.revision: 23
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
ms.openlocfilehash: 8b05a3a695064764618564293e6ccd92e2ce60be
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="benefits-of-generics-c-programming-guide"></a>泛型的优点（C# 编程指南）
公共语言运行时和 C# 语言早期版本中存在一个局限，其中通过将类型与通用基类型 <xref:System.Object> 相互强制完成泛化，泛型提供了此局限的解决方案。 通过创建泛型类，可在编译时创建类型安全的集合。  
  
 通过编写一个使用 .NET Framework 类库中 <xref:System.Collections.ArrayList> 集合类的小程序，可体现出使用非泛型集合类的局限。 <xref:System.Collections.ArrayList> 是一个极为方便的集合类，无需进行修改即可用于存储任何引用或值类型。  
  
 [!code-cs[csProgGuideGenerics#4](../../../csharp/programming-guide/generics/codesnippet/CSharp/benefits-of-generics_1.cs)]  
  
 但这种便利有一定代价。 添加到 <xref:System.Collections.ArrayList> 的任何引用或值类型均隐式向上转换为 <xref:System.Object>。 如果项为值类型，将它们添加到列表时必须将其装箱，检索它们时必须取消装箱。 转换与装箱/取消装箱这两种操作都会降低性能；在必须循环访问大型集合的方案中，装箱与取消装箱的影响非常大。  
  
 另一局限是缺少编译时类型检查；由于 <xref:System.Collections.ArrayList> 将所有内容都转换为 <xref:System.Object>，因此在编译时无法阻止客户端代码执行如下操作：  
  
 [!code-cs[csProgGuideGenerics#5](../../../csharp/programming-guide/generics/codesnippet/CSharp/benefits-of-generics_2.cs)]  
  
 虽然在创建异类集合时这完全可以接受，甚至有时是有意为之，但将字符串和 `ints` 合并到单个 <xref:System.Collections.ArrayList> 中更有可能属于编程错误，且此错误在运行时之前不会被检测出。  
  
 在 C# 语言 1.0 和 1.1 版中，仅可通过编写自己的类型特定集合来避免 .NET Framework 基类库集合类中出现泛化代码的风险。 当然，由于这样的类不能重复用于多个数据类型，因此你并不具有泛化的优势，且必须为要存储的每个类型重写类。  
  
 <xref:System.Collections.ArrayList> 以及其他相似的类真正需要的是一种方式，这种方式使客户端代码基于每个实例指定打算使用的特定数据类型。 这会省去向上转换为 `T:System.Object` 的必要，并且使编译器可能执行类型检查。 换而言之，<xref:System.Collections.ArrayList> 需要一个类型参数。 那正是泛型所提供的内容。 在泛型 <xref:System.Collections.Generic.List%601> 集合中，在 `N:System.Collections.Generic` 命名空间中，向集合添加项的操作类似于如下所示：  
  
 [!code-cs[csProgGuideGenerics#6](../../../csharp/programming-guide/generics/codesnippet/CSharp/benefits-of-generics_3.cs)]  
  
 对于客户端代码，与 <xref:System.Collections.ArrayList> 相比，<xref:System.Collections.Generic.List%601> 添加的唯一语法是声明和实例化中的类型参数。 虽然编码略为复杂，但与 <xref:System.Collections.ArrayList> 相比，你创建的列表不仅更加安全，而且创建速度大为提高，尤其是在列表项为值类型时。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Generic>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型简介](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)   
 [最佳实践集合](http://go.microsoft.com/fwlink/?LinkId=112403)

