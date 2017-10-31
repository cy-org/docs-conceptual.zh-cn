---
title: "使用索引器（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- indexers [C#], about indexers
ms.assetid: df70e1a2-3ce3-4aba-ad80-4b2f3538699f
caps.latest.revision: 30
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
ms.openlocfilehash: ac8990fa2efb1a2ea24497a3a5de3649795c7b23
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="using-indexers-c-programming-guide"></a>使用索引器（C# 编程指南）
索引器使你可从语法上方便地创建[类](../../../csharp/language-reference/keywords/class.md)、[结构](../../../csharp/language-reference/keywords/struct.md)或[接口](../../../csharp/language-reference/keywords/interface.md)，以便客户端应用程序能像访问数组一样访问它们。 在主要目标是封装内部集合或数组的类型中，常常要实现索引器。 例如，假设有一个名为 TempRecord 的类，它表示 24 小时的周期内在 10 个不同时间点所记录的温度（单位为华氏度）。 该类包含一个名为“temps”、类型为 float 的数组，用于表示温度；以及一个 <xref:System.DateTime>，用于表示记录温度的日期。 通过在此类中实现索引器，客户端可采用 `float temp = tr[4]` 的形式（而非 `float temp = tr.temps[4]`）访问 TempRecord 实例中的温度。 索引器表示法不但简化了客户端应用程序的语法；它还使类及其目标更容易直观地为其它开发者所理解。  
  
 若要在类或结构上声明索引器，请使用 [this](../../../csharp/language-reference/keywords/this.md) 关键字，如此例所示：  
  
```  
public int this[int index]    // Indexer declaration  
{  
    // get and set accessors  
}  
```  
  
## <a name="remarks"></a>备注  
 索引器及其参数的类型必须至少具有和索引器相同的可访问性。 有关可访问性级别的详细信息，请参阅[访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)。  
  
 有关如何在接口上使用索引器的详细信息，请参阅[接口索引器](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)。  
  
 索引器的签名由其形参的数目和类型所组成。 不包含索引器类型或形参的名称。 如果要在相同类中声明多个索引器，则它们的签名必须不同。  
  
 索引器值不分类为变量；因此，无法将索引器值作为 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 参数来传递。  
  
 若要使索引器的名称可为其他语言所用，请在声明中使用 `name` 属性。 例如：  
  
```  
[System.Runtime.CompilerServices.IndexerName("TheItem")]  
public int this [int index]   // Indexer declaration  
{  
}  
```  
  
 此索引器将具有名称 `TheItem`。 如果不提供名称属性，则 `Item` 将成为默认名称。  
  
## <a name="example-1"></a>示例 1  
  
### <a name="description"></a>描述  
 下列示例演示如何声明专用数组字段 `temps` 和索引器。 索引器可以实现对实例 `tempRecord[i]` 的直接访问。 若不使用索引器，则将数组声明为[公共](../../../csharp/language-reference/keywords/public.md)成员，并直接访问其成员 `tempRecord.temps[i]`。  
  
 请注意，当评估索引器访问时（例如在 `Console.Write` 语句中），将调用 [get](../../../csharp/language-reference/keywords/get.md) 访问器。 因此，如果不存在 `get` 访问器，则会发生编译时错误。  
  
### <a name="code"></a>代码  
 [!code-cs[csProgGuideIndexers#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-indexers_1.cs)]  
  
## <a name="indexing-using-other-values"></a>使用其他值进行索引  
 C# 不将索引类型限制为整数。 例如，对索引器使用字符串可能有用。 通过搜索集合内的字符串并返回相应的值，可以实现此类索引器。 由于访问器可被重载，字符串和整数版本可以共存。  
  
## <a name="example-2"></a>示例 2  
  
### <a name="description"></a>描述  
 在此例中，声明了存储星期几的类。 声明一个采用字符串（星期几）并返回对应整数的 `get` 访问器。 例如，星期日将返回 0，星期一将返回 1，依次类推。  
  
### <a name="code"></a>代码  
 [!code-cs[csProgGuideIndexers#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-indexers_2.cs)]  
  
## <a name="robust-programming"></a>可靠编程  
 提高索引器的安全性和可靠性有两种主要方法：  
  
-   请确保结合某一类型的错误处理策略，以处理万一客户端代码传入无效索引值的情况。 在本主题前面的第一个示例中，TempRecord 类提供了 Length 属性，使客户端代码能在将输入传递给索引器之前对其进行验证。 也可将错误处理代码放入索引器自身内部。 请确保为用户记录在索引器的访问器中引发的任何异常。  
  
-   在可接受的程度内，为 `get` 和 [set](../../../csharp/language-reference/keywords/set.md) 访问器的可访问性设置尽可能多的限制。 这一点对 `set` 访问器尤为重要。 有关详细信息，请参阅[限制访问器可访问性](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)

