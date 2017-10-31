---
title: "struct（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- struct_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- struct keyword [C#]
- structs [C#], struct keyword
ms.assetid: ff3dd9b7-dc93-4720-8855-ef5558f65c7c
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
ms.openlocfilehash: 309e68a57e1ee869850d960ffaac6cf35eb6e260
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="struct-c-reference"></a>struct（C# 参考）
`struct` 类型是一种值类型，通常用来封装小型相关变量组，例如，矩形的坐标或库存商品的特征。 下面的示例显示了一个简单的结构声明：  
  
```  
public struct Book  
{  
    public decimal price;  
    public string title;  
    public string author;  
}  
```  
  
## <a name="remarks"></a>备注  
 结构还可以包含[构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)、[常量](../../../csharp/programming-guide/classes-and-structs/constants.md)、[字段](../../../csharp/programming-guide/classes-and-structs/fields.md)、[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)、[属性](../../../csharp/programming-guide/classes-and-structs/properties.md)、[索引器](../../../csharp/programming-guide/indexers/index.md)、[运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)、[事件](../../../csharp/programming-guide/events/index.md)和[嵌套类型](../../../csharp/programming-guide/classes-and-structs/nested-types.md)，但如果同时需要上述几种成员，则应当考虑改为使用类作为类型。  
  
 有关示例，请参阅[使用结构](../../../csharp/programming-guide/classes-and-structs/using-structs.md)。  
  
 结构可以实现接口，但它们无法继承另一个结构。 因此，结构成员无法声明为 `protected`。  
  
 有关详细信息，请参阅[结构](../../../csharp/programming-guide/classes-and-structs/structs.md)。  
  
## <a name="examples"></a>示例  
 有关示例和详细信息，请参阅[使用结构](../../../csharp/programming-guide/classes-and-structs/using-structs.md)。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 有关示例，请参阅[使用结构](../../../csharp/programming-guide/classes-and-structs/using-structs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [默认值表](../../../csharp/language-reference/keywords/default-values-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)   
 [类](../../../csharp/language-reference/keywords/class.md)   
 [接口](../../../csharp/language-reference/keywords/interface.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)

