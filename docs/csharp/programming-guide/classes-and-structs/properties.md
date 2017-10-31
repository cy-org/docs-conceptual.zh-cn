---
title: "属性（C# 编程指南）"
ms.date: 2017-03-10
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.properties
dev_langs:
- CSharp
helpviewer_keywords:
- properties [C#]
- C# language, properties
ms.assetid: e295a8a2-b357-4ee7-a12e-385a44146fa8
caps.latest.revision: 38
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
ms.openlocfilehash: 127299a617cacee15f87964a12bb3877a2586204
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="properties-c-programming-guide"></a>属性（C# 编程指南）

属性是一种成员，它提供灵活的机制来读取、写入或计算私有字段的值。 属性可用作公共数据成员，但它们实际上是称为*访问器*的特殊方法。 这使得可以轻松访问数据，还有助于提高方法的安全性和灵活性。  

## <a name="properties-overview"></a>属性概述  
  
- 属性允许类公开获取和设置值的公共方法，而隐藏实现或验证代码。  
  
- [get](../../../csharp/language-reference/keywords/get.md) 属性访问器用于返回属性值，而 [set](../../../csharp/language-reference/keywords/set.md) 属性访问器用于分配新值。 这些访问器可以具有不同的访问级别。 有关详细信息，请参阅[限制访问器可访问性](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)。  
  
- [value](../../../csharp/language-reference/keywords/value.md) 关键字用于定义由 `set` 访问器分配的值。  
- 属性可以是*读-写*属性（既有 `get` 访问器又有 `set` 访问器）、*只读*属性（有 `get` 访问器，但没有 `set` 访问器）或*只写*访问器（有 `set` 访问器，但没有 `get` 访问器）。 只写属性很少出现，常用于限制对敏感数据的访问。

- 不需要自定义访问器代码的简单属性可以作为表达式主体定义或[自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)来实现。
 
## <a name="properties-with-backing-fields"></a>具有支持字段的属性

有一个实现属性的基本模式，该模式使用私有支持字段来设置和检索属性值。 `get` 访问器返回私有字段的值，`set` 访问器在向私有字段赋值之前可能会执行一些数据验证。 这两个访问器还可以在存储或返回数据之前对其执行某些转换或计算。

下面的示例阐释了此模式。 在此示例中，`TimePeriod` 类表示时间间隔。 在内部，该类将时间间隔以秒为单位存储在名为 `seconds` 的私有字段中。 名为 `Hours` 的读-写属性允许客户以小时为单位指定时间间隔。 `get` 和 `set` 访问器都会执行小时与秒之间的必要转换。 此外，`set` 访问器还会验证数据，如果小时数无效，则引发 @System.ArgumentOutOfRangeException。 
   
 [!code-cs[Properties#1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-1.cs)]  
  
## <a name="expression-body-definitions"></a>表达式主体定义  

 属性访问器通常由单行语句组成，这些语句只分配或只返回表达式的结果。 可以将这些属性作为 expression-bodied 成员来实现。 `=>` 符号后跟用于为属性赋值或从属性中检索值的表达式，即组成了表达式主体定义。

 从 C# 6 开始，只读属性可以将 `get` 访问器作为 expression-bodied 成员实现。 在这种情况下，既不使用 `get` 访问器关键字，也不使用 `return` 关键字。 下面的示例将只读 `Name` 属性作为 expression-bodied 成员实现。

 [!code-cs[Properties#2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-2.cs)]  

 从 C# 7 开始，`get` 和 `set` 访问器都可以作为 expression-bodied 成员实现。 在这种情况下，必须使用 `get` 和 `set` 关键字。 下面的示例阐释如何为这两个访问器使用表达式主体定义。 请注意，`return` 关键字不与 `get` 访问器搭配使用。
 
  [!code-cs[Properties#3](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-3.cs)]  

## <a name="auto-implemented-properties"></a>自动实现的属性

在某些情况下，属性 `get` 和 `set` 访问器仅向支持字段赋值或仅从其中检索值，而不包括任何附加逻辑。 通过使用自动实现的属性，既能简化代码，还能让 C# 编译器透明地提供支持字段。 

如果属性具有 `get` 和 `set` 访问器，则必须自动实现这两个访问器。 自动实现的属性通过以下方式定义：使用 `get` 和 `set` 关键字，但不提供任何实现。 下面的示例与上一个示例基本相同，只不过 `Name` 和 `Price` 是自动实现的属性。 请注意，该示例还删除了参数化构造函数，以便通过调用默认构造函数和[对象初始值设定项](object-and-collection-initializers.md)立即初始化 `SaleItem` 对象。

  [!code-cs[Properties#4](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-4.cs)]  

## <a name="related-sections"></a>相关章节  
  
-   [使用属性](../../../csharp/programming-guide/classes-and-structs/using-properties.md)  
  
-   [接口属性](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)  
  
-   [属性与索引器之间的比较](../../../csharp/programming-guide/indexers/comparison-between-properties-and-indexers.md)  
  
-   [限制访问器可访问性](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)  
  
-   [自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [使用属性](../../../csharp/programming-guide/classes-and-structs/using-properties.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [get 关键字](../../../csharp/language-reference/keywords/get.md)    
 [set 关键字](../../../csharp/language-reference/keywords/set.md)    

