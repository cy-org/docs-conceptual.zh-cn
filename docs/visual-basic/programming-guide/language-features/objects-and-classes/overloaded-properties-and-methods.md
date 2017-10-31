---
title: "重载属性和方法 (Visual Basic 中) |Microsoft 文档"
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
- properties [Visual Basic], overloading
- methods [Visual Basic], overloading
- shadowing
- names, multiple procedures with same
- procedures, mulltiples with same name
- classes [Visual Basic], properties
- classes [Visual Basic], methods
- method overloading
- Overloads keyword, overloaded members
ms.assetid: b686fb97-e7d7-4001-afaa-6650cba08f0d
caps.latest.revision: 12
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
ms.openlocfilehash: 6f379f04ca9b75161baf2bf2c33e87f05a9edf97
ms.lasthandoff: 03/13/2017

---
# <a name="overloaded-properties-and-methods-visual-basic"></a>重载属性和方法 (Visual Basic)
重载是创建多个过程、 实例构造函数或在具有相同名称但不同的参数类型的类中的属性。  
  
## <a name="overloading-usage"></a>重载用法  
 当您的对象模型指示您使用有关对不同的数据类型进行操作的过程相同的名称，则重载是特别有用。 例如，可以显示几种不同的数据类型的类可以具有`Display`过程如下所示︰  
  
 [!code-vb[VbVbalrOOP #&64;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_1.vb)]  
  
 如果没有重载，您需要创建不同的名称，为每个过程，即使它们做同样的内容，如下所示︰  
  
 [!code-vb[VbVbalrOOP #&65;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_2.vb)]  
  
 重载使得更轻松地使用属性或方法，因为它提供了一种可用的数据类型。 例如，重载`Display`以前可以与任何下面的代码行调用讨论的方法︰  
  
 [!code-vb[VbVbalrOOP #&66;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_3.vb)]  
  
 在运行时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]调用参数的数据类型的正确的过程基于您指定。  
  
## <a name="overloading-rules"></a>重载规则  
 通过添加两个或多个属性或方法具有相同名称创建一个类的重载的成员。 除了重载派生的成员，每个重载的成员必须具有不同的参数列表和以下各项不能用作区别特征，重载属性或过程时︰  
  
-   修饰符，如`ByVal`或`ByRef`，适用于一个成员或成员的参数。  
  
-   参数的名称  
  
-   过程的返回类型  
  
 `Overloads`关键字时是可选的重载，但如果任一重载成员使用`Overloads`关键字，则具有相同名称的所有其他重载的成员还必须指定此关键字。  
  
 派生的类可以重载具有相同的参数和参数类型，该过程称为的成员的继承的成员*按名称和签名隐藏*。 如果`Overloads`关键字按名称和签名隐藏，派生的类的成员将使用实现而不是在基的类中，实现和为该成员的所有其他重载将可供派生类的实例时使用。  
  
 如果`Overloads`重载具有相同的参数和参数类型的成员继承的成员时省略关键字，则该重载称为*按名称隐藏*。 按名称隐藏替换的继承成员的实现，并使所有其他重载实例派生的类和其对于都不可用。  
  
 `Overloads`和`Shadows`修饰符不能同时使用具有相同属性或方法。  
  
### <a name="example"></a>示例  
 下面的示例创建接受的重载的方法`String`或`Decimal`美元金额限度和返回一个包含增值税的字符串表示形式。  
  
##### <a name="to-use-this-example-to-create-an-overloaded-method"></a>若要使用此示例创建一个重载的方法  
  
1.  打开新项目并添加一个名为类`TaxClass`。  
  
2.  向 `TaxClass` 类添加下面的代码。  
  
     [!code-vb[VbVbalrOOP #&67;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_4.vb)]  
  
3.  向窗体中添加下面的过程。  
  
     [!code-vb[VbVbalrOOP #&68;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_5.vb)]  
  
4.  将按钮添加到表单中，然后调用`ShowTax`过程从`Button1_Click`该按钮的事件。  
  
5.  运行该项目并单击要测试的重载的窗体上的按钮`ShowTax`过程。  
  
 在运行时，编译器将选择与正在使用的参数匹配的适当重载的函数。 重载的方法时单击按钮时，与第一次调用`Price`参数是一个字符串，该邮件，"价格是一个字符串。 税是 $5.12"显示。 `TaxAmount`使用调用`Decimal`值的第二个时间和消息，"价格是十进制数。 税是 $5.12"显示。  
  
## <a name="see-also"></a>另请参阅  
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Visual Basic 中的隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [阴影](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)   
 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)   
 [重载](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
