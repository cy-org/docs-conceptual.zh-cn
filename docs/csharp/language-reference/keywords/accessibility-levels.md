---
title: "可访问性级别（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- access modifiers [C#], accessibility levels
- accessibility levels
ms.assetid: dc083921-0073-413e-8936-a613e8bb7df4
caps.latest.revision: 19
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
ms.openlocfilehash: 796802a407c486c1df5332d5b4920467f3a1171b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="accessibility-levels-c-reference"></a>可访问性级别（C# 参考）
使用访问修饰符 [public](../../../csharp/language-reference/keywords/public.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md) 或 [private](../../../csharp/language-reference/keywords/private.md)，以为成员指定以下声明的可访问性级别之一。  
  
|声明的可访问性|含义|  
|----------------------------|-------------|  
|`public`|访问不受限制。|  
|`protected`|访问限于包含类或派生自包含类的类型。|  
|`internal`|访问限于当前程序集。|  
|`protected internal`|访问限于当前程序集或派生自包含类的类型。|  
|`private`|访问限于包含类。|  
  
 除使用 `protected internal` 组合的情况外，一个成员或类型仅允许一个访问修饰符。  
  
 命名空间中不允许出现访问修饰符。 命名空间没有任何访问限制。  
  
 根据出现成员声明的上下文，仅允许某些声明的可访问性。 如果未在成员声明中指定访问修饰符，则将使用默认可访问性。  
  
 未嵌套在其他类型中的顶级类型只能具有 `internal` 或 `public` 可访问性。 这些类型的默认可访问性为 `internal`。  
  
 作为其他类型的成员的嵌套类型可以具有如下表所示的声明的可访问性。  
  
|成员|默认成员可访问性|允许的成员的声明的可访问性|  
|----------------|----------------------------------|--------------------------------------------------|  
|`enum`|`public`|无|  
|`class`|`private`|`public`<br /><br /> `protected`<br /><br /> `internal`<br /><br /> `private`<br /><br /> `protected internal`|  
|`interface`|`public`|无|  
|`struct`|`private`|`public`<br /><br /> `internal`<br /><br /> `private`|  
  
 嵌套类型的可访问性依赖于它的[可访问域](../../../csharp/language-reference/keywords/accessibility-domain.md)，该域是由已声明的成员可访问性和直接包含类型的可访问域这二者共同确定的。 但是，嵌套类型的可访问域不能超出包含类型的可访问域。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [可访问域](../../../csharp/language-reference/keywords/accessibility-domain.md)   
 [可访问性级别的使用限制](../../../csharp/language-reference/keywords/restrictions-on-using-accessibility-levels.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [内部](../../../csharp/language-reference/keywords/internal.md)

