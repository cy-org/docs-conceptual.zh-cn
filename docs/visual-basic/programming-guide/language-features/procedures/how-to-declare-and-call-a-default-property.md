---
title: "如何︰ 声明和调用默认属性在 Visual Basic |Microsoft 文档"
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
- defaults, properties
- properties [Visual Basic], default
- procedures, defining
- default properties, in Visual Basic
- Visual Basic code, procedures
- Visual Basic code, properties
- default properties
ms.assetid: 68b4026e-09ef-4613-808e-f6287494ff63
caps.latest.revision: 23
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
ms.openlocfilehash: ce98e7fe72a395f6c4cde481feaa60be28c6fcc3
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-and-call-a-default-property-in-visual-basic"></a>如何：在 Visual Basic 中声明和调用默认属性
一个*默认属性*是一个类或结构的属性，您的代码可以访问而无需指定它。 当一个类或结构，但不是属性，调用代码名称，上下文允许访问某一属性[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]解析对该类或结构的默认属性的访问权限，如果存在。  
  
 类或结构最多可以有一个默认属性。 但是，您可以重载的默认属性并且具有多个版本。  
  
 有关详细信息，请参阅[默认](../../../../visual-basic/language-reference/modifiers/default.md)。  
  
### <a name="to-declare-a-default-property"></a>若要声明的默认属性  
  
1.  以正常方式声明属性。 请不要指定`Shared`或`Private`关键字。  
  
2.  包括`Default`属性声明中的关键字。  
  
3.  指定的属性至少一个参数。 不能定义不带至少一个参数的默认属性。  
  
     [!code-vb[VbVbcnProcedures #&17;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_1.vb)]  
  
### <a name="to-call-a-default-property"></a>若要调用默认属性  
  
1.  声明包含的类或结构类型的变量。  
  
     [!code-vb[VbVbcnProcedures #&16;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_2.vb)]  
  
2.  使用的表达式中单独的变量名通常要包括的属性名称。  
  
     [!code-vb[VbVbcnProcedures #&21;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_3.vb)]  
  
3.  变量名后面加上括号中的参数列表。 默认属性必须采用至少一个参数。  
  
     [!code-vb[VbVbcnProcedures #&20;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_4.vb)]  
  
4.  若要检索其默认属性值，使用变量名称，用参数列表，在表达式中前面或后面等号 (`=`) 登录在赋值语句。  
  
     [!code-vb[VbVbcnProcedures #&15;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_5.vb)]  
  
5.  若要设置默认属性值，用参数列表，在赋值语句左侧使用的变量的名称。  
  
     [!code-vb[VbVbcnProcedures #&14;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_6.vb)]  
  
6.  像那样访问任何其他属性，始终可以指定默认属性名以及变量名。  
  
     [!code-vb[VbVbcnProcedures #&19;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_7.vb)]  
  
## <a name="example"></a>示例  
 下面的示例声明的类上的默认属性。  
  
 [!code-vb[VbVbcnProcedures #&12;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_8.vb)]  
  
## <a name="example"></a>示例  
 下面的示例演示如何调用默认属性`myProperty`类上`class1`。 三个赋值语句将值存储在`myProperty`，和<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>调用读取这些值。</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
  
 [!code-vb[VbVbcnProcedures #&13;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_9.vb)]  
  
 默认属性的最常见用法是<xref:Microsoft.VisualBasic.Collection.Item%2A>各种集合类的属性。</xref:Microsoft.VisualBasic.Collection.Item%2A>  
  
## <a name="robust-programming"></a>可靠编程  
 默认属性可能会导致稍微减少源代码的字符，但它们会使您的代码更难以阅读。 如果建立对类或结构名称的引用时，调用代码不熟悉类或结构，它无法确定该引用访问的类或结构本身或默认属性。 这可以导致编译器错误或细微的运行时逻辑错误。  
  
 某种程度上可以减少默认属性错误的机会，应始终使用[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)设置编译器类型将检查`On`。  
  
 如果您打算使用预定义的类或结构在代码中，您必须确定它是否具有默认属性，以及如果是这样，其名称是什么。  
  
 由于这些缺点，应考虑不定义默认属性。 有关代码的可读性，您应该还考虑始终显式引用的所有属性，包括默认属性。  
  
## <a name="see-also"></a>另请参阅  
 [属性过程](./property-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [默认值](../../../../visual-basic/language-reference/modifiers/default.md)   
 [在 Visual Basic 中属性和变量之间的差异](./differences-between-properties-and-variables.md)   
 [如何︰ 创建属性](./how-to-create-a-property.md)   
 [如何︰ 声明具有混合的访问级别的属性](./how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何︰ 调用 Property 过程](./how-to-call-a-property-procedure.md)   
 [如何︰ 在属性中放置值](./how-to-put-a-value-in-a-property.md)   
 [如何：从属性获取值](./how-to-get-a-value-from-a-property.md)
