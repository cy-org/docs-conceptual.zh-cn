---
title: "如何︰ 调用 Property 过程 (Visual Basic 中) |Microsoft 文档"
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
- Visual Basic code, procedures
- Visual Basic code, properties
- procedures, calling
- properties [Visual Basic], property procedures
- procedure calls, property procedures
ms.assetid: 96bc4d74-d9c3-4b7a-954d-58ac8553cd94
caps.latest.revision: 16
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
ms.openlocfilehash: 7dd3d53f602886f65c951de34b915b2672b1a817
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-property-procedure-visual-basic"></a>如何：调用 Property 过程 (Visual Basic)
在属性中存储一个值或检索其值由调用 property 过程。 访问属性相同的方式访问的变量。  
  
 该属性的`Set`过程存储一个值，并将其`Get`过程会检索该值。 但是，您不显式调用这些过程的名称。 就像将存储或检索变量的值时，才使用在赋值语句或表达式，该属性。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]调用该属性的过程。  
  
### <a name="to-call-a-propertys-get-procedure"></a>若要调用 property Get 过程  
  
1.  像使用变量名一样，在表达式中使用属性名称。 可以使用属性任何可以使用一个变量或常量。  
  
     - 或 -  
  
     使用属性名称后面等号 (`=`) 登录在赋值语句。  
  
     下面的示例读取的值<xref:Microsoft.VisualBasic.DateAndTime.Now%2A>属性外，隐式调用其`Get`过程。</xref:Microsoft.VisualBasic.DateAndTime.Now%2A>  
  
     [!code-vb[VbVbalrDateProperties #&4;](./codesnippet/VisualBasic/how-to-call-a-property-procedure_1.vb)]  
  
2.  如果该属性接受参数，请按照用括号括起的参数列表的属性名称。 如果不有任何参数，可以选择省略括号。  
  
3.  将参数放在括号内，用逗号分隔参数列表中。 请确保您的属性定义的相应参数的相同顺序的参数提供。  
  
 属性的值参与像变量表达式或常数那样，或存储在变量或赋值语句左侧的属性。  
  
### <a name="to-call-a-propertys-set-procedure"></a>若要调用的属性的设置过程  
  
1.  在赋值语句左侧使用的属性名称。  
  
     下面的示例设置的值<xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>属性外，隐式调用`Set`过程。</xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>  
  
     [!code-vb[VbVbcnProcedures #&11;](./codesnippet/VisualBasic/how-to-call-a-property-procedure_2.vb)]  
  
2.  如果该属性接受参数，请按照用括号括起的参数列表的属性名称。 如果不有任何参数，可以选择省略括号。  
  
3.  将参数放在括号内，用逗号分隔参数列表中。 请确保您的属性定义的相应参数的相同顺序的参数提供。  
  
 生成的赋值语句右侧的值存储在该属性。  
  
## <a name="see-also"></a>请参见  
 [属性过程](./property-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [在 Visual Basic 中属性和变量之间的差异](./differences-between-properties-and-variables.md)   
 [如何︰ 创建属性](./how-to-create-a-property.md)   
 [如何︰ 声明具有混合的访问级别的属性](./how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何︰ 声明和调用默认属性在 Visual Basic 中](./how-to-declare-and-call-a-default-property.md)   
 [如何︰ 在属性中放置值](./how-to-put-a-value-in-a-property.md)   
 [如何︰ 从属性获取一个值](./how-to-get-a-value-from-a-property.md)   
 [Get 语句](../../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set 语句](../../../../visual-basic/language-reference/statements/set-statement.md)
