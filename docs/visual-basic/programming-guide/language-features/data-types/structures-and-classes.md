---
title: "结构和类 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- classes [Visual Basic], vs. structures
- structures
- classes [Visual Basic]
- structures, compared to classes
- structures, structure variables
- structure variables
ms.assetid: a221e74a-ffcf-4bdc-a0f6-a088a9bf26cc
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e7402ec0fcfc279470d39a4919d3b5ec8b5d9dff
ms.lasthandoff: 03/13/2017

---
# <a name="structures-and-classes-visual-basic"></a>结构和类 (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]统一的结构和类，因此这两个实体支持的大多数功能相同的语法。 但是，也有重要区别结构和类。  
  
 类具有引用类型的优点 — 传递一个引用是传递的所有数据结构变量比效率更高。 另一方面，结构不需要全局堆上的内存的分配。  
  
 因为不能从一种结构进行继承，结构仅应该用于不需要进行扩展的对象。 当您想要创建的对象具有小型实例大小，并考虑类而不是结构的性能特征，请使用结构。  
  
## <a name="similarities"></a>相似之处  
 结构和类是在以下方面类似︰  
  
-   两者都是*容器*类型，这意味着它们包含作为其成员的其他类型。  
  
-   同时具有成员，其中可能包括构造函数、 方法、 属性、 字段、 常量、 枚举、 事件和事件处理程序。 但是，不要混淆这些成员与声明*元素*的结构。  
  
-   两者的成员可以分别有不同的访问级别。 例如，可以声明一个成员`Public`和另一个`Private`。  
  
-   都可实现接口。  
  
-   带有或不带参数，都可以有共享构造函数。  
  
-   两者都可以公开*默认属性*，前提是该属性带有至少一个参数。  
  
-   同时可以声明和引发事件，并且两者都可以声明的委托。  
  
## <a name="differences"></a>之间的差异  
 结构和类在以下方面有所不同︰  
  
-   结构是*值类型*; 类是*引用类型*。 结构类型的变量包含结构的数据，而不是那样包含对数据作为类类型的引用。  
  
-   结构使用堆栈堆分配。类使用堆分配。  
  
-   所有结构元素都是`Public`默认; 类变量和常量都是`Private`默认情况下，其他类成员时`Public`默认情况下。 此行为对于类成员提供了与 Visual Basic 6.0 中系统的默认设置的兼容性。  
  
-   结构必须具有至少一个非共享变量或非共享、 非自定义事件元素;类可以是完全为空。  
  
-   结构元素不能声明为`Protected`; 可以类成员。  
  
-   结构过程，才可以处理事件[共享](../../../../visual-basic/language-reference/modifiers/shared.md)`Sub`的过程中，并且只能[AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md); 任何类过程可以处理事件，使用[处理](../../../../visual-basic/language-reference/statements/handles-clause.md)关键字或`AddHandler`语句。 有关详细信息，请参阅[事件](../../../../visual-basic/programming-guide/language-features/events/index.md)。  
  
-   结构变量声明不能指定初始值设定项或数组; 初始大小可以类变量声明。  
  
-   结构隐式继承自<xref:System.ValueType?displayProperty=fullName>类，并从任何其他类型; 不能继承类可从任何类或其他<xref:System.ValueType?displayProperty=fullName>。</xref:System.ValueType?displayProperty=fullName>类继承</xref:System.ValueType?displayProperty=fullName>  
  
-   结构是不可继承;类是。  
  
-   永远不会终止结构，因此，公共语言运行时 (CLR) 永远不会调用<xref:System.Object.Finalize%2A>方法对任何结构; 类不能由垃圾回收器 (GC)，后者将调用结尾<xref:System.Object.Finalize%2A>类当它检测到有任何活动的引用。</xref:System.Object.Finalize%2A> </xref:System.Object.Finalize%2A>  
  
-   一种结构不需要构造函数;类一样。  
  
-   结构可以具有非共享的构造函数仅当它们采用的参数;类可以让它们使用或不带参数。  
  
 每个结构都有一个隐式公共构造函数不带参数。 此构造函数初始化为其默认值的结构的所有数据元素。 不能重新定义此行为。  
  
## <a name="instances-and-variables"></a>实例和变量  
 由于结构是值类型，每个结构变量是永久地绑定到单独的结构实例。 类是引用类型，但对象变量可以在不同时间指不同的类实例。 这一区别在通过以下方式影响您的结构和类的用法︰  
  
-   **初始化。** 结构变量隐式包含使用该结构的无参数构造函数的元素的初始化。 因此，`Dim s As struct1`等同于`Dim s As struct1 = New struct1()`。  
  
-   **为变量赋值。** 当将一个结构变量分配给另一个，或将结构实例传递给过程参数时，变量的所有元素的当前值复制到新结构。 当将一个对象变量赋给另一个，或传递给过程的对象变量时，将复制仅有引用指针。  
  
-   **分配执行任何操作。** 你可以分配值[Nothing](../../../../visual-basic/language-reference/nothing.md)指向一个结构变量，但此实例将继续与变量相关联。 仍可以调用其方法并访问它的数据元素，但由赋值重新初始化变量的元素。  
  
     与之相反，如果对象变量设置为`Nothing`、 取消任何类的实例，并向其分配另一个实例之前，不能通过变量访问任何成员。  
  
-   **多个实例。** 对象变量可以在不同时间赋给它的另一个类实例，并且多个对象变量在同一时间可以引用同一个类实例。 对类成员的值所做的更改会影响时通过指向同一个实例的另一个变量来访问这些成员。  
  
     结构元素，但是，是独立于其自身实例。 为其值的更改不会反映在其他任何结构变量，即使是相同的其他实例中`Structure`声明。  
  
-   **相等比较。** 逐个元素测试，必须执行的两个结构相等性测试。 可以使用比较两个对象变量<xref:System.Object.Equals%2A>方法。</xref:System.Object.Equals%2A> <xref:System.Object.Equals%2A>指示两个变量是否指向同一个实例。</xref:System.Object.Equals%2A>  
  
## <a name="see-also"></a>另请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [结构和其他编程元素](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
