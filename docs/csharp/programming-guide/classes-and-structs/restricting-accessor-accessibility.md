---
title: "限制访问器可访问性（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- read-only properties [C#]
- read-only indexers [C#]
- accessors [C#]
- properties [C#], read-only
- asymmetric accessor accesibility [C#]
- indexers [C#], read-only
ms.assetid: 6e655798-e112-4301-a680-6310a6e012e1
caps.latest.revision: 26
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
ms.openlocfilehash: 347fffa4f612c5cb674a6529e46c0b1785670c95
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="restricting-accessor-accessibility-c-programming-guide"></a>限制访问器可访问性（C# 编程指南）
属性或索引器的 [get](../../../csharp/language-reference/keywords/get.md) 和 [set](../../../csharp/language-reference/keywords/set.md) 部分称为访问器。 默认情况下，这些访问器具有相同的可见性或访问级别：其所属属性或索引器的可见性或访问级别。 有关详细信息，请参阅[可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)。 不过，有时限制对其中某个访问器的访问是有益的。 通常是在保持 `get` 访问器可公开访问的情况下，限制 `set` 访问器的可访问性。 例如:   
  
 [!code-cs[csProgGuideIndexers#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_1.cs)]  
  
 在此示例中，名为 `Name` 的属性定义 `get` 访问器和 `set` 访问器。 `get` 访问器接收该属性本身的可访问性级别（此示例中为 `public`），而对于 `set` 访问器，则通过对该访问器本身应用 [protected](../../../csharp/language-reference/keywords/protected.md) 访问修饰符来进行显式限制。  
  
## <a name="restrictions-on-access-modifiers-on-accessors"></a>对访问器的访问修饰符的限制  
 对属性或索引器使用访问修饰符受以下条件的制约：  
  
-   不能对接口或显式[接口](../../../csharp/language-reference/keywords/interface.md)成员实现使用访问器修饰符。  
  
-   仅当属性或索引器同时具有 `set` 和 `get` 访问器时，才能使用访问器修饰符。 这种情况下，只允许对其中一个访问器使用修饰符。  
  
-   如果属性或索引器具有 [override](../../../csharp/language-reference/keywords/override.md) 修饰符，则访问器修饰符必须与重写的访问器的访问器（如有）匹配。  
  
-   访问器的可访问性级别必须比属性或索引器本身的可访问性级别具有更严格的限制。  
  
## <a name="access-modifiers-on-overriding-accessors"></a>重写访问器的访问修饰符  
 重写属性或索引器时，被重写的访问器对重写代码而言必须是可访问的。 此外，属性/索引器和访问器的可访问性级别都必须与相应的被重写属性/索引器和访问器匹配。 例如:   
  
 [!code-cs[csProgGuideIndexers#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_2.cs)]  
  
## <a name="implementing-interfaces"></a>实现接口  
 使用访问器实现接口时，访问器不一定有访问修饰符。 但如果使用一个访问器（如 `get`）实现接口，则另一个访问器可以具有访问修饰符，如下面的示例所示：  
  
 [!code-cs[csProgGuideIndexers#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_3.cs)]  
  
## <a name="accessor-accessibility-domain"></a>访问器可访问性域  
 如果对访问器使用访问修饰符，则访问器的[可访问性域](../../../csharp/language-reference/keywords/accessibility-domain.md)由该修饰符确定。  
  
 如果未对访问器使用访问修饰符，则访问器的可访问性域由属性或索引器的可访问性级别确定。  
  
## <a name="example"></a>示例  
 下面的示例包含三个类：`BaseClass`、`DerivedClass` 和 `MainClass`。 每个类的 `BaseClass`、`Name` 和 `Id` 都有两个属性。 该示例演示在使用限制性访问修饰符（如 [protected](../../../csharp/language-reference/keywords/protected.md) 或 [private](../../../csharp/language-reference/keywords/private.md)）时，`BaseClass` 的 `Id` 属性如何隐藏 `DerivedClass` 的 `Id` 属性。 因此，向该属性赋值时将调用 `BaseClass` 类中的属性。 将访问修饰符替换为 [public](../../../csharp/language-reference/keywords/public.md) 将使该属性可供访问。  
  
 该示例还演示 `DerivedClass` 中 `Name` 属性上 `set` 访问器的限制性访问修饰符（如 `private` 或 `protected`）如何防止对该访问器的访问，并在向它赋值时生成错误。  
  
 [!code-cs[csProgGuideIndexers#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_4.cs)]  
  
## <a name="comments"></a>注释  
 注意，如果将声明 `new private string Id` 替换为 `new public string Id`，则得到如下输出：  
  
 `Name and ID in the base class: Name-BaseClass, ID-BaseClass`  
  
 `Name and ID in the derived class: John, John123`  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [索引器](../../../csharp/programming-guide/indexers/index.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)

