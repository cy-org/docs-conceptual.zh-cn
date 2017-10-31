---
title: "如何：为类型定义值相等性（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- overriding Equals method [C#]
- object equivalence [C#]
- Equals method [C#] , overriding
- value equality [C#]
- equivalence [C#]
ms.assetid: 4084581e-b931-498b-9534-cf7ef5b68690
caps.latest.revision: 15
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
ms.openlocfilehash: e008be022765ff7d2bb440f0a37193b882038b76
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-define-value-equality-for-a-type-c-programming-guide"></a>如何：为类型定义值相等性（C# 编程指南）
定义类或结构时，需确定为类型创建值相等性（或等效性）的自定义定义是否有意义。 通常，类型的对象预期要添加到某类集合时，或者这些对象主要用于存储一组字段或属性时，需实现值相等性。 可以基于类型中所有字段和属性的比较结果来定义值相等性，也可以基于子集进行定义。 但在任何一种情况下，类和结构中的实现均应遵循 5 个等效性保证条件：  
  
1.  x.`Equals`(x) 返回 `true.`。这称为自反属性。  
  
2.  x.`Equals`(y) 返回与 y.`Equals`(x) 相同的值。 这称为对称属性。  
  
3.  如果 (x.`Equals`(y) && y.`Equals`(z)) 返回 `true`，则 x.`Equals`(z) 返回 `true`。 这称为可传递属性。  
  
4.  只要不修改 x 和 y 引用的对象，x.`Equals`(y) 的后续调用就会返回相同的值。  
  
5.  x.`Equals`(null) 返回 `false`。 但是，null.Equals(null) 会引发异常；它未遵循上面的第 2 条规则。  
  
 定义的任何结构都已具有其从 <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName> 方法的 <xref:System.ValueType?displayProperty=fullName> 替代中继承的值相等性的默认实现。 此实现使用反射来检查类型中的所有字段和属性。 尽管此实现可生成正确的结果，但与专门为类型编写的自定义实现相比，它的速度相对较慢。  
  
 类和结构的值相等性的实现详细信息有所不同。 但是，类和结构都需要相同的基础步骤来实现相等性：  
  
1.  替代[虚拟](../../../csharp/language-reference/keywords/virtual.md) <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName> 方法。 大多数情况下，`bool Equals( object obj )` 实现应只调入作为 <xref:System.IEquatable%601?displayProperty=fullName> 接口的实现的类型特定 `Equals` 方法。 （请参阅步骤 2。）  
  
2.  通过提供类型特定的 `Equals` 方法实现 <xref:System.IEquatable%601?displayProperty=fullName> 接口。 实际的等效性比较将在此接口中执行。 例如，可能决定通过仅比较类型中的一两个字段来定义相等性。 不会从 `Equals` 引发异常。 仅适用于类：此方法应仅检查类中声明的字段。 它应调用 `base.Equals` 来检查基类中的字段。 （如果类型直接从 <xref:System.Object> 中继承，则不要这样做，因为 <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName> 的 <xref:System.Object> 实现会执行引用相等性检查。）  
  
3.  可选，但建议这样做：重载 [==](../../../csharp/language-reference/operators/equality-comparison-operator.md) 和 [!=](../../../csharp/language-reference/operators/not-equal-operator.md) 运算符。  
  
4.  替代 <xref:System.Object.GetHashCode%2A?displayProperty=fullName>，以便具有值相等性的两个对象生成相同的哈希代码。  
  
5.  可选：若要支持“大于”或“小于”定义，请为类型实现 <xref:System.IComparable%601> 接口，并同时重载 [<=](../../../csharp/language-reference/operators/less-than-equal-operator.md) 和 [>=](../../../csharp/language-reference/operators/greater-than-equal-operator.md) 运算符。  
  
 下面的第 1 个示例演示了类实现。 第 2 个示例演示了结构实现。  
  
## <a name="example"></a>示例  
 下面的示例演示如何在类（引用类型）中实现值相等性。  
  
 [!code-cs[csProgGuideStatements#19](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-value-equality-for-a-type_1.cs)]  
  
 在类（引用类型）上，两种 <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName> 方法的默认实现均执行引用相等性比较，而不是值相等性检查。 实施者替代虚方法时，目的是为其指定值相等性语义。  
  
 即使类不重载 `==` 和 `!=` 运算符，也可将这些运算符与类一起使用。 但是，默认行为是执行引用相等性检查。 在类中，如果重载 `Equals` 方法，则应重载 `==` 和 `!=` 运算符，但这并不是必需的。  
  
## <a name="example"></a>示例  
 下面的示例演示如何在结构（值类型）中实现值相等性：  
  
 [!code-cs[csProgGuideStatements#20](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-value-equality-for-a-type_2.cs)]  
  
 对于结构，<xref:System.Object.Equals%28System.Object%29?displayProperty=fullName>（<xref:System.ValueType?displayProperty=fullName> 中的替代版本）的默认实现通过使用反射来比较类型中每个字段的值，从而执行值相等性检查。 实施者替代结构中的 `Equals` 虚方法时，目的是提供更高效的方法来执行值相等性检查，并选择根据结构字段或属性的某个子集来进行比较。  
  
 除非结构显式重载了 [==](../../../csharp/language-reference/operators/equality-comparison-operator.md) 和 [!=](../../../csharp/language-reference/operators/not-equal-operator.md) 运算符，否则这些运算符无法对结构进行运算。  
  
## <a name="see-also"></a>请参阅  
 [相等比较](../../../csharp/programming-guide/statements-expressions-operators/equality-comparisons.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)

