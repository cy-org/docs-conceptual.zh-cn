---
title: "接口（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- interfaces [C#]
- C# language, interfaces
ms.assetid: 2feda177-ce11-432d-81b4-d50f5f35fd37
caps.latest.revision: 45
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
ms.openlocfilehash: 0552cea71f66ba8c299b1706cab6778c9e3367c9
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="interfaces-c-programming-guide"></a>接口（C# 编程指南）
接口包含[类](../../../csharp/language-reference/keywords/class.md)或[结构](../../../csharp/language-reference/keywords/struct.md)可以实现的一组相关功能的定义。  
  
 例如，使用接口可以在类中包括来自多个源的行为。 该功能在 C# 中十分重要，因为该语言不支持类的多重继承。 此外，如果要模拟结构的继承，也必须使用接口，因为它们无法实际从另一个结构或类继承。  
  
 可使用 [interface](../../../csharp/language-reference/keywords/interface.md) 关键字定义接口，如以下示例所示。  
  
 [!code-cs[csProgGuideInheritance#47](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/interfaces_1.cs)]  
  
 实现 <xref:System.IEquatable%601> 接口的任何类或结构都必须包含与该接口指定的签名匹配的 <xref:System.IEquatable%601.Equals%2A> 方法的定义。 因此，可以依靠实现 `IEquatable<T>` 的类来包含 `Equals` 方法，类的实例可以通过该方法确定它是否等于相同类的另一个实例。  
  
 `IEquatable<T>` 的定义不为 `Equals` 提供实现。 该接口仅定义签名。 这样，C# 中的接口便类似于其中所有方法都是抽象方法的抽象类。 但是，类或结构可以实现多个接口，但是类只能继承单个类（抽象或不抽象）。 因此，使用接口可以在类中包括来自多个源的行为。  
  
 有关抽象类的详细信息，请参阅[抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
 接口可以包含方法、属性、事件、索引器或这四种成员类型的任意组合。 有关示例的链接，请参阅[相关部分](../../../csharp/programming-guide/interfaces/index.md#BKMK_RelatedSections)。 接口不能包含常量、字段、运算符、实例构造函数、终结器或类型。 接口成员会自动成为公共成员，不能包含任何访问修饰符。 成员也不能是[静态](../../../csharp/language-reference/keywords/static.md)成员。  
  
 若要实现接口成员，实现类的对应成员必须是公共、非静态，并且具有与接口成员相同的名称和签名。  
  
 当类或结构实现接口时，类或结构必须为该接口定义的所有成员提供实现。 接口本身不提供类或结构可以通过继承基类功能的方式来继承的任何功能。 但是，如果基类实现接口，则从基类派生的任何类都会继承该实现。  
  
 下面的示例展示了 IEquatable<T\> 接口的实现代码。 实现类 `Car` 必须提供 <xref:System.IEquatable%601.Equals%2A> 方法的实现。  
  
 [!code-cs[csProgGuideInheritance#48](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/interfaces_2.cs)]  
  
 类的属性和索引器可以为接口中定义的属性或索引器定义额外的访问器。 例如，接口可能会声明包含 [get](../../../csharp/language-reference/keywords/get.md) 取值函数的属性。 实现此接口的类可以声明包含 `get` 和 [set](../../../csharp/language-reference/keywords/set.md) 取值函数的同一属性。 但是，如果属性或索引器使用显式实现，则访问器必须匹配。 有关显式实现的详细信息，请参阅[显式接口实现](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md)和[接口属性](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)。  
  
 接口可以实现其他接口。 类可能通过它继承的基类或通过其他接口实现的接口来多次包含某个接口。 但是，类只能提供接口的实现一次，并且仅当类将接口作为类定义的一部分 (`class ClassName : InterfaceName`) 进行声明时才能提供。 如果由于继承实现接口的基类而继承了接口，则基类会提供接口的成员的实现。 但是，派生类可以重新实现接口成员，而不是使用继承的实现。  
  
 基类还可以使用虚拟成员实现接口成员。 在这种情况下，派生类可以通过重写虚拟成员来更改接口行为。 有关虚拟成员的详细信息，请参阅[多形性](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)。  
  
## <a name="interfaces-summary"></a>接口摘要  
 接口具有以下属性：  
  
-   接口类似于抽象基类。 实现接口的任何类或结构都必须实现其所有成员。  
  
-   接口无法直接进行实例化。 其成员由实现接口的任何类或结构来实现。  
  
-   接口可以包含事件、索引器、方法和属性。  
  
-   接口不包含方法的实现。  
  
-   一个类或结构可以实现多个接口。 一个类可以继承一个基类，还可实现一个或多个接口。  
  
## <a name="in-this-section"></a>本节内容  
 [显式接口实现](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md)  
 说明如何创建特定于接口的类成员。  
  
 [如何：显式实现接口成员](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-interface-members.md)  
 提供有关如何显式实现接口的成员的示例。  
  
 [如何：显式实现两个接口的成员](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md)  
 提供有关如何使用继承显式实现接口的成员的示例。  
  
##  <a name="BKMK_RelatedSections"></a>相关部分  
  
-   [接口属性](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)  
  
-   [接口中的索引器](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)  
  
-   [如何：实现接口事件](../../../csharp/programming-guide/events/how-to-implement-interface-events.md)  
  
-   [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)  
  
-   [继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)  
  
-   [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [多态性](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)  
  
-   [抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)  
  
-   [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)  
  
-   [事件](../../../csharp/programming-guide/events/index.md)  
  
-   [索引器](../../../csharp/programming-guide/indexers/index.md)  
  
## <a name="featured-book-chapter"></a>重要章节  
 [学习 C# 3.0：掌握 C# 3.0 的基础知识](http://msdn.microsoft.com/library/orm-9780596521066-01.aspx)中的[接口](http://msdn.microsoft.com/library/orm-9780596521066-01-13.aspx)  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)

