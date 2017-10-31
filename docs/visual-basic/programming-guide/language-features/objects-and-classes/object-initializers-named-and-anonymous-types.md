---
title: "对象初始值设定项︰ 命名类型和匿名类型 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.ObjectInitializer
dev_langs:
- VB
helpviewer_keywords:
- object initializers [Visual Basic]
- anonymous types [Visual Basic], object initializers
- initializing properties [Visual Basic]
- initializers [Visual Basic]
- named types [Visual Basic]
ms.assetid: e2df3807-a70f-49dd-ac94-f1e07f472b1b
caps.latest.revision: 27
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
ms.openlocfilehash: d684ad4f3dd47dc7400ea401a94660af832ef866
ms.lasthandoff: 03/13/2017

---
# <a name="object-initializers-named-and-anonymous-types-visual-basic"></a>对象初始值设定项：命名类型和匿名类型 (Visual Basic)
对象初始值设定项，可以通过使用单个表达式中指定的复杂对象的属性。 可以使用它们来创建命名类型和匿名类型的实例。  
  
## <a name="declarations"></a>声明  
 命名和匿名类型的实例的声明可以看起来几乎完全相同，但它们的效果并不相同。 每个类别都有其自己的功能和限制。 下面的示例演示如何声明和初始化命名类的实例的捷径`Customer`，通过使用对象初始值设定项列表。 请注意，在关键字后指定的类名称是`New`。  
  
 [!code-vb[VbVbalrObjectInit #&1;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_1.vb)]  
  
 匿名类型有没有可用的名称。 因此匿名类型的实例化不能包含类名。  
  
 [!code-vb[VbVbalrObjectInit #&2;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_2.vb)]  
  
 要求和结果的两个声明都不相同。 有关`namedCust`、`Customer`类，该类具有`Name`属性必须已经存在，并且声明会创建此类的实例。 有关`anonymousCust`，编译器会定义一个新类，具有一个属性，它是一个字符串称为`Name`，并创建此类的新实例。  
  
## <a name="named-types"></a>命名的类型  
 对象初始值设定项提供了一种简单方法调用一种类型的构造函数，然后在单个语句中设置某些或所有属性的值。 编译器将调用适当的构造函数的语句︰ 如果未不提供任何参数，该默认构造函数或参数化构造函数，如果将发送一个或多个参数。 此后，初始值设定项列表中出现的顺序初始化指定的属性。  
  
 每个初始值设定项列表初始化包括分配给类的成员初始值。 定义类时确定的名称和数据类型的成员。 在下面的示例中，`Customer`类必须存在，并且必须命名成员`Name`和`City`，可以接受字符串值。  
  
 [!code-vb[VbVbalrObjectInit #&3;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_3.vb)]  
  
 或者，您可以通过使用下面的代码来获取相同的结果︰  
  
 [!code-vb[VbVbalrObjectInit #&4;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_4.vb)]  
  
 这些声明的每个等效于以下示例中，这将创建`Customer`通过使用默认构造函数中，对象，然后指定初始值`Name`和`City`属性使用`With`语句。  
  
 [!code-vb[VbVbalrObjectInit #&5;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_5.vb)]  
  
 如果`Customer`类包含的参数化构造函数，使您可以为输入值发送`Name`，例如，您可以声明和初始化`Customer`对象通过以下方式︰  
  
 [!code-vb[VbVbalrObjectInit #&6;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_6.vb)]  
  
 不需要初始化所有属性，如以下代码所示。  
  
 [!code-vb[VbVbalrObjectInit #&7;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_7.vb)]  
  
 但是，初始化列表不能为空。 未初始化的属性保留其默认值。  
  
### <a name="type-inference-with-named-types"></a>命名类型的类型推理  
 您可以缩短的声明的代码`cust1`通过组合对象初始值设定项和局部类型推理。 这使您可以省略`As`在变量声明中的子句。 该变量的数据类型是从创建进行的赋值的对象的类型推断出的。 在下面的示例的一种`cust6`是`Customer`。  
  
 [!code-vb[VbVbalrObjectInit #&8;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_8.vb)]  
  
### <a name="remarks-about-named-types"></a>有关命名类型的备注  
  
-   不止一次在对象初始值设定项列表中，无法初始化类成员。 声明`cust7`将导致错误。  
  
     [!code-vb[VbVbalrObjectInit #&9;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_9.vb)]  
  
-   成员可以用来初始化自身或另一个字段。 如果之前尚未初始化，如下所示的以下声明访问成员`cust8`，将使用默认值。 请记住，使用对象初始值设定项的声明，处理时，第一件事是调用适当的构造函数。 之后，将初始化初始值设定项列表中的各个字段。 在下面的示例中，默认值为`Name`为分配`cust8`，并将其初始化的值分配在`cust9`。  
  
     [!code-vb[VbVbalrObjectInit #&10;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_10.vb)]  
  
     下面的示例使用参数化构造函数从`cust3`和`cust4`如何声明和初始化`cust10`和`cust11`。  
  
     [!code-vb[VbVbalrObjectInit #&11;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_11.vb)]  
  
-   可以嵌套对象初始值设定项。 在下面的示例中，`AddressClass`是具有两个属性的类`City`和`State`，和`Customer`类具有`Address`的一个实例的属性`AddressClass`。  
  
     [!code-vb[VbVbalrObjectInit #&12;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_12.vb)]  
  
-   初始化列表不能为空。  
  
-   正在初始化的实例不能是类型对象。  
  
-   正在初始化的类成员不能为共享的成员、 只读成员、 常量或方法调用。  
  
-   无法索引或限定正在初始化的类成员。 下面的示例会产生编译器错误︰  
  
     `'' Not valid.`  
  
     `' Dim c1 = New Customer With {.OrderNumbers(0) = 148662}`  
  
     `' Dim c2 = New Customer with {.Address.City = "Springfield"}`  
  
## <a name="anonymous-types"></a>匿名类型  
 匿名类型使用对象初始值设定项来创建未显式定义的新类型和名称的实例。 相反，编译器将生成一种类型根据指定的属性在对象初始值设定项列表中。 由于未指定类型的名称，它被称为*匿名类型*。 例如，将比较以下声明与上一为`cust6`。  
  
 [!code-vb[VbVbalrObjectInit #&13;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_13.vb)]  
  
 唯一的区别在语法上是后未指定任何名称`New`数据类型。 但是，会发生什么情况却截然不同。 编译器会定义具有两个属性的新匿名类型`Name`和`City`，并使用指定的值创建它的一个实例。 类型推导用于确定类型的`Name`和`City`在示例中为字符串。  
  
> [!CAUTION]
>  匿名类型的名称由编译器生成，并且可能会有所不同编译的。 您的代码不应使用或依赖于一个匿名类型的名称。  
  
 类型的名称不可用，因为不能使用`As`子句声明`cust13`。 必须推断其类型。 如果不使用后期绑定，这限制了匿名类型的局部变量的使用。  
  
 匿名类型提供了对关键支持[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询。 有关使用查询中的匿名类型的详细信息，请参阅[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)和[在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)。  
  
### <a name="remarks-about-anonymous-types"></a>关于匿名类型的备注  
  
-   通常情况下，所有或大多数匿名类型声明中的属性将键属性，输入该关键字表示`Key`属性名称的前面。  
  
     [!code-vb[VbVbalrObjectInit #&14;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_14.vb)]  
  
     键属性的详细信息，请参阅[密钥](../../../../visual-basic/language-reference/modifiers/key.md)。  
  
-   对于匿名类型定义必须声明至少一个属性，如命名类型，初始值设定项列表。  
  
     [!code-vb[VbVbalrObjectInit #&2;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_2.vb)]  
  
-   当声明的匿名类型的实例时，编译器将生成匹配的匿名类型定义。 名称和属性的数据类型，将从实例声明中，并由编译器定义中包含。 这些属性不是名为和，事先定义而会为命名类型。 其类型会被推断。 不能通过使用指定的属性的数据类型`As`子句。  
  
-   匿名类型也可以建立名称和它们的属性的值在其他几种方式。 例如，匿名类型属性可能需要的名称和的变量，或者名称的值和另一个对象的属性的值。  
  
     [!code-vb[VbVbalrObjectInit #&15;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_15.vb)]  
  
     有关在匿名类型中定义属性的选项的详细信息，请参阅[如何︰ 推断属性名和匿名类型声明中的类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)。  
  
## <a name="see-also"></a>另请参阅  
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [如何︰ 推断匿名类型声明中属性名和类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)   
 [密钥](../../../../visual-basic/language-reference/modifiers/key.md)   
 [如何：使用对象初始值设定项声明对象](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
